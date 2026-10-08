### 嵌入式知识笔记
总结已知知识和经验
找学习目标



## 已知的，熟悉的，了解的
C语言，熟悉
C++，了解
汇编，了解
shell，了解
makefile，了解
git，熟悉


# soc bring up
1. 2700芯片启动流程熟悉，2800和qbit不太了解
2. ddr初始化，flash初始化，mmu初始化
3. 基本的bootloader，包括启动和usb烧录功能，uboot不太熟悉

# linux基础
1. 内核的menuconfig，初步了解
2. 设备树，了解
3. 驱动框架，熟悉
4. 并发控制子系统，互斥锁，自旋锁，熟悉，信号量，原子操作，了解
5. irq子系统，中断顶半部底半部，工作队列，熟悉，软中断，中断线程化，了解
6. time子系统，不了解
7. cache相关知识

# linux核心子系统
13. 内存管理，kmalloc，vmalloc等，初步了解
14. 进程调度，不了解
15. 虚拟文件系统，初步了解
16. 网络接口，初步了解
17. 进程间通信，初步了解

# linux驱动子系统
1. gpio子系统，ip寄存器熟悉，gpio和gpiod子系统了解
2. pinctl子系统，ip寄存器熟悉，pinctl子系统一般
3. tty子系统，uart协议熟悉，ip寄存器熟悉，tty子系统一般，调试工具不了解
4. i2c子系统，协议熟悉，ip寄存器一般，i2c子系统熟悉，调试工具熟悉（gpio扩展模块，触摸按键mcu模块,nfc模块）
5. spi子系统，协议熟悉，IP寄存器一般，spi子系统一般，调试工具不了解（像素屏，spi flash）
6. usb子系统，协议了解，ip寄存器不了解，usb子系统一般，调试工具了解（bushound和usb逻辑分析仪）
7.  pci子系统，不了解
8.  input子系统，熟悉
18. mtd子系统，spi nand了解，mtd子系统一般，调试工具一般
9.  framebuffer子系统，了解
10. clk子系统，了解
11. pwm子系统
12. rtc子系统
13. watchdog子系统
14. sdio，mmc子系统，了解
15. drm子系统，mipi dsi，不了解
16. media子系统，mipi csi，不了解
17. net子系统，can，不了解
18. power子系统，初步了解
19. char子系统
20. block子系统
21. dma子系统


# 文件系统
1. 挂载
2. 卸载
3. 打包生成烧录文件

# 项目管理工具
1. buildroot
2. busybox
3. 交叉编译链



# 硬件基础
1. 原理图
2. 芯片手册


# debug手段
1. 逻辑分析仪，熟悉
2. 示波器，熟悉
3. 反汇编，熟悉
4. JTAG，一般
5. gdb调试，一般
6. tftp传文件，熟悉
7. printk，熟悉



