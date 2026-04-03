# 嵌入式 Linux 锁机制与实践总结

## 一、锁机制全景概览

嵌入式 Linux 中的锁机制是并发控制的核心，主要分为 **自旋锁（Spinlock）**、**互斥锁（Mutex）**、**读写锁（RWLock）** 和 **信号量（Semaphore）** 四大类。在实时性要求高的嵌入式场景中，还需特别关注 **PREEMPT_RT** 补丁带来的锁机制变革。

| 锁类型 | 特性 | 适用场景 | 上下文限制 |
|--------|------|----------|-----------|
| **自旋锁** | 忙等待，不睡眠 | 短临界区、中断上下文 | 不可睡眠上下文 |
| **互斥锁** | 睡眠等待，支持优先级继承 | 长临界区、进程上下文 | 可睡眠上下文 |
| **读写锁** | 读并发、写独占 | 读多写少场景 | 视实现而定 |
| **信号量** | 计数机制，允许多个持有者 | 资源池管理 | 可睡眠上下文 |
| **RCU** | 读无锁、写延迟释放 | 极高读性能场景 | 宽限期限制 |

---

## 二、核心锁机制详解

### 2.1 自旋锁（Spinlock）

自旋锁是一种忙等待锁，线程获取锁失败时会循环检查（自旋）直到锁可用。

**特点：**
- **忙等待**：不释放 CPU，持续检查锁状态
- **低开销**：适用于锁持有时间极短的场景（几微秒级）
- **中断安全**：需配合中断禁用使用

**内核 API：**
```c
#include <linux/spinlock.h>

DEFINE_SPINLOCK(my_lock);           // 定义并初始化
spin_lock(&my_lock);                // 获取锁（禁用抢占）
spin_unlock(&my_lock);              // 释放锁

spin_lock_irqsave(&my_lock, flags);   // 保存中断状态并禁用本地中断
spin_unlock_irqrestore(&my_lock, flags); // 恢复中断状态
```

**ARM 裸机实现示例：**
```c
#include <stdatomic.h>

typedef atomic_flag spinlock_t;

void spinlock_init(spinlock_t *lock) {
    atomic_flag_clear(lock);
}

void spinlock_lock(spinlock_t *lock) {
    while (atomic_flag_test_and_set(lock)) {
        asm volatile("nop");  // 自旋等待，可插入指数退避
    }
}

void spinlock_unlock(spinlock_t *lock) {
    atomic_flag_clear(lock);
}
```

**重要约束：**
- 临界区代码 **禁止睡眠**（不能调用 kmalloc、schedule 等）
- 单核系统自旋锁退化为 **禁用抢占/中断**
- 锁持有时间必须极短，否则浪费 CPU 且可能引发优先级反转

---

### 2.2 互斥锁（Mutex）

互斥锁是睡眠锁，获取失败时线程进入睡眠状态，让出 CPU。

**内核 API：**
```c
#include <linux/mutex.h>

DEFINE_MUTEX(my_mutex);             // 定义并初始化

mutex_lock(&my_mutex);              // 获取锁（可能睡眠）
mutex_unlock(&my_mutex);            // 释放锁

mutex_trylock(&my_mutex);           // 非阻塞尝试获取
mutex_lock_interruptible(&my_mutex); // 可被信号中断
```

**POSIX 用户态接口：**
```c
#include <pthread.h>

pthread_mutex_t mutex;
pthread_mutex_init(&mutex, NULL);   // 初始化
pthread_mutex_lock(&mutex);         // 加锁
pthread_mutex_unlock(&mutex);       // 解锁
pthread_mutex_destroy(&mutex);      // 销毁
```

**与自旋锁的选择原则：**
- 临界区可能睡眠 → 必须用互斥锁
- 临界区极短且在中断上下文 → 必须用自旋锁
- 不确定时优先使用互斥锁（更安全）

---

### 2.3 读写锁（RWLock）

读写锁优化了 **读多写少** 的场景，允许多个读者并发访问，写者独占。

**内核 API：**
```c
#include <linux/rwlock.h>

DEFINE_RWLOCK(my_rwlock);           // 定义读写锁

read_lock(&my_rwlock);              // 获取读锁（共享）
read_unlock(&my_rwlock);            // 释放读锁

write_lock(&my_rwlock);             // 获取写锁（独占）
write_unlock(&my_rwlock);           // 释放写锁
```

