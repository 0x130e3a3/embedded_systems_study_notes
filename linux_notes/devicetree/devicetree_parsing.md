这是一个关于 Linux 设备树解析机制的技术问题。我将详细解释 U-Boot 和 Linux 内核如何解析设备树，以及它们之间的关系。

## 设备树解析流程总览

```
┌─────────────────────────────────────────────────────────────┐
│                    启动流程中的设备树                           │
├─────────────────────────────────────────────────────────────┤
│  1. 源码阶段                                                  │
│     ├── SoC 厂商提供 .dtsi（芯片级定义）                       │
│     └── 板子厂商提供 .dts（产品级定义）                        │
│                        ↓                                     │
│  2. 编译阶段                                                  │
│     └── dtc 编译器 → .dtb（Device Tree Blob）                 │
│                        ↓                                     │
│  3. 启动阶段                                                  │
│     ├── U-Boot 加载 .dtb 到内存                                │
│     ├── U-Boot 解析/修改设备树（可选）                         │
│     └── U-Boot 传递给内核（通过寄存器或内存）                   │
│                        ↓                                     │
│  4. 内核阶段                                                  │
│     ├── 早期解压/启动代码获取 dtb 地址                         │
│     ├── unflatten_device_tree() 解析为内核数据结构             │
│     └── 驱动 probe 时查询设备树节点                            │
└─────────────────────────────────────────────────────────────┘
```

## U-Boot 如何解析设备树

### 1. U-Boot 中的设备树支持

```c
// U-Boot 源码结构（简化）
// arch/arm/cpu/armv8/start.S 或其他启动汇编
// → 设置初始环境 → 调用 C 代码

// common/board_f.c
void board_init_f(ulong boot_flags)
{
    // 初始化序列...
    // 包括设备树初始化
}

// lib/fdtdec.c - U-Boot 的 FDT 解码库
// fdtdec 是 U-Boot 对 libfdt 的封装
```

### 2. U-Boot 设备树操作

```c
// U-Boot 命令行操作设备树示例

// 加载 dtb 到内存
load mmc 0:1 ${fdt_addr} boot/myboard.dtb

// 查看设备树信息
fdt addr ${fdt_addr}        // 设置当前操作的 dtb 地址
fdt header                // 查看 DTB 头信息
fdt print /               // 打印根节点
fdt print /soc/uart@101f0000  // 打印特定节点

// 修改设备树（运行时）
fdt set /chosen bootargs "console=ttyS0,115200 root=/dev/mmcblk0p2"
fdt set /soc/uart@101f0000 status "okay"
fdt set /memory@80000000 reg <0x80000000 0x40000000>

// 添加节点
fdt mknode /soc mydevice
fdt set /soc/mydevice compatible "mycompany,mydev"
fdt set /soc/mydevice reg <0x2000000 0x1000>
```

### 3. U-Boot 传递给内核的方式

```c
// 方法 1：ARM64 - 通过寄存器 x0-x3
// arch/arm/cpu/armv8/start.S
ENTRY(armv8_switch_to_el1)
    // x0 = dtb 物理地址
    // x1 = 0 (保留)
    // x2 = 0 (保留)
    // x3 = 0 (保留)
    
// 方法 2：ARM32 - 通过寄存器 r0-r2
// r0 = 0
// r1 = machine type (已废弃，设为 0xffffffff)
// r2 = dtb 物理地址

// 方法 3：通过 U-Boot 的 booti/bootm 命令
// 将 dtb 地址作为参数传递
booti ${kernel_addr} - ${fdt_addr}  // 无 initrd
booti ${kernel_addr} ${initrd_addr} ${fdt_addr}
```

## Linux 内核如何解析设备树

### 1. 早期启动阶段（汇编/解压）

```c
// arch/arm64/kernel/head.S（ARM64 示例）
// 或 arch/arm/boot/compressed/head.S（ARM32 解压）

/*
 * 入口点：内核启动时，x0 包含 dtb 物理地址（ARM64）
 * 或 r2 包含 dtb 地址（ARM32）
 */

ENTRY(stext)
    // 保存 dtb 地址到全局变量
    // ARM64: __pa_symbol(initial_boot_params) = x0
    // 保存后进入 C 代码初始化
```

