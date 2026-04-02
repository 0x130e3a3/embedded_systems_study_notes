我将为您生成一篇关于 Linux 设备树（Device Tree）的详细 Markdown 文档。设备树是嵌入式 Linux 开发的核心技术，我会基于我的知识来编写这份全面的技术文档。


# Linux 设备树（Device Tree）完全指南

## 目录
1. [概述](#概述)
2. [历史背景](#历史背景)
3. [基础语法](#基础语法)
4. [核心概念](#核心概念)
5. [标准属性详解](#标准属性详解)
6. [高级特性](#高级特性)
7. [绑定文档（Bindings）](#绑定文档bindings)
8. [编译与反编译](#编译与反编译)
9. [驱动开发接口](#驱动开发接口)
10. [调试与故障排查](#调试与故障排查)
11. [最佳实践](#最佳实践)

---

## 概述

### 什么是设备树？

设备树（Device Tree）是一种**描述硬件数据结构**的规范，采用树形结构，独立于内核源码，用于向操作系统传递硬件配置信息。

```
┌─────────────────────────────────────────────────────────┐
│                    传统方式（ARM）                        │
│  每个板子一个 mach-xxx.c 文件，硬编码硬件信息              │
│  内核臃肿，N 个板子 = N 个 20,000+ 行的 C 文件            │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                    设备树方式（ARM64/现代 ARM）           │
│  统一的 zImage/Image + 独立的 .dtb 硬件描述文件          │
│  内核精简，N 个板子 = N 个 500-2000 行的 .dts 文件        │
└─────────────────────────────────────────────────────────┘
```

### 核心优势

| 优势 | 说明 |
|------|------|
| **硬件抽象** | 同一内核镜像支持多种硬件平台 |
| **维护简化** | 硬件变更无需重新编译内核 |
| **代码精简** | 移除大量板级支持代码（arch/arm/mach-xxx/） |
| **社区协作** | 硬件厂商独立维护 DTS 文件，上游合并 |
| **动态配置** | 运行时通过 overlay 动态修改硬件配置 |

### 文件类型

| 扩展名 | 类型 | 说明 |
|--------|------|------|
| `.dts` | Device Tree Source | 源文件，人类可读 |
| `.dtsi` | Device Tree Source Include | 被包含的源文件（SoC 级定义） |
| `.dtb` | Device Tree Blob | 二进制 blob，内核实际加载 |
| `.dtbo` | Device Tree Blob Overlay | 动态 overlay 二进制文件 |
| `.yaml` | YAML Binding | 现代绑定文档格式（Linux 5.x+） |

---

## 历史背景

### 演进时间线

```
2005 年 - PowerPC 架构首次引入设备树（继承自 Open Firmware）
    ↓
2010 年 - ARM 架构开始讨论设备树方案
    ↓
2011 年 - Linux 3.1 合并 ARM 设备树支持
    ↓
2012 年 - Linux 3.7 大规模移除 mach-xxx 文件，强制使用 DT
    ↓
2014 年 - ARM64 架构强制要求设备树（无传统板级支持）
    ↓
2016 年 - 引入 Device Tree Overlay 支持（动态配置）
    ↓
2019 年 - YAML 绑定文档成为主流（Linux 5.2+）
    ↓
2023 年 - Device Tree 成为 RISC-V 标准启动方式
```

### 架构支持状态

| 架构 | 状态 | 备注 |
|------|------|------|
| PowerPC | ✅ 原生支持 | 历史最悠久，Open Firmware 继承 |
| ARM 32-bit | ✅ 强制要求 | 2012 年后新板子必须使用 |
| ARM 64-bit | ✅ 强制要求 | 唯一支持的硬件描述方式 |
| RISC-V | ✅ 强制要求 | 与 ARM64 类似 |
| x86/x86_64 | ⚠️ 可选 | 主要用于嵌入式（如 Intel Bay Trail） |
| MIPS | ✅ 支持 | 部分平台使用 |
| ARC | ✅ 支持 | Synopsys 架构 |

---

## 基础语法

### 1. 基本结构

```dts
// 文件：example.dts

// 1. 版本声明（必须）
/dts-v1/;

// 2. 包含头文件（可选）
#include "mysoc.dtsi"
#include <dt-bindings/gpio/gpio.h>

// 3. 根节点（必须，有且仅有一个）
/ {
    // 4. 属性（键值对）
    model = "My Company MyBoard";
    compatible = "mycompany,myboard", "mysoc,soc-generic";
    
    // 5. 子节点
    cpus {
        // ...
    };
    
    memory@80000000 {
        // ...
    };
    
    chosen {
        // ...
    };
    
    aliases {
        // ...
    };
};
```

### 2. 节点命名规则

```dts
// 标准格式：name@address
// name：小写字母、数字、连字符
// address：十六进制地址（可选，用于可寻址设备）

// ✅ 正确示例
serial@101f0000 {
    compatible = "arm,pl011";
};

gpio-keys {
    compatible = "gpio-keys";
};

i2c@1c2ac00 {
    compatible = "allwinner,sun6i-a31-i2c";
};

// ❌ 错误示例
SerialPort@101f0000 {  // 大写字母不允许
    // ...
};

uart 1 {               // 空格不允许，缺少 @ 地址
    // ...
};
```

### 3. 属性类型

| 类型 | 语法 | 示例 | 说明 |
|------|------|------|------|
| **空** | `property;` | `interrupt-controller;` | 存在即真 |
| **字符串** | `property = "value";` | `model = "MyBoard";` | 双引号包裹 |
| **字符串列表** | `property = "a", "b";` | `compatible = "a", "b";` | 逗号分隔 |
| **32位整数** | `property = <0x123>;` | `reg = <0x101f0000>;` | 尖括号，十六进制 |
| **64位整数** | `property = <0x1 0x2>;` | `reg = <0x0 0x80000000>;` | 两个 32 位单元 |
| **布尔** | `property = <1>;` 或 `<0>;` | `status = "okay";` | 通常用字符串形式 |
| **数组** | `property = <1 2 3>;` | `interrupts = <0 1 2>;` | 多个单元格 |
| **字节序列** | `property = [01 02 03];` | `mac-address = [00 11 22 33 44 55];` | 方括号，十六进制 |
| **引用** | `property = <&node>;` | `clocks = <&clk_uart>;` | phandle 引用 |

### 4. 引用与标签

```dts
/ {
    // 定义标签（Label）
    uart0: serial@101f0000 {
        compatible = "arm,pl011";
        status = "disabled";  // 默认禁用
    };
    
    i2c0: i2c@1c2ac00 {
        compatible = "allwinner,sun6i-a31-i2c";
        
        // 使用引用修改其他节点属性
        // 这是节点追加语法（Node addition）
    };
};

// 在根节点外追加/修改节点（必须带 & 标签）
&uart0 {
    status = "okay";           // 启用 uart0
    pinctrl-names = "default";
    pinctrl-0 = <&uart0_pins>; // 引用其他节点
    clocks = <&clk_uart>;      // 引用时钟节点
};

// 引用标签必须在同一文件或包含的文件中定义
```

---

## 核心概念

### 1. compatible（兼容性）

最重要的属性，用于**驱动匹配**。

```dts
// 格式："<厂商>,<型号>", ["<厂商>,<型号2>", ... "<兼容类>"]

// 示例 1：从具体到通用
compatible = "fsl,imx6q-sabresd", "fsl,imx6q", "fsl,imx6";  
// 驱动匹配顺序：imx6q-sabresd → imx6q → imx6（通用 fallback）

// 示例 2：多厂商兼容
compatible = "ti,am335x-bone-black", "ti,am335x-bone", "ti,am33xx";

// 示例 3：驱动中的匹配
// drivers/i2c/busses/i2c-imx.c
static const struct of_device_id i2c_imx_dt_ids[] = {
    { .compatible = "fsl,imx21-i2c", .data = &imx21_i2c_data, },
    { .compatible = "fsl,imx6q-i2c", .data = &imx6q_i2c_data, },
    { /* sentinel */ }
};
MODULE_DEVICE_TABLE(of, i2c_imx_dt_ids);
```

### 2. reg（寄存器地址）

描述设备的**可寻址资源**。

```dts
// 简单地址（32位系统）
serial@101f0000 {
    compatible = "arm,pl011";
    reg = <0x101f0000 0x1000>;  // 起始地址 0x101f0000，大小 0x1000
};

// 64位地址（需要两个单元格表示地址）
memory@80000000 {
    device_type = "memory";
    reg = <0x0 0x80000000 0x0 0x20000000>;  
    // 起始地址 0x0 0x80000000（64位），大小 0x20000000
};

// 多段地址（某些设备有多个寄存器区域）
ethernet@1c30000 {
    reg = <0x01c30000 0x10000>,   // 主寄存器
          <0x01c19000 0x1000>;    // MDIO 寄存器
    reg-names = "eth", "mdio";    // 命名，驱动中通过名称获取
};

// 带地址空间标识（PCI 等复杂总线）
pci@1f00000 {
    reg = <0x01f00000 0x1000>;           // 配置空间
    ranges = <0x81000000 0 0 0x01f10000 0x10000>,  // IO 空间
             <0x82000000 0 0x20000000 0x20000000 0x10000000>; // MEM 空间
};
```

### 3. interrupts（中断）

```dts
// 标准中断描述（GIC 中断控制器）
gic: interrupt-controller@1c80000 {
    compatible = "arm,cortex-a9-gic";
    interrupt-controller;
    #interrupt-cells = <3>;  // 需要 3 个单元格描述中断
};

// 使用中断的设备
uart@1c28000 {
    compatible = "ns16550a";
    interrupts = <GIC_SPI 24 IRQ_TYPE_LEVEL_HIGH>;  
    // <中断类型 中断号 触发方式>
    // GIC_SPI: 共享外设中断
    // 24: 中断号
    // IRQ_TYPE_LEVEL_HIGH: 高电平触发
};

// 中断类型定义（include/dt-bindings/interrupt-controller/irq.h）
#define IRQ_TYPE_NONE           0
#define IRQ_TYPE_EDGE_RISING    1
#define IRQ_TYPE_EDGE_FALLING   2
#define IRQ_TYPE_EDGE_BOTH      (IRQ_TYPE_EDGE_FALLING | IRQ_TYPE_EDGE_RISING)
#define IRQ_TYPE_LEVEL_HIGH     4
#define IRQ_TYPE_LEVEL_LOW      8
```

### 4. clocks（时钟）

```dts
// 时钟控制器
clocks {
    #address-cells = <1>;
    #size-cells = <0>;
    
    osc24m: osc24m {
        compatible = "fixed-clock";
        clock-frequency = <24000000>;
        clock-output-names = "osc24m";
        #clock-cells = <0>;  // 引用时不需要额外参数
    };
    
    pll1: pll1@0 {
        compatible = "allwinner,sun6i-a31-pll1-clk";
        reg = <0>;
        clocks = <&osc24m>;
        clock-output-names = "pll1";
        #clock-cells = <1>;  // 引用时需要 1 个参数（分频等）
    };
    
    clk_uart: clk_uart@2 {
        compatible = "allwinner,sun6i-a31-gates-clk";
        reg = <2>;
        clocks = <&pll1>;
        clock-output-names = "uart";
        #clock-cells = <0>;
    };
};

// 使用时钟
uart0: uart@1c28000 {
    compatible = "snps,dw-apb-uart";
    clocks = <&clk_uart>;  // 引用时钟节点
    clock-names = "baudclk";  // 驱动中通过名称识别
};
```

### 5. pinctrl（引脚控制）

详见 [pinctrl 子系统文档](pinctrl.md)，此处为快速参考：

```dts
// 定义引脚配置
&pinctrl {
    uart0_pins: uart0-pins {
        pins = "PA0", "PA1";
        function = "uart0";
        bias-pull-up;
    };
};

// 设备引用
&uart0 {
    pinctrl-names = "default", "sleep";
    pinctrl-0 = <&uart0_pins>;
    pinctrl-1 = <&uart0_sleep_pins>;
};
```

### 6. 总线架构

```dts
// SoC 级定义（mysoc.dtsi）
/ {
    cpus {
        #address-cells = <1>;
        #size-cells = <0>;
        
        cpu@0 {
            compatible = "arm,cortex-a53";
            reg = <0>;
        };
    };
    
    soc {
        compatible = "simple-bus";  // 简单总线，自动扫描子节点
        #address-cells = <2>;
        #size-cells = <2>;
        ranges;  // 1:1 映射，子节点地址直接等于 CPU 视角地址
        
        uart0: serial@7e215040 {
            compatible = "brcm,bcm2835-aux-uart";
            reg = <0x0 0x7e215040 0x0 0x40>;
            interrupts = <GIC_SPI 93 IRQ_TYPE_LEVEL_HIGH>;
            clocks = <&aux_uart_clk>;
        };
        
        i2c0: i2c@7e205000 {
            compatible = "brcm,bcm2835-i2c";
            reg = <0x0 0x7e205000 0x0 0x1000>;
            interrupts = <GIC_SPI 85 IRQ_TYPE_LEVEL_HIGH>;
            clocks = <&i2c_clk>;
            
            // I2C 设备作为子节点
            touchscreen@5d {
                compatible = "goodix,gt911";
                reg = <0x5d>;
                interrupt-parent = <&gpio>;
                interrupts = <25 IRQ_TYPE_EDGE_FALLING>;
            };
        };
    };
};

// 板级定义（myboard.dts）
#include "mysoc.dtsi"

/ {
    model = "MyBoard Version 1.0";
    compatible = "mycompany,myboard", "mysoc,soc-generic";
    
    // 追加内存信息
    memory@80000000 {
        device_type = "memory";
        reg = <0x0 0x80000000 0x0 0x40000000>;  // 1GB RAM
    };
    
    // 选择启动参数
    chosen {
        bootargs = "console=ttyS0,115200 root=/dev/mmcblk0p2 rw rootwait";
        stdout-path = "serial0:115200n8";
    };
    
    // 别名（简化设备路径引用）
    aliases {
        serial0 = &uart0;
        i2c0 = &i2c0;
        ethernet0 = &eth0;
    };
};

// 启用设备（覆盖 status）
&uart0 {
    status = "okay";
    current-speed = <115200>;
};

&i2c0 {
    status = "okay";
    clock-frequency = <400000>;
};
```

---

## 标准属性详解

### 1. 根节点标准属性

| 属性 | 必需 | 说明 |
|------|------|------|
| `model` | 推荐 | 板子人类可读名称 |
| `compatible` | 必须 | 板子兼容性列表 |
| `#address-cells` | 必须 | 子节点地址单元格数（默认 2） |
| `#size-cells` | 必须 | 子节点大小单元格数（默认 2） |

### 2. 设备节点标准属性

| 属性 | 说明 |
|------|------|
| `compatible` | 驱动匹配标识 |
| `reg` | 寄存器地址和大小 |
| `reg-names` | 寄存器区域命名 |
| `interrupts` | 中断描述 |
| `interrupt-parent` | 中断控制器引用 |
| `interrupt-names` | 中断命名 |
| `clocks` | 时钟引用 |
| `clock-names` | 时钟命名 |
| `resets` | 复位信号引用 |
| `reset-names` | 复位信号命名 |
| `power-domains` | 电源域引用 |
| `status` | 状态："okay", "disabled", "reserved", "fail" |
| `phandle` | 节点唯一标识（自动生成或手动指定） |

### 3. 特殊节点

#### chosen（启动参数）

```dts
chosen {
    bootargs = "root=/dev/nfs nfsroot=192.168.1.1:/rootfs rw";
    stdout-path = "serial0:115200n8";
    linux,initrd-start = <0x82000000>;
    linux,initrd-end = <0x83000000>;
    
    // U-Boot 传递的额外参数
    u-boot,version = "2023.01";
};
```

#### aliases（别名）

```dts
aliases {
    // 为长路径创建短别名
    serial0 = &uart0;           // /dev/ttyS0
    serial1 = &uart1;           // /dev/ttyS1
    i2c0 = &i2c_0;              // /dev/i2c-0
    spi0 = &spi_0;              // /dev/spidev0.0
    ethernet0 = &emac;           // eth0
    mmc0 = &sdhci;              // mmcblk0
    
    // 用于确定设备序号
};
```

#### reserved-memory（保留内存）

```dts
reserved-memory {
    #address-cells = <2>;
    #size-cells = <2>;
    ranges;
    
    // CMA（连续内存分配器）区域
    linux,cma {
        compatible = "shared-dma-pool";
        reusable;
        size = <0x0 0x10000000>;  // 256MB
        alignment = <0x0 0x400000>;  // 4MB 对齐
        alloc-ranges = <0x0 0x80000000 0x0 0x40000000>;
    };
    
    // 显存保留
    gpu_reserved: gpu@90000000 {
        compatible = "removed-dma-pool";
        no-map;
        reg = <0x0 0x90000000 0x0 0x10000000>;  // 256MB @ 0x90000000
    };
    
    // VPU 固件区域
    vpu_firmware: vpu@a0000000 {
        compatible = "removed-dma-pool";
        no-map;
        reg = <0x0 0xa0000000 0x0 0x2000000>;   // 32MB
    };
};

// 设备引用保留内存
&vpu {
    memory-region = <&vpu_firmware>;
};
```

---

## 高级特性

### 1. Device Tree Overlay（动态覆盖）

允许在**运行时**动态修改设备树，无需重新编译。

```dts
// 文件：enable-i2c-rtc.dtso（源文件）

/dts-v1/;
/plugin/;  // 声明为 overlay

/ {
    fragment@0 {
        target-path = "/soc/i2c@7e205000";  // 目标路径
        __overlay__ {
            status = "okay";  // 启用 I2C
            
            rtc@68 {
                compatible = "nxp,pcf8563";
                reg = <0x68>;
            };
        };
    };
    
    fragment@1 {
        target = <&gpio>;  // 通过 phandle 引用
        __overlay__ {
            pinctrl-0 = <&i2c_pins>;
        };
    };
};
```

**编译与应用：**

```bash
# 编译 overlay
dtc -@ -I dts -O dtb -o enable-i2c-rtc.dtbo enable-i2c-rtc.dtso

# 方法一：启动时加载（U-Boot）
setenv overlays "enable-i2c-rtc"
saveenv
boot

# 方法二：运行时加载（Linux 4.10+）
mkdir /sys/kernel/config/device-tree/overlays/enable-rtc
cat enable-i2c-rtc.dtbo > /sys/kernel/config/device-tree/overlays/enable-rtc/dtbo

# 查看应用状态
cat /sys/kernel/config/device-tree/overlays/enable-rtc/status
```

### 2. 符号与 fixups

```dts
// 在 base dts 中声明符号（用于 overlay 引用）
/ {
    symbols {
        i2c0 = "/soc/i2c@7e205000";
        gpio = "/soc/gpio@7e200000";
    };
    
    // __fixups__ 用于运行时地址修正（较少使用）
    __fixups__ {
        i2c0 = "/fragment@0:target:0";
    };
};
```

### 3. 条件编译（C 预处理器）

```dts
// 使用 C 预处理器实现条件编译
#include <dt-bindings/gpio/gpio.h>

#ifdef CONFIG_MYBOARD_V2
    #define UART0_STATUS "disabled"
    #define UART1_STATUS "okay"
#else
    #define UART0_STATUS "okay"
    #define UART1_STATUS "disabled"
#endif

&uart0 {
    status = UART0_STATUS;
};

&uart1 {
    status = UART1_STATUS;
};
```

**Makefile 中定义：**

```makefile
# arch/arm/boot/dts/Makefile
dtb-$(CONFIG_ARCH_MYSOC) += \
    myboard-v1.dtb \
    myboard-v2.dtb

DTC_FLAGS_myboard-v2 += -DCONFIG_MYBOARD_V2
```

### 4. 复杂时钟示例

```dts
// 多时钟设备（如 MMC/SD 需要多个时钟）
&mmc0 {
    compatible = "allwinner,sun50i-h5-mmc";
    reg = <0x01c0f000 0x1000>;
    clocks = <&ccu CLK_BUS_MMC0>, <&ccu CLK_MMC0>;
    clock-names = "ahb", "mmc";
    resets = <&ccu RST_BUS_MMC0>;
    reset-names = "ahb";
    
    // 时钟相位配置（某些平台需要）
    assigned-clocks = <&ccu CLK_MMC0>;
    assigned-clock-rates = <50000000>;  // 50MHz
};
```

---

## 绑定文档（Bindings）

绑定文档定义了设备树节点的**规范**，包括必需属性、可选属性、子节点等。

### 1. 传统 txt 格式（已弃用）

```txt
// Documentation/devicetree/bindings/i2c/i2c-imx.txt
Freescale i2c controller

Required properties:
- compatible: "fsl,imx21-i2c", "fsl,imx6q-i2c", etc.
- reg: I2C register address and length
- interrupts: I2C interrupt
- clocks: I2C clock source

Optional properties:
- clock-frequency: Desired I2C bus clock frequency in Hz (default 100kHz)
- dmas: DMA specifiers for tx and rx
- dma-names: Must be "tx" and "rx"
```

### 2. 现代 YAML 格式（推荐）

```yaml
# Documentation/devicetree/bindings/i2c/fsl,imx21-i2c.yaml
%YAML 1.2
---
$id: http://devicetree.org/schemas/i2c/fsl,imx21-i2c.yaml#
$schema: http://devicetree.org/meta-schemas/core.yaml#

title: Freescale iMX I2C controller

maintainers:
  - Shawn Guo <shawnguo@kernel.org>

properties:
  compatible:
    enum:
      - fsl,imx21-i2c
      - fsl,imx6q-i2c
      - fsl,imx7d-i2c

  reg:
    maxItems: 1

  interrupts:
    maxItems: 1

  clocks:
    maxItems: 1

  clock-frequency:
    description: Desired I2C bus clock frequency in Hz
    default: 100000

required:
  - compatible
  - reg
  - interrupts
  - clocks

additionalProperties: false

examples:
  - |
    i2c@21a0000 {
        compatible = "fsl,imx6q-i2c";
        reg = <0x21a0000 0x4000>;
        interrupts = <0 36 IRQ_TYPE_LEVEL_HIGH>;
        clocks = <&clks IMX6QDL_CLK_I2C1>;
        clock-frequency = <400000>;
    };
```

### 3. 验证绑定

```bash
# 使用 dt-schema 工具验证
pip3 install dtschema
make dt_binding_check DT_SCHEMA_FILES=fsl,imx21-i2c.yaml

# 验证完整设备树
make dtbs_check
```

---

## 编译与反编译

### 1. 工具链

| 工具 | 用途 |
|------|------|
| `dtc` | Device Tree Compiler（编译/反编译） |
| `fdtdump` | 可读格式打印 DTB |
| `fdtget`/`fdtput` | 读取/修改 DTB 属性 |
| `dtmerge` | 合并基础 DTB 和 Overlay |
| `dtdiff` | 比较两个 DTS/DTB |

### 2. 编译命令

```bash
# 基础编译（dts → dtb）
dtc -I dts -O dtb -o output.dtb input.dts

# 带符号（支持 overlay）
dtc -@ -I dts -O dtb -o output.dtb input.dts

# 内核中编译（推荐）
make dtbs                    # 编译所有 DTB
make ARCH=arm dtbs          # 指定架构
make myboard.dtb            # 编译特定板子

# 指定 include 路径
dtc -I dts -O dtb -i /path/to/include -o output.dtb input.dts
```

### 3. 反编译

```bash
# dtb → dts（用于调试）
dtc -I dtb -O dts -o output.dts input.dtb

# 带源码信息（保留 phandle 等）
dtc -I dtb -O dts -o output.dts -f input.dtb

# 查看二进制信息
fdtdump input.dtb | less
```

### 4. 运行时工具

```bash
# 查看当前设备树（sysfs）
ls /sys/firmware/devicetree/base/
cat /sys/firmware/devicetree/base/model
cat /sys/firmware/devicetree/base/compatible
xxd /sys/firmware/devicetree/base/memory@80000000/reg  # 二进制属性

# 查看设备树结构
find /sys/firmware/devicetree/base/ -type d | head -20

# 查看已应用 overlay
ls /sys/kernel/config/device-tree/overlays/
```

---

## 驱动开发接口

### 1. 查询 API

```c
#include <linux/of.h>

// 查找节点
struct device_node *of_find_node_by_path(const char *path);
struct device_node *of_find_node_by_name(struct device_node *from, const char *name);
struct device_node *of_find_compatible_node(struct device_node *from, 
                                            const char *type, 
                                            const char *compat);
struct device_node *of_find_node_by_phandle(phandle handle);

// 示例
struct device_node *np = of_find_node_by_path("/soc/uart@101f0000");
// 或
struct device_node *np = of_find_compatible_node(NULL, NULL, "arm,pl011");

// 遍历子节点
struct device_node *child;
for_each_child_of_node(np, child) {
    // 处理子节点
}

// 读取属性
const char *str;
of_property_read_string(np, "model", &str);

u32 val;
of_property_read_u32(np, "clock-frequency", &val);

u32 array[4];
of_property_read_u32_array(np, "reg", array, 4);

// 读取布尔属性
bool exists = of_property_read_bool(np, "interrupt-controller");

// 获取字符串数组
const char *strs[4];
int count = of_property_count_strings(np, "compatible");
of_property_read_string_array(np, "compatible", strs, count);

// 获取 phandle 引用的节点
struct device_node *clk_np = of_parse_phandle(np, "clocks", 0);
```

### 2. 资源获取 API

```c
#include <linux/of_address.h>
#include <linux/of_irq.h>
#include <linux/of_gpio.h>

// 内存资源（自动处理 ranges 映射）
struct resource res;
of_address_to_resource(np, 0, &res);  // 第 0 个 reg 项
void __iomem *base = of_iomap(np, 0);   // 直接映射

// 或 devm 版本
struct resource *res = platform_get_resource(pdev, IORESOURCE_MEM, 0);
void __iomem *base = devm_ioremap_resource(&pdev->dev, res);

// 中断
unsigned int irq = irq_of_parse_and_map(np, 0);  // 第 0 个 interrupts 项
// 或
unsigned int irq = of_irq_get(np, 0);

// 或 devm 版本
int irq = platform_get_irq(pdev, 0);

// GPIO
#include <linux/of_gpio.h>
int gpio = of_get_gpio(np, 0);  // 第 0 个 gpios 项
int gpio = of_get_named_gpio(np, "reset-gpio", 0);  // 通过名称

// 或 devm 版本
int gpio = devm_gpiod_get(&pdev->dev, "reset", GPIOD_OUT_HIGH);
```

### 3. 平台设备匹配

```c
#include <linux/platform_device.h>
#include <linux/of_device.h>

// 设备 ID 表（传统方式）
static const struct platform_device_id my_drv_ids[] = {
    { "mydevice", (kernel_ulong_t)&my_data_v1 },
    { "mydevice-v2", (kernel_ulong_t)&my_data_v2 },
    { },
};

// 设备树匹配表（现代方式）
static const struct of_device_id my_drv_dt_ids[] = {
    { .compatible = "mycompany,mydevice-v1", .data = &my_data_v1 },
    { .compatible = "mycompany,mydevice-v2", .data = &my_data_v2 },
    { },
};
MODULE_DEVICE_TABLE(of, my_drv_dt_ids);

static struct platform_driver my_driver = {
    .probe = my_probe,
    .remove = my_remove,
    .driver = {
        .name = "my-driver",
        .of_match_table = my_drv_dt_ids,  // 设备树匹配
    },
    .id_table = my_drv_ids,  // 传统匹配（fallback）
};

// probe 函数中获取设备树数据
static int my_probe(struct platform_device *pdev)
{
    struct device_node *np = pdev->dev.of_node;  // 设备树节点
    
    if (!np) {
        // 非设备树启动（传统平台设备）
        return -ENODEV;
    }
    
    // 读取属性
    u32 speed;
    of_property_read_u32(np, "speed-hz", &speed);
    
    // 获取资源
    struct resource *mem = platform_get_resource(pdev, IORESOURCE_MEM, 0);
    int irq = platform_get_irq(pdev, 0);
    
    // ...
    return 0;
}
```

### 4. 总线设备（I2C/SPI 示例）

```c
// I2C 设备自动从设备树创建
static const struct of_device_id my_i2c_of_match[] = {
    { .compatible = "mycompany,sensor-v1" },
    { .compatible = "mycompany,sensor-v2" },
    { }
};
MODULE_DEVICE_TABLE(of, my_i2c_of_match);

static struct i2c_driver my_sensor_driver = {
    .driver = {
        .name = "my-sensor",
        .of_match_table = my_i2c_of_match,
    },
    .probe = my_sensor_probe,
    .remove = my_sensor_remove,
};

// probe 中访问设备树
static int my_sensor_probe(struct i2c_client *client)
{
    struct device_node *np = client->dev.of_node;
    
    // 读取自定义属性
    u32 poll_interval;
    of_property_read_u32(np, "poll-interval", &poll_interval);
    
    // 获取 GPIO
    int irq_gpio = of_get_gpio(np, 0);
    
    // ...
    return 0;
}
```

### 5. 设备树节点创建（动态）

```c
#include <linux/of_device.h>

// 动态创建节点（较少使用，通常用于测试）
struct device_node *new_np;
new_np = of_create_node(parent_np, "new-device@0");
of_add_property(new_np, "compatible", "my,dynamic-device", strlen("my,dynamic-device")+1);

// 更常见：使用 overlay
```

---

## 调试与故障排查

### 1. 内核日志

```bash
# 开启设备树调试
echo 'file drivers/of/base.c +p' > /sys/kernel/debug/dynamic_debug/control
echo 'file drivers/of/platform.c +p' >> /sys/kernel/debug/dynamic_debug/control

# 查看启动日志
dmesg | grep -i "of\|device tree\|platform"

# 查看未匹配设备
dmesg | grep "Failed to find"
```

### 2. 常见问题

#### 问题 1：设备未创建

```
// 现象：驱动 probe 未调用，/sys 下无设备节点

// 检查 1：compatible 是否匹配
dmesg | grep "compatible"
// 应显示：of_device_check_compatible: comparing mydrv,dev1 with mycompany,mydevice

// 检查 2：status 是否为 "okay"
cat /sys/firmware/devicetree/base/soc/mydevice@1000000/status
// 如果是 "disabled"，驱动不会加载

// 检查 3：依赖资源是否存在（clock、regulator 等）
dmesg | grep "Failed to get"
```

#### 问题 2：地址映射错误

```
// 现象：寄存器读写失败，内核崩溃

// 检查 reg 属性
xxd /sys/firmware/devicetree/base/soc/uart@101f0000/reg
// 确认大小端、单元格数正确

// 检查 ranges 映射（简单总线）
cat /sys/firmware/devicetree/base/soc/ranges
// 确保子总线地址正确映射到 CPU 物理地址
```

#### 问题 3：中断不触发

```
// 现象：request_irq 成功，但无中断

// 检查 interrupt-parent
cat /sys/firmware/devicetree/base/soc/mydevice/interrupt-parent
// 确认指向正确的中断控制器

// 检查 interrupts 格式
// 查看中断控制器 #interrupt-cells
cat /sys/firmware/devicetree/base/interrupt-controller/#interrupt-cells
// 确保设备 interrupts 属性单元格数匹配
```

### 3. 调试工具脚本

```bash
#!/bin/bash
# dt-debug.sh - 设备树调试助手

echo "=== Device Tree Info ==="
echo "Model: $(cat /sys/firmware/devicetree/base/model 2>/dev/null)"
echo "Compatible: $(cat /sys/firmware/devicetree/base/compatible 2>/dev/null)"

echo ""
echo "=== Active Devices ==="
ls /sys/bus/platform/devices/ | head -10

echo ""
echo "=== Unpopulated Nodes (status != okay) ==="
find /sys/firmware/devicetree/base -name "status" -exec grep -l -v "okay" {} \; 2>/dev/null | head -5

echo ""
echo "=== Overlay Status ==="
if [ -d /sys/kernel/config/device-tree/overlays ]; then
    for dir in /sys/kernel/config/device-tree/overlays/*; do
        [ -d "$dir" ] && echo "$(basename $dir): $(cat $dir/status 2>/dev/null)"
    done
else
    echo "Overlay configfs not mounted"
fi
```

---

## 最佳实践

### 1. 文件组织

```
arch/arm64/boot/dts/
├── vendor/                    # 厂商目录
│   ├── mysoc.dtsi            # SoC 级定义（寄存器、中断、时钟）
│   ├── mysoc-clk.dtsi        # 时钟定义（复杂时分离）
│   ├── mysoc-pinctrl.dtsi    # 引脚定义
│   ├── myboard.dts           # 具体板子（内存、外设启用）
│   └── myboard-v2.dts        # 硬件版本 2
├── include/
│   └── dt-bindings/          # 头文件（寄存器地址、宏定义）
│       ├── clock/
│       ├── gpio/
│       └── interrupt-controller/
```

### 2. 设计原则

| 原则 | 说明 |
|------|------|
| **SoC 与板子分离** | `.dtsi` 描述芯片，`.dts` 描述具体产品 |
| **默认禁用** | SoC 级 `status = "disabled"`，板级启用 |
| **最小板级 DTS** | 板级文件只包含差异（内存、外设选择） |
| **使用标准绑定** | 优先复用内核已有 compatible |
| **完整文档** | 每个自定义属性添加注释 |

### 3. 示例：良好结构

```dts
// mysoc.dtsi - SoC 级（上游维护）
/ {
    compatible = "mysoc,soc-generic";
    #address-cells = <2>;
    #size-cells = <2>;
    interrupt-parent = <&gic>;
    
    cpus { /* ... */ };
    
    soc {
        compatible = "simple-bus";
        ranges;
        
        uart0: serial@1000000 {
            compatible = "mysoc,uart-v1";
            reg = <0x0 0x1000000 0x0 0x1000>;
            interrupts = <GIC_SPI 10 IRQ_TYPE_LEVEL_HIGH>;
            clocks = <&clk_uart0>;
            status = "disabled";  // 默认禁用
        };
        
        // ... 其他外设
    };
};

// myboard.dts - 板级（产品维护）
/dts-v1/;
#include "mysoc.dtsi"

/ {
    model = "MyCompany MyProduct V1.0";
    compatible = "mycompany,myproduct", "mysoc,soc-generic";
    
    // 产品特定硬件
    backlight: backlight {
        compatible = "pwm-backlight";
        pwms = <&pwm0 0 50000>;
        brightness-levels = <0 10 20 50 100>;
        default-brightness-level = <50>;
    };
};

// 启用外设
&uart0 {
    status = "okay";
    current-speed = <115200>;
    pinctrl-0 = <&uart0_console_pins>;
};

&i2c0 {
    status = "okay";
    clock-frequency = <400000>;
    
    touchscreen@5d {
        compatible = "goodix,gt911";
        reg = <0x5d>;
        interrupt-parent = <&gpio0>;
        interrupts = <25 IRQ_TYPE_EDGE_FALLING>;
    };
};
```

### 4. 版本管理

```dts
// 使用 /plugin/ 支持多硬件版本
// myproduct-common.dtsi - 通用部分
// myproduct-v1.dts - 版本 1 特定
// myproduct-v2.dts - 版本 2 特定（使用 overlay 或覆盖）

// 或同一文件内使用条件（简单情况）
/ {
    myproduct-hwrev = <2>;  // 硬件版本标记
};

// 驱动中读取版本适配
u32 hwrev;
of_property_read_u32(np, "myproduct-hwrev", &hwrev);
if (hwrev >= 2) {
    // 版本 2 特定处理
}
```

### 5. 与 bootloader 协作

```dts
// 预留 bootloader 修改区域
/ {
    // U-Boot 会填充这些
    chosen {
        bootargs = "";  // U-Boot 覆盖
        linux,initrd-start = <0>;  // U-Boot 填充
    };
    
    // 内存由 bootloader 探测填充
    memory {
        device_type = "memory";
        reg = <0>;  // U-Boot: fdt set memory reg <0x0 0x80000000 0x0 0x40000000>
    };
};
```

---

## 参考资源

### 官方文档

- `Documentation/devicetree/` - 内核设备树文档目录
- `Documentation/devicetree/usage-model.rst` - 使用模型
- `Documentation/devicetree/bindings/` - 绑定文档（YAML）
- [Device Tree Specification](https://www.devicetree.org/specifications/) - 官方规范

### 工具源码

- `scripts/dtc/` - 内核 DTC 编译器源码
- `include/dt-bindings/` - 标准头文件

### 社区资源

- [Device Tree Wiki](https://elinux.org/Device_Tree)
- [Devicetree Specification GitHub](https://github.com/devicetree-org/devicetree-specification)

---

*文档版本: 2.0*  
*适用内核版本: Linux 4.x - 6.x*  
*最后更新: 2024*
```

这篇文档涵盖了 Linux 设备树的完整知识体系：

1. **基础概念**：历史背景、语法规则、文件类型
2. **核心机制**：compatible 匹配、reg 地址、中断、时钟、pinctrl
3. **高级特性**：Overlay 动态配置、YAML 绑定、条件编译
4. **实战开发**：完整驱动 API 示例（平台设备、I2C、资源获取）
5. **调试技巧**：常见问题排查、调试脚本、内核日志
6. **工程实践**：文件组织、版本管理、SoC/板子分离设计原则

文档采用标准技术文档格式，包含大量代码示例、表格对比和实际命令，适合作为嵌入式 Linux 开发的参考手册。