**用户态 C++ 实现示例：**
```cpp
#include <atomic>

class SharedSpinLock {
    std::atomic<int32_t> state_{0};  // >=0: 读者数, -1: 写者
    
public:
    void lock_shared() noexcept {   // 读锁
        uint32_t backoff = 1;
        for (;;) {
            int32_t s = state_.load(std::memory_order_relaxed);
            if (s >= 0 && state_.compare_exchange_weak(
                    s, s + 1,
                    std::memory_order_acquire)) {
                return;
            }
            // 指数退避，避免总线风暴
            for (volatile int i = 0; i < backoff; ++i);
            backoff = (backoff << 1) | 1;
        }
    }
    
    void lock() noexcept {          // 写锁
        uint32_t backoff = 1;
        for (;;) {
            int32_t expected = 0;
            if (state_.compare_exchange_weak(
                    expected, -1,
                    std::memory_order_acquire)) {
                return;
            }
            // 退避等待
        }
    }
};
```

---

### 2.4 顺序锁（Seqlock）

针对 **写少读多** 且读操作可重复的场景，内核提供顺序锁：
```c
#include <linux/seqlock.h>

DEFINE_SEQLOCK(my_seqlock);

// 写者
write_seqlock(&my_seqlock);
// 修改共享数据
write_sequnlock(&my_seqlock);

// 读者
do {
    seq = read_seqbegin(&my_seqlock);
    // 读取数据
} while (read_seqretry(&my_seqlock, seq));
```

---

## 三、实时性与 PREEMPT_RT 锁机制变革

### 3.1 实时内核的锁改造

标准 Linux 内核中，自旋锁会 **禁用抢占**，导致实时任务无法及时调度。PREEMPT_RT 补丁对锁机制进行了根本性变革：

| 标准内核 | PREEMPT_RT 内核 |
|---------|----------------|
| `spinlock_t` → 原始自旋锁（禁用抢占） | `spinlock_t` → 基于 `rt_mutex` 的 **睡眠自旋锁** |
| `rwlock_t` → 原始读写锁 | `rwlock_t` → 基于 `rt_mutex` 的睡眠锁 |
| `mutex` → 原子操作 + 原始自旋锁 | `mutex` → 基于 `rt_mutex`（支持优先级继承） |

**关键特性：**
- **睡眠自旋锁**：等待锁时线程进入睡眠，可被高优先级任务抢占
- **优先级继承**：解决优先级反转问题，临时提升锁持有者优先级
- **中断线程化**：中断处理程序转为内核线程，具备优先级管理

### 3.2 优先级继承机制

**优先级反转问题：**
- 高优先级任务 P1 等待低优先级任务 P3 持有的锁
- 中优先级任务 P2 抢占 P3，导致 P1 被间接阻塞（优先级反转）

**PREEMPT_RT 解决方案：**
```c
// 当 P1 请求 P3 持有的 rt_mutex 时：
// 1. P3 的优先级临时提升至 P1 的优先级
// 2. P3 执行完毕释放锁，恢复原始优先级
// 3. P1 获得锁并继续执行
```

**限制条件：**
- 优先级继承仅在 **可抢占上下文** 有效
- 中断禁用区域或原始自旋锁（`raw_spinlock_t`）保护区无效

### 3.3 原始自旋锁（raw_spinlock_t）

PREEMPT_RT 保留 `raw_spinlock_t` 用于关键核心代码，行为与传统自旋锁一致：

```c
#include <linux/spinlock_types_raw.h>

DEFINE_RAW_SPINLOCK(my_raw_lock);

raw_spin_lock(&my_raw_lock);    // 禁用抢占，忙等待
raw_spin_unlock(&my_raw_lock);
```

**使用场景：**
- 调度器核心代码
- 低级别中断处理
- 硬件状态访问（需禁用抢占/中断）
- 极短临界区（避免 rt_mutex 开销）

---

## 四、ARM 架构原子操作与内存屏障

### 4.1 原子操作实现

ARM 架构通过 **LDREX/STREX** 指令对实现原子操作：

