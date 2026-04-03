# 嵌入式 Linux 调试方法与实践总结

## 一、调试方法全景概览

嵌入式 Linux 调试可分为 **应用层调试**、**内核层调试** 和 **硬件层调试** 三个层次。不同层次的问题需要选用不同的工具和方法。

| 调试层次 | 常用工具 | 适用场景 |
|---------|---------|---------|
| **应用层** | GDB + gdbserver、strace、valgrind | 用户程序崩溃、内存泄漏、性能分析 |
| **内核层** | printk、KGDB、KDB、Kprobes、ftrace | 驱动异常、内核崩溃、系统调用跟踪 |
| **硬件层** | JTAG/OpenOCD、逻辑分析仪 | 启动失败、硬件初始化、底层寄存器调试 |

---

## 二、应用层调试实践

### 2.1 交叉编译与远程 GDB 调试

嵌入式设备资源受限，通常采用 **宿主机交叉编译 + 目标机远程调试** 的模式。

**编译配置：**
```bash
# 使用交叉编译工具链（以 ARM 为例）
aarch64-linux-gnu-gcc -g -O0 myapp.c -o myapp
```

**目标机启动 gdbserver：**
```bash
gdbserver :2345 /path/to/myapp > /tmp/debug.log 2>&1
```

**宿主机连接调试：**
```bash
aarch64-linux-gnu-gdb ./myapp
(gdb) target remote 192.168.1.100:2345
(gdb) break main
(gdb) continue
```

### 2.2 VSCode 图形化远程调试

现代开发更推荐使用 VSCode + 交叉 GDB + gdbserver 的图形化方案，避免在资源受限的开发板上直接运行 GDB。

**配置要点：**
- 主机通过 WSL 或 Linux 环境进行交叉编译
- 使用 `gdb-multiarch` 或对应架构的 GDB 工具链
- VSCode 配置 `launch.json` 指定远程连接参数

---

## 三、内核层调试技术

### 3.1 printk 与动态调试（Dynamic Debug）

最基础但最有效的内核调试手段：

```c
// 传统 printk
printk(KERN_DEBUG "Value: %d\n", value);

// 动态调试（无需重新编译）
// 在运行时开启/关闭特定文件的调试信息
echo 'file driver.c +p' > /sys/kernel/debug/dynamic_debug/control
```

### 3.2 KGDB 源码级内核调试

KGDB 是嵌入式 Linux 内核调试的终极利器，允许像调试用户程序一样在内核源码级别设置断点、单步执行、查看变量。

**内核配置（make menuconfig）：**
```
Kernel hacking  --->
  [*] Kernel debugging
  [*] KGDB: kernel debugger
  [*] KGDB: use kgdb over the serial console
  [*] KGDB: internal test suite
```

**启动参数配置：**
```bash
# 通过 U-Boot 或 GRUB 传递参数
kgdboc=ttyS0,115200 kgdbwait nokaslr
```

| 参数 | 说明 |
|-----|------|
| `kgdboc` | 指定 KGDB 使用的串口和波特率 |
| `kgdbwait` | 内核启动时暂停，等待 GDB 连接 |
| `nokaslr` | 关闭内核地址随机化，便于调试 |

**GDB 连接流程：**
```bash
# 宿主机启动 GDB（使用带符号的 vmlinux）
aarch64-linux-gnu-gdb ./vmlinux

(gdb) set remotebaud 115200
(gdb) target remote /dev/ttyUSB0    # 串口连接
# 或
(gdb) target remote 192.168.1.100:2345  # 网络连接（kgdboe）

(gdb) break my_driver_probe
(gdb) continue
```

**运行时进入 KGDB：**
```bash
# 通过 Magic SysRq 随时触发调试
echo g > /proc/sysrq-trigger
```

### 3.3 KDB 轻量级内核调试器

KDB 内建于内核，无需外部 GDB 连接，适合现场快速诊断：

```bash
# 进入 KDB
echo g > /proc/sysrq-trigger

# KDB 常用命令
bp <addr>          # 设置断点
go                 # 继续执行
md <addr> <count>  # 显示内存
dmesg              # 查看内核日志
```

### 3.4 Kprobes 动态探针

无需修改源码、无需重启即可在任意内核函数插入探针：

```c
// 注册 kprobe
static struct kprobe kp = {
    .symbol_name = "do_fork",
    .pre_handler = handler_pre,
    .post_handler = handler_post,
};
```