### 2. 核心解析函数：unflatten_device_tree()

```c
// drivers/of/fdt.c - Flattened Device Tree 核心代码

// 早期初始化（setup_arch 中调用）
void __init unflatten_device_tree(void)
{
    // 1. 验证 DTB 魔数（0xd00dfeed）
    // 检查 fdt_header 的 magic 和 version
    
    // 2. 计算需要分配的内存大小
    // 遍历整个 fdt，统计节点数和属性数
    
    // 3. 分配内存
    // 使用 memblock_alloc 分配（此时 slab 尚未初始化）
    
    // 4. 递归解析，创建 device_node 树
    // 从根节点开始，逐层展开
    unflatten_dt_nodes(blob, NULL, NULL, &mem);
    
    // 5. 设置全局变量
    // of_root = 根节点指针
    // of_chosen = /chosen 节点指针
    // of_aliases = /aliases 节点指针
}

// 关键数据结构转换
/*
 * DTB (二进制) → device_node (内核结构) → platform_device (平台设备)
 * 
 * fdt 中的每个节点 → struct device_node
 * fdt 中的每个属性 → struct property
 */
```

### 3. 核心数据结构

```c
// include/linux/of.h

// 设备树节点（内核中的表示）
struct device_node {
    const char *name;           // 节点名（如 "uart@101f0000"）
    const char *type;           // 设备类型（如 "serial"）
    phandle phandle;            // 唯一标识符
    const char *full_name;      // 完整路径（如 "/soc/uart@101f0000"）
    
    struct property *properties; // 属性链表
    struct property *deadprops;  // 已删除属性
    struct device_node *parent;  // 父节点
    struct device_node *child;   // 第一个子节点
    struct device_node *sibling; // 兄弟节点
    
    struct kobject kobj;        // sysfs 表示
    unsigned long _flags;
    void *data;                // 平台特定数据
};

// 属性结构
struct property {
    char *name;                // 属性名（如 "compatible"）
    int length;                // 属性值长度（字节）
    void *value;              // 属性值（二进制数据）
    struct property *next;    // 下一个属性
    struct bin_attribute attr; // sysfs 二进制属性
};
```

### 4. 详细解析流程

```c
// drivers/of/fdt.c - 展开节点的核心逻辑

static void __unflatten_device_tree(const void *blob,
                                    struct device_node *dad,
                                    struct device_node **nodepp)
{
    struct device_node *root;
    
    // 1. 扫描 DTB，计算需要的内存
    // 包括所有 device_node 结构和 property 结构
    size = unflatten_dt_nodes(blob, NULL, dad, NULL);
    
    // 2. 分配内存（使用 memblock，早期启动阶段）
    mem = dt_alloc(size + 4, __alignof__(struct device_node));
    
    // 3. 再次扫描，实际填充结构
    // 这次传入分配的内存指针，创建实际节点
    unflatten_dt_nodes(blob, mem, dad, &root);
    
    // 4. 设置全局根节点
    if (nodepp)
        *nodepp = root;
}

// 递归解析每个节点
static int unflatten_dt_nodes(const void *blob,
                              void *mem,
                              struct device_node *dad,
                              struct device_node **nodepp)
{
    struct device_node *root = NULL;
    int offset = 0, depth = 0;
    
    // 遍历 FDT 的所有节点
    for (offset = fdt_next_node(blob, offset, &depth);
         offset >= 0 && depth >= 0;
         offset = fdt_next_node(blob, offset, &depth)) {
        
        // 填充 device_node 结构
        // 复制节点名、解析属性、建立父子关系
        populate_node(blob, offset, &mem, &root, dad);
    }
    
    return 0;
}
```

### 5. 从 device_node 到 platform_device