```c
// ARM 原子操作伪代码
uint32_t atomic_add(uint32_t *ptr, uint32_t val) {
    uint32_t tmp, result;
    do {
        tmp = __LDREX(ptr);         // 独占加载
        result = tmp + val;
    } while (__STREX(result, ptr)); // 独占存储，失败则重试
    return result;
}
```

**Linux 内核原子操作 API：**
```c
#include <linux/atomic.h>

atomic_t v = ATOMIC_INIT(0);
atomic_inc(&v);                     // 原子递增
atomic_dec(&v);                     // 原子递减
atomic_add(5, &v);                  // 原子加
atomic_sub(3, &v);                  // 原子减

// 64位原子操作
atomic64_t v64 = ATOMIC64_INIT(0);
atomic64_add(100, &v64);
```

### 4.2 内存屏障（Memory Barrier）

ARM 采用 **弱一致性内存模型**，需显式内存屏障保证执行顺序：

| 屏障指令 | 功能 |
|---------|------|
| **DMB** (Data Memory Barrier) | 确保内存访问顺序，不影响指令执行 |
| **DSB** (Data Synchronization Barrier) | 确保所有内存访问完成，后续指令才能执行 |
| **ISB** (Instruction Synchronization Barrier) | 刷新指令流水线，确保指令可见性 |

**Linux 内核内存屏障 API：**
```c
#include <linux/barrier.h>

smp_mb();   // 全屏障（StoreLoad）
smp_rmb();  // 读屏障（LoadLoad）
smp_wmb();  // 写屏障（StoreStore）

// 与原子操作结合
smp_mb__before_atomic();
smp_mb__after_atomic();
```

**缓存一致性考虑：**
- ARM 使用 **MOESI** 协议维护多核缓存一致性
- 原子操作通过 **缓存行锁定** 或 **总线锁定** 实现
- DMA 操作需注意 **缓存一致性**（使用 `dma_sync_sg_for_cpu/device`）

---

## 五、死锁防御与最佳实践

### 5.1 死锁产生的四个必要条件

1. **互斥条件**：资源独占访问
2. **请求与保持**：持有锁的同时请求新锁
3. **不可剥夺**：锁只能由持有者释放
4. **循环等待**：形成等待环路

### 5.2 防御策略

**策略一：锁顺序规范化**
```c
// 定义全局锁获取顺序
enum lock_order {
    LOCK_ORDER_A = 1,
    LOCK_ORDER_B = 2,
    LOCK_ORDER_C = 3,
};

void lock_with_order(struct mutex *lock, enum lock_order order) {
    // 检查顺序，确保全局一致
    mutex_lock(lock);
}
```

**策略二：超时与尝试机制**
```c
// 使用 trylock 避免无限等待
if (!mutex_trylock(&lock_a)) {
    return -EBUSY;  // 获取失败，优雅退出
}
// 或使用超时
if (mutex_lock_interruptible_timeout(&lock_a, HZ) != 0) {
    return -ETIMEDOUT;
}
```

**策略三：无锁设计**
- 使用 **RCU**（Read-Copy-Update）实现读多写少场景的无锁访问
- 使用 **原子操作** 替代锁（如计数器、标志位）
- 使用 **per-CPU 变量** 避免跨 CPU 同步

**策略四：指数退避自旋锁**
```c
// 避免总线风暴，确保其他线程获得 CPU 时间
void lock_with_backoff(spinlock_t *lock) {
    uint32_t backoff = 1;
    while (spin_trylock(lock)) {
        for (volatile int i = 0; i < backoff; ++i);
        backoff = min(backoff << 1, MAX_BACKOFF);
    }
}
```

### 5.3 优先级反转防护

**在 PREEMPT_RT 中：**
- 使用 `rt_mutex` 替代普通互斥锁（自动支持优先级继承）
- 避免在关键实时路径中使用 `raw_spinlock_t`
- 合理设置线程优先级，避免过大优先级差

**传统内核中的替代方案：**
```c
// 使用优先级继承互斥锁（PI-futex）
pthread_mutexattr_t attr;
pthread_mutexattr_init(&attr);
pthread_mutexattr_setprotocol(&attr, PTHREAD_PRIO_INHERIT);
pthread_mutex_init(&mutex, &attr);
```