适用场景：生产环境问题定位、性能热点分析。

---

## 四、硬件层调试：JTAG/OpenOCD

当系统无法启动或需要调试 Bootloader、底层初始化代码时，需使用 JTAG 调试。

### 4.1 环境搭建

**硬件需求：**
- JTAG 调试器（如 FT2232H、Olimex ARM-USB-OCD-H、ESP-Prog）
- 目标板 JTAG 接口（TCK、TMS、TDI、TDO、GND）

**OpenOCD 配置示例：**
```tcl
# openocd.cfg
interface ftdi
ftdi_device_desc "Dual RS232-HS"
ftdi_vid_pid 0x0403 0x6010

source [find target/stm32f4x.cfg]
transport select swd
adapter speed 4000

init
targets
reset halt
```

### 4.2 调试流程

```bash
# 启动 OpenOCD 服务
openocd -f openocd.cfg

# 另一个终端连接 GDB
gdb-multiarch /path/to/firmware.elf
(gdb) target remote localhost:3333
(gdb) monitor reset halt
(gdb) load
(gdb) continue
```

**OpenOCD 常用命令：**
```gdb
(gdb) monitor halt           # 停止目标
(gdb) monitor reset          # 复位目标
(gdb) monitor flash write_image erase firmware.bin 0x08000000
(gdb) monitor flash verify_image firmware.bin 0x08000000
```

---

## 五、典型问题调试实战

### 5.1 I2C 驱动卡死调试（KGDB 实战）

**问题现象：** I2C 驱动在 probe 时系统重启

**调试步骤：**
```gdb
# 1. 在 probe 函数设置断点
(gdb) b my_i2c_probe
(gdb) c

# 2. 单步执行定位问题
(gdb) s
(gdb) s

# 3. 发现空指针访问
(gdb) p client
$1 = (struct i2c_client *) 0x0

# 4. 查看结构体成员
(gdb) p *client
Cannot access memory at address 0x0
```

**根因：** `read_reg(NULL)` 访问了空指针。

### 5.2 网络中断丢包分析（QEMU + KGDB）

**调试场景：** rtl8139 驱动高并发下丢包

```gdb
# 设置中断处理函数断点
(gdb) b rtl8139_interrupt

# 触发网络流量后命中断点
(gdb) info args
(gdb) p *dev
(gdb) bt          # 查看调用栈
```

---

## 六、调试工具选型建议

| 问题类型 | 首选工具 | 备选方案 |
|---------|---------|---------|
| 用户程序崩溃 | gdbserver + GDB | strace、valgrind |
| 内核模块异常 | KGDB | KDB、printk |
| 启动失败/UBoot | JTAG/OpenOCD | 串口打印 |
| 性能瓶颈 | perf、ftrace | BPF/BCC |
| 内存泄漏 | valgrind | kmemleak |
| 竞态条件 | KGDB + 断点 | Kprobes + 数据断点 |

---

## 七、调试环境安全与优化

### 7.1 安全考虑

```bash
# 使用 SSH 隧道加密调试连接
ssh -L 3333:localhost:3335 user@remote-host

# 防火墙限制调试端口
iptables -A INPUT -p tcp --dport 3333 -s 192.168.1.0/24 -j ACCEPT
iptables -A INPUT -p tcp --dport 3333 -j DROP
```

### 7.2 故障排查 checklist

```bash
# 检查串口设备
ls -l /dev/ttyUSB*
dmesg | grep tty

# 检查网络连通性
ping 192.168.1.100
nc -zv 192.168.1.100 2345

# 验证 OpenOCD 连接
openocd -f interface/ftdi/jtagkey.cfg -c "init; scan_chain; exit"
```

---

## 八、总结

嵌入式 Linux 调试是一项系统工程，需要根据不同场景灵活选用工具：

1. **日常开发**：优先使用 gdbserver + GDB 远程调试应用层代码
2. **内核问题**：配置 KGDB 进行源码级调试，配合 Kprobes 做动态分析
3. **启动/硬件问题**：使用 JTAG + OpenOCD 进行底层调试
4. **生产环境**：利用动态调试（dynamic debug）和 ftrace 进行无侵入式诊断

掌握这些调试技术，能够在最复杂的硬件环境下快速定位问题，是嵌入式工程师的核心竞争力。