```c
// drivers/of/platform.c - 平台设备创建

// 在 of_platform_default_populate_init() 中调用
// 这是一个 early_initcall

int of_platform_default_populate(struct device_node *root,
                                 const struct of_dev_auxdata *lookup,
                                 struct device *parent)
{
    // 遍历所有 "simple-bus" 或 "simple-mfd" 或 "arm,amba-bus" 节点
    // 为这些总线下的子节点创建 platform_device
    
    return of_platform_populate(root, of_default_bus_match_table,
                                lookup, parent);
}

// 匹配表 - 哪些节点会被自动创建为平台设备
static const struct of_device_id of_default_bus_match_table[] = {
    { .compatible = "simple-bus", },      // 简单总线
    { .compatible = "simple-mfd", },       // 多功能设备
    { .compatible = "arm,amba-bus", },      // AMBA 总线
    { .compatible = "isa", },               // ISA 总线
#ifdef CONFIG_MIPS
    { .compatible = "mti,mdb", },          // MIPS 调试总线
#endif
    {} /* 结束标记 */
};

// 创建设备的递归函数
static int of_platform_bus_create(struct device_node *bus,
                                  const struct of_device_id *matches,
                                  const struct of_dev_auxdata *lookup,
                                  struct device *parent, bool strict)
{
    struct device_node *child;
    struct platform_device *dev;
    
    // 1. 检查 compatible 是否匹配总线类型
    // 如果不匹配且 strict=true，则不处理子节点
    
    // 2. 为当前总线节点创建 platform_device（如果它不是根节点）
    dev = of_platform_device_create_pdata(bus, bus_id, platform_data, parent);
    
    // 3. 递归处理子节点
    for_each_child_of_node(bus, child) {
        // 如果子节点也是总线，递归处理
        // 否则直接创建 platform_device
        of_platform_bus_create(child, matches, lookup, &dev->dev, strict);
    }
    
    return 0;
}
```

### 6. 驱动匹配时机

```c
// 启动流程中的设备树解析时间线

start_kernel()                    // init/main.c
    └── setup_arch()              // 架构特定设置
        └── unflatten_device_tree()  // 解析 DTB → device_node 树
            // 此时：内存分配器刚初始化，只能使用 memblock
    
    └── mm_init()                 // 内存管理初始化
    
    └── rest_init()
        └── kernel_init()
            └── kernel_init_freeable()
                └── do_basic_setup()
                    └── driver_init()        // 驱动核心初始化
                        └── of_platform_default_populate_init()  // 创建 platform_device
                    
                    └── do_initcalls()       // 调用所有 __initcall
                        // 驱动注册（module_init）
                        // platform_driver_register()
                        
                        // 当 driver 注册时，如果匹配已存在的 device
                        // 或 device 创建时匹配已注册的 driver
                        // → 调用 driver.probe()
```

## 关键代码详解

### 1. 早期 DTB 地址获取

```c
// arch/arm64/kernel/setup.c

void __init setup_arch(char **cmdline_p)
{
    // 1. 从 early_init_dt_scan 获取 DTB 地址
    // 这个地址由启动汇编保存在 initial_boot_params
    
    // 2. 解析早期信息（bootargs、内存等）
    early_init_dt_scan_nodes();
    
    // 3. 完整的设备树展开
    unflatten_device_tree();
    
    // 4. 后续架构初始化...
}

// early_init_dt_scan_nodes 在 unflatten 之前执行
// 因为它需要读取 /chosen/bootargs 和 /memory 信息
// 此时使用 libfdt 直接操作原始 DTB，无需展开
```

### 2. libfdt 与 of 层的区别

```c
/*
 * 两个层面的设备树操作：
 * 
 * 1. libfdt - 操作原始 DTB（扁平格式）
 *    - 用于早期启动（unflatten 之前）
 *    - 直接操作 blob 内存
 *    - 函数前缀：fdt_*
 * 
 * 2. of 层 - 操作展开的 device_node 树
 *    - 用于驱动和内核代码
 *    - 操作内核数据结构
 *    - 函数前缀：of_*
 */

// libfdt 示例（早期启动）
int nodeoffset = fdt_path_offset(blob, "/soc/uart@101f0000");
const char *compat = fdt_getprop(blob, nodeoffset, "compatible", NULL);

// of 层示例（驱动代码）
struct device_node *np = of_find_node_by_path("/soc/uart@101f0000");
const char *compat;
of_property_read_string(np, "compatible", &compat);
```