## 未知的，感兴趣的
对 BSP 工程师来说，重点看这些
做芯片原厂 BSP，最常用的是：
架构与启动：arch/arm64/、arch/riscv/、init/
中断与时钟：kernel/irq/、kernel/time/、drivers/clk/
内存与 MM：mm/、arch/*/mm/
设备模型与总线：drivers/base/、drivers/i2c/、drivers/spi/、drivers/pci/、drivers/usb/
常用外设：drivers/gpio/、drivers/pinctrl/、drivers/tty/、drivers/input/、drivers/mtd/、drivers/regulator/、drivers/pwm/、drivers/rtc/、drivers/watchdog/
显示/音视频/网络：drivers/gpu/drm/、drivers/media/、sound/、drivers/net/
电源管理：drivers/power/、kernel/power/、drivers/cpufreq/



整体看，你这份清单已经挺完整了，尤其 I2C、Input、GPIO/Pinctrl、调试工具这几块比较扎实。但面向芯片原厂 BSP，有几个关键缺口：U-Boot、ARM64/启动流程、设备树深度、时钟/电源/复位、DMA、Cache/MMU、内存分配、U-Boot 构建、交叉编译、产测、英文文档阅读。下面按优先级补。

建议优先补：芯片原厂 BSP 高频缺口
缺口   为什么重要   建议补到
U-Boot / SPL / FIT   原厂 BSP 基本绕不开启动、烧录、环境变量、bootcmd、bootargs、SPL、DDR 初始化   至少熟悉 U-Boot 启动流程、常用命令、驱动模型、设备树加载

ARM64 启动流程   你熟悉 2700，但 2800/qbit 不熟悉，面试容易被问到通用流程   BootROM → SPL → U-Boot → Kernel → Rootfs，以及 BL1/BL2/ATF 概念

设备树 DTS/DTSI   原厂需要输出 SDK、参考板支持   会写 compatible、reg、interrupts、clocks、pinctrl、status

时钟/电源/复位/PMIC   SoC bring-up 里比驱动更常见   clk、regulator、reset、pmic、power domain、runtime PM

DMA / Cache / MMU   驱动里数据异常、性能问题多半和它们有关   DMA 映射、cache clean/invalidate、coherent 内存、物理/虚拟地址

内核内存分配   面试高频，驱动里也常用   kmalloc、vmalloc、devm_kzalloc、GFP_KERNEL、GFP_ATOMIC

交叉编译 / 工具链   Buildroot 只是上层，工具链、sysroot、模块编译要懂   会用交叉编译器编译内核模块、驱动、busybox、rootfs

产测 / 量产支持   原厂岗位很看重   烧录、分区、固件打包、产测脚本、稳定性测试、log 分析

你当前清单里可以补强的点

Linux 基础部分

menuconfig：不要只停留在“初步了解”。建议会配置驱动为模块/内置、裁剪不需要的子系统、查看 .config。
设备树：建议从“了解”提升到“能根据原理图改 DTS”。
并发控制：你已经熟悉互斥锁、自旋锁，建议补 原子操作、RCU、内存屏障。面试常问“中断上下文能不能用 mutex/信号量”。
中断子系统：建议补 threaded IRQ、IRQ affinity、/proc/interrupts。
time 子系统：建议了解 clocksource、hrtimer、timer、jiffies、delay、RTC 与系统时间关系。

核心子系统部分

这部分不必全部深入，但 BSP 面试常问：

内存管理：建议知道页表、slab/slub、vmalloc、DMA 内存、OOM。
进程调度：知道 CFS、实时调度、负载、优先级、CPU 亲和性即可。
VFS：知道字符设备、块设备、proc/sysfs、设备节点创建。
网络：至少知道 socket、ifconfig/ip、ethtool、CAN 属于 SocketCAN。
IPC：知道 pipe、FIFO、共享内存、消息队列、signal 即可。

驱动子系统部分

你列得很细，建议这样补：

tty/UART：补 console、earlycon、/dev/ttyS*、stty、minicom、screen。
SPI：补 spi_transfer、spi_message、m25p80/spi-nor、spi-nand。
USB：补 USB gadget、USB host、lsusb、usbmon、枚举流程。
PCIe：至少知道 BAR、枚举、MSI/MSI-X、lspci。
MTD：补 UBI/UBIFS、JFFS2、分区表、坏块管理。
DRM/MIPI DSI：建议了解 panel、bridge、DSI host、KMS 基本概念。
Media/MIPI CSI：了解 V4L2、subdev、sensor、ISP 链路。
CAN：了解 SocketCAN、ip link set can0 up、bitrate、termination。
DMA：补 dmaengine、scatter-gather、DMA 映射 API。
pwm/rtc/watchdog/clk/regulator：这些在 bring-up 里很常见，建议至少知道子系统 API 和用户空间接口。

构建与系统部分

你现在有 Buildroot、Busybox，建议补：

U-Boot 编译与配置：defconfig、menuconfig、环境变量、bootcmd、bootargs。
内核模块编译：M= 外置模块、insmod/rmmod/modprobe。
文件系统类型：ext4、squashfs、UBIFS、JFFS2、initramfs。
init 系统：至少知道 Busybox init、systemd 基本概念。
打包烧录：分区表、raw image、uboot 烧录、fastboot、tftp/nfs 调试。

调试能力部分

你已经不错，可以再补：

printk / dmesg：日志等级、early printk、串口 log。
ftrace / perf：启动慢、中断延迟、驱动耗时定位。
crash / kdump：内核 panic 分析。
strace / ltrace：用户空间问题定位。
JTAG / Trace32：原厂 bring-up 很加分，建议从“一般”提升到“能看寄存器、栈回溯”。
英文文档阅读：原厂岗位非常看重，建议明确写进简历。

可以这样调整你的清单

把你原来的条目升级成更贴近面试的版本：

U-Boot：从“不太熟悉”补到“熟悉启动流程、环境变量、常用命令、SPL/FIT 概念”。
设备树：从“了解”补到“能根据原理图修改 DTS”。
time 子系统：补到“了解 clocksource、hrtimer、timer、delay”。
内存管理：补到“了解页表、slab、vmalloc、DMA 内存、GFP 标志”。
DMA / Cache / MMU：单独列出来，作为 bring-up 必备。
USB / PCIe / CAN / DRM / Media：不需要全部精通，但至少知道子系统归属和基本调试方法。
构建工具：在 Buildroot/Busybox 之外，补 U-Boot 构建、内核模块编译、交叉工具链。
调试：补 printk、dmesg、ftrace、crash、strace、JTAG。

如果你接下来要投芯片原厂 BSP，最建议先补这三块：U-Boot、设备树、ARM64 启动流程 + DDR/Flash 初始化。这三块最容易把你从“驱动工程师”拉到“原厂 BSP 工程师”的画像里。

需要我为你整理U-Boot、设备树和ARM64启动流程的面试高频考点清单，方便你快速备战吗？