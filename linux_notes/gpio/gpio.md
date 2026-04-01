根据搜索结果，我现在可以为您生成一篇关于 Linux GPIO 子系统的专业技术文档。

---

# Linux GPIO 子系统详解

> 作者：资深嵌入式工程师  
> 文档版本：v1.0  
> 适用内核：Linux 4.8+

## 目录
1. [概述](#1-概述)
2. [架构设计](#2-架构设计)
3. [核心数据结构](#3-核心数据结构)
4. [控制器驱动开发](#4-控制器驱动开发)
5. [消费者接口](#5-消费者接口)
6. [用户空间访问](#6-用户空间访问)
7. [设备树配置](#7-设备树配置)
8. [最佳实践](#8-最佳实践)

---

## 1. 概述

GPIO（General Purpose Input/Output）是嵌入式系统中最基础、最常用的硬件接口。Linux 内核提供了完整的 GPIO 子系统，用于统一管理 SoC 内置 GPIO 控制器及外部扩展 GPIO 芯片（如 I2C/SPI 扩展 GPIO）。

**重要提示**：从 Linux 内核 4.8 版本开始，传统的 `/sys/class/gpio` sysfs 接口已被标记为**弃用（deprecated）**。新项目和驱动开发应使用基于字符设备的 `libgpiod` 库或新的描述符 API。

---

## 2. 架构设计

Linux GPIO 子系统采用分层架构设计，主要由以下三层组成：

```
┌─────────────────────────────────────────────────────────┐
│                    消费者驱动层                          │
│    (LED Driver / Key Driver / GPIO 扩展设备驱动)         │
├─────────────────────────────────────────────────────────┤
│                    GPIO 抽象层 (gpiolib)                 │
│         提供统一接口，管理所有 GPIO 控制器                 │
├─────────────────────────────────────────────────────────┤
│                    GPIO 控制器驱动层                     │
│    (SoC GPIO / I2C GPIO 扩展芯片 / SPI GPIO 扩展芯片)    │
├─────────────────────────────────────────────────────────┤
│                    GPIO 硬件层                           │
│              (寄存器 / 中断控制器 / 引脚)                 │
└─────────────────────────────────────────────────────────┘
```

### 2.1 核心组件

| 组件 | 功能说明 | 源码位置 |
|------|----------|----------|
| **gpiolib** | GPIO 核心库，提供注册和管理接口 | `drivers/gpio/gpiolib.c` |
| **gpio_chip** | 描述一个 GPIO 控制器 | `include/linux/gpio/driver.h` |
| **gpio_desc** | 描述单个 GPIO 引脚 | `drivers/gpio/gpiolib.h` |
| **gpio_device** | 控制器设备实例 | 内核内部管理 |

---

## 3. 核心数据结构

### 3.1 struct gpio_chip

`struct gpio_chip` 是 GPIO 控制器驱动的核心数据结构，用于描述一个 GPIO 控制器的硬件特性与操作方法：

```c
#include <linux/gpio/driver.h>

struct gpio_chip {
    const char      *label;           // 控制器名称
    struct device   *parent;          // 父设备指针
    struct module   *owner;
    
    int             (*request)(struct gpio_chip *chip, unsigned offset);
    void            (*free)(struct gpio_chip *chip, unsigned offset);
    
    int             (*get_direction)(struct gpio_chip *chip, unsigned offset);
    int             (*direction_input)(struct gpio_chip *chip, unsigned offset);
    int             (*direction_output)(struct gpio_chip *chip, unsigned offset, int value);
    
    int             (*get)(struct gpio_chip *chip, unsigned offset);
    void            (*set)(struct gpio_chip *chip, unsigned offset, int value);
    void            (*set_multiple)(struct gpio_chip *chip, unsigned long *mask, unsigned long *bits);
    
    int             base;             // 起始 GPIO 编号（-1 表示动态分配）
    u16             ngpio;            // 控制器管理的 GPIO 数量
    bool            can_sleep;        // 操作是否可能休眠（如 I2C/SPI 扩展 GPIO）
    
    struct gpio_irq_chip *irq;        // 中断相关配置
    // ... 其他字段
};
```

### 3.2 关键成员说明

| 成员 | 说明 |
|------|------|
| `base` | 该控制器管理的第一个 GPIO 的全局编号。设为 `-1` 让内核自动分配 |
| `ngpio` | 控制器包含的 GPIO 引脚总数 |
| `can_sleep` | 如果访问该控制器可能休眠（如通过 I2C/SPI 总线），设为 `true`。此时不能在原子上下文（如中断处理程序）中调用 |
| `label` | 控制器标识名称，如 `"imx6ul-gpio1"` |

---

## 4. 控制器驱动开发

### 4.1 注册 GPIO 控制器

控制器驱动需要初始化 `struct gpio_chip` 并注册到内核：

```c
#include <linux/gpio/driver.h>

struct my_gpio_controller {
    struct gpio_chip chip;
    void __iomem *reg_base;
    struct clk *clk;
    // 其他私有数据
};

static int my_gpio_get(struct gpio_chip *chip, unsigned offset)
{
    struct my_gpio_controller *priv = gpiochip_get_data(chip);
    // 读取硬件寄存器获取 GPIO 值
    return readl(priv->reg_base + GPIO_DATA_REG) & BIT(offset);
}

static void my_gpio_set(struct gpio_chip *chip, unsigned offset, int value)
{
    struct my_gpio_controller *priv = gpiochip_get_data(chip);
    u32 reg_val = readl(priv->reg_base + GPIO_DATA_REG);
    
    if (value)
        reg_val |= BIT(offset);
    else
        reg_val &= ~BIT(offset);
    
    writel(reg_val, priv->reg_base + GPIO_DATA_REG);
}

static int my_gpio_direction_output(struct gpio_chip *chip, 
                                    unsigned offset, int value)
{
    struct my_gpio_controller *priv = gpiochip_get_data(chip);
    u32 reg_val = readl(priv->reg_base + GPIO_DIR_REG);
    
    reg_val |= BIT(offset);  // 设为输出
    writel(reg_val, priv->reg_base + GPIO_DIR_REG);
    
    my_gpio_set(chip, offset, value);
    return 0;
}

static int my_gpio_probe(struct platform_device *pdev)
{
    struct my_gpio_controller *priv;
    struct resource *res;
    int ret;
    
    priv = devm_kzalloc(&pdev->dev, sizeof(*priv), GFP_KERNEL);
    if (!priv)
        return -ENOMEM;
    
    // 获取寄存器资源
    res = platform_get_resource(pdev, IORESOURCE_MEM, 0);
    priv->reg_base = devm_ioremap_resource(&pdev->dev, res);
    if (IS_ERR(priv->reg_base))
        return PTR_ERR(priv->reg_base);
    
    // 初始化 gpio_chip
    priv->chip.label = "my-gpio-controller";
    priv->chip.parent = &pdev->dev;
    priv->chip.owner = THIS_MODULE;
    priv->chip.get = my_gpio_get;
    priv->chip.set = my_gpio_set;
    priv->chip.direction_input = my_gpio_direction_input;
    priv->chip.direction_output = my_gpio_direction_output;
    priv->chip.base = -1;        // 动态分配 base
    priv->chip.ngpio = 32;       // 32 个 GPIO
    priv->chip.can_sleep = false; // 寄存器访问，不会休眠
    
    // 注册到内核
    ret = devm_gpiochip_add_data(&pdev->dev, &priv->chip, priv);
    if (ret) {
        dev_err(&pdev->dev, "Failed to register GPIO chip\n");
        return ret;
    }
    
    platform_set_drvdata(pdev, priv);
    return 0;
}

static const struct of_device_id my_gpio_of_match[] = {
    { .compatible = "myvendor,my-gpio", },
    { }
};
MODULE_DEVICE_TABLE(of, my_gpio_of_match);

static struct platform_driver my_gpio_driver = {
    .probe = my_gpio_probe,
    .driver = {
        .name = "my-gpio",
        .of_match_table = my_gpio_of_match,
    },
};
module_platform_driver(my_gpio_driver);
```

### 4.2 中断支持

GPIO 控制器通常也作为中断控制器使用。需要配置 `struct gpio_irq_chip`：

```c
static int my_gpio_irq_set_type(struct irq_data *d, unsigned int type)
{
    // 配置触发类型：上升沿、下降沿、双边沿、电平触发
    return 0;
}

static void my_gpio_irq_handler(struct irq_desc *desc)
{
    struct gpio_chip *chip = irq_desc_get_handler_data(desc);
    struct my_gpio_controller *priv = gpiochip_get_data(chip);
    
    // 读取中断状态寄存器，确定哪个引脚触发
    u32 pending = readl(priv->reg_base + GPIO_IRQ_STATUS);
    
    // 遍历所有置位的中断，调用对应的 handler
    for_each_set_bit(offset, &pending, chip->ngpio) {
        generic_handle_irq(irq_find_mapping(chip->irq.domain, offset));
    }
    
    // 清除中断状态
    writel(pending, priv->reg_base + GPIO_IRQ_STATUS);
}

static int my_gpio_probe(struct platform_device *pdev)
{
    // ... 前面的初始化代码 ...
    
    // 设置中断支持
    struct gpio_irq_chip *girq = &priv->chip.irq;
    girq->chip = &my_gpio_irq_chip;
    girq->parent_handler = my_gpio_irq_handler;
    girq->num_parents = 1;
    girq->parents = devm_kcalloc(&pdev->dev, 1, sizeof(*girq->parents), GFP_KERNEL);
    if (!girq->parents)
        return -ENOMEM;
    girq->parents[0] = platform_get_irq(pdev, 0);
    girq->default_type = IRQ_TYPE_NONE;
    girq->handler = handle_simple_irq;
    
    ret = devm_gpiochip_add_data(&pdev->dev, &priv->chip, priv);
    // ...
}
```

---

## 5. 消费者接口

驱动程序作为 GPIO 消费者时，应使用描述符-based API（`gpiod_*` 函数），而非传统的整数-based API。

### 5.1 新旧 API 对比

| 特性 | 旧 API (`gpio_*`) | 新 API (`gpiod_*`) |
|------|-------------------|-------------------|
| 标识方式 | 全局 GPIO 编号（如 `120`） | `struct gpio_desc` 描述符 |
| 设备树支持 | 不友好，需手动解析 | 原生支持，自动映射 |
| 资源管理 | 手动 `gpio_request/free` | 自动释放（`devm_*` 版本） |
| 休眠安全 | 无检查 | 提供 `_cansleep` 版本 |
| 状态 | 遗留接口，不推荐 | 官方推荐 |

### 5.2 获取 GPIO 描述符

```c
#include <linux/gpio/consumer.h>

// 从设备树获取 GPIO
struct gpio_desc *gpiod_get(struct device *dev, 
                            const char *con_id,
                            enum gpiod_flags flags);

// 带索引版本（当设备有多个同名 GPIO 时）
struct gpio_desc *gpiod_get_index(struct device *dev,
                                    const char *con_id,
                                    unsigned int idx,
                                    enum gpiod_flags flags);

// 自动资源管理版本（推荐）
struct gpio_desc *devm_gpiod_get(struct device *dev,
                                  const char *con_id,
                                  enum gpiod_flags flags);
```

**flags 参数**：
- `GPIOD_ASIS`：不初始化，后续手动设置方向
- `GPIOD_IN`：初始化为输入
- `GPIOD_OUT_LOW` / `GPIOD_OUT_HIGH`：初始化为输出，并设置初始值
- `GPIOD_OUT_LOW_OPEN_DRAIN`：开漏输出

### 5.3 使用示例

```c
static int led_driver_probe(struct platform_device *pdev)
{
    struct led_priv *priv;
    int ret;
    
    priv = devm_kzalloc(&pdev->dev, sizeof(*priv), GFP_KERNEL);
    
    // 从设备树获取 "led" GPIO，初始化为输出低电平
    priv->led_gpio = devm_gpiod_get(&pdev->dev, "led", GPIOD_OUT_LOW);
    if (IS_ERR(priv->led_gpio)) {
        ret = PTR_ERR(priv->led_gpio);
        if (ret != -EPROBE_DEFER)
            dev_err(&pdev->dev, "Failed to get LED GPIO\n");
        return ret;
    }
    
    // 设置 GPIO 值（考虑设备树中的 active-low 属性）
    gpiod_set_value(priv->led_gpio, 1);  // 逻辑 1 = 有效电平
    
    // 如果需要获取物理电平（忽略 active-low）
    gpiod_set_raw_value(priv->led_gpio, 1);  // 物理高电平
    
    return 0;
}
```

### 5.4 GPIO 数组操作

当设备需要多个 GPIO 时：

```c
// 获取 GPIO 数组
struct gpio_descs *gpiod_get_array(struct device *dev,
                                    const char *con_id,
                                    enum gpiod_flags flags);

// 使用示例
struct gpio_descs *leds;
int i;

leds = devm_gpiod_get_array(&pdev->dev, "led", GPIOD_OUT_LOW);
if (IS_ERR(leds))
    return PTR_ERR(leds);

// 批量设置所有 LED
for (i = 0; i < leds->ndescs; i++) {
    gpiod_set_value(leds->desc[i], 1);
}

// 原子方式批量设置（如果硬件支持）
gpiod_set_array_value(leds->ndescs, leds->desc, values);
```

### 5.5 中断使用

```c
// 将 GPIO 转换为 IRQ 号
int irq = gpiod_to_irq(priv->button_gpio);
if (irq < 0)
    return irq;

// 申请中断
ret = request_irq(irq, button_irq_handler, 
                  IRQF_TRIGGER_FALLING | IRQF_TRIGGER_RISING,
                  "my-button", priv);
```

### 5.6 休眠安全判断

对于可能通过慢速总线（I2C/SPI）访问的 GPIO 扩展芯片，必须使用 `_cansleep` 版本：

```c
// 判断该 GPIO 操作是否可能休眠
if (gpiod_cansleep(priv->gpio))
    gpiod_set_value_cansleep(priv->gpio, 1);  // 可以在进程上下文使用
else
    gpiod_set_value(priv->gpio, 1);           // 可以在中断上下文使用
```

---

## 6. 用户空间访问

### 6.1 现代接口：libgpiod

从 Linux 4.8 开始，推荐使用字符设备接口 `/dev/gpiochipN` 配合 `libgpiod` 库。

**命令行工具**：
```bash
# 查看系统中所有 GPIO 控制器
gpiodetect

# 查看某个 chip 的所有 line 信息
gpioinfo gpiochip0

# 设置 GPIO 输出
gpioset gpiochip0 23=1   # 设置 gpiochip0 line 23 为高
gpioset gpiochip0 23=0   # 设置 gpiochip0 line 23 为低

# 读取 GPIO 输入
gpioget gpiochip0 24

# 监听 GPIO 事件（中断）
gpiomon --rising gpiochip0 24
```

**C API 示例**：
```c
#include <gpiod.h>

struct gpiod_chip *chip;
struct gpiod_line *line;
int ret;

// 打开 GPIO 控制器
chip = gpiod_chip_open("/dev/gpiochip0");
if (!chip)
    return -1;

// 获取指定 line
line = gpiod_chip_get_line(chip, 23);
if (!line) {
    gpiod_chip_close(chip);
    return -1;
}

// 请求为输出
ret = gpiod_line_request_output(line, "my-app", 0);
if (ret < 0)
    goto cleanup;

// 设置值
gpiod_line_set_value(line, 1);

cleanup:
    gpiod_line_release(line);
    gpiod_chip_close(chip);
```

### 6.2 sysfs 接口（已弃用）

**警告**：`/sys/class/gpio` 接口已在 Linux 4.8+ 中弃用，新系统可能已完全移除。

```bash
# 旧方法（不推荐）
echo 23 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio23/direction
echo 1 > /sys/class/gpio/gpio23/value
echo 23 > /sys/class/gpio/unexport
```

---

## 7. 设备树配置

### 7.1 GPIO 控制器节点

```dts
gpio0: gpio@20ac000 {
    compatible = "myvendor,my-gpio";
    reg = <0x020ac000 0x4000>;
    interrupts = <GIC_SPI 66 IRQ_TYPE_LEVEL_HIGH>;
    gpio-controller;
    #gpio-cells = <2>;          // 引用时需要 2 个参数：controller, flags
    interrupt-controller;
    #interrupt-cells = <2>;
    clocks = <&clkc 67>;
};
```

### 7.2 GPIO 消费者节点

```dts
leds {
    compatible = "gpio-leds";
    
    led-red {
        gpios = <&gpio0 23 GPIO_ACTIVE_LOW>;  // gpio0, line 23, 低电平有效
        default-state = "off";
        linux,default-trigger = "heartbeat";
    };
};

my-device {
    compatible = "myvendor,my-device";
    
    // 单个 GPIO
    reset-gpios = <&gpio0 15 GPIO_ACTIVE_HIGH>;
    
    // 多个 GPIO（同名）
    led-gpios = <&gpio0 20 GPIO_ACTIVE_LOW>,
                <&gpio0 21 GPIO_ACTIVE_LOW>;
    
    // 带中断的 GPIO
    button-gpios = <&gpio0 24 GPIO_ACTIVE_LOW>;
};
```

### 7.3 常用 GPIO 标志

| 标志 | 说明 |
|------|------|
| `GPIO_ACTIVE_HIGH` | 高电平有效（默认） |
| `GPIO_ACTIVE_LOW` | 低电平有效 |
| `GPIO_OPEN_DRAIN` | 开漏输出 |
| `GPIO_OPEN_SOURCE` | 开源输出 |
| `GPIO_PULL_UP` / `GPIO_PULL_DOWN` | 内部上拉/下拉（需硬件支持） |

---

## 8. 最佳实践

### 8.1 驱动开发建议

1. **始终使用描述符 API**：新驱动应使用 `gpiod_*` 函数，而非遗留的 `gpio_*` 函数
2. **使用 devm_ 版本**：利用设备资源管理自动释放 GPIO，避免资源泄漏
3. **正确处理错误**：检查 `IS_ERR()` 并正确处理 `-EPROBE_DEFER`
4. **考虑休眠安全**：对于可能休眠的 GPIO（如 I2C 扩展），使用 `_cansleep` 版本
5. **逻辑电平 vs 物理电平**：理解 `gpiod_set_value()` 会考虑设备树中的 `active-low` 属性，而 `gpiod_set_raw_value()` 直接操作物理电平

### 8.2 用户空间建议

1. **迁移到 libgpiod**：新项目不要使用 sysfs 接口
2. **使用 chip+line 定位**：不要依赖 GPIO 全局编号，应通过 `/dev/gpiochipN` + line offset 定位
3. **批量操作优先**：使用 `gpiod_line_bulk` 或 `gpiod_set_array_value` 进行原子批量操作

### 8.3 调试技巧

```bash
# 查看 GPIO 使用情况
cat /sys/kernel/debug/gpio

# 查看控制器信息
ls /sys/bus/gpio/devices/
cat /sys/class/gpio/gpiochip*/label
cat /sys/class/gpio/gpiochip*/base
cat /sys/class/gpio/gpiochip*/ngpio
```

---

## 参考文档

-  Documentation/gpio/consumer.txt - Linux 内核官方文档
-  野火嵌入式 Linux 驱动开发实战指南 - GPIO 子系统架构
-  Linux 设备驱动开发 - GPIO 控制器驱动程序详解
-  RK3588 GPIO 驱动分析 - 数据结构关系
-  Toradex GPIO (Linux) 开发指南 - libgpiod 使用
-  Red Hat - GPIO Sysfs 接口弃用说明
-  Linux 驱动编程 - gpio、gpiod 函数详解
-  Linux 驱动编程 - 逻辑电平与物理电平区别

---

*本文档基于 Linux 内核 5.x/6.x 编写，适用于现代嵌入式 Linux 开发。*