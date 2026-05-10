# DDR学习笔记 — 第三部分：控制器分析与实战调试

> **本文档**：SoC 内存控制器的架构分析与 DDR 初始化调试实战。当前以 i.MX 6ULL 为主，后续每接触新的 SoC 会增加对应章节（不同 SoC 的 DDR 控制器差异很大，每个控制器独立一章）。
>
> **配套文档**：
> - [第一部分：DDR相关理论知识](01_ddr_theory.md) — 基础概念、芯片组织结构、各代演进
> - [第二部分：具体DDR芯片分析](02_ddr_chip_analysis.md) — 各代芯片规格与数据手册解读

## 11. DDR 控制器概述

> 在深入具体 SoC 的控制器实现之前，先建立一个全局认知：**DDR 控制器是什么、干什么、为什么需要这么多功能模块。**

### 11.1 什么是内存控制器

CPU **不能直接**操作 DDR 芯片。原因很简单：CPU 通过 AXI 总线发起"读写某个地址"的请求，而 DDR 芯片只认 JEDEC 标准定义的命令（ACT、READ、WRITE、PRE、REF……）和严格的时序约束。两者语言不通，需要一个**翻译官**。

```
内存控制器的定位：

  CPU / SoC          DDR 控制器           DDR 芯片
  (AXI 协议)        (翻译 + 调度)       (JEDEC 命令)
      │                   │                  │
      │── 读 0x8000 ──→   │                  │
      │                   │── ACT → READ ──→ │
      │                   │←──── 数据 ───────│
      │←── 返回数据 ───── │                  │
```

一句话总结：**内存控制器 = CPU 与 DDR 芯片之间的桥梁**。它接收 CPU 的通用读写请求，翻译成 DDR 能理解的命令序列，并保证每一步都满足时序要求。

### 11.2 控制器的三大职责

| 职责 | 做什么 | 类比 |
|------|--------|------|
| **协议翻译** | 把 AXI 读写请求转成 DDR 命令序列（ACT → READ/WRITE → PRE） | 翻译官 |
| **时序管理** | 确保每次操作满足 tRCD、tRP、tRAS、tRFC 等时序约束，期间自动插入等待 | 交通指挥员 |
| **性能优化** | 重排序请求、Bank 预测、Page 管理，让 DDR 少等少空转 | 调度员 |

这三个职责是理解控制器所有功能模块的**总纲**。后面学到的每一个机制，都可以归入这三个职责之一。

### 11.3 控制器内部长什么样

下面是 DDR 控制器的简化框图，标注了各个子模块的位置和关系：

```
CPU ──→ [AXI 接口] ──→ [请求队列] ──→ [重排序/仲裁] ──→ [命令引擎] ──→ DDR 芯片
                              ↕                               ↕
                        [地址解码]                      [PHY / 校准引擎]
```

各模块一句话说明：

| 模块 | 做什么 |
|------|--------|
| **AXI 接口** | 接收 SoC 内部总线的读写请求，处理位宽转换（如 32-bit AXI → x16 DDR） |
| **请求队列** | 缓存等待中的读写请求（读队列通常比写队列大，因为读对延迟更敏感） |
| **重排序/仲裁** | 决定哪个请求先执行，通过 Page Hit、Bank 预测等策略提高总线利用率 |
| **地址解码** | 把 CPU 给的线性地址拆成片选、Bank、行号、列号，DDR 芯片只认这些字段 |
| **命令引擎** | 按 JEDEC 时序要求，生成 ACT/READ/WRITE/PRE/REF 等命令序列 |
| **PHY / 校准** | 处理高速信号的时序对齐（DQS/DQ 延迟、ZQ 阻抗校准、Write Leveling 等） |

### 11.4 本章节知识地图

第 12 章和第 13 章涉及的知识点很多，下面按**功能层面**分类，帮你建立框架认知：

