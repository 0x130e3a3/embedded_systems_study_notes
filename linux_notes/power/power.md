根据搜索结果，我为您生成一份详细的Linux电源管理子系统技术文档：


# Linux 电源管理子系统详解

## 目录

1. [概述](#概述)
2. [电源管理架构总览](#电源管理架构总览)
3. [系统级电源管理](#系统级电源管理)
4. [运行时电源管理 Runtime PM](#运行时电源管理-runtime-pm)
5. [设备电源管理](#设备电源管理)
6. [CPUFreq 子系统](#cpufreq-子系统)
7. [Regulator 子系统](#regulator-子系统)
8. [电源域 Power Domain](#电源域-power-domain)
9. [驱动开发实践](#驱动开发实践)
10. [调试与工具](#调试与工具)

---

## 概述

Linux电源管理子系统是一个复杂而完善的框架，负责管理从整个系统到单个设备的各级电源状态。它涵盖系统级挂起/恢复、运行时动态电源管理、CPU频率/电压调节等多个层面，旨在平衡设备性能与功耗。

### 主要功能模块

| 模块 | 功能 | 适用场景 |
|-----|------|---------|
| **系统睡眠** | Suspend-to-RAM、Hibernate | 笔记本合盖、系统待机 |
| **Runtime PM** | 设备级动态电源开关 | 设备空闲时自动断电 |
| **CPUFreq** | 动态调整CPU频率/电压 | 根据负载调节性能 |
| **CPUIdle** | CPU空闲状态管理 | 系统空闲时降低功耗 |
| **Regulator** | 电压/电流调节 | 多电压域设备管理 |
| **Power Domain** | 电源域统一管理 | SoC级电源控制 |

---

## 电源管理架构总览

Linux电源管理采用分层架构设计，从用户空间到硬件层形成完整的电源控制链路。

### 架构层次图

```
┌─────────────────────────────────────────────────────────────┐
│                    用户空间 (User Space)                     │
│              echo mem > /sys/power/state                     │
│              /sys/devices/.../power/control                  │
├─────────────────────────────────────────────────────────────┤
│                   电源管理核心 (PM Core)                     │
│    系统睡眠管理 / 设备PM回调协调 / Runtime PM框架             │
├─────────────────────────────────────────────────────────────┤
│              子系统与驱动层 (Subsystems & Drivers)            │
│    Platform / Bus / Class / Driver 各级PM操作                │
│    struct dev_pm_ops / struct platform_suspend_ops           │
├─────────────────────────────────────────────────────────────┤
│               平台相关代码 (Platform Code)                    │
│    SoC特定挂起/恢复操作 / 电源域控制 / 时钟管理               │
├─────────────────────────────────────────────────────────────┤
│                    硬件层 (Hardware)                         │
│            CPU / DDR / 外设 / PMIC / 时钟树                  │
└─────────────────────────────────────────────────────────────┘
```

### 核心组件关系

```
PM Core
  ├── System Sleep (suspend/resume/hibernate)
  │     └── platform_suspend_ops (平台级操作)
  ├── Runtime PM (运行时电源管理)
  │     └── dev_pm_ops.runtime_suspend/resume
  └── Device PM (设备电源管理)
        ├── Power Domain (电源域)
        ├── Device Class (设备类)
        ├── Device Bus (总线类型)
        └── Device Driver (设备驱动)
              └── dev_pm_ops
```

---

## 系统级电源管理

系统级电源管理负责整个系统的挂起和恢复，包括Suspend-to-RAM、Hibernate等模式。

### 系统睡眠状态

| 状态 | 名称 | 功耗 | 恢复时间 | 特点 |
|-----|------|------|---------|------|
| **S0** | Working | 正常 | - | 正常工作状态 |
| **S1/S2** | Standby | 低 | 快 | CPU停止，RAM保持 |
| **S3** | Suspend-to-RAM | 很低 | 较快 | RAM自刷新，CPU断电 |
| **S4** | Hibernate | 极低 | 慢 | 内存保存到磁盘，完全断电 |
| **S5** | Power Off | 无 | 冷启动 | 完全关机 |

### 平台级挂起操作

平台代码通过`struct platform_suspend_ops`向PM Core注册系统级挂起操作：

```c
struct platform_suspend_ops {
    int (*valid)(suspend_state_t state);    /* 检查状态是否有效 */
    int (*begin)(suspend_state_t state);    /* 开始挂起 */
    int (*prepare)(void);                   /* 准备阶段 */
    int (*enter)(suspend_state_t state);    /* 进入低功耗状态 */
    void (*wake)(void);                     /* 唤醒回调 */
    void (*finish)(void);                   /* 完成挂起 */
    void (*end)(void);                       /* 结束 */
    void (*recover)(void);                   /* 恢复错误 */
};
```

注册示例：
```c
static const struct platform_suspend_ops my_suspend_ops = {
    .valid = my_suspend_valid,
    .enter = my_suspend_enter,
};

static int __init my_pm_init(void)
{
    suspend_set_ops(&my_suspend_ops);
    return 0;
}
```

### 系统挂起流程

```
用户空间请求挂起
    ↓
PM Core冻结进程
    ↓
调用所有设备的 ->prepare()
    ↓
调用所有设备的 ->suspend()
    ↓
禁用非启动CPU
    ↓
调用所有设备的 ->suspend_late()
    ↓
禁用IRQ，调用 ->suspend_noirq()
    ↓
平台代码进入低功耗状态 (suspend_ops->enter)
    ↓
[系统睡眠...]
    ↓
唤醒中断触发
    ↓
平台代码恢复 (suspend_ops->wake)
    ↓
调用所有设备的 ->resume_noirq()
    ↓
启用IRQ，调用 ->resume_early()
    ↓
启用非启动CPU，调用 ->resume()
    ↓
调用所有设备的 ->complete()
    ↓
解冻进程，系统恢复运行
```

---

## 运行时电源管理 Runtime PM

Runtime PM允许设备在系统运行期间动态进入低功耗状态，是实现精细化电源管理的关键机制。

### 核心概念

- **Usage Count（使用计数）**：设备被使用的引用计数，计数为0时设备可挂起
- **Idle（空闲）**：设备空闲回调，决定是否允许挂起
- **Suspend（挂起）**：设备进入低功耗状态
- **Resume（恢复）**：设备从低功耗状态恢复

### 状态转换图

```
        ┌─────────────┐
        │   Active    │ ← 设备正在使用
        │  (使用计数>0) │
        └──────┬──────┘
               │ pm_runtime_put()
               ↓
        ┌─────────────┐
        │    Idle     │ ← 设备空闲，可挂起
        │  (使用计数=0) │
        └──────┬──────┘
               │ 自动或手动触发suspend
               ↓
        ┌─────────────┐
        │  Suspended  │ ← 设备已挂起
        │  (低功耗状态) │
        └──────┬──────┘
               │ pm_runtime_get()
               ↓
        ┌─────────────┐
        │  Resuming   │ ← 正在恢复
        └─────────────┘
```

### Runtime PM API

```c
/* 初始化与使能 */
void pm_runtime_enable(struct device *dev);      /* 使能Runtime PM */
void pm_runtime_disable(struct device *dev);     /* 禁止Runtime PM */

/* 使用计数管理 */
int pm_runtime_get(struct device *dev);          /* 增加计数，必要时恢复 */
int pm_runtime_get_sync(struct device *dev);     /* 同步版本 */
int pm_runtime_put(struct device *dev);          /* 减少计数 */
int pm_runtime_put_sync(struct device *dev);     /* 同步版本 */
int pm_runtime_put_noidle(struct device *dev);   /* 减少计数，不触发idle */

/* 手动控制 */
int pm_runtime_suspend(struct device *dev);      /* 尝试挂起设备 */
int pm_runtime_resume(struct device *dev);       /* 恢复设备 */
int pm_runtime_idle(struct device *dev);         /* 触发idle回调 */

/* 状态查询 */
bool pm_runtime_active(struct device *dev);      /* 检查是否active */
bool pm_runtime_suspended(struct device *dev);   /* 检查是否suspended */
```

### 使用示例

```c
/* 在probe中使能Runtime PM */
static int my_driver_probe(struct platform_device *pdev)
{
    struct device *dev = &pdev->dev;
    
    /* 初始化设备 */
    /* ... */
    
    /* 设置运行时挂起延迟（可选） */
    pm_runtime_set_autosuspend_delay(dev, 1000);  /* 1秒延迟 */
    pm_runtime_use_autosuspend(dev);
    
    /* 使能Runtime PM，初始状态为suspended */
    pm_runtime_set_suspended(dev);
    pm_runtime_enable(dev);
    
    return 0;
}

/* 在remove中禁止Runtime PM */
static int my_driver_remove(struct platform_device *pdev)
{
    struct device *dev = &pdev->dev;
    
    pm_runtime_disable(dev);
    pm_runtime_set_suspended(dev);
    
    return 0;
}

/* 数据访问前获取设备 */
static ssize_t my_read(struct file *file, char __user *buf, 
                       size_t count, loff_t *pos)
{
    struct my_device *mydev = file->private_data;
    int ret;
    
    ret = pm_runtime_get_sync(mydev->dev);
    if (ret < 0)
        return ret;
    
    /* 访问设备硬件 */
    /* ... */
    
    pm_runtime_put(mydev->dev);  /* 异步减少计数 */
    return count;
}
```

---

## 设备电源管理

设备电源管理通过`struct dev_pm_ops`定义设备在系统睡眠和Runtime PM中的行为。

### dev_pm_ops 结构体

```c
struct dev_pm_ops {
    /* 系统睡眠回调 */
    int (*prepare)(struct device *dev);
    void (*complete)(struct device *dev);
    int (*suspend)(struct device *dev);
    int (*resume)(struct device *dev);
    int (*freeze)(struct device *dev);
    int (*thaw)(struct device *dev);
    int (*poweroff)(struct device *dev);
    int (*restore)(struct device *dev);
    
    /* 延迟回调（IRQ仍可用） */
    int (*suspend_late)(struct device *dev);
    int (*resume_early)(struct device *dev);
    int (*freeze_late)(struct device *dev);
    int (*thaw_early)(struct device *dev);
    int (*poweroff_late)(struct device *dev);
    int (*restore_early)(struct device *dev);
    
    /* 无IRQ回调（IRQ已禁用） */
    int (*suspend_noirq)(struct device *dev);
    int (*resume_noirq)(struct device *dev);
    int (*freeze_noirq)(struct device *dev);
    int (*thaw_noirq)(struct device *dev);
    int (*poweroff_noirq)(struct device *dev);
    int (*restore_noirq)(struct device *dev);
    
    /* Runtime PM回调 */
    int (*runtime_suspend)(struct device *dev);
    int (*runtime_resume)(struct device *dev);
    int (*runtime_idle)(struct device *dev);
};
```

### 回调函数优先级

PM Core按以下顺序查找并执行回调：

1. **Power Domain** (`dev->pm_domain->ops`)
2. **Device Type** (`dev->type->pm`)
3. **Device Class** (`dev->class->pm`)
4. **Device Bus** (`dev->bus->pm`)
5. **Device Driver** (`dev->driver->pm`)

**注意**：找到第一个匹配的回调即停止搜索，不会级联执行。

### 完整驱动示例

```c
#include <linux/module.h>
#include <linux/platform_device.h>
#include <linux/pm_runtime.h>

struct my_device {
    void __iomem *base;
    struct clk *clk;
    u32 saved_reg;  /* 用于保存寄存器状态 */
};

/* Runtime Suspend */
static int my_runtime_suspend(struct device *dev)
{
    struct my_device *mydev = dev_get_drvdata(dev);
    
    /* 保存寄存器状态 */
    mydev->saved_reg = readl(mydev->base + REG_CTRL);
    
    /* 关闭时钟 */
    clk_disable_unprepare(mydev->clk);
    
    /* 关闭电源（如有） */
    /* regulator_disable(mydev->reg); */
    
    return 0;
}

/* Runtime Resume */
static int my_runtime_resume(struct device *dev)
{
    struct my_device *mydev = dev_get_drvdata(dev);
    int ret;
    
    /* 使能时钟 */
    ret = clk_prepare_enable(mydev->clk);
    if (ret)
        return ret;
    
    /* 恢复寄存器状态 */
    writel(mydev->saved_reg, mydev->base + REG_CTRL);
    
    return 0;
}

/* System Suspend */
static int my_suspend(struct device *dev)
{
    struct my_device *mydev = dev_get_drvdata(dev);
    
    /* 如果设备处于runtime suspended，可能需要先恢复 */
    if (pm_runtime_suspended(dev)) {
        /* 设备已在低功耗状态，但可能需要调整唤醒设置 */
    }
    
    /* 保存完整状态 */
    mydev->saved_reg = readl(mydev->base + REG_CTRL);
    
    /* 关闭时钟和电源 */
    clk_disable_unprepare(mydev->clk);
    
    return 0;
}

/* System Resume */
static int my_resume(struct device *dev)
{
    struct my_device *mydev = dev_get_drvdata(dev);
    int ret;
    
    ret = clk_prepare_enable(mydev->clk);
    if (ret)
        return ret;
    
    writel(mydev->saved_reg, mydev->base + REG_CTRL);
    
    /* 恢复后更新Runtime PM状态 */
    pm_runtime_disable(dev);
    pm_runtime_set_active(dev);
    pm_runtime_enable(dev);
    
    return 0;
}

/* dev_pm_ops定义 */
static const struct dev_pm_ops my_pm_ops = {
    .runtime_suspend = my_runtime_suspend,
    .runtime_resume = my_runtime_resume,
    .suspend = my_suspend,
    .resume = my_resume,
    SET_LATE_SYSTEM_SLEEP_PM_OPS(my_suspend_late, my_resume_early)
};

/* 平台驱动定义 */
static struct platform_driver my_driver = {
    .probe = my_probe,
    .remove = my_remove,
    .driver = {
        .name = "my-device",
        .pm = &my_pm_ops,
        .of_match_table = my_of_match,
    },
};

module_platform_driver(my_driver);
```

---

## CPUFreq 子系统

CPUFreq负责在系统运行时动态调整CPU频率和电压，实现DVFS（动态电压频率调整）。

### 核心结构

```c
struct cpufreq_driver {
    char name[CPUFREQ_NAME_LEN];
    unsigned int flags;
    
    /* 初始化 */
    int (*init)(struct cpufreq_policy *policy);
    int (*verify)(struct cpufreq_policy *policy);
    
    /* 设置频率 */
    int (*target)(struct cpufreq_policy *policy,
                  unsigned int target_freq,
                  unsigned int relation);
    int (*target_index)(struct cpufreq_policy *policy,
                        unsigned int index);
    
    /* 获取当前频率 */
    unsigned int (*get)(unsigned int cpu);
    
    /* 电源管理 */
    int (*suspend)(struct cpufreq_policy *policy);
    int (*resume)(struct cpufreq_policy *policy);
    
    /* 属性 */
    struct freq_attr **attr;
};
```

### 驱动实现示例

```c
static struct cpufreq_frequency_table freq_table[] = {
    { 0, 0,  66000 },
    { 0, 0, 133000 },
    { 0, 1, 266000 },
    { 0, 1, 533000 },
    { 0, 2, 800000 },
    { 0, 0, CPUFREQ_TABLE_END },
};

static int my_cpufreq_target_index(struct cpufreq_policy *policy,
                                   unsigned int index)
{
    unsigned int new_freq = freq_table[index].frequency;
    
    /* 设置CPU时钟频率 */
    clk_set_rate(policy->clk, new_freq * 1000);
    
    return 0;
}

static int my_cpufreq_init(struct cpufreq_policy *policy)
{
    policy->clk = clk_get(NULL, "cpu_clk");
    policy->freq_table = freq_table;
    
    return cpufreq_generic_init(policy, freq_table, 100000);
}

static struct cpufreq_driver my_cpufreq_driver = {
    .flags = CPUFREQ_NEED_INITIAL_FREQ_CHECK,
    .verify = cpufreq_generic_frequency_table_verify,
    .target_index = my_cpufreq_target_index,
    .get = cpufreq_generic_get,
    .init = my_cpufreq_init,
    .name = "my-cpufreq",
};

static int __init my_cpufreq_init(void)
{
    return cpufreq_register_driver(&my_cpufreq_driver);
}
module_init(my_cpufreq_init);
```

---

## Regulator 子系统

Regulator子系统用于管理电源稳压器（PMIC、LDO、BUCK等），实现电压和电流的动态调节。

### 架构层次

| 层次 | 功能 | 关键API |
|-----|------|--------|
| 用户接口层 | 供驱动使用的API | `regulator_get()`、`regulator_enable()` |
| Core管理层 | 电压/电流管理、状态记录 | 约束检查、共享管理 |
| 硬件驱动层 | 具体PMIC/LDO操作 | 寄存器读写 |

### 核心API

```c
/* 获取/释放regulator */
struct regulator *regulator_get(struct device *dev, const char *id);
void regulator_put(struct regulator *regulator);

/* 使能/禁用 */
int regulator_enable(struct regulator *regulator);
int regulator_disable(struct regulator *regulator);
int regulator_is_enabled(struct regulator *regulator);

/* 电压操作 */
int regulator_set_voltage(struct regulator *regulator, 
                          int min_uV, int max_uV);
int regulator_get_voltage(struct regulator *regulator);
int regulator_list_voltage(struct regulator *regulator, unsigned selector);

/* 电流操作 */
int regulator_set_current_limit(struct regulator *regulator,
                                int min_uA, int max_uA);
```

### 使用示例

```c
static int my_probe(struct platform_device *pdev)
{
    struct my_device *dev;
    int ret;
    
    dev = devm_kzalloc(&pdev->dev, sizeof(*dev), GFP_KERNEL);
    
    /* 获取regulator */
    dev->vdd = devm_regulator_get(&pdev->dev, "vdd");
    if (IS_ERR(dev->vdd))
        return PTR_ERR(dev->vdd);
    
    /* 设置电压范围 */
    ret = regulator_set_voltage(dev->vdd, 1800000, 3300000);
    if (ret)
        return ret;
    
    /* 使能电源 */
    ret = regulator_enable(dev->vdd);
    if (ret)
        return ret;
    
    platform_set_drvdata(pdev, dev);
    return 0;
}

static int my_remove(struct platform_device *pdev)
{
    struct my_device *dev = platform_get_drvdata(pdev);
    
    regulator_disable(dev->vdd);
    
    return 0;
}
```

---

## 电源域 Power Domain

电源域（Power Domain）是SoC中共享电源资源的设备集合，支持嵌套结构。

### 核心结构

```c
struct generic_pm_domain {
    struct dev_pm_domain domain;      /* PM域操作 */
    const char *name;
    struct list_head gpd_list;        /* 全局链表 */
    
    /* 状态管理 */
    bool status;                      /* 是否开启 */
    unsigned int device_count;        /* 设备数量 */
    unsigned int suspended_count;     /* 挂起设备数 */
    
    /* 电源操作 */
    int (*power_off)(struct generic_pm_domain *domain);
    int (*power_on)(struct generic_pm_domain *domain);
    
    /* 设备管理 */
    struct device *(*attach_dev)(struct device *dev);
    void (*detach_dev)(struct device *dev);
};
```

### 设备与电源域关联

```c
/* 在设备树中定义电源域 */
&device_node {
    power-domains = <&power_domain_0>;
};

/* 驱动中获取电源域 */
static int my_probe(struct platform_device *pdev)
{
    struct device *dev = &pdev->dev;
    
    /* 设备自动关联power-domains属性指定的电源域 */
    /* 电源域的power_on会在设备probe时自动调用 */
    
    return 0;
}
```

---

## 驱动开发实践

### 最佳实践清单

1. **始终实现Runtime PM**：即使设备不支持硬件断电，也应实现Runtime PM回调以配合系统睡眠
2. **正确使用使用计数**：`get`/`put`必须成对出现，避免引用计数错误
3. **状态保存与恢复**：在suspend中保存设备状态，在resume中恢复
4. **异步操作谨慎使用**：`pm_runtime_get_sync()`在原子上下文外使用，`pm_runtime_get()`在中断上下文使用
5. **处理嵌套电源域**：确保父设备先于子设备恢复，后于子设备挂起

### 常见陷阱

```c
/* 错误：忘记处理Runtime PM和System Sleep的交互 */
static int my_suspend(struct device *dev)
{
    /* 如果设备已被runtime suspended，直接返回可能导致问题 */
    if (pm_runtime_suspended(dev))
        return 0;  /* 错误！可能需要调整唤醒设置 */
}

/* 正确：正确处理runtime suspended设备 */
static int my_suspend(struct device *dev)
{
    if (pm_runtime_suspended(dev)) {
        /* 需要恢复设备以调整唤醒设置，然后再挂起 */
        pm_runtime_resume(dev);
    }
    /* 执行挂起操作 */
}

/* 错误：resume后未更新Runtime PM状态 */
static int my_resume(struct device *dev)
{
    /* 恢复硬件 */
    /* ... */
    /* 忘记更新Runtime PM状态，导致状态不一致 */
}

/* 正确：恢复后同步Runtime PM状态 */
static int my_resume(struct device *dev)
{
    /* 恢复硬件 */
    /* ... */
    pm_runtime_disable(dev);
    pm_runtime_set_active(dev);
    pm_runtime_enable(dev);
}
```

### Smart Suspend优化

设置`DPM_FLAG_SMART_SUSPEND`标志，允许设备在runtime suspended状态下跳过系统挂起回调：

```c
static int my_probe(struct platform_device *pdev)
{
    struct device *dev = &pdev->dev;
    
    /* 设置Smart Suspend标志 */
    dev_pm_set_driver_flags(dev, DPM_FLAG_SMART_SUSPEND);
    
    /* 初始化设备 */
    /* ... */
    
    pm_runtime_enable(dev);
    return 0;
}
```

---

## 调试与工具

### 内核配置

```bash
Power management options  --->
    [*] Power Management support
    [*]   Suspend to RAM and standby
    [*]   Hibernation (aka 'suspend to disk')
    [*]   Device power management core functionality
    [*]   Power Management Debug Support  --->
        [*]     Verbose Power Management debugging
        [*]     Suspend/resume event tracing

CPU Power Management  --->
    CPU Frequency scaling  --->
        [*] CPU Frequency scaling
        [*]   CPU frequency transition statistics
    CPU Idle  --->
        [*] CPU idle PM support
```

### 调试接口

```bash
# 查看系统睡眠状态
cat /sys/power/state
# 输出: freeze mem disk （支持的睡眠状态）

# 触发系统挂起
echo mem > /sys/power/state      # 挂起到RAM
echo freeze > /sys/power/state   # 冻结（浅睡眠）
echo disk > /sys/power/state     # 休眠到磁盘

# 查看设备Runtime PM状态
cat /sys/devices/.../power/runtime_status
# 输出: active suspended unsupported disabled

# 控制设备Runtime PM
echo on > /sys/devices/.../power/control      # 禁止runtime suspend
echo auto > /sys/devices/.../power/control    # 允许runtime suspend

# 查看Runtime PM统计
cat /sys/devices/.../power/runtime_suspended_time
cat /sys/devices/.../power/runtime_active_time

# 强制runtime suspend（调试用）
echo 0 > /sys/devices/.../power/runtime_usage
echo auto > /sys/devices/.../power/control
```

### 调试日志

```bash
# 启用PM调试
echo 'file drivers/base/power/*.c +p' > /sys/kernel/debug/dynamic_debug/control

# 查看PM相关日志
dmesg | grep -i "suspend\|resume\|pm_runtime"

# 使用ftrace跟踪PM操作
echo 1 > /sys/kernel/debug/tracing/events/power/enable
cat /sys/kernel/debug/tracing/trace
```

### 常见问题排查

| 问题 | 可能原因 | 解决方法 |
|-----|---------|---------|
| 系统无法挂起 | 设备拒绝挂起 | 检查`dmesg`中哪个设备返回错误 |
| 设备无法runtime suspend | 使用计数未归零 | 检查`runtime_usage`计数 |
| 唤醒后设备失效 | 状态未正确恢复 | 检查resume回调实现 |
| 功耗未降低 | 时钟/电源未关闭 | 检查`clk_disable`和`regulator_disable`调用 |
| 父设备已挂起但子设备活跃 | 电源域配置错误 | 检查设备树power-domains属性 |

---

## 参考资源

- [Linux内核文档：Runtime PM](https://www.kernel.org/doc/html/latest/power/runtime_pm.html)
- [Linux内核文档：Device PM](https://www.kernel.org/doc/html/latest/driver-api/pm/devices.html)
- [Microchip SAMA5D2低功耗实现指南](https://ww1.microchip.com/downloads/en/Appnotes/SAMA5D2-Low-Power-Modes-Implementation-Application-Note-DS00002896A.pdf)
- [Mastering Linux Device Driver Development - Chapter 10](https://www.booktopia.com.au/mastering-linux-device-driver-development-john-madieu/ebook/9781789342208.html)

---

*文档版本：1.0*  
*最后更新：2026年4月*


这份文档涵盖了Linux电源管理子系统的完整知识体系，包括：

1. **架构总览**：从用户空间到硬件层的完整电源管理架构
2. **系统级电源管理**：Suspend-to-RAM、Hibernate等系统睡眠状态的实现
3. **Runtime PM**：设备级动态电源管理框架，包括使用计数机制和状态转换
4. **设备电源管理**：`struct dev_pm_ops`详解和回调函数优先级
5. **CPUFreq子系统**：动态电压频率调整的实现
6. **Regulator子系统**：电源稳压器管理框架
7. **电源域**：SoC级电源域管理和嵌套结构
8. **驱动开发实践**：完整的驱动示例、最佳实践和常见陷阱
9. **调试工具**：内核配置、调试接口和故障排查方法