### 3. 内存布局信息传递

```c
// 早期内存初始化（setup_arch 中）

void __init early_init_dt_add_memory_arch(u64 base, u64 size)
{
    // 将 /memory 节点信息添加到 memblock
    memblock_add(base, size);
}

// 读取 /memory 节点
int __init early_init_dt_scan_memory(unsigned long node, const char *uname,
                                     int depth, void *data)
{
    // 查找 "device_type" = "memory" 的节点
    // 读取 reg 属性
    // 调用 early_init_dt_add_memory_arch 注册内存
}
```

## 调试与验证

### 1. 内核命令行查看设备树

```bash
# 查看当前设备树（通过 sysfs）
ls /sys/firmware/devicetree/base/
cat /sys/firmware/devicetree/base/model
cat /sys/firmware/devicetree/base/compatible

# 查看特定节点
ls /sys/firmware/devicetree/base/soc/
cat /sys/firmware/devicetree/base/soc/serial@101f0000/compatible
xxd /sys/firmware/devicetree/base/soc/serial@101f0000/reg  # 二进制数据

# 查看展开的节点数（procfs）
cat /proc/device-tree/  # 符号链接到 /sys/firmware/devicetree/base/
```

### 2. 启动日志分析

```bash
# 开启详细设备树日志
# 内核配置：CONFIG_DEBUG_DRIVER=y
# 或动态调试：
echo 'file drivers/of/base.c +p' > /sys/kernel/debug/dynamic_debug/control

# 查看启动日志
dmesg | grep -E "of:|device tree|Machine model"
# 预期输出：
[    0.000000] OF: fdt: Machine model: MyCompany MyBoard
[    0.000000] OF: fdt: Ignoring memory range 0x80000000 - 0x80200000
[    0.052000] OF: /soc/uart@101f0000: compatible: arm,pl011
```

### 3. 验证 DTB 是否正确传递

```c
// 如果怀疑 U-Boot 传递的地址错误
// 在内核 early 代码中添加检查（arch/arm64/kernel/head.S）

// 检查 x0 是否指向有效的 DTB
// DTB 魔数：0xd00dfeed（大端）

// 或在内核命令行添加：
// earlyprintk=serial dtdebug=1
```

## 总结：解析流程图

```
┌─────────────────────────────────────────────────────────────┐
│  U-Boot 阶段                                                 │
│  ├── 从磁盘/Flash 加载 dtb 到 RAM（fdt_addr）                 │
│  ├── 可选：fdt 命令修改设备树（添加节点、修改属性）             │
│  └── 通过 booti 启动内核，dtb 地址存入 x0/r2 寄存器            │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│  内核早期（汇编）                                             │
│  ├── 保存 dtb 地址到全局变量（initial_boot_params）            │
│  └── 跳转到 C 代码（start_kernel）                            │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│  setup_arch()                                                │
│  ├── early_init_dt_scan_nodes()                              │
│  │   └── 使用 libfdt 直接读取 /chosen、/memory（原始 dtb）    │
│  └── unflatten_device_tree()                                 │
│      ├── 验证 DTB 头（magic=0xd00dfeed）                      │
│      ├── 计算内存需求，memblock_alloc 分配                     │
│      └── 递归解析，创建 device_node 树结构                     │
│          └── of_root（全局根节点）                            │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│  驱动初始化阶段（do_initcalls）                                │
│  └── of_platform_default_populate_init()                     │
│      └── 为 "simple-bus" 等总线下的节点创建 platform_device    │
│          └── 触发 driver probe，驱动使用 of_* API 查询设备树   │
└─────────────────────────────────────────────────────────────┘
```

设备树的核心价值在于**硬件描述与内核代码分离**，U-Boot 负责**传递和修改**，内核负责**解析和使用**，两者通过**DTB 二进制格式**和**寄存器约定**实现无缝协作。