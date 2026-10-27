| 分类 | 技术栈条目 | 掌握程度 |
|---|---|---|
| 编程语言 | C 语言（指针、内存模型、位操作、volatile/static/const） | |
| 编程语言 | C++（了解，能读写简单类） | |
| 编程语言 | 汇编（能读懂启动代码、异常向量、链接脚本） | |

| 工具链与构建 | 交叉编译链（gcc/ld/binutils、float-abi、multilib） | |
| 工具链与构建 | Makefile / CMake / Kconfig | |
| 工具链与构建 | U-Boot 与 Kernel 构建流程 | |
| 工具链与构建 | objdump / readelf / nm / addr2line / strip | |

| 版本管理与工程规范 | Git（分支、rebase、cherry-pick、patch 管理） | |
| 版本管理与工程规范 | 代码规范：checkpatch / sparse / commit message | |
| 版本管理与工程规范 | 版本发布：tag、changelog、补丁回合 | |

| 根文件系统构建 | BusyBox / 基础命令集 | |
| 根文件系统构建 | Buildroot | |
| 根文件系统构建 | Yocto / OpenEmbedded（了解） | |
| 根文件系统构建 | rootfs 分区规划与挂载流程 | |
| 根文件系统构建 | 打包烧录镜像（tar / ext4 / ubi / img） | |

| 硬件基础与仪器 | 原理图 / datasheet / TRM 阅读 | |
| 硬件基础与仪器 | 示波器 / 逻辑分析仪 / 万用表 | |
| 硬件基础与仪器 | 焊接飞线、电平转换、上下拉与开漏 | |
| 硬件基础与仪器 | 上电时序 / 复位时序 / 电源树 / 时钟树 | |

| 体系结构与固件 | ARMv7/v8 或 RISC-V 架构与异常模型 | |
| 体系结构与固件 | MMU / 页表 / Cache / TLB / 内存屏障 | |
| 体系结构与固件 | GIC（或 PLIC）中断控制器 | |
| 体系结构与固件 | PSCI / SMC / SMP 多核启动 | |
| 体系结构与固件 | 厂商 boot flow 与 SDK（rkbin / imx-mkimage 等） | |

| Bootloader 与启动 | BootROM / SPL / FSBL / TF-A（BL31） | |
| Bootloader 与启动 | U-Boot：配置、命令、环境变量、设备树、启动脚本 | |
| Bootloader 与启动 | DDR 初始化与调试 | |
| Bootloader 与启动 | Flash / eMMC / SD / UFS 初始化 | |
| Bootloader 与启动 | Kernel 启动流程与 initcall | |
| Bootloader 与启动 | RootFS 挂载与 init 流程 | |
| Bootloader 与启动 | USB / 串口烧录与量产烧录方式 | |

| 内核配置与设备树 | menuconfig / Kconfig / defconfig | |
| 内核配置与设备树 | 设备树语法、dtc 编译、overlay | |
| 内核配置与设备树 | compatible 匹配与 binding 阅读 | |
| 内核配置与设备树 | 内核模块：insmod/rmmod/modprobe、符号导出 | |

| 内核机制与驱动框架 | 并发控制：spinlock / mutex / semaphore / atomic | |
| 内核机制与驱动框架 | 中断：顶半部 / 底半部 / workqueue / threaded irq | |
| 内核机制与驱动框架 | 时间：timer / hrtimer / clocksource | |
| 内核机制与驱动框架 | 调度与内存管理基础（kmalloc/vmalloc/slab/page） | |
| 内核机制与驱动框架 | DMA / DMA Engine / CMA / cache 一致性 | |
| 内核机制与驱动框架 | Linux 设备模型：bus/device/driver/sysfs/uevent | |
| 内核机制与驱动框架 | platform 驱动与 probe 流程 | |
| 内核机制与驱动框架 | devm/devres、probe deferral、of_* API、request_firmware | |
| 内核机制与驱动框架 | Char 设备驱动（Block 设备了解） | |
| 内核机制与驱动框架 | 常用小框架：misc / hwmon / nvmem / mfd / phy / input | |

| 外设与子系统 | GPIO / gpiod、Pinctrl | |
| 外设与子系统 | I2C、SPI、UART / TTY | |
| 外设与子系统 | PWM、CLK、Regulator / PMIC、RTC、Watchdog | |
| 外设与子系统 | Mailbox、remoteproc / rpmsg（了解） | |
| 外设与子系统 | MTD / SPI-NAND / SPI-NOR | |
| 外设与子系统 | eMMC / SDIO / UFS | |
| 外设与子系统 | USB 子系统、PCIe（视平台） | |
| 外设与子系统 | Ethernet MAC / PHY / MDIO、CAN / CAN-FD | |
| 外设与子系统 | Wi-Fi / BT（SDIO/USB）、4G 模组（ECM/MBIM/QMI） | |
| 外设与子系统 | FrameBuffer、DRM / KMS、MIPI DSI | |
| 外设与子系统 | V4L2、MIPI CSI | |
| 外设与子系统 | ALSA SoC、I2S / PCM | |
| 外设与子系统 | IIO / ADC、Touch、Sensor | |

| 存储与文件系统 | 分区表：cmdlinepart / ofpart / GPT | |
| 存储与文件系统 | ext4 / ubifs / squashfs / overlayfs | |
| 存储与文件系统 | NAND：OOB / ECC、UBI volume、坏块管理 | |
| 存储与文件系统 | eMMC：boot 分区、RPMB、生命周期（了解） | |
| 存储与文件系统 | OTA / 固件升级、A/B 分区与回滚 | |
| 存储与文件系统 | 只读 rootfs / dm-verity（了解） | |

| 电源、热与可靠性 | CPUIdle、suspend / resume、runtime PM | |
| 电源、热与可靠性 | DVFS、功耗测试与测量 | |
| 电源、热与可靠性 | 电源域 / clock gate / wakeup source | |
| 电源、热与可靠性 | Thermal 与 cooling 策略 | |
| 电源、热与可靠性 | 稳定性 / 压力 / 异常掉电测试 | |

| 安全与信任链 | Secure Boot、TrustZone / OP-TEE（了解） | |
| 安全与信任链 | 签名校验、密钥与熔丝（OTP）管理 | |
| 安全与信任链 | anti-rollback、JTAG 锁定（了解） | |

| 调试与问题定位 | printk / dmesg / dynamic_debug、console 配置 | |
| 调试与问题定位 | ftrace / trace-cmd / bootgraph / initcall_debug | |
| 调试与问题定位 | perf、strace、lsof | |
| 调试与问题定位 | kdump / crash、pstore / ramoops、Oops / panic 分析 | |
| 调试与问题定位 | KASAN / lockdep / hung task（了解） | |
| 调试与问题定位 | sysfs / procfs / debugfs、devmem | |
| 调试与问题定位 | i2c-tools / spi-tools、ethtool / tcpdump / iperf | |
| 调试与问题定位 | TFTP / NFS 网络调试、Bus Hound | |
| 调试与问题定位 | git bisect 二分定位、最小复现 | |

| 自动化、量产与质量 | Shell / Python 脚本、sed / awk | |
| 自动化、量产与质量 | 自动烧录 / 自动打包 / CI（GitLab-CI / Jenkins） | |
| 自动化、量产与质量 | 量产工具、产测模式、MAC / SN 写入 | |
| 自动化、量产与质量 | 驱动设计文档、测试用例、移植报告 | |
| 自动化、量产与质量 | Docker 化编译环境（了解） | |

