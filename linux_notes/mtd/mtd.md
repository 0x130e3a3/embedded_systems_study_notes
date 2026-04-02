根据搜索结果，我为您生成一份详细的Linux MTD子系统技术文档：


# Linux MTD 子系统详解

## 目录

1. [概述](#概述)
2. [MTD 与块设备的区别](#mtd-与块设备的区别)
3. [MTD 子系统架构](#mtd-子系统架构)
4. [核心数据结构](#核心数据结构)
5. [MTD 设备驱动开发](#mtd-设备驱动开发)
6. [NAND Flash 驱动开发](#nand-flash-驱动开发)
7. [NOR Flash 驱动开发](#nor-flash-驱动开发)
8. [分区管理](#分区管理)
9. [文件系统集成](#文件系统集成)
10. [调试与工具](#调试与工具)

---

## 概述

MTD（Memory Technology Device，存储技术设备）是Linux内核中专为管理各类非易失性存储设备（如NAND Flash、NOR Flash、EEPROM等）设计的核心子系统。它位于硬件与文件系统之间，提供统一的接口抽象，屏蔽底层Flash物理特性差异。

### 主要特点

- **原始设备访问**：直接暴露Flash的物理特性（按页写入、按块擦除）
- **坏块管理**：自动处理NAND Flash的坏块
- **ECC支持**：硬件/软件纠错码机制
- **磨损均衡**：配合文件系统实现Flash寿命管理
- **分区支持**：支持将Flash划分为多个逻辑分区

### 支持的设备类型

| 设备类型 | 特点 | 典型应用 |
|---------|------|---------|
| **NAND Flash** | 容量大、成本低、存在坏块 | 大容量存储、嵌入式系统 |
| **NOR Flash** | 读取快、可XIP执行、可靠性高 | 代码存储、Bootloader |
| **OneNAND** | 结合NOR和NAND优点 | 移动设备 |
| **SPI NOR/NAND** | 接口简单、引脚少 | 小型嵌入式设备 |

---

## MTD 与块设备的区别

MTD设备与传统块设备（如eMMC、SD卡、硬盘）有本质区别：

| 特性 | MTD设备 | 块设备 |
|-----|---------|--------|
| **擦除操作** | 必须先擦除再写入，擦除单位为块(64KB-256KB) | 直接覆盖写入，无需擦除 |
| **写入粒度** | 按页写入(512B-4KB)，写入前需确保已擦除 | 按扇区写入(512B-4KB) |
| **坏块** | 存在坏块，需跳过或标记 | 无坏块概念，由FTL管理 |
| **寿命** | 擦写次数有限(1k-100k次) | 通常无擦写次数限制 |
| **访问接口** | 原始Flash操作接口 | 标准块设备接口 |
| **文件系统** | JFFS2、UBIFS、YAFFS2 | ext4、FAT32、NTFS |

> **注意**：eMMC、SD卡等虽然内部使用Flash，但包含FTL（Flash Translation Layer）闪存转换层，对外表现为块设备，不属于MTD子系统管理范围。

---

## MTD 子系统架构

MTD子系统采用四层架构设计，实现硬件与上层的完全解耦。

### 架构层次图

```
┌─────────────────────────────────────────────────────────────┐
│                    应用层 (Applications)                     │
│              用户空间工具: flashcp, flash_erase, mtd-utils   │
├─────────────────────────────────────────────────────────────┤
│              MTD 设备层 (MTD Device Layer)                   │
│    ┌──────────────┐    ┌──────────────┐                     │
│    │ 字符设备层    │    │  块设备层     │                     │
│    │ mtdchar.c    │    │  mtdblock.c  │                     │
│    │ /dev/mtd0    │    │  /dev/mtdblock0                  │
│    │ 主设备号90   │    │  主设备号31    │                     │
│    └──────────────┘    └──────────────┘                     │
├─────────────────────────────────────────────────────────────┤
│              MTD 原始设备层 (MTD Raw Device)                 │
│         mtdcore.c (核心接口) / mtdpart.c (分区管理)          │
│              struct mtd_info / struct mtd_partition          │
├─────────────────────────────────────────────────────────────┤
│              Flash 硬件驱动层 (Flash Driver)                 │
│    ┌──────────────┐    ┌──────────────┐                     │
│    │  NAND Flash  │    │   NOR Flash   │                     │
│    │  nand_base.c │    │   cfi_probe.c │                     │
│    │  nand_chip   │    │   map_info    │                     │
│    └──────────────┘    └──────────────┘                     │
├─────────────────────────────────────────────────────────────┤
│                    硬件层 (Hardware)                         │
│              NAND芯片 / NOR芯片 / Flash控制器                │
└─────────────────────────────────────────────────────────────┘
```

### 核心组件说明

| 组件 | 源文件 | 功能描述 |
|-----|--------|---------|
| **MTD Core** | `mtdcore.c` | MTD子系统核心，提供设备注册、注销、通用接口 |
| **MTD Partition** | `mtdpart.c` | 分区管理，支持主设备和从设备分区 |
| **MTD Char** | `mtdchar.c` | 字符设备接口，支持原始Flash访问 |
| **MTD Block** | `mtdblock.c` | 块设备接口，提供缓存层（不推荐用于文件系统） |
| **NAND Base** | `nand/base.c` | NAND Flash通用驱动框架 |
| **NAND ECC** | `nand/ecc.c` | ECC纠错算法实现 |
| **CFI Probe** | `chips/cfi_probe.c` | NOR Flash CFI接口探测 |

---

## 核心数据结构

### 1. mtd_info（MTD设备信息）

`struct mtd_info`是MTD子系统最核心的数据结构，描述一个MTD设备的完整信息。

```c
struct mtd_info {
    u_char type;              /* MTD类型: MTD_NANDFLASH/MTD_NORFLASH */
    uint32_t flags;           /* 标志位: MTD_WRITEABLE/MTD_NO_ERASE等 */
    uint64_t size;            /* 总容量 */
    uint32_t erasesize;       /* 擦除块大小 */
    uint32_t writesize;       /* 写入页大小 */
    uint32_t oobsize;         /* OOB区域大小(NAND) */
    uint32_t bitflip_threshold; /* ECC纠错阈值 */
    
    /* 设备操作函数 */
    int (*_erase) (struct mtd_info *mtd, struct erase_info *instr);
    int (*_read) (struct mtd_info *mtd, loff_t from, size_t len, 
                  size_t *retlen, u_char *buf);
    int (*_write) (struct mtd_info *mtd, loff_t to, size_t len,
                   size_t *retlen, const u_char *buf);
    int (*_read_oob) (struct mtd_info *mtd, loff_t from, 
                      struct mtd_oob_ops *ops);
    int (*_write_oob) (struct mtd_info *mtd, loff_t to,
                       struct mtd_oob_ops *ops);
    int (*_block_isbad) (struct mtd_info *mtd, loff_t ofs);
    int (*_block_markbad) (struct mtd_info *mtd, loff_t ofs);
    
    /* 设备模型 */
    struct device dev;
    int index;                /* MTD设备索引 */
    struct mtd_partition *partitions;  /* 分区表 */
    int nr_partitions;        /* 分区数量 */
    
    void *priv;               /* 私有数据指针 */
};
```

### 2. mtd_partition（分区信息）

```c
struct mtd_partition {
    const char *name;         /* 分区名称 */
    uint64_t size;            /* 分区大小 */
    uint64_t offset;          /* 分区偏移 */
    uint32_t mask_flags;      /* 掩码标志 */
    struct device_node *of_node; /* 设备树节点 */
};
```

### 3. nand_chip（NAND芯片描述）

`struct nand_chip`用于描述NAND Flash芯片的硬件特性和操作接口。

```c
struct nand_chip {
    void __iomem *IO_ADDR_R;  /* 读数据寄存器地址 */
    void __iomem *IO_ADDR_W;  /* 写数据寄存器地址 */
    
    /* 硬件控制函数 */
    void (*cmd_ctrl)(struct mtd_info *mtd, int dat, unsigned int ctrl);
    void (*cmdfunc)(struct mtd_info *mtd, unsigned command, 
                    int column, int page_addr);
    int (*waitfunc)(struct mtd_info *mtd, struct nand_chip *chip);
    void (*select_chip)(struct mtd_info *mtd, int chip);
    
    /* 读写函数 */
    uint8_t (*read_byte)(struct mtd_info *mtd);
    void (*read_buf)(struct mtd_info *mtd, uint8_t *buf, int len);
    void (*write_buf)(struct mtd_info *mtd, const uint8_t *buf, int len);
    
    /* ECC相关 */
    struct nand_ecc_ctrl ecc;
    
    /* 坏块管理 */
    uint8_t *bbt;             /* 坏块表 */
    int (*block_bad)(struct mtd_info *mtd, loff_t ofs, int getchip);
    int (*block_markbad)(struct mtd_info *mtd, loff_t ofs);
    
    /* 芯片参数 */
    int chipsize;             /* 单芯片容量 */
    int page_shift;           /* 页地址偏移 */
    int phys_erase_shift;     /* 物理擦除偏移 */
    int bbt_erase_shift;      /* BBT擦除偏移 */
    int chip_shift;           /* 芯片地址偏移 */
    int numchips;             /* 芯片数量 */
    int badblockpos;          /* 坏块标记位置 */
    
    void *priv;               /* 私有数据 */
};
```

### 4. map_info（NOR Flash映射信息）

```c
struct map_info {
    const char *name;         /* 映射名称 */
    unsigned long size;       /* 映射大小 */
    phys_addr_t phys;         /* 物理地址 */
    void __iomem *virt;       /* 虚拟地址 */
    int bankwidth;            /* 总线宽度(字节) */
    
    /* 操作函数 */
    map_word (*read)(struct map_info *map, unsigned long ofs);
    void (*copy_from)(struct map_info *map, void *to, 
                      unsigned long from, ssize_t len);
    void (*write)(struct map_info *map, const map_word datum, 
                  unsigned long ofs);
    void (*copy_to)(struct map_info *map, unsigned long to, 
                    const void *from, ssize_t len);
};
```

---

## MTD 设备驱动开发

### 注册与注销

MTD设备驱动的基本注册流程：

```c
#include <linux/module.h>
#include <linux/mtd/mtd.h>
#include <linux/mtd/partitions.h>

static struct mtd_info *my_mtd;

/* 模块初始化 */
static int __init my_mtd_init(void)
{
    int ret;
    
    /* 1. 分配mtd_info结构体 */
    my_mtd = kzalloc(sizeof(*my_mtd), GFP_KERNEL);
    if (!my_mtd)
        return -ENOMEM;
    
    /* 2. 设置MTD设备参数 */
    my_mtd->name = "my_flash";
    my_mtd->type = MTD_NANDFLASH;  /* 或 MTD_NORFLASH */
    my_mtd->size = 128 * 1024 * 1024;  /* 128MB */
    my_mtd->erasesize = 128 * 1024;    /* 128KB擦除块 */
    my_mtd->writesize = 2048;          /* 2KB页大小 */
    my_mtd->oobsize = 64;              /* 64字节OOB */
    my_mtd->owner = THIS_MODULE;
    
    /* 3. 设置操作函数 */
    my_mtd->_erase = my_erase;
    my_mtd->_read = my_read;
    my_mtd->_write = my_write;
    my_mtd->_read_oob = my_read_oob;
    my_mtd->_write_oob = my_write_oob;
    my_mtd->_block_isbad = my_block_isbad;
    my_mtd->_block_markbad = my_block_markbad;
    
    /* 4. 注册MTD设备（无分区） */
    ret = mtd_device_register(my_mtd, NULL, 0);
    if (ret) {
        kfree(my_mtd);
        return ret;
    }
    
    /* 或带分区注册 */
    /*
    static struct mtd_partition parts[] = {
        { .name = "boot", .offset = 0, .size = 4 * 1024 * 1024 },
        { .name = "rootfs", .offset = 4 * 1024 * 1024, 
          .size = MTDPART_SIZ_FULL },
    };
    ret = mtd_device_register(my_mtd, parts, ARRAY_SIZE(parts));
    */
    
    return 0;
}

/* 模块退出 */
static void __exit my_mtd_exit(void)
{
    mtd_device_unregister(my_mtd);
    kfree(my_mtd);
}

module_init(my_mtd_init);
module_exit(my_mtd_exit);
MODULE_LICENSE("GPL");
```

### 核心操作函数实现

```c
/* 擦除操作 */
static int my_erase(struct mtd_info *mtd, struct erase_info *instr)
{
    /* 1. 检查参数合法性 */
    if (instr->addr + instr->len > mtd->size)
        return -EINVAL;
    
    /* 2. 确保地址和长度对齐到擦除块 */
    if (!IS_ALIGNED(instr->addr, mtd->erasesize) ||
        !IS_ALIGNED(instr->len, mtd->erasesize))
        return -EINVAL;
    
    /* 3. 执行硬件擦除 */
    /* ... 调用具体硬件擦除函数 ... */
    
    /* 4. 回调通知 */
    if (instr->callback)
        instr->callback(instr);
    
    return 0;
}

/* 读操作 */
static int my_read(struct mtd_info *mtd, loff_t from, size_t len,
                   size_t *retlen, u_char *buf)
{
    /* 检查地址和长度 */
    if (from + len > mtd->size)
        return -EINVAL;
    
    /* 执行硬件读取 */
    /* ... */
    
    *retlen = len;
    return 0;
}

/* 写操作 */
static int my_write(struct mtd_info *mtd, loff_t to, size_t len,
                    size_t *retlen, const u_char *buf)
{
    /* 检查地址和长度 */
    if (to + len > mtd->size)
        return -EINVAL;
    
    /* 确保写入区域已擦除 */
    /* ... */
    
    /* 执行硬件写入 */
    /* ... */
    
    *retlen = len;
    return 0;
}
```

---

## NAND Flash 驱动开发

NAND Flash驱动基于MTD子系统，利用内核提供的通用NAND驱动框架（`nand_base.c`）简化开发。

### 典型驱动结构

```c
#include <linux/module.h>
#include <linux/platform_device.h>
#include <linux/mtd/mtd.h>
#include <linux/mtd/rawnand.h>

struct my_nand_host {
    struct nand_chip chip;
    struct mtd_info *mtd;
    void __iomem *base;
    struct clk *clk;
    struct dma_chan *dma_chan;
};

/* 硬件控制函数 */
static void my_nand_cmd_ctrl(struct mtd_info *mtd, int dat, 
                             unsigned int ctrl)
{
    struct nand_chip *chip = mtd_to_nand(mtd);
    struct my_nand_host *host = nand_get_controller_data(chip);
    
    if (ctrl & NAND_CLE)
        writeb(dat, host->base + CMD_REG);
    else if (ctrl & NAND_ALE)
        writeb(dat, host->base + ADDR_REG);
}

/* 等待就绪 */
static int my_nand_waitfunc(struct mtd_info *mtd, struct nand_chip *chip)
{
    struct my_nand_host *host = nand_get_controller_data(chip);
    int status;
    
    /* 等待R/B引脚就绪或轮询状态 */
    /* ... */
    
    status = readb(host->base + STATUS_REG);
    return status;
}

/* 初始化读取 */
static uint8_t my_nand_read_byte(struct mtd_info *mtd)
{
    struct nand_chip *chip = mtd_to_nand(mtd);
    struct my_nand_host *host = nand_get_controller_data(chip);
    
    return readb(host->base + DATA_REG);
}

/* 批量读取 */
static void my_nand_read_buf(struct mtd_info *mtd, uint8_t *buf, int len)
{
    struct nand_chip *chip = mtd_to_nand(mtd);
    struct my_nand_host *host = nand_get_controller_data(chip);
    
    ioread8_rep(host->base + DATA_REG, buf, len);
}

/* Probe函数 */
static int my_nand_probe(struct platform_device *pdev)
{
    struct device_node *np = pdev->dev.of_node;
    struct my_nand_host *host;
    struct nand_chip *chip;
    struct mtd_info *mtd;
    int ret;
    
    /* 1. 分配host结构 */
    host = devm_kzalloc(&pdev->dev, sizeof(*host), GFP_KERNEL);
    if (!host)
        return -ENOMEM;
    
    /* 2. 获取资源 */
    host->base = devm_platform_ioremap_resource(pdev, 0);
    if (IS_ERR(host->base))
        return PTR_ERR(host->base);
    
    host->clk = devm_clk_get(&pdev->dev, NULL);
    if (IS_ERR(host->clk))
        return PTR_ERR(host->clk);
    
    clk_prepare_enable(host->clk);
    
    /* 3. 初始化nand_chip */
    chip = &host->chip;
    nand_set_controller_data(chip, host);
    nand_set_flash_node(chip, np);
    
    chip->IO_ADDR_R = host->base + DATA_REG;
    chip->IO_ADDR_W = host->base + DATA_REG;
    chip->cmd_ctrl = my_nand_cmd_ctrl;
    chip->waitfunc = my_nand_waitfunc;
    chip->read_byte = my_nand_read_byte;
    chip->read_buf = my_nand_read_buf;
    chip->write_buf = my_nand_write_buf;
    
    /* 4. 设置ECC */
    chip->ecc.mode = NAND_ECC_HW;  /* 硬件ECC */
    chip->ecc.algo = NAND_ECC_BCH;
    chip->ecc.strength = 8;
    chip->ecc.size = 1024;
    chip->ecc.bytes = 14;
    chip->ecc.write_page = my_nand_write_page_hwecc;
    chip->ecc.read_page = my_nand_read_page_hwecc;
    
    /* 5. 扫描NAND设备 */
    mtd = nand_to_mtd(chip);
    mtd->owner = THIS_MODULE;
    mtd->dev.parent = &pdev->dev;
    
    ret = nand_scan(chip, 1);  /* 1表示单芯片 */
    if (ret)
        goto err_disable_clk;
    
    /* 6. 注册MTD设备（带分区） */
    ret = mtd_device_register(mtd, NULL, 0);
    if (ret)
        goto err_cleanup_nand;
    
    platform_set_drvdata(pdev, host);
    return 0;

err_cleanup_nand:
    nand_cleanup(chip);
err_disable_clk:
    clk_disable_unprepare(host->clk);
    return ret;
}

/* Remove函数 */
static int my_nand_remove(struct platform_device *pdev)
{
    struct my_nand_host *host = platform_get_drvdata(pdev);
    struct nand_chip *chip = &host->chip;
    struct mtd_info *mtd = nand_to_mtd(chip);
    
    mtd_device_unregister(mtd);
    nand_cleanup(chip);
    clk_disable_unprepare(host->clk);
    
    return 0;
}

static const struct of_device_id my_nand_dt_ids[] = {
    { .compatible = "vendor,my-nand-controller" },
    { /* sentinel */ }
};
MODULE_DEVICE_TABLE(of, my_nand_dt_ids);

static struct platform_driver my_nand_driver = {
    .probe = my_nand_probe,
    .remove = my_nand_remove,
    .driver = {
        .name = "my_nand",
        .of_match_table = my_nand_dt_ids,
    },
};
module_platform_driver(my_nand_driver);
```

### NAND扫描流程

`nand_scan()`函数执行以下步骤：

1. **nand_scan_ident()**：识别NAND芯片
   - 读取厂商ID和设备ID
   - 匹配芯片参数（页大小、块大小、容量等）
   - 设置默认操作函数

2. **nand_scan_tail()**：完成初始化
   - 初始化ECC配置
   - 分配坏块表(BBT)内存
   - 扫描坏块并建立BBT

---

## NOR Flash 驱动开发

NOR Flash驱动基于CFI（Common Flash Interface）标准或JEDEC标准。

### CFI标准NOR Flash驱动

```c
#include <linux/module.h>
#include <linux/mtd/mtd.h>
#include <linux/mtd/map.h>
#include <linux/mtd/cfi.h>
#include <linux/mtd/gen_probe.h>

/* 定义map_info */
static struct map_info my_map = {
    .name = "my_nor_flash",
    .size = 32 * 1024 * 1024,  /* 32MB */
    .bankwidth = 2,            /* 16位总线 */
};

/* 平台特定初始化 */
static int __init my_nor_init(void)
{
    struct mtd_info *mtd;
    
    /* 1. 映射物理地址到虚拟地址 */
    my_map.phys = 0x20000000;  /* NOR物理基地址 */
    my_map.virt = ioremap(my_map.phys, my_map.size);
    if (!my_map.virt)
        return -ENOMEM;
    
    simple_map_init(&my_map);
    
    /* 2. 探测CFI接口 */
    mtd = do_map_probe("cfi_probe", &my_map);
    if (!mtd) {
        /* 尝试JEDEC探测 */
        mtd = do_map_probe("jedec_probe", &my_map);
    }
    
    if (!mtd) {
        iounmap(my_map.virt);
        return -ENODEV;
    }
    
    mtd->owner = THIS_MODULE;
    
    /* 3. 添加分区 */
    static struct mtd_partition parts[] = {
        { .name = "bootloader", .offset = 0, .size = 0x40000 },
        { .name = "kernel", .offset = 0x40000, .size = 0x200000 },
        { .name = "rootfs", .offset = 0x240000, .size = MTDPART_SIZ_FULL },
    };
    
    mtd_device_register(mtd, parts, ARRAY_SIZE(parts));
    
    return 0;
}

static void __exit my_nor_exit(void)
{
    struct mtd_info *mtd = my_map.mtd;
    
    mtd_device_unregister(mtd);
    map_destroy(mtd);
    iounmap(my_map.virt);
}

module_init(my_nor_init);
module_exit(my_nor_exit);
```

---

## 分区管理

MTD支持两种分区定义方式：

### 方式一：设备树定义（推荐）

```dts
nand@0 {
    compatible = "vendor,my-nand";
    reg = <0>;
    
    partitions {
        compatible = "fixed-partitions";
        #address-cells = <1>;
        #size-cells = <1>;
        
        partition@0 {
            label = "u-boot";
            reg = <0x0 0x40000>;       /* 256KB */
            read-only;
        };
        
        partition@40000 {
            label = "kernel";
            reg = <0x40000 0x500000>;  /* 5MB */
        };
        
        partition@540000 {
            label = "rootfs";
            reg = <0x540000 0x0>;      /* 剩余空间 */
        };
    };
};
```

### 方式二：代码中静态定义

```c
static struct mtd_partition my_partitions[] = {
    {
        .name = "bootloader",
        .offset = 0,
        .size = 0x40000,
    },
    {
        .name = "kernel",
        .offset = MTDPART_OFS_APPEND,  /* 紧接上一个分区 */
        .size = 0x500000,
    },
    {
        .name = "rootfs",
        .offset = MTDPART_OFS_APPEND,
        .size = MTDPART_SIZ_FULL,      /* 剩余所有空间 */
    },
};

/* 注册时传入分区表 */
mtd_device_register(master_mtd, my_partitions, ARRAY_SIZE(my_partitions));
```

### 分区相关宏

| 宏 | 说明 |
|---|------|
| `MTDPART_OFS_APPEND` | 分区偏移紧跟上一个分区 |
| `MTDPART_OFS_NXTBLK` | 对齐到下一个擦除块边界 |
| `MTDPART_SIZ_FULL` | 使用剩余所有空间 |

---

## 文件系统集成

MTD设备支持多种专用闪存文件系统：

| 文件系统 | 适用场景 | 特点 |
|---------|---------|------|
| **JFFS2** | NOR Flash、小容量NAND | 日志结构、压缩、磨损均衡 |
| **UBIFS** | 大容量NAND Flash | 基于UBI层、快速挂载、写缓存 |
| **YAFFS2** | NAND Flash | 简单高效、启动快、无压缩 |
| **SquashFS** | 只读分区 | 高压缩率、只读 |
| **CRAMFS** | 小容量只读 | 简单、内存映射 |

### UBI/UBIFS层次

```
┌─────────────────┐
│    UBIFS        │  文件系统层
├─────────────────┤
│    UBI          │  卷管理层（坏块管理、磨损均衡）
├─────────────────┤
│    MTD          │  设备抽象层
├─────────────────┤
│   NAND/NOR      │  硬件驱动层
└─────────────────┘
```

---

## 调试与工具

### 内核配置

```bash
Device Drivers  --->
    <*> Memory Technology Device (MTD) support  --->
        <*>   MTD tests support                 # 测试模块
        <*>   CFI Flash device support  --->    # NOR Flash
            <*>   Support for Intel/Sharp flash chips
            <*>   Support for AMD/Fujitsu/Spansion flash chips
        NAND  --->
            <*>   Raw/Parallel NAND device support  --->  # NAND Flash
        <*>   SPI-NOR device support            # SPI NOR
        Self-contained MTD device drivers  --->
            <*>   Support for AT45xxx DataFlash
```

### mtd-utils工具集

```bash
# 安装
sudo apt-get install mtd-utils

# 查看MTD设备信息
cat /proc/mtd
mtdinfo /dev/mtd0

# 擦除Flash
flash_erase /dev/mtd0 0 0        # 擦除整个MTD0
flash_erase /dev/mtd0 0 10       # 从块0开始擦除10个块

# 写入/读取
flashcp -v image.bin /dev/mtd0   # 写入镜像
nanddump /dev/mtd0 -f backup.bin # 备份NAND
nandwrite /dev/mtd0 image.bin    # 写入NAND

# 坏块管理
nandtest /dev/mtd0               # 测试NAND
flash_erase --jffs2 /dev/mtd0 0 0  # 标记坏块

# UBI工具
ubiformat /dev/mtd0              # 格式化UBI
ubiattach /dev/ubi_ctrl -m 0     # 附加MTD设备到UBI
ubimkvol /dev/ubi0 -N rootfs -s 100MiB  # 创建卷
```

### 调试接口

```bash
# sysfs接口
ls /sys/class/mtd/
cat /sys/class/mtd/mtd0/erasesize
cat /sys/class/mtd/mtd0/writesize
cat /sys/class/mtd/mtd0/size

# 调试日志
dmesg | grep -i mtd
dmesg | grep -i nand

# 启用MTD调试
echo 'file drivers/mtd/nand/*.c +p' > /sys/kernel/debug/dynamic_debug/control
```

### 常见问题排查

| 问题 | 可能原因 | 解决方法 |
|-----|---------|---------|
| 无法识别NAND | 时序配置错误 | 检查NAND控制器时序参数 |
| ECC校验失败 | ECC模式不匹配 | 确认硬件ECC配置与驱动一致 |
| 坏块过多 | 坏块表未建立 | 执行nand_scan重新扫描 |
| 写入失败 | 未擦除直接写 | 确保写入前已擦除 |
| 挂载失败 | 文件系统损坏 | 使用flash_erase格式化后重新写入 |

---

## 参考资源

- [Linux MTD官方文档](http://www.linux-mtd.infradead.org/doc/general.html)
- [Linux内核源码：drivers/mtd/](https://github.com/torvalds/linux/tree/master/drivers/mtd)
- [MTD子系统架构详解](https://blog.csdn.net/zouhaicheng/article/details/144576325)
- [NAND Flash驱动开发指南](https://blog.csdn.net/yellow1988/article/details/145022641)

---

*文档版本：1.0*  
*最后更新：2026年4月*


这份文档涵盖了Linux MTD子系统的完整知识体系，包括：

1. **架构分层**：详细解释四层架构模型（应用层、设备层、原始设备层、硬件驱动层）
2. **核心数据结构**：`mtd_info`、`mtd_partition`、`nand_chip`、`map_info`等关键结构体
3. **NAND驱动开发**：完整的NAND Flash驱动示例，包含平台设备驱动框架
4. **NOR驱动开发**：基于CFI标准的NOR Flash驱动实现
5. **分区管理**：设备树和代码两种分区定义方式
6. **文件系统集成**：JFFS2、UBIFS、YAFFS2等闪存文件系统介绍
7. **调试工具**：mtd-utils使用方法和内核调试技巧