---

## 六、典型场景实践

### 6.1 驱动程序中的锁选择

```c
#include <linux/spinlock.h>
#include <linux/mutex.h>

struct my_driver {
    spinlock_t reg_lock;        // 保护硬件寄存器访问（短、不可睡眠）
    mutex_t state_lock;         // 保护设备状态（长、可睡眠）
};

// 中断上下文（必须自旋锁）
static irqreturn_t my_irq_handler(int irq, void *dev_id) {
    struct my_driver *drv = dev_id;
    u32 status;
    
    spin_lock(&drv->reg_lock);
    status = readl(drv->base + REG_STATUS);
    writel(status, drv->base + REG_CLEAR);
    spin_unlock(&drv->reg_lock);
    
    return IRQ_HANDLED;
}

// 进程上下文（使用互斥锁）
static int my_ioctl(struct file *filp, unsigned int cmd, unsigned long arg) {
    struct my_driver *drv = filp->private_data;
    
    mutex_lock(&drv->state_lock);
    // 可能睡眠的操作：copy_from_user、kmalloc 等
    mutex_unlock(&drv->state_lock);
    
    return 0;
}
```

### 6.2 多核系统中的缓存行优化

```c
// 避免伪共享（False Sharing），将锁与数据分离到不同缓存行
struct padded_lock {
    spinlock_t lock;
    char padding[64 - sizeof(spinlock_t)];  // 填充至缓存行大小（通常64字节）
} ____cacheline_aligned;

struct my_data {
    struct padded_lock lock;
    int value;
} ____cacheline_aligned;
```

### 6.3 实时任务中的锁使用

```c
// PREEMPT_RT 环境下，实时任务应使用睡眠锁
#include <linux/rtmutex.h>

struct rt_mutex my_rt_lock;

// 实时线程
static int rt_thread(void *data) {
    struct sched_param param = { .sched_priority = 80 };
    sched_setscheduler(current, SCHED_FIFO, &param);
    
    while (!kthread_should_stop()) {
        rt_mutex_lock(&my_rt_lock);  // 可被抢占，支持优先级继承
        // 临界区
        rt_mutex_unlock(&my_rt_lock);
    }
    
    return 0;
}
```

---

## 七、调试与验证

### 7.1 锁相关调试工具

| 工具/机制 | 用途 |
|----------|------|
| **lockdep** | 静态死锁检测，运行时锁依赖分析 |
| **CONFIG_DEBUG_MUTEXES** | 互斥锁调试，检测非法使用 |
| **CONFIG_DEBUG_SPINLOCK** | 自旋锁调试，检测未初始化/重复释放 |
| **CONFIG_PROVE_LOCKING** | 锁验证，检测潜在死锁 |
| **tracepoints** | 跟踪锁获取/释放事件 |

### 7.2 Lockdep 使用示例

```bash
# 内核配置
CONFIG_LOCKDEP=y
CONFIG_DEBUG_LOCK_ALLOC=y
CONFIG_PROVE_LOCKING=y

# 运行时查看锁依赖
cat /proc/lockdep
cat /proc/lockdep_stats
```

---

## 八、总结与选型建议

| 场景 | 推荐锁类型 | 注意事项 |
|------|-----------|---------|
| **中断上下文** | `raw_spinlock_t` + 禁用中断 | 禁止睡眠 |
| **短临界区（<1μs）** | `spinlock_t`（标准）/ `raw_spinlock_t`（RT） | 考虑缓存行对齐 |
| **长临界区、可睡眠** | `mutex` / `rt_mutex` | 避免死锁，考虑超时 |
| **读多写少** | `rwlock_t` / `percpu_rw_semaphore` | 写者饥饿问题 |
| **极高读性能** | RCU | 宽限期延迟 |
| **实时任务（PREEMPT_RT）** | `rt_mutex` | 利用优先级继承 |

嵌入式 Linux 锁机制的选择需综合考虑 **上下文环境**、**持有时间**、**实时性要求** 和 **多核扩展性**。在 PREEMPT_RT 实时内核中，优先使用支持优先级继承的睡眠锁，仅在必要时使用原始自旋锁，以确保系统的实时响应能力。