| 层面 | 涉及的知识点 | 解决什么问题 |
|------|------------|-------------|
| **接口层** | [12.1 外部信号引脚映射](#121-外部信号引脚映射)、[12.2 时钟系统](#122-时钟系统)、[12.4 AXI 接口与请求队列](#124-axi-接口与请求队列)、[12.5 DDR 突发长度](#125-ddr-突发长度说明) | 控制器与外部世界的物理连接和传输协议 |
| **架构层** | [12.3 MMDC 架构](#123-mmdc-架构core--phy) | 控制器内部的 Core + PHY 分工 |
| **地址层** | [12.6 地址解码与地址空间](#126-地址解码与地址空间) | 控制器怎么理解 CPU 给的一个地址 |
| **调度层** | [12.7 重排序与 Bank 预测](#127-重排序机制与-bank-预测)、[12.8 Page Hit/Miss](#128-page-hit--page-miss-优化)、[12.9 AXI 错误处理与独占访问](#129-axi-错误处理与独占访问) | 控制器怎么安排请求顺序让 DDR 跑得更快 |
| **物理层** | [12.10 校准机制](#1210-校准机制)、[12.11 DLL 切换](#1211-dll-切换dll-switching) | 控制器怎么保证高速信号不丢数据 |
| **维护层** | [12.12 刷新方案](#1212-刷新方案refresh-scheme) | 维持 DDR 正常工作的基础设施 |
| **电源层** | [12.13 省电模式](#1213-省电模式) | 没人用 DDR 时怎么降低功耗 |
| **系统层** | [12.14 复位机制](#1214-复位机制) | 系统级别的异常和恢复机制 |
| **调试层** | [12.15 调试监视器与性能分析](#1215-调试监视器与性能分析debug--profiling) | 出了问题怎么查、性能怎么样 |
| **实战层** | [13.x 实战调试](#13-imx-6ull-实战与调试) | 把前面所有知识落地：提取参数 → 生成脚本 → 上电验证 |

### 11.5 学习路径建议

建议的学习顺序：

1. **先通读本节**，建立"控制器 = 翻译官 + 调度员 + 交通指挥员"的整体认知
2. **带着框架读后续章节**：每学一个知识点，问自己"这属于哪一层？解决三大职责中的哪一个？"
3. **最后看实战**（第 13 章）：把理论知识映射到真实寄存器和初始化流程上

---

## 12. i.MX 6ULL MMDC 控制器

> **本章是核心配置章节**，涉及的寄存器：
> | 寄存器 | 用途 | 说明 |
> |--------|------|------|
> | `MDCTL` | 物理参数配置 | ROW/COL/DSIZ/BL/SDE 等 |
> | `MDASP` | 片选分区 | CS0_END 设置 |
> | `MDCFG0` | 时序参数 | tCKE/CL/tXP/tXPDLL |
> | `MDCFG1` | 时序参数 | tRC/tRAS/tCWL |
> | `MDCFG2` | 时序参数 | tRCD/tRP/tRRD |
> | `MDOTC` | ODT 时序 | tAOFPD/tAONPD/tANPD/tAXPD/tODTLon |
> | `MDREF` | 刷新控制 | REF_CNT/REF_SEL |
> | `MDSCR` | 特殊命令 | CON_REQ/CON_ACK/MRS 命令配置 |
> | `MAPSR` | 电源管理 | 低功耗/自刷新参数 |

### 12.1 外部信号引脚映射

> **对应手册**：§35.2 External Signals、§35.4.5 LPDDR2 and DDR3 pin mux mapping

| MMDC 信号 | 描述 | 方向 |
|-----------|------|------|
| DRAM_ADDR[15:0] | 地址总线 | 输出 |
| DRAM_CAS | 列地址选通 | 输出 |
| DRAM_CS[1:0] | 片选 | 输出 |
| DRAM_DATA[31:0] | 数据总线 | 双向 |
| DRAM_DQM[1:0] | 数据掩码 | 输出 |
| DRAM_ODT[1:0] | 片上终端匹配 | 输出 |
| DRAM_RAS | 行地址选通 | 输出 |
| DRAM_RESET | 复位信号 | 输出 |
| DRAM_SDBA[2:0] | Bank 选择 | 输出 |
| DRAM_SDCKE[1:0] | 时钟使能 | 输出 |
| DRAM_SDCLK0_P/N | 差分时钟 | 输出 |
| DRAM_SDQS[1:0]_P/N | 差分 DQS | 双向 |
| DRAM_SDWE | 写使能 | 输出 |
| DRAM_ZQPAD | ZQ 校准 | 输出 |


### 12.2 时钟系统

> **对应手册**：§35.3 Clocks

| 时钟名称 | 时钟根 | 描述 |
|---------|--------|------|
| aclk_fast_core_p0 | mmdc_axi_clk_root | 快速时钟（Core） |
| ipg_clk_p0 | ipg_clk_root | 外设时钟 |
| aclk_fast_phy_p0 | mmdc_axi_clk_root | 快速时钟（PHY） |

**注意**：i.MX 6ULL 中术语 clocks 和 cycles 可互换使用，均指主 DDR 时钟（mmdc_axi_clk_root）的周期。


### 12.3 MMDC 架构：Core + PHY

> **对应手册**：`IMX6ULL_Reference_Manual_Ch35_MMDC.md` — §35.1 Overview、§35.1.1 MMDC feature summary

```

  ┌──────────────────────────────────────────────────────┐
  │                    SoC (ARM Core)                    │
  │                        ↕ AXI 总线                     │
  ├──────────────────────────────────────────────────────┤
  │                   MMDC_CORE                          │
  │  ┌────────────┐  ┌──────────────┐  ┌──────────────┐ │
  │  │ AXI 接口    │  │ 请求队列      │  │ 重排序/优化   │ │
  │  │ (8/16/64b) │  │ 写:8 / 读:16  │  │ Bank 预测    │ │
  │  └────────────┘  └──────────────┘  └──────────────┘ │
  │         ↕                                              │
  │                   MMDC_PHY                           │
  │  ┌────────────┐  ┌──────────────┐  ┌──────────────┐ │
  │  │ 校准引擎    │  │ 延迟线调整    │  │ 时序控制      │ │
  │  │ ZQ/RD/WR   │  │ DQS/DQ/CK    │  │ 频率/占空比   │ │
  │  └────────────┘  └──────────────┘  └──────────────┘ │
  └────────────────────────┬─────────────────────────────┘
                           │ DDR 接口 (x16)
  ┌────────────────────────┴─────────────────────────────┐
  │  地址/命令/控制     │  数据/选通    │  特殊信号       │
  │  ADDR[15:0]        │  DQ[31:0]    │  ZQPAD          │
  │  CAS/RAS/WE        │  DQS_P/N     │  ODT[1:0]       │
  │  CS[1:0]           │  DQM[1:0]    │  RESET          │
  │  CKE[1:0]          │              │                 │
  │  CLK0_P/N          │              │                 │
  │  BA[2:0]           │              │                 │
  └──────────────────────────────────────────────────────┘
```

- **MMDC_CORE**：通过 AXI 接口与系统通信，生成 DDR 命令、执行命令优化（重排序、Bank 预测）、管理读写数据路径。
- **MMDC_PHY**：负责时序调整，使用特殊校准机制确保高达 400MHz 时钟速率下的数据捕获余量。

> **参考资料**：MMDC 完整框图见 `IMX6ULL_section35_1_4.md` 中的 MMDC Architecture 章节。

#### 配置模式（Configuration Mode）

在初始化 DDR 之前，需要让 MMDC 进入**配置模式**——这是一个"安全窗口"，期间所有 AXI 访问被阻断，可以安全地修改时序和几何参数寄存器。

**进入流程**（握手协议）：
1. 设置 `MDSCR[CON_REQ] = 1`，发出配置请求
2. 轮询 `MDSCR[CON_ACK]`，等待控制器确认
3. 确认收到后，MMDC 进入配置模式，**此时所有 AXI 访问被阻止**

**退出流程**：
- 清除 `MDSCR[CON_REQ] = 0`，MMDC 退出配置模式，恢复 AXI 访问

> **类比**：配置模式就像铁路维修窗口——拉下护栏（CON_REQ），等确认灯亮起（CON_ACK），此时没有列车（AXI 请求）能进入轨道，维修人员（软件）可以安全更换铁轨（寄存器配置）。修完后抬起护栏（清除 CON_REQ），恢复通车。

**DCD 脚本中的体现**：在 13.4 节脚本中，`setmem 0x021b001c = 0x00008000` 就是置位 CON_REQ，进入配置模式后后续的 MDCTL/MDCFG 等寄存器写入才能生效。

#### 读写数据流：一个 AXI 请求的生命周期

理解数据流有助于搞清楚"MMDC 收到 CPU 的读/写请求后，到底经历了什么"。

**写数据流**（§35.4.1.1）：

```
CPU 写请求
    ↓
[1] 进入写请求 FIFO（8 条目）
    └─ 要求至少有 2 个空位才接受
    └─ 如果 burst length > 8，拆成两次（一次 BL=8，一次余数）
    └─ 必须等所有数据 beat 都收到后才进入下一步
    ↓
[2] 轮询仲裁（Round-Robin，在读/写之间选）
    ↓
[3] 进入重排序队列，按动态评分选最优执行顺序
    ↓
[4] 胜出者被 dispatch
    ↓
[5] 命令引擎按需发 PRE/ACT 命令（根据 Bank 状态和时序参数）
    ↓
[6] 数据通过 PHY 驱动到 DDR 芯片
```

**读数据流**（§35.4.1.2）：

```
CPU 读请求
    ↓
[1] 进入读请求 FIFO（16 条目，是写队列的两倍）
    └─ 要求至少有 2 个空位才接受
    └─ burst > 8 时同样拆分
    ↓
[2] 轮询仲裁
    ↓
[3] 进入重排序队列
    ↓
[4] 胜出者等待：read data buffer 有空位才能 dispatch ← 这是读特有的 gating
    ↓
[5] 命令引擎发 PRE/ACT 命令
    ↓
[6] PHY 采样 DDR 返回的数据，存入 read data buffer
    ↓
[7] 数据返回给 AXI master
    └─ 关键字（critical word）一到就立即返回，不等全部读完
```

**为什么读队列（16）比写队列（8）大一倍？**
读操作对延迟更敏感——CPU 等数据回来才能继续执行，而写操作发出去就可以继续干别的事。更大的读队列能缓存更多待处理的读请求，让重排序机制有更多选择空间，提高 Page Hit 率和总线利用率。

### 12.4 AXI 接口与请求队列

> **对应手册**：§35.1.1（AXI interface 特性表）、§35.4.1 Write/Read data flow

#### SoC 内部总线位宽 vs DDR 控制器接口位宽

这是一个常见的疑惑：**为什么 SoC 的 AXI 数据总线可以是 32-bit 或 64-bit，而 DDR 控制器对外接口只有 x16？它们不一致怎么办？**

答案是：**MMDC 内部有一个位宽转换（数据拼接）模块**。

```
数据流示意（以 i.MX 6ULL 为例，AXI=32-bit，DDR=x16）:

SoC 内部（AXI 32-bit）       MMDC 内部转换           DDR 接口（x16）
  ┌──────────┐                                    ┌──────────┐
  │ D31...D0 │── 一次 AXI 读写（32bit）──→ │ 拆分/拼接  │── 第1次 DQS ──→│ D15...D0 │
  └──────────┘                            │  FIFO    │── 第2次 DQS ──→│ D15...D0 │
                                          └──────────┘            └──────────┘

写操作：SoC 发来 32bit → MMDC 拆成 2 次 x16 写到 DDR
读操作：MMDC 从 DDR 读 2 次 x16 → 拼成 32bit 返回给 SoC
```

**关键理解**：
1. **SoC 视角**：CPU 通过 AXI 总线发起 32-bit 的读写请求，它不关心 DDR 端是怎么传输的
2. **DDR 视角**：MMDC 把每次 32-bit 请求拆成 2 次 x16 的 DDR 事务
3. **带宽守恒**：DDR 接口频率足够高（如 400MHz × 16bit = 6.4Gb/s），能跟上 SoC 内部总线的带宽需求

这不是 i.MX 6ULL 特有的现象，**所有嵌入式 SoC 都存在类似的位宽转换**：
- 如果 AXI 总线 = DDR 接口位宽（都是 x16），则 1:1 传输，不需要拆分
- 如果 AXI 总线 > DDR 接口位宽（32 > 16），则 1 次 AXI = 2 次 DDR 事务
- 如果 AXI 总线 < DDR 接口位宽（理论上少见），则多次 AXI 拼成 1 次 DDR 事务

**类比**：就像快递运输——工厂（SoC）一次产出 32 个包裹，但卡车（DDR 接口）一次只能装 16 个，那就分两趟运。只要卡车跑得够快，工厂不会觉得慢。

| 特性 | 值 |
|------|-----|
| 总线协议 | AXI |
| 传输位宽 | 8 / 16 / 64 bit |
| 运行频率 | 最高 400MHz |
| 突发长度 | 最高 16 |
| 突发类型 | WRAP / INCR / FIXED |
| AXI ID 位宽 | 16 bit |

**请求队列**：
- 写请求 FIFO：8 条目
- 读请求 FIFO：16 条目


### 12.5 DDR 突发长度说明

> **对应手册**：§35.4.9 Burst Length options towards DDR

| 模式 | DDR 突发长度 |
|------|-------------|
| DDR3 | **固定为 8** |
| LPDDR2 | **固定为 4** |

> **注意**：前面表格中"AXI 突发长度最高 16"指的是 AXI 总线协议层的突发长度，不是 DDR 侧的突发长度。DDR3 模式下，所有 DDR 读写访问始终是 8 个字（x16），并按照 JEDEC 标准对齐。对于非对齐的 AXI INCREMENT 访问，无关字节通过 DQM 数据掩码屏蔽；对于非对齐的 AXI WRAP 访问，MMDC 内部有优化机制来提高 DDR 数据总线效率。


### 12.6 地址解码与地址空间

> **对应手册**：§35.4.4 MMDC Address Space（§35.4.4.1 Address decoding、§35.4.4.2 Chip select settings、§35.4.4.4 Address mirroring）

#### 12.6.1 地址解码规则

> **对应手册**：§35.4.4.1 Address decoding

MMDC 接收到的 AXI 地址是 32 位的，需要解码为四个字段：

1. **片选（Chip Select）**
2. **Bank 号**
3. **行号（Row）**
4. **列号（Column）**

定义 DDR 地址空间的关键寄存器：

| 寄存器字段 | 作用 |
|-----------|------|
| `MDMISC[DDR_4_BANK]` | 定义 DDR 是 4 Bank 还是 8 Bank |
| `MDCTL[DSIZ]` | 定义 DDR 数据总线位宽（x16） |
| `MDMISC[BI]` | 定义 Bank Interleaving 开/关 |
| `MDCTL[COL]` | 定义列地址位数 |
| `MDCTL[ROW]` | 定义行地址位数 |

**片选判决**：MMDC 比较 AXI 地址的最高 7 位（`ARADDR[31:25]` / `AWADDR[31:25]`）与 `MDASP[CS0_END]` 来决定访问 CS0 还是 CS1。

**地址位映射表**（以 x16 DDR、8 Bank、15 行、10 列为例）：

| AXI 地址位 | Bank Interleaving OFF | Bank Interleaving ON |
|-----------|----------------------|---------------------|
| A29 | — | ROW[14] |
| A28 | BANK[2] | ROW[13] |
| A27 | BANK[1] | ROW[12] |
| A26 | BANK[0] | ROW[11] |
| A25 | ROW[14] | ROW[10] |
| A24 ~ A12 | ROW[13] ~ ROW[1] | ROW[9] ~ ROW[0] |
| A14 | ROW[0] | BANK[2] |
| A13 | BANK[2] | BANK[1] |
| A12 | BANK[1] | BANK[0] |
| A11 | BANK[0] | COL[9] |
| A10 ~ A2 | COL[9] ~ COL[0] | COL[8] ~ COL[0] |
| A1 ~ A0 | — | — |

> **理解**：Bank Interleaving OFF 时，Bank 号从 AXI 的高位取（紧邻片选位），连续的地址可能跨 Bank；ON 时，Bank 号从行地址中"借用"低位，有利于连续地址落在同一 Bank 内。

**AXI 到 DDR 访问的转换**：
- **WRAP 突发（读）**：MMDC 会将非对齐的 AXI WRAP 突发拆分成多次 DDR 访问，并**优先返回关键字（critical word）**，剩余数据通过内部缓冲重排后按 AXI 顺序返回。
- **INCREMENT 突发（写）**：非对齐的 INCREMENT 写会被拆成两次 DDR 写，无关字节通过 **DQM 数据掩码**屏蔽。

#### 12.6.2 片选分区设置

> **对应手册**：§35.4.4.2 Chip select settings（§35.4.4.2.1 ~ §35.4.4.2.2 具体配置示例）

MMDC 支持最多两个连续的片选，每个片选密度相同，总密度必须是 2 的幂。

以 2 Gbyte 总空间、每片选 1 Gbyte 为例，有三种 `MDASP[CS0_END]` 配置选项：

| CS0_END 值 | CS0 范围 | CS1 范围 |
|-----------|---------|---------|
| `001_1111` | 0 ~ 1 Gbyte | 1 ~ 2 Gbyte |
| `011_1111` | 0 ~ 2 Gbyte（全部映射到 CS0） | 未使用 |
| `101_1111` | 0 ~ 3 Gbyte（含空洞） | 2 ~ 3 Gbyte |

#### 12.6.3 地址镜像（Address Mirroring）

> **对应手册**：§35.4.4.4 Address mirroring

当同一通道上挂有两颗 DDR 颗粒时，为简化 PCB 布线，硬件上可能将 CS1 的地址线交叉连接。MMDC 支持地址镜像配置，使控制器在向 CS1 发命令时自动交换地址位，确保逻辑地址与物理布线一致。

**引脚交换规则**（相邻位两两交换）：

| MMDC 引脚 | CS0 实际输出 | CS1 实际输出（镜像后） |
|----------|-------------|----------------------|
| DRAM_A3 | DRAM_A3 | DRAM_A4 |
| DRAM_A4 | DRAM_A4 | DRAM_A3 |
| DRAM_A5 | DRAM_A5 | DRAM_A6 |
| DRAM_A6 | DRAM_A6 | DRAM_A5 |
| DRAM_A7 | DRAM_A7 | DRAM_A8 |
| DRAM_A8 | DRAM_A8 | DRAM_A7 |
| DRAM_SDBA0 | DRAM_SDBA0 | DRAM_SDBA1 |
| DRAM_SDBA1 | DRAM_SDBA1 | DRAM_SDBA0 |

> **规律**：相邻位两两交换：(A3↔A4)、(A5↔A6)、(A7↔A8)、(SDBA0↔SDBA1)。这样 PCB 布线时可以走对称的蛇形线，减少交叉。

> **注意**：i.MX 6ULL 对 DDR3 只支持单片选，地址镜像主要适用于 LPDDR2 场景。

#### 12.6.4 AXI 到 DDR 的访问转换示例

> **对应手册**：§35.4.4.3 Translation of AXI accesses to DDR accesses

CPU 发出的 AXI 突发访问到达 MMDC 后，可能被拆分成多次 DDR 访问。理解这些例子有助于搞清楚"地址对齐、突发拆分、DQM 掩码"这三个核心概念。

**示例 1：Wrap 突发跨越边界（非对齐读）**

| AXI 属性 | 值 |
|---------|-----|
| 突发类型 | WRAP |
| AXI 位宽 | 128 bit（16B） |
| 突发长度 | 8 |
| 起始地址 | 0x...B0（非对齐） |
| DDR 位宽 | x32（4B） |

- AXI wrap 边界：每 16B × 8 = **128B (0x80)**
- DDR wrap 边界：每 4B × 8 = **32B (0x20)**
- CPU 期望的地址序列：**0xB0, 0xC0, 0xD0, 0xE0, 0xF0, 0x80, 0x90, 0xA0**

MMDC 拆成 **4 次 DDR 读访问**：

| DDR 访问 | 目标地址 | 说明 |
|---------|---------|------|
| 第1次 | 0xA0 | 最近的 DDR 边界，覆盖 0xA0~0xBF |
| 第2次 | 0xC0 | 覆盖 0xC0~0xDF |
| 第3次 | 0xE0 | 覆盖 0xE0~0xFF |
| 第4次 | 0x80 | 覆盖 0x80~0x9F（wrap 回到起点） |

**关键**：MMDC 先把 **0xB0 的关键字**（critical word）立即返回给 CPU，然后再按顺序返回其余数据。0xA0 的数据虽然最先从 DDR 读出，但被缓冲，最后才返回给 CPU。

**示例 2：Increment 突发跨越 DDR 边界（写）**

| AXI 属性 | 值 |
|---------|-----|
| 突发类型 | INCREMENT |
| AXI 位宽 | 64 bit（8B） |
| 突发长度 | 8 |
| 起始地址 | 0x...B0（对齐到 8B） |
| DDR 位宽 | x64（8B） |

- DDR 边界：每 8B × 8 = **64B (0x40)**
- CPU 写入地址：**0xB0, 0xB8, 0xC0, 0xC8, 0xD0, 0xD8, 0xE0, 0xE8**

MMDC 拆成 **2 次 DDR 写访问**：

| DDR 访问 | 目标地址 | DQM 掩码范围 |
|---------|---------|-------------|
| 第1次 | 0x80 | 0x80~0xAF 中的无关字节被 DQM 屏蔽 |
| 第2次 | 0xC0 | 0xF0~0xFF 中的无关字节被 DQM 屏蔽 |

**类比**：就像用固定大小的印章盖图章——如果图案跨了两张纸，那就盖两次，空白部分用白纸（DQM）遮住不盖。

**示例 3：Wrap 突发，边界完美对齐**

| AXI 属性 | 值 |
|---------|-----|
| 突发类型 | WRAP |
| AXI 位宽 | 128 bit |
| 突发长度 | 4 |
| 起始地址 | 0x...80（对齐） |
| DDR 位宽 | x64（8B） |

- AXI wrap 边界：16B × 4 = **64B (0x40)**
- DDR wrap 边界：8B × 8 = **64B (0x40)** ← **边界一致！**
- CPU 写入地址：**0x80, 0x90, 0xA0, 0xB0**

**结果**：只需 **1 次 DDR 写访问**到 0x80，因为边界对齐且起始地址对齐。

**示例 4：Increment 突发，非对齐起始地址**

| AXI 属性 | 值 |
|---------|-----|
| 突发类型 | INCREMENT |
| AXI 位宽 | 64 bit（8B） |
| 突发长度 | 2 |
| 起始地址 | 0x...05（非对齐） |
| WSTRB | 0xE0 |

- AXI 对齐边界：每 8B
- DDR 边界：每 4B × 8 = **32B (0x20)**
- CPU 写入：0x5（WSTRB=0xE0 表示部分字节有效）、0x8~0xF

MMDC 合并为 **1 次 DDR 写访问**到 0x0，地址 0x0~0x4 和 0x10~0x1F 通过 DQM 屏蔽。

**示例 5：Increment 突发，跨越 DDR 边界**

| AXI 属性 | 值 |
|---------|-----|
| 突发类型 | INCREMENT |
| AXI 位宽 | 64 bit（8B） |
| 突发长度 | 8 |
| 起始地址 | 0x...10（对齐） |
| DDR 位宽 | x64（8B） |

- DDR 边界：每 8B × 8 = **64B (0x40)**
- CPU 写入地址：**0x10, 0x18, 0x20, 0x28, 0x30, 0x38, 0x40, 0x48** ← 在 0x40 处跨越边界

MMDC 拆成 **2 次 DDR 写访问**：

| DDR 访问 | 目标地址 | DQM 掩码范围 |
|---------|---------|-------------|
| 第1次 | 0x00 | 0x00~0x0F 被 DQM 屏蔽 |
| 第2次 | 0x40 | 0x50~0x7F 被 DQM 屏蔽 |

**总结规律**：
- WRAP 突发可能被拆成多次 DDR 访问，但 MMDC 会**优先返回关键字**
- INCREMENT 突发如果跨越 DDR 边界，会被拆分，**无关字节用 DQM 掩码屏蔽**
- 当 AXI 和 DDR 的 wrap 边界**恰好一致**时，只需一次 DDR 访问


### 12.7 重排序机制与 Bank 预测

> **对应手册**：§35.5 Performance（§35.5.1 Arbitration and reordering mechanism、§35.5.2 Prediction mechanism、§35.5.3 Special Optimization for DDR3）

#### 仲裁流程（Arbitration General）

MMDC 的完整仲裁流程如下：

1. AXI 访问被采样进入读/写请求队列
2. 读/写仲裁器选择获胜者
3. 获胜者被采样进入**重排序队列**（Reordering Queue）
4. 重排序机制在合法请求中选择最优顺序，最大化 DDR 总线利用率
5. 完成后的访问从重排序队列中清除

#### 动态评分模式（Dynamic Scoring）

MMDC 为每个待处理请求计算**总分**，分数最高者获胜。评分由四个因素组成：

| 评分因子 | 寄存器字段 | 默认值 | 说明 |
|---------|-----------|--------|------|
| Page Hit 分数 | `MAARCR[ARCR_PAG_HIT]` | 4 | 如果请求命中已打开的 Page，加此分 |
| Access Hit 分数 | `MAARCR[ARCR_ACC_HIT]` | 2 | 如果请求类型与上一次相同，加此分 |
| 动态跳跃分数 | `MAARCR[ARCR_DYN_JMP]` | 1 | 每次请求**未被选中**时，此分 +1（饥饿计数） |
| QoS 分数 | AXI `arqos/awqos` 侧带信号 | — | 4 位优先级，值越高分数越高 |

总分上限为 **0xF**，防止溢出。

#### 保护机制（Guarding / Aging）

为防止低优先级请求被**永久饥饿**，MMDC 内置保护机制：

- 当某请求的动态跳跃分数达到最大值（`MAARCR[ARCR_DYN_MAX]`，默认 15），启动保护计数器
- 保护计数器每轮未选中 +1，达到 `MAARCR[ARCR_GUARD]`（默认 15）后，该请求获得**最高优先级**
- 除非有实时通道（Real-Time Channel）请求到达，否则必须优先处理

> **默认配置**：`ARCR_DYN_MAX = 15`, `ARCR_GUARD = 15`，即一个请求最多等待 15 轮后强制优先。

#### 实时通道模式（Real-Time Channel）

当 `MAARCR[ARCR_RCH_EN] = 1`（默认启用）时，QoS = `0xF` 的访问**绕过所有其他待处理访问**，直接优先执行。这为音视频等对延迟敏感的实时数据流提供了硬件级保障。

#### Bank 预测

MMDC 在重排序的同时并行执行**预测机制**，在 dispatch 之前预测 CS、Bank 和 Row。预测使用三个层级的待处理访问：
1. 处于第一流水线的访问
2. AXI 总线上的合法访问
3. 来自仲裁的合法访问（下一个 miss 访问）

通过 `MDMISC[MIF3_MODE]` 启用。

#### DDR3 特殊优化

**非对齐 WRAP 访问优化**：当 AXI wrap 突发非对齐但**其 wrap 边界与 DDR wrap 边界一致**时，MMDC 会优化为只发一次 DDR 访问（而不是拆分多次），内部进行数据重排。

**具体例子**（写访问）：
- AXI 位宽 128 bit，长度 4，起始地址 0x10（非对齐到 64B 边界）
- AXI wrap 边界：16B × 4 = **64B (0x40)**
- DDR3 x64 (BL=8)：8B × 8 = **64B (0x40)** ← **边界一致！**
- MMDC 收到数据的顺序是：**0x10, 0x20, 0x30, 0x00**
- MMDC 内部重排为：**0x00, 0x10, 0x20, 0x30**
- 然后只发**一次 DDR 写访问**到地址 0x00

如果不做这个优化，MMDC 需要发两次 DDR 写访问（用 DQM 掩码屏蔽无关字节），效率更低。

**读访问的关键字优先**：同样的场景，MMDC 在发一次 DDR 读访问到 0x00 后，一旦拿到 0x10 的数据（关键字），**立即返回给 CPU**，不等 0x00, 0x20, 0x30 全部读完。这对 CPU 性能至关重要——CPU 可以尽早拿到它最需要的数据。


### 12.8 Page Hit / Page Miss 优化

> **对应手册**：§35.1.1（Page hit/page miss optimizations）

| 情况 | 说明 | 优化 |
|------|------|------|
| Page Hit | 目标 Row 已在行缓冲区中 | 直接发送 READ/WRITE，跳过 ACT |
| Page Miss | 目标 Row 不在行缓冲区中 | 需要先 ACT，再 READ/WRITE |
| Page Close | 目标 Bank 空闲 | ACT → READ/WRITE |

MMDC 自动跟踪打开的内存页面，最大化 Page Hit 率。


### 12.9 AXI 错误处理与独占访问

> **对应手册**：§35.4.10 Exclusive accesses handling、§35.4.11 AXI Error Handling

#### AXI 响应类型

| 响应 | 触发条件 |
|------|---------|
| **OKAY** | 访问成功，或独占访问失败 |
| **SLV Error** | 安全违规（可通过 `MAARCR[30]` 配置为返回 OKAY） |
| **EXOKAY** | 独占读/写成功 |

读错误时，MMDC 在返回的读数据总线上驱动全零。

#### 独占访问（Exclusive Accesses）

MMDC 内置 **4 个独占监视器**，每个监视器对应一个配置的 AXI ID（通过 `MAEXIDR0` 和 `MAEXIDR1` 寄存器）。

**合法独占访问的条件**（全部必须满足）：
- 地址对齐（AXI 地址对齐到 AXI 大小）
- 单次访问（AXI 突发长度 ≤ 1）
- AXI 大小不超过 64 位
- AXI 非缓存访问（`ARCACHE[1]` / `AWCACHE[1]` = 0）
- AXI ID 匹配已配置的四个独占 ID 之一

**独占访问完整行为决策树**：

```
独占读请求到达
    │
    ├─ 安全违规？
    │   ├─ 是 → 阻断，不发往 DDR
    │   │       └─ MAARCR[30]=1 → SLV Error
    │   │       └─ MAARCR[30]=0 → OKAY
    │   │
    │   └─ 否 → 其他规则违规？
    │           ├─ 是 → 仍然发往 DDR，但响应类型不可预测
    │           │
    │           └─ 否 → 发往 DDR，监视器 ON，响应 EXOKAY ✓
    │
    └─ 同 ID 的另一次合法独占读？
        └─ 监视器更新为最新属性（覆盖之前的）


独占写请求到达
    │
    ├─ 安全违规？
    │   ├─ 是 → 阻断，监视器保持 ON
    │   │       └─ MAARCR[30]=1 → SLV Error
    │   │       └─ MAARCR[30]=0 → OKAY
    │   │
    │   └─ 否 → 其他规则违规？
    │           └─ 是 → 阻断，不发往 DDR，响应不可预测
    │
    ├─ 监视器 OFF？
    │   └─ 是 → 阻断
    │           └─ MAARCR[28]=1 → SLV Error
    │           └─ MAARCR[28]=0 → OKAY
    │
    ├─ 同 ID 但属性不同？
    │   └─ 是 → 阻断，监视器 OFF
    │           └─ MAARCR[28]=1 → SLV Error
    │           └─ MAARCR[28]=0 → OKAY
    │
    ├─ 非独占写（普通写）到同地址？
    │   └─ 发往 DDR，监视器 OFF（后续独占写将失败）
    │
    └─ 合法独占写，监视器 ON？
        └─ 发往 DDR，响应 EXOKAY ✓
```

**关键配置位**：

| 寄存器位 | 名称 | 作用 |
|---------|------|------|
| `MAARCR[28]` | ARCR_EXC_ERR_EN | 独占违规时返回 SLV Error（=1）还是 OKAY（=0） |
| `MAARCR[30]` | ARCR_SEC_ERR_EN | 安全违规时返回 SLV Error（=1）还是 OKAY（=0） |

> **类比**：独占访问就像银行的"保险箱租用协议"——你先登记（独占读，监视器 ON），然后你可以来取（独占写，返回 EXOKAY）。但如果期间有人普通访问了同一个保险箱（非独占写），你的协议就失效了（监视器 OFF），再来取就失败了（返回 OKAY 表示独占失败）。



### 12.10 ODT 配置（On-Die Termination）

> **对应手册**：§35.10 ODT Configuration

#### ODT 配置（MMDC 侧）

| 寄存器 | 作用 |
|--------|------|
| `MDOTC` | ODT 时序控制（tAOFPD/tAONPD/tANPD/tAXPD/tODTLon） |
| `MPODTCTRL` | 读写访问时 ODT 的通断控制 |
| `MDMRR` | MRR 数据 |

**tODTLon = WL - 2 规则**：

JEDEC DDR3 标准规定，从控制器断言 DRAM_ODT 信号到 DDR 芯片内部的 RTT 终端电阻真正导通，中间有一个固定延迟。这个延迟等于**写延迟（WL）减 2**。因此在 MMDC 中配置 `MDOTC[tODTLon]` 时必须与 `MDCFG1[tCWL]` 对应：如果 CWL=6（DDR3-1600 典型值），则 tODTLon = 6-2 = 4。



**MDOTC 寄存器字段详解**：

| 字段 | 含义 | DDR3 典型配置 |
|------|------|--------------|
| `tAOFPD` | 异步 RTT 关闭延迟（Power Down 时 DLL 冻结）。从终止电路开始关闭到高阻抗完全建立的时间 | 由 DDR 芯片规格决定 |
| `tAONPD` | 异步 RTT 开启延迟（Power Down 时 DLL 冻结）。从高阻抗到 RTT 电阻完全导通的时间 | 由 DDR 芯片规格决定 |
| `tANPD` | 异步 ODT 到 Power Down 进入的延迟。DDR3 中应设为 tCWL-1 | tCWL-1 |
| `tAXPD` | ODT 到 Power Down 退出的延迟 | 由规格决定 |
| `tODTLon` | ODT 信号到 RTT 的延迟，= WL-2 | 对应 MDCFG1[tCWL] |
| `tODT_idle_off` | 空闲时 ODT 自动关闭的计数器 | 可配，用于省电 |

**ODT 断言规则**（`MPODTCTRL` 控制）：

| 场景 | ODT 行为 |
|------|---------|
| 对**非活跃** CS 发写命令 | 如果 `MPODTCTRL[0]=1`，对未参与访问的 CS 也断言 ODT（终结未选中芯片的反射） |
| 对**非活跃** CS 发读命令 | 如果 `MPODTCTRL[1]=1`，同上 |
| 对**活跃** CS 发写命令 | 由 JEDEC RTT_WR（MR1[A10,A9]）控制，MMDC 不额外干预 |
| 对**活跃** CS 发读命令 | 由 JEDEC RTT_NOM（MR1[A6,A2]）控制 |
| Precharge Power Down | 使用 tAOFPD/tAONPD 时序，ODT 根据配置断言或关闭 |

> **类比**：ODT 就像给没在说话的 DDR 芯片穿上吸音棉——即使它没被访问，信号线上传播的电信号也会到达它的引脚，如果不终结就会产生反射。MPODTCTRL 就是决定什么时候给谁穿吸音棉的开关。

### 12.11 刷新方案（Refresh Scheme）

> **对应手册**：§35.4.8 Refresh Scheme

MMDC 的自动刷新由 `MDREF` 寄存器控制，支持灵活的刷新策略，允许系统在每次刷新周期内配置期望的 AXI 访问延迟。

**周期性自动刷新的时钟源**（三选一）：

| 时钟源 | 说明 |
|--------|------|
| 32 kHz | 低频时钟 |
| 64 kHz | 低频时钟 |
| MMDC 工作时钟 | DDR 主时钟 |

**四种刷新方案配置**（以 3.9μs 刷新周期为基准，tREFI = 3.9μs）：

| 方案 | 描述 | REFR | REF_SEL | REF_CNT | DDR 挂起时间 |
|------|------|------|---------|---------|-------------|
| 1 | 每 31,250 ns 发 8 次刷新 | 0x7 (8次) | 0x0 (64 kHz) | 不需要 | tRFC × 8 |
| 2 | 每 15,625 ns 发 4 次刷新 | 0x3 (4次) | 0x1 (32 kHz) | 不需要 | tRFC × 4 |
| 3 | 每 7,800 ns 发 2 次刷新 | 0x1 (2次) | 0x2 (REF_CNT) | 3120 (0xC30) | tRFC × 2 |
| 4 | 每 3,900 ns 发 1 次刷新 | 0x0 (1次) | 0x2 (REF_CNT) | 1560 (0x618) | tRFC |

> **权衡理解**：方案 1 一次性连续发 8 次刷新命令，DDR 在 tRFC × 8 时间内不能读写（挂起最长），但两次刷新间隔最长（31.25μs），AXI 总线有更多连续可用时间；方案 4 每次只发 1 次刷新，DDR 挂起最短，但需要更频繁地打断 AXI 访问。**选择哪个方案取决于系统对延迟突发性的容忍度**。


### 12.12 省电模式（Power Saving）

> **对应手册**：§35.4.6 Power Saving and Clock Frequency Change modes（§35.4.6.1 Power saving general、§35.4.6.2 Self refresh and Frequency change entry/exit）

#### Self-Refresh（自刷新）

DDR 芯片在 Self Refresh 模式下**自行管理刷新操作**，MMDC 可以关闭 DDR 时钟。

**进入方式**：
1. **LPMD（Low Power Mode）**：用于**省电目的**
   - 硬件握手：LPMD/LPACK 信号与系统时钟模块交互
   - 软件握手：设置 `MAPSR[LPMD]`，轮询 `MAPSR[LPACK]`
   - **自动进入**：通过 `MAPSR[PST]` 配置空闲周期数（64 ~ 16320 个时钟周期），清空 `MAPSR[PSD]`
2. **DVFS（Dynamic Voltage and Frequency Change）**：用于**时钟频率变化**
   - 硬件握手：DVFS/DVACK 信号
   - 软件握手：设置 `MAPSR[DVFS]`，轮询 `MAPSR[DVACK]`
3. **自动进入**：配置空闲周期数后自动进入

> **LPMD vs DVFS 的区别**：两者进入/退出流程相同，但目的不同。LPMD 纯粹为了省电（降低功耗），DVFS 是为了改变 DDR 工作频率（配合 DVFS 调频调压）。SR 期间不需要发周期性的刷新命令。

**SR 进入流程**：
1. 检测到 LPMD/DVFS 请求后，MMDC **立即**反断言 AXI `ARREADY/AWREADY`，阻止新请求（即使 ACK 还未断言）
2. 完成所有已打开的 AXI 访问
3. 按正确时序关闭（预充电）所有 Bank
4. 满足 tRP/tRPA 后，驱动自刷新命令（反断言 CKE + 刷新命令）
5. 反断言 DDR 时钟（CK）
6. 断言 LPACK/DVACK

**退出流程**：
1. 打开 MMDC 工作时钟（必须在 LPMD/DVFS 反断言**之前**）
2. 驱动 CK 时钟到 DDR
3. 满足 tCKSRX 后，断言 CKE
4. 解除 LPACK/DVACK
5. 满足 tXS 后，发出 REF 命令
6. 如果 ZQ 校准启用，执行 ZQ Long（满足 tZQoper）
7. 满足 tDLLK 后，恢复正常操作

> **注意**：检测到 LPMD/DVFS 请求时，MMDC 会**立即**反断言 `ARREADY/AWREADY`，在 ACK 断言之前就阻止新的 AXI 读写请求。

#### Power Down（掉电模式）

比 Self Refresh 更轻量级的省电模式：

| 类型 | 说明 |
|------|------|
| Precharge Power Down | 所有 Bank 预充电后进入掉电 |
| Active Power Down | 保持 Row 激活状态下进入掉电 |
| Fast Exit | 快速退出（功耗略高，退出快） |
| Slow Exit | 慢速退出（功耗更低，退出慢），DDR3 中通过 `MDPDC[SLOW_PD]` 配置 |

**自动进入配置**：`ESDPDC` 寄存器中的 `PWDT_0`/`PWDT_1` 定义每个片选的空闲周期数，可分别配置。

**BOTH_CS_PS**：MMDC 可以独立让每个片选进入 Power Down（根据各自空闲状态），也可以要求**两个片选都空闲**才一起进入。

#### 自动预充电（Auto Precharge）

通过 `ESDPDC` 的 `PRCT_0` 和 `PRCT_1` 字段，可配置每个片选在空闲 N 个周期后**自动预充电所有 Bank**。可配置值范围：2 ~ 128 个周期。


### 12.13 复位机制（Reset）

> **对应手册**：§35.4.7 Reset（§35.4.7.1 Hard reset、§35.4.7.2 Warm reset、§35.4.7.3 Software reset）

MMDC 支持三种复位方式，按影响程度从轻到重排列：

| 复位类型 | 触发方式 | 配置/状态寄存器 | DDR 数据 | 需重新初始化 |
|---------|---------|---------------|---------|-----------|
| 软件复位 | `MDMISC[RST] = 1` | 保留 | 保留 | 否 |
| 热复位 | `warm_reset` + `aresetn` 信号 | 保留 | 保留 | 否 |
| 硬复位 | `aresetn = 0`（`warm_reset = 0`） | 全部清零 | **丢失** | **是** |

#### 硬复位（Hard Reset）

当 `aresetn` 被拉低且 `warm_reset` 为低时，整个 MMDC 被初始化——所有配置/状态寄存器和状态机全部复位。**DDR 必须重新配置**才能访问。

#### 热复位（Warm Reset）

热复位会复位 MMDC 内部寄存器，但**保留配置和状态寄存器**，因此 DDR 中的数据不会丢失，也无需重新初始化序列。

**操作流程**：
1. MMDC 进入自刷新模式（通过 LPMD 或 DVFS 请求）
2. 等待 LPMD/DVFS 确认（ACK）
3. 拉高 `warm_reset` 信号
4. 拉低 `aresetn` 信号
5. 释放 `aresetn`
6. 释放 `warm_reset`
7. 退出 LPMD/DVFS 模式

#### 软件复位（Software Reset）

与热复位类似，但通过软件设置 `MDMISC[RST]` 触发。配置/状态寄存器保留。

**操作流程**：
1. MMDC 进入自刷新模式（通过 LPMD 或 DVFS 请求）
2. 等待 LPMD/DVFS 确认
3. 设置 `MDMISC[RST]` 断言软件复位
4. 退出 LPMD/DVFS 模式

> **应用场景**：热复位和软件复位适用于需要在不复位 DDR 内容的前提下复位 MMDC 控制器的场景，如 SoC 系统级复位但保持 DDR 数据。


### 12.14 DLL 切换（DLL Switching）

> **对应手册**：§35.9 DLL Switching（§35.9.1 DLL Off mode）

#### DLL Off 模式

仅在 DDR3 模式下支持，允许 DDR 在**低频**下运行（低于 125 MHz，JEDEC 标准定义）。DLL Off 模式用于 DVFS 降频场景。

**DLL On → DLL Off 切换步骤**：

1. 断言 `CON_REQ`，等待 `CON_ACK`
2. 禁用可能冲突的 Power Down 定时器（`MAPSR[PSD]`, `MDPDC[PWDT_0/1]`, `MDPDC[PRCT_0/1]`）
3. 执行 Precharge All 命令（通过 `MDSCR`）
4. MRW 到 MR1：禁用 RTT Nom（A9,A6,A2=0），DLL ON（A0=1）
5. MRW 到 MR2：更新 CWL = 6
6. MRW 到 MR0：更新 CL = 6
7. 反断言 `CON_REQ`
8. 进入自刷新模式，在 ACK 后**切换频率**
9. 退出自刷新
10. 断言 `CON_REQ`，等待 `CON_ACK`
11. 通过 IOMUX 在 DQS 上使能下拉电阻
12. 更新 MMDC 寄存器：tCWL=6、tCL=6（`MDCFG0/1`），禁用 ODT（`MPODTCTRL=0`），禁用 DQS 门控（`MPDGCTRL0[DG_DIS]=1`）
13. 恢复 Power Down 定时器
14. 反断言 `CON_REQ`

**DLL Off → DLL On 切换步骤**：

1. Precharge All
2. 进入自刷新 → 切换频率 → 退出自刷新
3. 断言 `CON_REQ`，等待 `CON_ACK`
4. 禁用 Power Down 定时器
5. MRW 到 MR1：启用 RTT Nom，DLL ON（A0=0）
6. MRW 到 MR0：重置 DLL（A8），更新 CL
7. MRW 到 MR2：更新 CWL
8. 执行 ZQ 命令
9. 重新配置 MMDC：更新 tCWL/tCL，启用 ODT，启用 DQS 门控，禁用 DQS 下拉
10. 恢复 Power Down 定时器
11. 反断言 `CON_REQ`


### 12.15 校准机制

> **对应手册**：§35.11 Calibration Process（§35.11.2 ZQ calibration、§35.11.3~§35.11.6 读/写/Write Leveling 校准、§35.11.10 Duty cycle adjustment）

MMDC PHY 支持多种校准（可硬件自动或软件手动）。ZQ/ODT 的原理详见 [01_ddr_theory.md](01_ddr_theory.md) 第 7 章 DDR3 部分，本节只列出 MMDC 寄存器层面的校准配置。ODT 配置见 12.10 节。

#### ZQ 校准（MMDC 侧）

**校准触发时机**：

| 类型 | 触发方式 | MMDC 寄存器 | 说明 |
|------|---------|-----------|------|
| ZQ Short | 硬件自动（周期性） | `MPZQHWCTRL` | 短期校准，维持驱动强度精度 |
| ZQ Long | 硬件自动（退出 Self Refresh） | `MPZQHWCTRL` | 长期校准，完全重新校准 |
| ZQ INIT | 软件手动 | `MPZQHWCTRL` | 初始化时执行 |

**MMDC 硬件 ZQ 校准算法**（5 位二进制搜索）详见 13.4.5 节。

#### 读/写数据校准

| 校准类型 | MMDC 寄存器 | 说明 |
|---------|-----------|------|
| 读数据校准 | `MPRDDLCTL` | 调整读 DQS 与读数据字节的对齐 |
| 读 DQS 门控校准 | `MPDGCTRL` | 调整 DQS 门控与读前导窗口的对齐（仅 DDR3） |
| 写数据校准 | `MPWRDLCTL` | 调整写 DQS 与写数据字节的对齐 |
| Write Leveling | `MPWLDECTRL` | 调整写 DQS 与 CK 差分时钟的对齐 |
| 读精细调优 | `MPRDDQBYnDL` | 每个读数据位最多 7 个延迟线单位 |
| 写精细调优 | `MPWRDQBYnDL` | 每个写数据位最多 3 个延迟线单位 |


#### 精细调优（Fine Tuning）

在校准（粗调）完成后，MMDC 还提供了一组精细调优电路，用于补偿每个引脚级别的微小偏差。

**写精细调优**（Write Fine Tuning，`§35.11.7`）：

对每个 DQ/DM 引脚相对于 DQS 进行**最多 100 ps**的微调。通过 `MPWRDQBYnDL` 寄存器，每个 DQ/DM 可独立配置 0~3 个延迟单位，每个单位约 **30~35 ps**。

```
总写延迟 = MPWRDLCTL[WR_DL_ABS_OFFSET]（粗调，可达半个周期）
         + MPWRDQBYnDL[wr_dqN_del]（精细，最多 3 × 35ps ≈ 100ps）
```

**读精细调优**（Read Fine Tuning，`§35.11.8`）：

对每个读入的 DQ 引脚相对于 DQS 进行 **±100 ps** 的微调。通过 `MPRDDQBYnDL` 寄存器，每个 DQ 可独立配置最多 7 个延迟单位。

> **有趣的读精细调优机制**：如果 DQ 落后 DQS 太多（即使精细调优加到最大也追不上），MMDC 采用一个巧妙的方法——先把 DQS 延迟减 100 ps（让"裁判"等一等），再把 DQ 加 200 ps（让"选手"跑快点），净效果 = DQ 相对 DQS 提前了 100 ps。

**ZQ 精细调优**（ZQ Fine Tuning，`§35.11.9`）：

通过 `MPPDCMPR2[ZQ_PU_OFFSET]` 和 `MPPDCMPR2[ZQ_PD_OFFSET]` 在 ZQ 校准结果基础上额外偏移 **-7 ~ +7**。用于补偿：
- PCB 走线长度差异导致的阻抗变化
- 特殊负载场景（多颗粒并联时总负载不同）
- 温度补偿（高温下驱动强度下降，可手动偏移补偿）

**DDR 时钟精细调优**：

通过 `MPCKDL` 寄存器对 DDR 时钟 CK0 进行微调（`SDclk0_del` 字段，0~3 个延迟单位）。用于补偿 CLK 与 DQS/地址线之间的 PCB 走线 skew。

**占空比调整**（Duty Cycle Adjustment，`MPDCCR`）：

DDR 时钟是差分信号（CK/CKB），理想情况下高低各占 50%。但由于 PCB 走线或缓冲器差异，可能产生占空比失真。`MPDCCR` 寄存器可以调整 CK/CKB 的占空比，确保时钟波形对称。这在高频 DDR3 运行时尤为重要，因为非对称时钟会导致 setup/hold 时间裕量不均匀。


### 12.16 调试监视器与性能分析（Debug & Profiling）

> **对应手册**：§35.6 MMDC Debug（Hardware debug monitor、SBS software monitor）、§35.7 MMDC Profiling

#### 硬件调试监视器（Hardware Debug Monitor）

启用 `MADPCR0[DBG_EN] = 1` 后，每个被 dispatch 到 DDR 的访问都会通过 I/O 引脚（`ipp_do_ddr_debug[50:0]`）输出观测信号：

| 信号 | 位数 | 说明 |
|------|------|------|
| `acc_addr` | [31:0] | AXI 地址 |
| `acc_type` | 1 | 0=写，1=读 |
| `acc_id` | [15:0] | AXI 事务 ID |
| `valid_strobe` | 1 | 有效请求指示（1 个时钟周期） |

信号组织：`MMDC_DEBUG[50:0] = {1'b0, valid_strobe, acc_id, access_type, addr}`

这些信号可通过 IOMUX 配置为芯片外部引脚输出，方便示波器或逻辑分析仪抓取。

#### 逐步（SBS）软件监视器

启用 `MADPCR0[SBS_EN] = 1` 后，**所有 DDR 访问暂停**。每次设置 `MADPCR0[SBS] = 1` 会：
1. 仅 dispatch MMDC 队列头部的一个待处理访问（读或写）
2. 该访问的 AXI 属性被采样到 `MASBS0` 和 `MASBS1` 寄存器
3. `MADPCR0[SBS]` 自动清零

> **应用**：SBS 模式常用于 DDR 时钟频率缩放过渡期间，防止频率切换过程中发生 DDR 访问。**注意**：`MAARCR[ARCR_ARB_REO_DIS]` 会禁用 SBS 功能。

#### 性能分析（Profiling）

MMDC 提供 6 个性能计数器，可计算 DDR 利用率和读写统计：

| 寄存器 | 计数器 | 说明 |
|--------|--------|------|
| `MADPSR0` | 总周期数 | profiling 期间的总时钟周期（最大 2^32） |
| `MADPSR1` | 忙周期数 | MMDC 状态机非空闲的周期数 |
| `MADPSR2` | 读访问次数 | 发往 DDR 的读访问总数 |
| `MADPSR3` | 写访问次数 | 发往 DDR 的写访问总数 |
| `MADPSR4` | 读字节数 | 从 DDR 读取的总字节数 |
| `MADPSR5` | 写字节数 | 写入 DDR 的总字节数 |

**控制位**（`MADPCR0`）：
- `DBG_EN`：启用 profiling
- `PRF_FRZ`：冻结计数器（暂停统计）
- `DBG_RST`：清零所有计数器
- `CYC_OVF`：总周期溢出标志

**按 AXI ID 过滤**（`MADPCR1`）：通过 `PRF_AXI_ID` 和 `PRF_AXI_ID_MASK` 可只统计特定 AXI ID 的访问。匹配公式：`(AXI-ID & MASK) Xnor (PRF_AXI_ID & MASK)`。例如要监控 ID 范围 A100~A1FF：`PRF_AXI_ID = 0xA100`, `PRF_AXI_ID_MASK = 0xFF00`。

---

## 13. i.MX 6ULL 实战与调试

> **本章是最终目的**：前面第 12 章 MMDC 控制器的架构知识都在这里落地——将正确的参数填入正确的寄存器，完成 DDR 初始化和调试。

以 **i.MX6ULL** 为例，DDR 初始化是一个软硬件深度结合的过程，核心目标是让处理器能够正确识别并稳定读写板载的 DDR 内存。如果初始化失败，系统通常会在启动阶段（如 U-Boot）直接卡死。

### 13.1 工程师的准备工作

DDR 初始化不是千篇一律的，必须根据实际硬件"量体裁衣"。在板子上电之前，工程师需要完成两项工作：**从芯片手册提取参数**和**生成 DCD 初始化脚本**。

#### 13.1.1 参数提取

从 DDR 芯片数据手册中获取关键参数（容量、位宽、行列地址、时序参数等）。详见 13.2 节。

#### 13.1.2 DCD 脚本生成

使用 NXP 官方的 **ddr_stress_tester** 工具，填入硬件参数进行时序校准和验证，生成包含成百上千条"寄存器地址 + 配置值"的 **.inc 初始化脚本**（即 DCD，Device Configuration Data）。详见 13.3 节。

> **产出物**：一份 `.inc` 文件，内容是一系列 `setmem` 指令。这份文件就是板子运行时 Boot ROM 要执行的"操作说明书"。

---

### 13.2 板载 DDR 初始化流程

> **对应手册**：§35.4.2 MMDC initialization、§35.4 MMDC Functional Description

前面两节讲的是工程师**离线**做的准备工作，本节讲板子上电后 DDR 初始化的**运行时**完整流程。

#### 13.2.1 Boot ROM 与 DCD 机制

**Boot ROM：芯片里的"第一推动力"**

i.MX6ULL 上电复位后，CPU 执行的第一行代码是内部固化的 **Boot ROM**（不可修改）。它的首要任务：

1. 检查启动引脚（BOOT_MODE）电平，判断从哪个设备启动（SD/eMMC/NAND）
2. 从该设备的固定偏移地址读取镜像头部到片内 **OCRAM**（片内 RAM，此时 DDR 尚未初始化）
3. 解析镜像头部，执行 DCD 数据完成 DDR 初始化
4. 将真正的程序（U-Boot）搬运到 DDR 并跳转执行

**DCD：DDR 初始化的"操作说明书"**

DCD（Device Configuration Data）的本质是一串**静态数据**，不是可执行代码。它包含一组组"寄存器地址 + 配置值"的键值对，由 Boot ROM 读取并照单配置寄存器。

**DCD vs SPL 对比**：

| 方案 | 启动流程 |
|------|---------|
| **传统 SPL**（如 S3C2440） | Boot ROM → 搬运 SPL 代码到 SRAM → CPU 执行 SPL 初始化 DDR → 搬运 U-Boot 到 DDR → 跳转 |
| **i.MX6ULL DCD** | Boot ROM → 读取 DCD 数据到 OCRAM → Boot ROM 直接解析 DCD 配置寄存器完成 DDR 初始化 → 搬运 U-Boot 到 DDR → 跳转 |

i.MX6ULL 通过硬件级优化，用 Boot ROM + DCD 数据**代替了传统 SPL 代码**的工作，因此常规开发中看不到 `spl.bin` 文件，直接面对 `u-boot.imx`。

**镜像头部结构（IVT + Boot Data + DCD）**：

编译出的普通 `.bin` 文件不能直接烧录启动，必须在前面加上特殊头部生成 `.imx` 文件（如 `u-boot.imx`）。前 1KB 区域排布严格固定：

```
u-boot.imx 头部结构（前 1KB）：
┌──────────────────────────────────────┐
│ IVT (Image Vector Table)  32 字节    │ ← "目录"：程序入口、DCD 地址等
├──────────────────────────────────────┤
│ Boot Data                    12 字节  │ ← 镜像大小、搬运目标地址
├──────────────────────────────────────┤
│ DCD (Device Config Data)    可变长度  │ ← 成百上千条 Address + Value 指令
└──────────────────────────────────────┘
```

**Boot ROM 执行流程**：
1. 从外部存储读取镜像头部（IVT + Boot Data + DCD）到 OCRAM
2. 解析 IVT，通过偏移 `0x2C` 处的指针定位 DCD 数据
3. 逐条执行 DCD 指令（向指定地址写入配置值）
4. DCD 执行完毕 → DDR 就绪 → 搬运 U-Boot 主体到 DDR

**DCD 数据格式**：

| 字段 | 值 | 说明 |
|------|-----|------|
| **DCD Header Tag** | `0xD2` | 标识"我是 DCD 数据" |
| **Length** | 可变 | DCD 区域总长度（含包头） |
| **Version** | `0x40`/`0x41` | 版本号 |
| **Write Command Tag** | `0xCC` | 标识"写寄存器"指令 |
| **Address** | 32 位 | 目标寄存器地址 |
| **Value** | 32 位 | 要写入的配置值 |

在 U-Boot 源码中，这些配置写在 `imximage.cfg` 文件中，编译时 `mkimage` 工具将其打包进 `u-boot.imx` 头部。

#### 13.2.2 JEDEC 标准 DDR3 上电初始化流程

JEDEC 规范（JESD79-3D）严格规定了 DDR3 上电后的初始化顺序，**一步都不能少，顺序不能改**。

**上电冷启动状态**：电容无电荷、模式寄存器未配置、DLL 未锁定、所有 Bank 关闭。此时 DDR 完全不响应读写命令。

**标准初始化序列**：

```
Step 1: 上电，等待电压稳定
         ↓
Step 2: 驱动 CKE = 0（关闭时钟使能）
         DDR 处于 NOP/Standby 状态，不听命令
         ↓
Step 3: 等待至少 200μs
         让 DLL 内部电路稳定，电容预充电
         ↓
Step 4: Precharge All
         关闭所有 Bank，确保干净状态
         ↓
Step 5: Auto Refresh × 2（连续两次）
         给电容"充电"，建立电荷状态
         第一次刷新后电荷还不稳定，
         第二次确保电容完全充满
         ↓
Step 6: Load Mode Register（加载模式寄存器）
         MR0: CAS 延迟（CL）、突发长度
         MR1: 驱动强度、ODT、DLL 开关
         MR2: CAS 写延迟（CWL）
         MR3: 温度刷新率（可选）
         ↓
Step 7: ZQ 校准（ZQCL 命令）
         DDR 芯片和控制器各自校准驱动强度
         ↓
Step 8: DLL 锁定完成
         DLL 需要额外 200 个时钟周期来锁定
         ↓
Step 9: 就绪，可以发读写命令
```

**为什么是这个顺序？**

- Step 2 必须最早做——上电就关 CKE，防止 DDR 在不稳定状态下误操作
- Step 4-5 必须在 Step 6 之前——行缓冲区和电容必须处于已知状态，才能加载模式寄存器
- Step 6（MR）必须在 Step 7（ZQ）之前——ZQ 校准需要知道驱动强度配置（MR1）
- Step 7 必须在 Step 8 之前——ZQ 和 DLL 都需要时间稳定

#### 13.2.3 i.MX6ULL 实际初始化流程

JEDEC 标准只规定了 DDR 芯片侧的开机仪式（Step 4~Step 8），但 SoC 端还需要配置自身的控制器和 PHY。下面是 JEDEC 标准 + MMDC 控制器初始化的完整流程：

```
Boot ROM 上电
    ↓
读取 DCD 数据到 OCRAM
    ↓
逐条执行 DCD 指令（写寄存器）：

  ┌─ SoC 端准备（与 JEDEC 无关）
  │  1. 禁用看门狗（WDOG）
  │  2. 使能 MMDC 时钟（CCM_CCGR）
  │  3. 配置 IOMUX（引脚复用 + 电气特性）
  │
  ├─ MMDC 控制器预配置（DDR 尚未激活）
  │  4. 设置 MDSCR CON_REQ（进入手动配置模式）
  │  5. 配置 PHY 校准预设值（ZQ/WL/DG/RD/WR 延迟线初始值）
  │  6. 配置 MMDC 时序与几何参数（MDCTL/MDCFG0/1/2/MDMISC/MDOTC/MDOR）
  │
  ├─ JEDEC 标准开机仪式（对应 JEDEC 流程 Step 4~8）
  │  7. Precharge All（通过 MDSCR 发出）
  │  8. Auto Refresh × 2（通过 MDSCR 发出，MMDC 自动等待 tRFC）
  │  9. Load Mode Register: MR2 → MR3 → MR1 → MR0（通过 MDSCR 逐条写入）
  │  10. ZQCL 校准命令（通过 MDSCR 发出）
  │
  └─ 收尾与功耗管理
     11. 配置自动刷新（MDREF）+ ODT 控制（MPODTCTRL）
     12. 使能 Power Down（MDPDC）+ 自动 Self-Refresh（MAPSR）
     13. 清除 MDSCR CON_REQ（退出配置模式，DDR 就绪）
    ↓
搬运 U-Boot 到 DDR
    ↓
跳转到 U-Boot 执行
```

> **关键理解**：DCD 脚本中的 PHY 校准参数（第5步）是**预设初始值**，不是运行时执行校准。真正的校准由 NXP **ddr_stress_tester** 工具在目标板子上跑完后，将最优值填入这些寄存器。Boot ROM 只是把预设值写入寄存器，后续 MMDC 硬件自动校准时会在此基础上精细调整。

**MDSCR 特殊命令寄存器**：

JEDEC 开机仪式通过 `MDSCR[CMD]` 发出命令：

| CMD 值 | 命令 | 说明 |
|--------|------|------|
| `0x0` | Precharge All | 关闭所有 Bank |
| `0x2` | Auto Refresh | 刷新命令（发两次） |
| `0x3` | Load Mode Register | 加载模式寄存器 |

每个命令发出去后，MMDC 自动等待对应的时序（tRP、tRFC 等），不用软件手动延迟。

**时间线**：

```
上电 ──→ Boot ROM 执行 DCD ──→ JEDEC 初始化 ──→ DDR Training ──→ DDR 就绪
 |            |                      |                 |               |
 0ms        ~10ms                 ~100μs            ~1ms          可以读写了
```

整个初始化通常在几十毫秒内完成。如果 DCD 参数写错了（如行列地址配错），DDR Training 阶段就会失败，Boot ROM 卡死。

### 13.3 芯片手册参数提取

初始化 i.MX6ULL 的 DDR 之前，需要从 DDR 芯片（如 Micron、Nanya 等）的 DataSheet 中提取以下三类参数。这是 13.1.1 节"参数提取"的具体展开。

#### 静态参数清单

**几何架构参数**（决定 MMDC 如何编址和寻址）：

| 参数 | 说明 | 示例 |
|------|------|------|
| **DRAM Density** | 芯片容量（Gb → MB 需 ÷8） | 4Gb = 512MB |
| **Bus Width** | 数据位宽 | 16-bit / 32-bit |
| **Banks** | Bank 数量（DDR3 = 8） | 8 |
| **ROW Addresses** | 行地址线数量 | 14 或 15 |
| **COLUMN Addresses** | 列地址线数量 | 10 或 11 |
| **Page Size** | 页大小 = 2^列地址数 × 位宽 | 2K / 4K |

**核心时序参数**（来自 "AC Electrical Characteristics" 表格）：

| 参数 | 全称 | 物理意义 | 单位 |
|------|------|---------|------|
| **tCL** | CAS Latency | 读命令 → 数据出现在总线的延迟 | tCK |
| **tRCD** | RAS to CAS Delay | 激活行 → 可读写列的延迟 | ns/tCK |
| **tRP** | Row Precharge Time | 关闭当前行 → 可打开新行的时间 | ns/tCK |
| **tRAS** | Active to Precharge | 行激活到预充电的最小间隔 | ns/tCK |
| **tRFC** | Refresh Cycle Time | 刷新周期（期间不能读写） | ns/tCK |
| **tWR** | Write Recovery Time | 最后一次写 → 可执行预充电的延迟 | ns/tCK |
| **tRC** | Row Cycle Time | 两次行激活之间的最小间隔 | ns/tCK |

**速度等级**：

| 参数 | 说明 |
|------|------|
| **Memory Type** | DDR3 / DDR3L / LPDDR2 等 |
| **Speed Bin** | DDR3-1600 / DDR3-1866 等，决定 MMDC 时钟频率 |

> **ns → tCK 换算**：MMDC 频率 400MHz → tCK = 1/400MHz = 2.5ns。例如 tRCD = 13.75ns → 13.75/2.5 ≈ 5.5 → **向上取整为 6 个 tCK**。实际开发中，这些繁琐的换算和寄存器拼装通常由 NXP 官方的 **DDR Script Aid**（Excel 工具）或 **ddr_stress_tester** 工具自动完成。

#### 动态信号认知（ODT / ZQ / DQS）

这些不属于"从手册抄参数"的范畴，而是在后续寄存器配置和硬件自动训练中解决。

| 信号 | 全称 | 作用 | 初始化关注点 |
|------|------|------|-------------|
| **ODT** | On-Die Termination | 片内终端电阻，消除信号反射 | 在 MMDC 寄存器中配置阻值（如 40Ω、120Ω），参考 NXP 评估板经验值 |
| **ZQ** | Impedance Calibration | 阻抗校准，抵抗 PVT 漂移 | 通过外部 240Ω 参考电阻（RZQ），发送 ZQCL 命令触发硬件自动校准 |
| **DQS** | Data Strobe | 数据选通信号，配合 DQ 精准采样 | 通过 Training 动态调整 DQS 与 DQ 的延迟对齐 |

> ODT/ZQ/DQS 的详细原理说明见 [01_ddr_theory.md](01_ddr_theory.md) 第 7 章 DDR3 部分。

### 13.4 DCD 初始化脚本实例

以下脚本由 NXP **ddr_stress_tester** 工具生成，对应硬件配置：

| 项目 | 值 |
|------|-----|
| SoC | i.MX6ULL |
| DDR 类型 | DDR3 |
| 颗粒型号 | Micron MT41K256M16HA-125 |
| 容量 | 4Gb（512MB） |
| 位宽 | x16 |
| 频率 | 400MHz |
| 片选数 | 1（CS0 only） |

#### 完整脚本源码

```text
//=============================================================================
// init script for i.MX6UL DDR3
//=============================================================================

wait = on

//=============================================================================
// Disable WDOG
//=============================================================================
setmem /16    0x020bc000 =    0x30

//=============================================================================
// Enable all clocks (they are disabled by ROM code)
//=============================================================================
setmem /32    0x020c4068 =    0xffffffff
setmem /32    0x020c406c =    0xffffffff
setmem /32    0x020c4070 =    0xffffffff
setmem /32    0x020c4074 =    0xffffffff
setmem /32    0x020c4078 =    0xffffffff
setmem /32    0x020c407c =    0xffffffff
setmem /32    0x020c4080 =    0xffffffff

//=============================================================================
// IOMUX
//=============================================================================
// DDR IO TYPE:
setmem /32    0x020e04b4 =    0x000C0000    // IOMUXC_SW_PAD_CTL_GRP_DDR_TYPE
setmem /32    0x020e04ac =    0x00000000    // IOMUXC_SW_PAD_CTL_GRP_DDRPKE

// CLOCK:
setmem /32    0x020e027c =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_SDCLK_0

// ADDRESS:
setmem /32    0x020e0250 =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_CAS
setmem /32    0x020e024c =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_RAS
setmem /32    0x020e0490 =    0x00000028    // IOMUXC_SW_PAD_CTL_GRP_ADDDS

// Control:
setmem /32    0x020e0288 =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_RESET
setmem /32    0x020e0270 =    0x00000000    // IOMUXC_SW_PAD_CTL_PAD_DRAM_SDBA2
setmem /32    0x020e0260 =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_SDODT0
setmem /32    0x020e0264 =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_SDODT1
setmem /32    0x020e04a0 =    0x00000028    // IOMUXC_SW_PAD_CTL_GRP_CTLDS

// Data Strobes:
setmem /32    0x020e0494 =    0x00020000    // IOMUXC_SW_PAD_CTL_GRP_DDRMODE_CTL
setmem /32    0x020e0280 =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_SDQS0
setmem /32    0x020e0284 =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_SDQS1

// Data:
setmem /32    0x020e04b0 =    0x00020000    // IOMUXC_SW_PAD_CTL_GRP_DDRMODE
setmem /32    0x020e0498 =    0x00000028    // IOMUXC_SW_PAD_CTL_GRP_B0DS
setmem /32    0x020e04a4 =    0x00000028    // IOMUXC_SW_PAD_CTL_GRP_B1DS

setmem /32    0x020e0244 =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_DQM0
setmem /32    0x020e0248 =    0x00000028    // IOMUXC_SW_PAD_CTL_PAD_DRAM_DQM1

//=============================================================================
// DDR Controller Registers
//=============================================================================
// Manufacturer:    Micron
// Device Part Number: MT41K256M16HA-125
// Clock Freq.:     400MHz
// Density per CS in Gb: 4
// Chip Selects used:  1
// Number of Banks:    8
// Row address:        15
// Column address:     10
// Data bus width      16
//=============================================================================
setmem /32    0x021b001c =    0x00008000    // MMDC0_MDSCR, set Configuration request bit

//=============================================================================
// Calibration setup.
//=============================================================================
setmem /32    0x021b0800 =    0xA1390003    // DDR_PHY_P0_MPZQHWCTRL, enable HW ZQ calibration
setmem /32    0x021b080c  =    0x00000000   // Write Leveling delay (may need fine tuning)

// Read DQS Gating calibration
setmem /32    0x021b083c =    0x00000000    // MPDGCTRL0 PHY0

// Read calibration
setmem /32    0x021b0848 =    0x40404040    // MPRDDLCTL PHY0

// Write calibration
setmem /32    0x021b0850 =    0x40404040    // MPWRDLCTL PHY0

// Read data bit delay
setmem /32    0x021b081c =    0x33333333    // MMDC_MPRDDQBY0DL
setmem /32    0x021b0820 =    0x33333333    // MMDC_MPRDDQBY1DL

// Write data bit delay
setmem /32    0x021b082c =    0xF3333333    // MMDC_MPWRDQBY0DL
setmem /32    0x021b0830 =    0xF3333333    // MMDC_MPWRDQBY1DL

// DQS & CLK Duty Cycle
setmem /32    0x021b08c0 =    0x00921012    // MMDC_MPDCCR

// Complete calibration by forced measurement
setmem /32    0x021b08b8 =    0x00000800    // DDR_PHY_P0_MPMUR0, frc_msr

// MMDC init:
setmem /32    0x021b0004 =    0x0002002D    // MMDC0_MDPDC
setmem /32    0x021b0008 =    0x1B333030    // MMDC0_MDOTC
setmem /32    0x021b000c =    0x676B52F3    // MMDC0_MDCFG0
setmem /32    0x021b0010 =    0xB66D0B63    // MMDC0_MDCFG1
setmem /32    0x021b0014 =    0x01FF00DB    // MMDC0_MDCFG2
setmem /32    0x021b0018 =    0x00211740    // MMDC0_MDMISC
setmem /32    0x021b001c =    0x00008000    // MMDC0_MDSCR
setmem /32    0x021b002c =    0x000026D2    // MMDC0_MDRWD
setmem /32    0x021b0030 =    0x006B1023    // MMDC0_MDOR
setmem /32    0x021b0040 =    0x0000004F    // Chan0 CS0_END
setmem /32    0x021b0000 =    0x84180000    // MMDC0_MDCTL

setmem /32    0x021b0890 =    0x00400a38    // MPPDCMPR2

// Mode register writes
setmem /32    0x021b001c =    0x02008032    // MMDC0_MDSCR, MR2 write, CS0
setmem /32    0x021b001c =    0x00008033    // MMDC0_MDSCR, MR3 write, CS0
setmem /32    0x021b001c =    0x00048031    // MMDC0_MDSCR, MR1 write, CS0
setmem /32    0x021b001c =    0x15208030    // MMDC0_MDSCR, MR0 write, CS0
setmem /32    0x021b001c =    0x04008040    // MMDC0_MDSCR, ZQ calibration, CS0

// CS1 mode register writes (commented out — only 1 CS used)
// setmem /32    0x021b001c =    0x0200803A    // MR2 write, CS1
// setmem /32    0x021b001c =    0x0000803B    // MR3 write, CS1
// setmem /32    0x021b001c =    0x00048039    // MR1 write, CS1
// setmem /32    0x021b001c =    0x15208038    // MR0 write, CS1
// setmem /32    0x021b001c =    0x04008048    // ZQ calibration, CS1

setmem /32    0x021b0020 =    0x00007800    // MMDC0_MDREF
setmem /32    0x021b0818 =    0x00000227    // DDR_PHY_P0_MPODTCTRL
setmem /32    0x021b0004 =    0x0002556D    // MMDC0_MDPDC, power down enabled
setmem /32    0x021b0404 =    0x00011006    // MMDC0_MAPSR, auto self-refresh
setmem /32    0x021b001c =    0x00000000    // MMDC0_MDSCR, clear configuration bit
```

#### 逐段解析

**第一段：禁用看门狗**

向 WDOG1 控制寄存器写入 `0x30`，禁用看门狗定时器。DDR 初始化耗时数十毫秒，如果不关闭看门狗，期间没有喂狗会导致系统复位。

**第二段：使能所有时钟**

CCM（Clock Controller Module）的 CCGR0~CCGR6 寄存器全部写 `0xFFFFFFFF`。ROM code 上电后会关闭部分外设时钟，这里粗暴地全部打开——这是 NXP 评估板的常见做法，量产时可以精细控制只打开 MMDC 所需的时钟门。

**第三段：IOMUX 引脚复用与电气配置**

将 SoC 引脚复用为 DDR 功能，并设置驱动强度、压摆率、差分模式等电气参数：

| 寄存器地址 | 值 | 寄存器名 | 作用 |
|-----------|-----|----------|------|
| `0x020e04b4` | `0x000C0000` | GRP_DDR_TYPE | 设置 DDR IO 类型为 DDR3（1.5V） |
| `0x020e04ac` | `0x00000000` | GRP_DDRPKE | 禁用 DDR 引脚 keeper（保持电路） |
| `0x020e027c` | `0x00000028` | DRAM_SDCLK_0 | 时钟引脚驱动强度 DSE ≈ 34Ω |
| `0x020e0250` | `0x00000028` | DRAM_CAS | 列地址选通驱动强度 |
| `0x020e024c` | `0x00000028` | DRAM_RAS | 行地址选通驱动强度 |
| `0x020e0490` | `0x00000028` | GRP_ADDDS | 地址总线驱动强度组 |
| `0x020e0288` | `0x00000028` | DRAM_RESET | 复位引脚驱动强度 |
| `0x020e0260` | `0x00000028` | DRAM_SDODT0 | ODT0 引脚驱动强度 |
| `0x020e0264` | `0x00000028` | DRAM_SDODT1 | ODT1 引脚驱动强度 |
| `0x020e04a0` | `0x00000028` | GRP_CTLDS | 控制信号驱动强度组 |
| `0x020e0494` | `0x00020000` | GRP_DDRMODE_CTL | DQS 设置为 DDR 差分模式 |
| `0x020e0280` | `0x00000028` | DRAM_SDQS0 | DQS0 驱动强度 |
| `0x020e0284` | `0x00000028` | DRAM_SDQS1 | DQS1 驱动强度 |
| `0x020e04b0` | `0x00020000` | GRP_DDRMODE | 数据总线 DDR 模式 |
| `0x020e0498` | `0x00000028` | GRP_B0DS | 数据 Byte0 驱动强度组 |
| `0x020e04a4` | `0x00000028` | GRP_B1DS | 数据 Byte1 驱动强度组 |
| `0x020e0244` | `0x00000028` | DRAM_DQM0 | 数据掩码 0 驱动强度 |
| `0x020e0248` | `0x00000028` | DRAM_DQM1 | 数据掩码 1 驱动强度 |

`0x28` 是常见的驱动强度配置（约 34Ω），`0x00020000` 设置 DDR 差分模式。如果板子上信号质量差（过冲/下冲严重），可适当调整 DSE 值。

**第四段：PHY 校准预设值**

在初始化前预设 PHY 层的延迟线初始值，后续硬件自动校准会在此基础上精细调整：

| 寄存器 | 值 | 含义 |
|--------|-----|------|
| `MPZQHWCTRL` (0x021b0800) | `0xA1390003` | 使能硬件 ZQ 校准（一次性 + 周期性） |
| `MPWLDECTRL` (0x021b080c) | `0x00000000` | Write Leveling 延迟初始值 = 0 |
| `MPDGCTRL0` (0x021b083c) | `0x00000000` | Read DQS Gating 起始延迟 = 0 |
| `MPRDDLCTL` (0x021b0848) | `0x40404040` | Read DQS 延迟 = 0x40（默认值） |
| `MPWRDLCTL` (0x021b0850) | `0x40404040` | Write DQS 延迟 = 0x40（默认值） |
| `MPRDDQBY0DL` (0x021b081c) | `0x33333333` | Read DQ Byte0 延迟 |
| `MPRDDQBY1DL` (0x021b0820) | `0x33333333` | Read DQ Byte1 延迟 |
| `MPWRDQBY0DL` (0x021b082c) | `0xF3333333` | Write DQ Byte0 延迟 |
| `MPWRDQBY1DL` (0x021b0830) | `0xF3333333` | Write DQ Byte1 延迟 |
| `MPDCCR` (0x021b08c0) | `0x00921012` | DQS/CLK 占空比校准 |
| `MPMUR0` (0x021b08b8) | `0x00000800` | 强制测量完成校准（frc_msr） |

> **注意**：注释明确写了 *"may need to run write leveling calibration to fine tune these settings"*。这些默认值只是起点，不同 PCB 布局需要重新运行 ddr_stress_tester 获取最优值。

**第五段：MMDC 控制器核心寄存器**

核心寄存器配置（时序、几何、ODT、片选分区等）。其中 `MDCTL`（`0x84180000`）最为关键：

| 字段 | 值 | 含义 |
|------|-----|------|
| `SDE_TO_CHIP` | 1 | 片选使能 |
| `SDDRC` | DDR3 | DDR3 类型 |
| `ROW` | 15 | 15 位行地址 |
| `COL` | 10 | 10 位列地址 |
| `BANK` | 3（= 8 Bank） | 8 Bank |
| `DSIZ` | 1（= x16） | 16 位数据总线 |

`MDMISC`（`0x00211740`）包含 RALAT=5（读访问延迟）、COL=10 等配置。

**第六段：JEDEC 模式寄存器写入序列**

通过 MDSCR 寄存器依次写入 MR2→MR3→MR1→MR0→ZQCL：

```text
setmem /32    0x021b001c =    0x02008032    // MR2: CWL=6, RttWR
setmem /32    0x021b001c =    0x00008033    // MR3: 0
setmem /32    0x021b001c =    0x00048031    // MR1: ODIC, DLL 使能
setmem /32    0x021b001c =    0x15208030    // MR0: BL=8, CL=11, DLL Reset
setmem /32    0x021b001c =    0x04008040    // ZQCL 校准命令
```

MDSCR 寄存器格式：`[CMD_TYPE:15:12][CS:11:8][MR_VALUE:7:0]`。例如 `0x02008032`：
- `0x2`（bit 13-12）= Load Mode Register 命令
- `0x0`（bit 11-8）= CS0
- `0x32` = MR2 值 = `0b00000010`（CWL=6）

ZQCL 命令 `0x04008040`：`0x4` = ZQ Calibration 命令类型。

**第七段：功耗管理与收尾**

最后清除 `MDSCR` 的 configuration bit，MMDC 退出配置模式，DDR 进入正常工作状态。

#### JEDEC 标准步骤 → DCD 脚本段落对应关系

| JEDEC 步骤 | DCD 脚本段落 | 说明 |
|-----------|------------|------|
| 上电等待，CKE=0 | 第1~3段（WDOG + 时钟 + IOMUX） | SoC 端准备，非 JEDEC 流程 |
| — | 第4段（PHY 校准预设值） | MMDC PHY 预设延迟线初始值，非 JEDEC |
| — | 第5段（MMDC 核心寄存器） | MMDC Core 预配置（时序/几何/ODT），非 JEDEC |
| **Precharge All** | — | MMDC 控制器在配置模式下**自动执行**，脚本中无独立 setmem 行 |
| **Refresh × 2** | — | 同上，MMDC 自动执行并等待 tRFC |
| **MR2** | 第6段 | `0x02008032`（CWL=6） |
| **MR3** | 第6段 | `0x00008033`（值为 0） |
| **MR1** | 第6段 | `0x00048031`（ODT/驱动强度/DLL 使能） |
| **MR0** | 第6段 | `0x15208030`（BL=8, CL=11） |
| **ZQCL** | 第6段末尾 | `0x04008040` |
| DLL 锁定 | 第4段（PHY 预设值） | 预设值写入，后续硬件自动校准 |
| 就绪 | 第7段（功耗管理收尾） | 清除 CON_REQ，退出配置模式 |

> **注意**：Precharge All 和 Refresh × 2 在 DCD 脚本中**没有对应的 setmem 行**。当 `MDSCR[CON_REQ]` 被置位后，MMDC 控制器会**自动**按 JEDEC 顺序执行 Precharge All → Refresh × 2 →（等待用户写 MR），脚本只需写 MR 相关的 setmem。

### 13.5 MMDC 核心寄存器详解

MMDC（Multi-Mode DDR Controller）寄存器的基地址为 `0x021B0000`。各寄存器的详细说明见 13.3 节脚本实例，本节仅列出汇总。

**核心控制器寄存器**：

| 寄存器 | 地址 | 用途 |
|--------|------|------|
| **MDCTL** | `0x021B0000` | 几何架构（SDDRC/ROW/COL/BANK/DSIZ） |
| **MDPDC** | `0x021B0004` | 预充电控制 / Power Down 配置 |
| **MDOTC** | `0x021B0008` | ODT 时序 |
| **MDCFG0** | `0x021B000C` | 时序配置 0（tCL/tRCD/tRP/tXP 等） |
| **MDCFG1** | `0x021B0010` | 时序配置 1（tRC/tRAS/tWR/tCWL 等） |
| **MDCFG2** | `0x021B0014` | 时序配置 2（tRFC/tXSR 等） |
| **MDMISC** | `0x021B0018` | 杂项（RALAT/COL/BI 等） |
| **MDSCR** | `0x021B001C` | 特殊命令（CON_REQ/CON_ACK/MRS 命令） |
| **MDRWD** | `0x021B002C` | 超时控制 |
| **MDOR** | `0x021B0030` | 输出延迟 |
| **MDREF** | `0x021B0020` | 刷新控制 |
| **MAPSR** | `0x021B0404` | 电源管理（自刷新/低功耗） |

**PHY 寄存器**：

| 寄存器 | 地址 | 用途 |
|--------|------|------|
| **MPZQHWCTRL** | `0x021b0800` | ZQ 硬件校准控制 |
| **MPWLDECTRL** | `0x021b080c` | Write Leveling 延迟控制 |
| **MPDGCTRL0** | `0x021b083c` | Read DQS Gating 控制 |
| **MPRDDLCTL** | `0x021b0848` | 读数据延迟控制 |
| **MPWRDLCTL** | `0x021b0850` | 写数据延迟控制 |
| **MPRDDQBY0/1DL** | `0x021b081c/0820` | 读 DQ 字节 lane 延迟 |
| **MPWRDQBY0/1DL** | `0x021b082c/0830` | 写 DQ 字节 lane 延迟 |
| **MPDCCR** | `0x021b08c0` | DQS/CLK 占空比控制 |
| **MPMUR0** | `0x021b08b8` | 强制测量控制 |
| **MPPDCMPR2** | `0x021b0890` | ZQ 校准偏移微调 |
| **MPODTCTRL** | `0x021b0818` | ODT 控制 |

### 13.6 DDR 校准算法详解

> **对应手册**：§35.11 Calibration Process（完整涵盖 ZQ、Read DQS Gating、Read/Write Calibration、Write Leveling、Fine Tuning、Duty Cycle）

#### 校准前置条件

**开始任何校准前必须**：
- 禁用省电功能（`MDPDC[PWDTn]`, `MDPDC[PRCTn]`, `MAPSR[PSD]`）
- 涉及 DDR MPR 模式或 Write Leveling 的校准前，还需：
  - 禁用周期刷新（`MDREF[REF_SEL] = 0x3`），手动发刷新命令（`MDSCR[CMD] = 0x2`）
  - 禁用自动省电（`MAPSR[PSD] = 1`）

#### 延迟线（Delay-line）基础

- 默认延迟 = **1/4 时钟周期**
- 最高频率下，最大可调至 **1/2 时钟周期**
- 正常运行时，延迟线在每次 DDR 刷新周期内**自动测量**以保持精度
- 校准开始前，延迟线的初始值必须是"合法值"（即 strobe 位于对应 data window 内），但不必是最优值

#### ZQ 校准详细过程

ZQ 校准分为两类：**DDR I/O 焊盘驱动强度校准**和**DDR 芯片 ZQ 命令**。

**ZQ 命令时序要求**：
- 发 ZQCL/ZQCS 前必须 **Precharge All** + 等待 tRP（让所有 bank 回到空闲状态）
- ZQ 期间除 CK 外所有内存线保持静默（quiet-line 要求）——不能有任何其他命令干扰
- ZQCL 时长：复位后首次 512 周期，其他 ZQCL 256 周期，ZQCS 64 周期
- ZQ 命令通过 A10 引脚区分 Long/Short，通过 CS 选择目标芯片（CS0/CS1/两者）

**MPZQHWCTRL 寄存器关键字段**：

| 字段 | 作用 |
|------|------|
| \`ZQ_HW_PER\` | ZQ Short 周期计数器（多少周期自动触发一次短期校准） |
| \`ZQ_MODE\` | 决定 MMDC 执行 I/O 焊盘校准和/或发 ZQ 命令给 DDR 芯片 |
| \`ZQ_HW_FOR\` | 强制单次硬件 ZQ 校准（非周期性） |
| \`ZQ_EARLY_COMPARATOR_EN_TIMER\` | 比较器使能前的等待周期数（确保 ZQ 信号稳定） |
| \`ZQ_HW_PU_RES\` / \`ZQ_HW_PD_RES\` | 存储上拉/下拉校准结果（5 位值） |
| \`ZQ_CMP_OUT_SMP\` | ZQ 信号驱动到采样比较器之间的延迟（00=7周期, 01=15周期） |

**硬件自动 ZQ 校准算法**（5 位二进制搜索）：
1. 上拉校准：从 \`zq_pu_val = 0\` 开始，通过比较器对比外部 240Ω 参考电阻（RZQ），判断输出电压是否 > Vdd/2 → 确定内部电阻是否 < 240Ω，逐位收敛到 5 位最优值
2. 下拉校准：同理，从 \`zq_pd_val = 0\` 开始逐位试探
3. 结果分别写入 \`MPZQHWCTRL[ZQ_HW_PU_RES]\` 和 \`MPZQHWCTRL[ZQ_HW_PD_RES]\`

**ZQ 校准触发时机**：

| 类型 | 触发方式 | 说明 |
|------|---------|------|
| ZQ Long | 上电初始化、退出 Self Refresh、退出慢速 Precharge PD | 完全重新校准，时间长 |
| ZQ Short | 硬件周期性（由 ZQ_HW_PER 计数器触发） | 维持驱动强度精度，补偿温度/电压漂移 |
| ZQ Init | 软件手动（首次上电，在 MMDC 使能之前） | 初始化校准 |

> **类比**：把 ZQ 校准想象定期给吉他调音。ZQ Init = 新琴首次调音（大调）；ZQ Long = 换了弦后重新调（大调）；ZQ Short = 演奏过程中偶尔微调（小调）。温度变化、电压波动就像温湿度变化让琴弦松紧变化，需要定期 Short 校准来补偿。

**ZQ 微调**（Fine Tuning）：通过 \`MPPDCMPR2[ZQ_PU_OFFSET]\` 和 \`MPPDCMPR2[ZQ_PD_OFFSET]\` 可在校准结果基础上额外偏移 -7 ~ +7。用于补偿 PCB 走线差异或特殊负载场景。

#### Read DQS Gating 校准

**它校准什么**：Read DQS Gating 校准的是**DQS 门控信号与读前导（preamble）窗口的中心对齐**。DDR3 读操作时，控制器需要知道"什么时候打开耳朵听 DDR 返回的数据"——开早了听到噪声，开晚了错过数据。

**两种操作模式**：
- **MPR 模式**（Multi Purpose Register）：让 DDR 芯片从内部多功能寄存器返回已知固定数据（JEDEC 标准定义的测试模式）
- **预定义值模式**：控制器先向 DDR 写入一组预定义数据（通过 `MPPDCMPR1[PDV1, PDV2]` 配置），再读回比较

**Tmod + 4 要求**：在 MPR 模式下，两次 MRS 命令之间至少间隔 Tmod 周期（DDR3 中 Tmod = max(tMRD, tMOD)）。MMDC 在校准中等待 Tmod+4 周期确保 DDR 内部状态完全更新。

**HC_DEL vs DL_ABS_OFFSET 的区别**：

| 字段 | 精度 | 范围 | 含义 |
|------|------|------|------|
| `DG_HC_DEL` | 半周期（0.5 cycle）步进 | 0~15（4 位） | 粗调延迟 = HC_DEL × 0.5 × 周期 |
| `DG_DL_ABS_OFFSET` | 1/256 周期步进 | 0~127（7 位） | 精细延迟 = (OFFSET/256) × 周期 |

总延迟 = HC_DEL × 0.5 × 周期 + (OFFSET/256) × 周期

**硬件自动校准算法**（边界搜索法，35 步）：

阶段一 — 找初始点是否合法：
1. 等待延迟线更新完成，满足 Tmod+4 要求
2. 发读命令到 DDR，等待 16 或 32 周期（由 `DG_CMP_CYC` 决定）
3. 比较返回数据与预定义/MPR 值
4. 如果比较失败 → DQS 门控在非法时间点，报错 `HW_DG_ERR`
5. 如果比较通过 → 进入阶段二

阶段二 — 向下搜索下边界（减延迟）：
6. 重置读 FIFO（`RST_RD_FIFO = 1`）
7. 每个字节的 DQS 门控延迟减少半个周期（`DG_HC_DEL + 1`）
8. 发读命令 + 比较
9. 重复 6~8，直到比较失败 → 记录临时下边界

阶段三 — 向上搜索上边界（加延迟）：
10. 从下边界开始，每次增加半个周期
11. 发读命令 + 比较
12. 比较通过继续加，直到比较失败 → 记录临时上边界

阶段四 — 精确定位边界（用 DL_ABS_OFFSET 步进）：
13. 回到下边界 - 半个周期位置
14. 每次增加 1 个 DL_ABS_OFFSET 单位（1/256 周期）
15. 发读 + 比较，精确找到下边界
16. 回到上边界 - 半个周期位置
17. 同样方式精确找到上边界 - 1

阶段五 — 计算最优值：
18. 最优值 = (下边界 + 上边界) / 2，写入 `MPDGCTRLn[DG_DL_ABS_OFFSETn]`
19. 清零 `HW_DG_EN` 表示校准完成
20. 边界结果同时存入 `MPDGHWSTn[HW_DG_UPn]` 和 `MPDGHWSTn[HW_DG_LOWn]` 供软件读取

> **关键理解**：为什么先找边界再取平均？因为数据窗口（DQ valid window）在 DQS 周期内有一个"有效区间"。找到这个区间的左边界和右边界，取中间点就是最安全的位置——即使温度漂移或电压波动，也有最大裕量。

软件手动校准原理完全相同，但每一步由软件通过 `MPDGCTRL` 手动触发并读取比较结果，通常用于调试。

#### 读校准（Read Calibration）

**它校准什么**：在 Read DQS Gating 已经找到"什么时候打开耳朵"之后，读校准确保**打开耳朵后听到的 DQ 数据确实是对齐在 DQS  strobe 中心的**。Gating 校准的是"门控信号何时开启"，Read 校准的是"DQS strobe 相对于 DQ 数据的相位"。

**前置条件**：Read DQS Gating 校准必须已完成。

**硬件自动校准步骤**（与 DQS Gating 类似的边界搜索法）：

1. 等待读延迟线更新完成，满足 Tmod+4 要求
2. 发读命令到 DDR，等待 16 或 32 周期（由 `MPRDDLHWCTL[HW_RD_DL_CMP_CYC]` 决定）
3. 比较返回数据与预定义/MPR 值
4. 如果比较失败 → 初始读 DQS 不在 DQ 窗口内，报错 `MPRDDLHWCTL[HW_RD_DL_ERRn]`（n = 字节编号）
5. 如果比较通过 → 开始向下搜索

向下搜索下边界：
6. 重置读 FIFO（`MPDGCTRL[RST_RD_FIFO] = 1`）
7. 读延迟减 1（`MPRDDLCTL[RD_DL_ABS_OFFSETn] -= 1`）
8. 发读 + 比较
9. 重复 6~8 直到比较失败 → 下边界存入 `MPRDDLHWSTn[HW_RD_DL_LOWn]`

向上搜索上边界：
10. 从下边界开始，读延迟每次加 1
11. 发读 + 比较
12. 比较通过继续加，直到比较失败 → 上边界存入 `MPRDDLHWSTn[HW_RD_DL_UPn]`

计算最优值：
13. 最优值 = (下边界 + 上边界) / 2，写入 `MPRDDLCTL[RD_DL_ABS_OFFSETn]`
14. 清零 `HW_RD_DL_EN` 表示校准完成

**错误处理**：如果初始值就不在 DQ 窗口内（步骤 4 失败），MMDC 在 `MPRDDLHWCTL[HW_RD_DL_ERRn]` 中标记对应字节出错。排查方法：检查 DCD 中的初始延迟值是否合理，或 PCB 走线是否存在严重 skew。

#### 写校准（Write Calibration）

**它校准什么**：确保控制器发出的**写 DQS strobe 与写 DQ 数据在 DDR 芯片端对齐**。写操作时，DQS 和 DQ 同时从控制器发出，但由于 PCB 走线差异和芯片内部延迟，到达 DDR 芯片时可能不同步。

**前置条件**：Write Leveling 校准必须已完成（确保 DQS 与 CLK 对齐）。

**硬件自动校准步骤**（20 步）：

1. 等待写延迟线更新完成（`MPWRDLCTL[WR_DL_ABS_OFFSETn]`）
2. 发写命令到 DDR（bank 0, address 0），等待 16 或 32 周期
3. 从 DDR 读回数据
4. 与预定义值比较（使用 `MPPDCMPR1` 中配置的值）
5. 如果比较失败 → 初始写 DQS 不在 DQ 窗口内，报错 `MPWRDLHWCTL[HW_WR_DL_ERRn]`

向下搜索下边界：
6. 重置读 FIFO
7. 写延迟减 1（`MPWRDLCTL[WR_DL_ABS_OFFSETn] -= 1`）
8. 发写 → 读回 → 比较
9. 重复直到比较失败 → 下边界存入 `MPWRDLHWSTn[HW_WR_DL_LOWn]`

向上搜索上边界：
10. 从下边界开始，写延迟每次加 1
11. 发写 → 读回 → 比较
12. 比较通过继续加，直到比较失败 → 上边界存入 `MPWRDLHWSTn[HW_WR_DL_UPn]`

计算最优值：
13. 最优值 = (下边界 + 上边界) / 2，写入 `MPWRDLCTL[WR_DL_ABS_OFFSETn]`
14. 清零 `HW_WR_DL_EN` 表示校准完成

> **重要**：写校准的"写"是往 DDR 写数据，"校"是从 DDR 读回验证——写进去什么就读回什么来比对。所以写校准实际上依赖读通路的正确性（Read DQS Gating 和 Read Calibration 必须先完成）。

#### Write Leveling 校准

**Write Leveling 解决什么问题**：补偿 CLK 和 DQS 之间的 PCB 走线 skew（偏移）。

**Fly-by 拓扑的引入**：

DDR3 频率升高（800MT/s 起步），传统的 T 型分支走线产生信号反射。DDR3 改用 **Fly-by 拓扑**——命令/地址/时钟线像串糖葫芦一样依次穿过每颗 DDR 颗粒，但**数据线仍然是点对点直连**：

```
控制器 ── CLK/ADDR/CMD ──▶ ──▶ ──▶  (Fly-by)
                             │      │
                           DDR1   DDR2

控制器 DQ/DQS ──────▶ DDR1（直连，距离短）
```

**结果**：写操作时，CLK 走 Fly-by 长路径，DQS 走点对点短路径，两者到达 DDR 芯片的时间不同，产生 skew。规范要求 **DQS 的中心要对齐 CLK 的边沿**，如果错位，DDR 用 DQS 采样 DQ 时可能采在跳变沿上。

**Write Leveling 的校准过程**：

1. 控制器通过 MRS 命令让 DDR 进入 Write Leveling 模式
2. 控制器发出 DQS 脉冲
3. DDR 芯片用本地收到的 **CLK 边沿** 采样 **DQS**，将结果反馈到 DQ 引脚
4. 控制器读取 DQ 反馈：DQ = 0 → DQS 还没到，DQ = 1 → DQS 已经到了
5. 逐步调整 DQS 延迟，直到找到 0→1 的跳变点

**关键设计约束**：
- 硬件自动校准最多检测 **1 个时钟周期**的 skew
- 如果 DDR3 距离控制器太远，skew 超过 1 周期，需手动设置 `MPWLDECTRL[WL_CYC_DEL]`
- **PCB Layout 要求**：DDR3 尽量靠近控制器，计算时钟信号到最远 DDR3 的飞行时间

**硬件自动校准步骤**：
1. DDR 进入 Write Leveling 模式（MRS 命令）
2. MMDC 发 DQS 脉冲，采样反馈 DQ 位
3. 每次增加 1/8 周期延迟，重复采样，直到 1 周期
4. 查找 DQ 从 0→1 的第一次跳变点
5. 精细调优：以 1/256 周期为步长微调
6. 结果写入 `MPWLDECTRL[WL_DL_ABS_OFFSET]`
7. DDR 退出 Write Leveling 模式（MRS 命令）

> **重要**：如果校准结果是 100/256 周期，但设计者预估 skew 超过 2 周期，则 `MPWLDECTRL[WL_CYC_DEL]` 应设为 2，总延迟 = 2 + 100/256 周期。

### 13.7 DDR 校准失败排查

如果 U-Boot 报错 `DRAM init failed` 或系统启动卡死，从以下维度逐一排查：

| 排查方向 | 常见原因 | 检查方法 |
|---------|---------|---------|
| **参数不匹配** | DCD/设备树中的频率、时序与实际 DDR 芯片规格不符 | 对照 DDR 芯片 DataSheet 验证 tCL、tRCD、tRP 等参数 |
| **电源不稳定** | VDD_SOC 纹波过大或电压跌落 | 示波器测量 DDR 供电电压 |
| **PCB 信号问题** | 走线过长、阻抗控制不良、等长没做 | 检查 Layout，必要时重做板 |
| **IOMUX 配置错误** | 引脚误配置为其他功能或驱动强度不合理 | 检查 IOMUXC 寄存器配置 |
| **校准参数过期** | 换了 DDR 颗粒批次或板子改版后仍用旧 DCD | 重新用 ddr_stress_tester 跑校准 |
| **ZQ 电阻异常** | 外部 240Ω 参考电阻焊接不良或精度不够 | 万用表测量 RZQ 电阻值 |
| **温度漂移** | 高温/低温环境下校准参数失效 | 在高低温箱中验证，必要时做温度补偿 |

### 13.8 信号完整性基础

<!-- TODO: 信号完整性基础知识，如反射、串扰、时序裕量等 -->

> 待补充：PCB 走线长度匹配、阻抗控制、差分信号设计要点。
