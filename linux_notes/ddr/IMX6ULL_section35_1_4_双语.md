# Chapter 35 Multi Mode DDR Controller (MMDC)
# 第35章 多模式DDR控制器(MMDC)

## 35.1 Overview | 35.1 概述

MMDC is a multi-mode DDR controller that supports DDR3/DDR3L x16 and LPDDR2x16 memory types. MMDC is configurable, high performance, and optimized. The following figure shows the MMDC block diagram.
MMDC是一款多模式DDR控制器,支持DDR3/DDR3L x16和LPDDR2 x16存储器类型。MMDC可配置、高性能且经过优化。下图显示了MMDC的功能框图。

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/38b044e75ed1b59d806a215d31c9ae0ade0dbf737840b05492e7c8cf9170bdb3.jpg)

**Figure 35-1. MMDC block diagram | 图35-1. MMDC功能框图**

MMDC consists of a core (MMDC_CORE) and PHY (MMDC_PHY).
MMDC由一个核心(MMDC_CORE)和一个PHY(MMDC_PHY)组成。

i.MX 6ULL Applications Processor Reference Manual, Rev. 1, 11/2017
i.MX 6ULL应用处理器参考手册,修订版1,2017年11月

### Overview | 概述

• The core is responsible for communication with the system through an AXI interface, DDR command generation, DDR command optimizations, and a read/write data path.
• 核心负责通过AXI接口与系统通信,生成DDR命令,优化DDR命令,以及读写数据路径。

• The PHY is responsible for the timing adjustment; it uses special calibration mechanisms to ensure data capture margin at a clock rate of up to 400 MHz.
• PHY负责时序调整;它使用特殊的校准机制来确保在高达400 MHz的时钟速率下的数据捕获余量。

The internal memory map (configuration registers) of the MMDC can be configured through an IP channel (IP0).
MMDC的内部存储器映射(配置寄存器)可以通过IP通道(IP0)进行配置。

## 35.1.1 MMDC feature summary | 35.1.1 MMDC功能摘要

The table found here summarizes the MMDC features.
下表总结了MMDC的功能。

**Table 35-1. MMDC feature summary | 表35-1. MMDC功能摘要**

| Feature | Details | 功能 | 详情 |
|---------|---------|------|------|
| DDR standards | • DDR3L, DDR3 x16 | DDR标准 | • DDR3L, DDR3 x16 |
|  | • LPDDR2 x16 |  | • LPDDR2 x16 |
|  | • Does not support LPDDR1MDDR or DDR2 |  | • 不支持LPDDR1MDDR或DDR2 |
| DDR interface | • x16 data bus width | DDR接口 | • x16数据总线宽度 |
|  | • Density per DDR device of 256 Mbits-8 Gbits |  | • 每个DDR设备密度为256 Mbits-8 Gbits |
|  | • Column size of 8-12 bits |  | • 列大小8-12位 |
|  | • Row size of 11-16 bits |  | • 行大小11-16位 |
|  | • Two chip selects (one chip select for DDR3/DDR3L, LPDDR2) |  | • 两个片选(DDR3/DDR3L、LPDDR2各一个片选) |
|  | • Up to 4 Gbytes of address space |  | • 高达4 Gbytes地址空间 |
|  | • Supports burst length of 8 (aligned) for DDR3 |  | • DDR3支持突发长度8(对齐) |
|  | • Supports burst length of 4 for LPDDR2 |  | • LPDDR2支持突发长度4 |
| DDR performance | • MMDC running at up to 400 MHz (800MT/s) | DDR性能 | • MMDC运行频率高达400 MHz (800MT/s) |
|  | • Supports Real-Time priority via QoS signals |  | • 通过QoS信号支持实时优先级 |
|  | • Page hit/page miss optimizations |  | • 页命中/页未命中优化 |
|  | • Consecutive read/write access optimizations |  | • 连续读/写访问优化 |
|  | • Supports deep read and write request queues |  | • 支持深度读写请求队列 |
|  | • Drives critical word first in read transactions |  | • 读事务中优先返回关键数据字 |
|  | • Keeps tracking of open memory pages |  | • 跟踪打开的存储器页面 |
|  | • Supports bank interleaving |  | • 支持bank交错 |
| AXI interface | • AXI bus compliant | AXI接口 | • 符合AXI总线标准 |
|  | • Supports bus transfers of 8, 16, 64 bits at 400 MHz |  | • 支持8、16、64位总线传输,运行频率400 MHz |
|  | • Supports AXI bursts up to 16 |  | • 支持高达16的AXI突发长度 |
|  | • Supports WRAP, INCR and FIXED burst types |  | • 支持WRAP、INCR和FIXED突发类型 |
|  | • Supports 16 bits AXI ID |  | • 支持16位AXI ID |
|  | • Write data interleave depth is 1 |  | • 写数据交织深度为1 |
|  | • Supports four exclusive monitors per configurable ID |  | • 每个可配置ID支持四个独占监视器 |
| DDR calibration | • ZQ calibration for external DDR device | DDR校准 | • 外部DDR设备的ZQ校准 |
|  | • Read data calibration |  | • 读数据校准 |
|  | • Write data calibration |  | • 写数据校准 |
|  | • Write leveling calibration |  | • 写电平校准 |
|  | • Read fine tuning (up to 7 delay-line units) |  | • 读精细调谐(最多7个延迟线单元) |
|  | • Write fine tuning (up to 3 delay-line units) |  | • 写精细调谐(最多3个延迟线单元) |
| Power saving | • Dynamic voltage, frequency change | 功耗管理 | • 动态电压、频率变化 |
|  | • Self-refresh mode entry |  | • 自刷新模式进入 |
|  | • Automatic self-refresh and power down entry/exit |  | • 自动自刷新和掉电进入/退出 |
| DDR general | • Configurable timing parameters | DDR通用 | • 可配置的时序参数 |
|  | • Configurable refresh scheme |  | • 可配置的刷新方案 |
|  | • Page boundary crossing support |  | • 支持跨页边界 |
|  | • Various ODT control schemes |  | • 多种ODT控制方案 |
|  | • MRW and MRR commands for LPDDR2 |  | • LPDDR2的MRW和MRR命令 |
|  | • Debug and profiling capabilities |  | • 调试和性能分析功能 |

## 35.2 External Signals | 35.2 外部信号

The table found here describes the external signals of MMDC.
下表描述了MMDC的外部信号。

**Table 35-2. MMDC External Signals | 表35-2. MMDC外部信号**

| Signal | Description | Pad | Mode | Direction | 信号 | 描述 | 引脚 | 模式 | 方向 |
|--------|-------------|-----|------|----------|------|------|------|------|------|
| DRAM_ADDR[15:0] | Address Bus Signals | DRAM_A[15:0] | No Muxing | O | DRAM_ADDR[15:0] | 地址总线信号 | DRAM_A[15:0] | 无复用 | O |
| DRAM_CAS | Column Address Strobe Signal | DRAM_CAS | No Muxing | O | DRAM_CAS | 列地址选通信号 | DRAM_CAS | 无复用 | O |
| DRAM_CS[1:0] | Chip Selects | DRAM_CS[1:0] | No Muxing | O | DRAM_CS[1:0] | 片选 | DRAM_CS[1:0] | 无复用 | O |
| DRAM_DATA[31:0] | Data Bus Signals | DRAM_D[31:0] | No Muxing | I/O | DRAM_DATA[31:0] | 数据总线信号 | DRAM_D[31:0] | 无复用 | I/O |
| DRAM_DQM[1:0] | Data Mask Signals | DRAM_DQM[1:0] | No Muxing | O | DRAM_DQM[1:0] | 数据掩码信号 | DRAM_DQM[1:0] | 无复用 | O |
| DRAM_ODT[1:0] | On-Die Termination Signals | DRAM_SDODT[1:0] | No Muxing | O | DRAM_ODT[1:0] | 片内终端信号 | DRAM_SDODT[1:0] | 无复用 | O |
| DRAM_RAS | Row Address Strobe Signal | DRAM_RAS | No Muxing | O | DRAM_RAS | 行地址选通信号 | DRAM_RAS | 无复用 | O |
| DRAM_RESET | Reset Signal | DRAM_RESET | No Muxing | O | DRAM_RESET | 复位信号 | DRAM_RESET | 无复用 | O |
| DRAM_SDBA[2:0] | Bank Select Signals | DRAM_SDBA[2:0] | No Muxing | O | DRAM_SDBA[2:0] | Bank选择信号 | DRAM_SDBA[2:0] | 无复用 | O |
| DRAM_SDCKE[1:0] | Clock Enable Signals | DRAM_SDCKE[1:0] | No Muxing | O | DRAM_SDCKE[1:0] | 时钟使能信号 | DRAM_SDCKE[1:0] | 无复用 | O |
| DRAM_SDCLK0_N | Negative Clock Signals | DRAM_SDCLK_1:0] | No Muxing | O | DRAM_SDCLK0_N | 负时钟信号 | DRAM_SDCLK_1:0] | 无复用 | O |
| DRAM_SDCLK0_P | Positive Clock Signals | DRAM_SDCLK_1:0] | No Muxing | O | DRAM_SDCLK0_P | 正时钟信号 | DRAM_SDCLK_1:0] | 无复用 | O |
| DRAM_SDQS[1:0]_N | Negative DQS Signals | DRAM_SDQS[1:0]_N | No Muxing | I/O | DRAM_SDQS[1:0]_N | 负DQS信号 | DRAM_SDQS[1:0]_N | 无复用 | I/O |
| DRAM_SDQS[1:0]_P | Positive DQS Signals | DRAM_SDQS[1:0]_P | No Muxing | I/O | DRAM_SDQS[1:0]_P | 正DQS信号 | DRAM_SDQS[1:0]_P | 无复用 | I/O |
| DRAM_SDWE | WE signal | DRAM_SDWE | No Muxing | O | DRAM_SDWE | WE信号 | DRAM_SDWE | 无复用 | O |
| DRAM_ZQPAD | ZQ signal | DRAM_ZQPAD | No Muxing | O | DRAM_ZQPAD | ZQ信号 | DRAM_ZQPAD | 无复用 | O |

## 35.3 Clocks | 35.3 时钟

The table found here describes the clock sources for MMDC.
下表描述了MMDC的时钟源。

See Clock Controller Module (CCM) for clock setting, configuration and gating information.
有关时钟设置、配置和门控信息,请参阅时钟控制器模块(CCM)。

> **NOTE | 注** The terms clocks and cycles are used interchangeably and refer to the clock period of the main ddr clock (mmdc_axi_clk_root), commonly referred to as the DDR frequency.
> 术语clocks和cycles可互换使用,指的是主ddr时钟(mmdc_axi_clk_root)的时钟周期,通常称为DDR频率。

**Table 35-3. MMDC Clocks | 表35-3. MMDC时钟**

| Clock name | Clock Root | Description | 时钟名称 | 时钟根 | 描述 |
|------------|------------|-------------|----------|--------|------|
| aclk_fast_core_p0 | mmdc_axi_clk_root | Fast clock (channel 1) | aclk_fast_core_p0 | mmdc_axi_clk_root | 快速时钟(通道1) |
| ipg_clk_p0 | ipg_clk_root | Peripheral clock (channel 1) | ipg_clk_p0 | ipg_clk_root | 外设时钟(通道1) |
| aclk_fast_phy_p0 | mmdc_axi_clk_root | Fast clock (channel 1 - PHY) | aclk_fast_phy_p0 | mmdc_axi_clk_root | 快速时钟(通道1 - PHY) |

## 35.4 Functional Description | 35.4 功能描述

This section provides a complete functional description of the block.
本节提供该模块的完整功能描述。

### 35.4.1 Write/Read data flow | 35.4.1 写/读数据流

#### 35.4.1.1 Write data flow | 35.4.1.1 写数据流

1. Write requests are received into an 8 entry request FIFO. Access is received only when there are at least two available entries. Each entry holds all of the AXI attributes.
1. 写请求被接收到一个8条目的请求FIFO中。只有当至少有两个可用条目时才接收访问。每个条目包含所有AXI属性。

• If the burst length is greater than 8, the access splits into two accesses: one with burst length 8 and the other with the remainder.
• 如果突发长度大于8,访问将分成两个访问:一个突发长度为8,另一个为剩余部分。

• The access can be performed as soon as the entire data phase of the associated write request is completed (all data beats were received).
• 整个数据阶段完成后(收到所有数据节拍),即可执行访问。

2. A simple round-robin arbitration between the pending read and write accesses is performed, and the pointer to this stage's winner access is sent to the re-ordering buffer.
2. 对挂起的读和写访问执行简单的轮询仲裁,并将该阶段获胜访问的指针发送到重排序缓冲区。

3. The reordering mechanism is activated to find the winner access, which is the access that best utilizes the DDR bus, based on its dynamic score. For further information see Dynamic scoring mode (Arbitration Winning Conditions).
3. 激活重排序机制以找到获胜访问,这是基于其动态分数最能利用DDR总线的访问。有关详细信息,请参阅动态评分模式(仲裁获胜条件)。

4. The winner write access at the previous stage is received and is held for dispatch to the DDR logic.
4. 接收上一阶段的获胜写访问,并等待发送到DDR逻辑。

5. When the DDR command control unit is ready to accept the write request, it issues (if needed) a precharge/active command to the DDR device according to the status of the bank model and the parameters of the timers.
5. 当DDR命令控制单元准备好接受写请求时,它根据bank模型的状态和计时器的参数向DDR设备发出(如果需要)预充电/激活命令。

6. The DDR logic drives the associated data to the DDR device through the DDR PHY.
6. DDR逻辑通过DDR PHY将相关数据驱动到DDR设备。

#### 35.4.1.2 Read data flow | 35.4.1.2 读数据流

1. Read requests are received into a 16 entry request FIFO in MMDC if there are at least two available entries. Each entry holds all of the AXI attributes.
1. 如果至少有两个可用条目,则在MMDC中接收到的读请求进入16条目的请求FIFO。每个条目包含所有AXI属性。

> **NOTE | 注** If the burst length is greater than 8, the access splits into 2 accesses (one with burst length 8 and the other with the remainder).
> 如果突发长度大于8,访问将分成2个访问(一个突发长度为8,另一个为剩余部分)。

2. A simple round-robin arbitration between the pending read and write accesses is performed and the pointer to this phase's winner access is sent to the re-ordering buffer.
2. 对挂起的读和写访问执行简单的轮询仲裁,并将该阶段获胜访问的指针发送到重排序缓冲区。

3. The reordering mechanism is activated to find the winner access, which is the access that best utilizes the DDR bus, based on its dynamic score. For further information see Dynamic scoring mode (Arbitration Winning Conditions).
3. 激活重排序机制以找到获胜访问,这是基于其动态分数最能利用DDR总线的访问。有关详细信息,请参阅动态评分模式(仲裁获胜条件)。

4. The winner read access at the previous stage is sampled and is held for dispatch to the DDR logic. This read access will be dispatched when there is at least one free slot in the read data buffer to store the data.
4. 对上一阶段的获胜读访问进行采样并等待发送到DDR逻辑。当读数据缓冲区中至少有一个空闲槽来存储数据时,将发送此读访问。

5. When the DDR command control unit is ready to accept the read request, it issues (if needed) a precharge/active command to the DDR device according to the status of the bank model and the parameters of the timers.
5. 当DDR命令控制单元准备好接受读请求时,它根据bank模型的状态和计时器的参数向DDR设备发出(如果需要)预充电/激活命令。

6. The MMDC PHY samples the read data, and the DDR logic transfers the data to the associated slot in the read data buffer.
6. MMDC PHY对读数据进行采样,DDR逻辑将数据转移到读数据缓冲区中的相关槽。

7. MMDC transfers the data back to the master.
7. MMDC将数据返回给主设备。

### 35.4.2 MMDC initialization | 35.4.2 MMDC初始化

Because the MMDC is disabled when the chip exits reset, no clock is driven to the DDR device and the whole interface towards the DDR device is inactive. The following steps are required to activate the MMDC properly.
因为当芯片退出复位时MMDC被禁用,所以没有时钟驱动到DDR设备,整个DDR设备接口处于非激活状态。需要以下步骤来正确激活MMDC。

> **NOTE | 注** To guarantee that the DRAM_RESET and DRAM_SDCKE signals are kept low during the power-up and reset sequences of the chip (as defined by JEDEC), you must connect those signals to pull-down resistors.
> 为保证DRAM_RESET和DRAM_SDCKE信号在芯片的上电和复位序列期间保持低电平(按照JEDEC定义),您必须将这些信号连接到下拉电阻。

1. Set MDSCR[CON_REQ], which sets the configuration request; note that because the MMDC is disabled, there is no need to poll the configuration acknowledge bit at MDSCR[CON_ACK].
1. 设置MDSCR[CON_REQ],设置配置请求;注意,由于MMDC被禁用,不需要轮询MDSCR[CON_ACK]中的配置确认位。

2. Configure the desired timing parameters at the MDCFG0, MDCFG1, MDOTC, and MDCFG2 registers.
2. 在MDCFG0、MDCFG1、MDOTC和MDCFG2寄存器中配置所需的时序参数。

3. Configure the DDR type and other miscellaneous parameters at the MDMISC register.
3. 在MDMISC寄存器中配置DDR类型和其他杂项参数。

4. Configure the required delay while leaving reset, at the MDOR register.
4. 在MDOR寄存器中配置退出复位所需的延迟。

5. Configure the DDR physical parameters (density and burst length) at the MDCTL register.
5. 在MDCTL寄存器中配置DDR物理参数(密度和突发长度)。

6. Perform a ZQ calibration of the MMDC module to correctly initialize drive strengths.
6. 对MMDC模块执行ZQ校准以正确初始化驱动强度。

7. Enable MMDC with the desired chip select at MDCTL[SDE_0] (for chip select 0) and MDCTL[SDE_1] (for chip select 1). At this point, MMDC starts the reset and initialization sequence related to DRAM_RESET/DRAM_SDCKE as defined by JEDEC.
7. 在MDCTL[SDE_0](用于片选0)和MDCTL[SDE_1](用于片选1)处用所需的片选启用MMDC。此时,MMDC开始按照JEDEC定义启动与DRAM_RESET/DRAM_SDCKE相关的复位和初始化序列。

8. Complete the initialization sequence as defined by JEDEC by issuing MRS/MRW commands for (ZQ, ODT, PRE, and so on). To issue those commands, configure the appropriate command and address at the MDSCR register.
8. 通过发出MRS/MRW命令(用于ZQ、ODT、PRE等)来完成JEDEC定义的初始化序列。要发出这些命令,需要在MDSCR寄存器中配置适当的命令和地址。

9. Program the DDR mode registers by configuring the appropriate command and address at the MDSCR register.
9. 通过在MDSCR寄存器中配置适当的命令和地址来编程DDR模式寄存器。

10. Configure the power down and self-refresh entry and exit parameters at the MDPDC and MAPSR registers.
10. 在MDPDC和MAPSR寄存器中配置掉电和自刷新进入和退出参数。

11. Configure the ZQ scheme at the MPZQHWCTRL and MPZQLP2CTL registers.
11. 在MPZQHWCTRL和MPZQLP2CTL寄存器中配置ZQ方案。

12. Configure and activate the periodic refresh scheme at the MDREF register.
12. 在MDREF寄存器中配置并激活周期性刷新方案。

13. Deassert the configuration request by clearing MDSCR[CON_REQ].
13. 通过清除MDSCR[CON_REQ]来解除配置请求。

> **NOTE | 注** Steps 1 through 6 are non-blocking and can be done in any order.
> 步骤1至6是非阻塞的,可以任何顺序完成。

Upon completion of these steps, MMDC is ready for work and to process AXI accesses.
完成这些步骤后,MMDC准备好工作并处理AXI访问。

> **NOTE | 注** To achieve better timing and better precision, it is recommended that users configure the MMDC PHY delay parameters by operating either the automatic or manual calibration process. Before starting any calibration process, you must disable the periodic refresh scheme (MDREF[REF_SEL] = 11) and then issue a manual refresh command by configuring MDSCR[CMD] to 2h. For further information, see Calibration Process.
> 为获得更好的时序和精度,建议用户通过自动或手动校准过程来配置MMDC PHY延迟参数。在开始任何校准过程之前,必须禁用周期性刷新方案(MDREF[REF_SEL] = 11),然后通过将MDSCR[CMD]配置为2h来发出手动刷新命令。有关详细信息,请参阅校准过程。

### 35.4.3 Configuring the MMDC registers | 35.4.3 配置MMDC寄存器

To safely modify MMDC's internal configuration registers, MMDC must be placed into configuration mode.
要安全地修改MMDC的内部配置寄存器,MMDC必须进入配置模式。

Use the following steps to enter configuration mode.
使用以下步骤进入配置模式。

1. Issue a configuration request by setting MDSCR[CON_REQ].
1. 通过设置MDSCR[CON_REQ]发出配置请求。

2. Poll on configuration acknowledge until it is set at MDSCR[CON_ACK].
2. 轮询配置确认,直到在MDSCR[CON_ACK]中设置。

At this point, MMDC enters configuration mode and accessing the MMDC registers is permitted.
此时,MMDC进入配置模式,可以访问MMDC寄存器。

> **NOTE | 注** During configuration mode, MMDC prevents further AXI accesses from being acknowledged.
> 在配置模式期间,MMDC阻止进一步的AXI访问被确认。

Upon deassertion of MDSCR[CON_REQ], MMDC leaves configuration mode and AXI accesses are processed.
解除MDSCR[CON_REQ]后,MMDC离开配置模式并处理AXI访问。

### 35.4.4 MMDC Address Space | 35.4.4 MMDC地址空间

#### 35.4.4.1 Address decoding | 35.4.4.1 地址解码

MMDC supports up to two consecutive chip selects, each with the same density.
MMDC支持最多两个连续片选,每个片选密度相同。

It is optional to configure the partition between the chip selects through MDASP[CS0_END].
可以通过MDASP[CS0_END]配置片选之间的分区(可选)。

The incoming AXI address bus is 32 bits. MMDC decodes each access as follows:
输入的AXI地址总线为32位。MMDC按以下方式解码每个访问:

1. chip select | 片选
2. bank number | bank号
3. row number | 行号
4. column number | 列号

The following registers in the MMDC define the DDR address space:
MMDC中的以下寄存器定义DDR地址空间:

• MDMISC[DDR_4_BANK]—Defines either 4 or 8 banks in the DDR device | 定义DDR设备中是4个还是8个bank
• MDCTL[DSIZ]—Defines the DDR data bus width of x16 | 定义DDR数据总线宽度为x16
• MDMISC[BI]—Defines whether bank interleaving is on or off | 定义bank交错是打开还是关闭
• MDCTL[COL]—Defines the column size of the DDR device | 定义DDR设备的列大小
• MDCTL[ROW]—Defines the row size of the DDR device | 定义DDR设备的行大小

The following tables show address decoding examples for x16 bit DDR devices when bank interleaving is both on and off. It is assumed that the configuration is as follows: 8 banks (3 bits), 15 bit assignment for the row, and 10 bit assignment for the column. The total density is 256 MWords (512 Mbytes for x16).
下表显示了bank交错打开和关闭时x16位DDR设备的地址解码示例。假设配置如下:8个bank(3位),行为15位分配,列为10位分配。总密度为256 MWords(x16为512 Mbytes)。

> **NOTE | 注** Chip selection is done by comparing the 7 most significant address bits (ARADDR[31:25]/AWADDR[31:25]) with MDASP[CS0_END].
> 片选通过将7个最高地址位(ARADDR[31:25]/AWADDR[31:25])与MDASP[CS0_END]进行比较来完成。

**Table 35-4. Address decoding—bank interleaving off | 表35-4. 地址解码—bank交错关闭**

| AXI ADDRESS | x16 DDR | x32 DDR | AXI地址 | x16 DDR | x32 DDR |
|-------------|---------|---------|----------|---------|---------|
| A29 | — | BANK[2] | A29 | — | BANK[2] |
| A28 | BANK[2] | BANK[1] | A28 | BANK[2] | BANK[1] |
| A27 | BANK[1] | BANK[0] | A27 | BANK[1] | BANK[0] |
| A26 | BANK[0] | ROW[14] | A26 | BANK[0] | ROW[14] |
| A25 | ROW[14] | ROW[13] | A25 | ROW[14] | ROW[13] |
| A24 | ROW[13] | ROW[12] | A24 | ROW[13] | ROW[12] |
| A23 | ROW[12] | ROW[11] | A23 | ROW[12] | ROW[11] |
| A22 | ROW[11] | ROW[10] | A22 | ROW[11] | ROW[10] |
| A21 | ROW[10] | ROW[9] | A21 | ROW[10] | ROW[9] |
| A20 | ROW[9] | ROW[8] | A20 | ROW[9] | ROW[8] |
| A19 | ROW[8] | ROW[7] | A19 | ROW[8] | ROW[7] |
| A18 | ROW[7] | ROW[6] | A18 | ROW[7] | ROW[6] |
| A17 | ROW[6] | ROW[5] | A17 | ROW[6] | ROW[5] |
| A16 | ROW[5] | ROW[4] | A16 | ROW[5] | ROW[4] |
| A15 | ROW[4] | ROW[3] | A15 | ROW[4] | ROW[3] |
| A14 | ROW[3] | ROW[2] | A14 | ROW[3] | ROW[2] |
| A13 | ROW[2] | ROW[1] | A13 | ROW[2] | ROW[1] |
| A12 | ROW[1] | ROW[0] | A12 | ROW[1] | ROW[0] |
| A11 | ROW[0] | COL[9] | A11 | ROW[0] | COL[9] |
| A10 | COL[9] | COL[8] | A10 | COL[9] | COL[8] |
| A9 | COL[8] | COL[7] | A9 | COL[8] | COL[7] |
| A8 | COL[7] | COL[6] | A8 | COL[7] | COL[6] |
| A7 | COL[6] | COL[5] | A7 | COL[6] | COL[5] |
| A6 | COL[5] | COL[4] | A6 | COL[5] | COL[4] |
| A5 | COL[4] | COL[3] | A5 | COL[4] | COL[3] |
| A4 | COL[3] | COL[2] | A4 | COL[3] | COL[2] |
| A3 | COL[2] | COL[1] | A3 | COL[2] | COL[1] |
| A2 | COL[1] | COL[0] | A2 | COL[1] | COL[0] |
| A1 | COL[0] | — | A1 | COL[0] | — |
| A0 | — | — | A0 | — | — |

**Table 35-5. Address decoding—bank interleaving on | 表35-5. 地址解码—bank交错打开**

| AXI ADDRESS | x16 DDR | x32 DDR | AXI地址 | x16 DDR | x32 DDR |
|-------------|---------|---------|----------|---------|---------|
| A29 | — | ROW[14] | A29 | — | ROW[14] |
| A28 | ROW[14] | ROW[13] | A28 | ROW[14] | ROW[13] |
| A27 | ROW[13] | ROW[12] | A27 | ROW[13] | ROW[12] |
| A26 | ROW[12] | ROW[11] | A26 | ROW[12] | ROW[11] |
| A25 | ROW[11] | ROW[10] | A25 | ROW[11] | ROW[10] |
| A24 | ROW[10] | ROW[9] | A24 | ROW[10] | ROW[9] |
| A23 | ROW[9] | ROW[8] | A23 | ROW[9] | ROW[8] |
| A22 | ROW[8] | ROW[7] | A22 | ROW[8] | ROW[7] |
| A21 | ROW[7] | ROW[6] | A21 | ROW[7] | ROW[6] |
| A20 | ROW[6] | ROW[5] | A20 | ROW[6] | ROW[5] |
| A19 | ROW[5] | ROW[4] | A19 | ROW[5] | ROW[4] |
| A18 | ROW[4] | ROW[3] | A18 | ROW[4] | ROW[3] |
| A17 | ROW[3] | ROW[2] | A17 | ROW[3] | ROW[2] |
| A16 | ROW[2] | ROW[1] | A16 | ROW[2] | ROW[1] |
| A15 | ROW[1] | ROW[0] | A15 | ROW[1] | ROW[0] |
| A14 | ROW[0] | BANK[2] | A14 | ROW[0] | BANK[2] |
| A13 | BANK[2] | BANK[1] | A13 | BANK[2] | BANK[1] |
| A12 | BANK[1] | BANK[0] | A12 | BANK[1] | BANK[0] |
| A11 | BANK[0] | COL[9] | A11 | BANK[0] | COL[9] |
| A10 | COL[9] | COL[8] | A10 | COL[9] | COL[8] |
| A9 | COL[8] | COL[7] | A9 | COL[8] | COL[7] |
| A8 | COL[7] | COL[6] | A8 | COL[7] | COL[6] |
| A7 | COL[6] | COL[5] | A7 | COL[6] | COL[5] |
| A6 | COL[5] | COL[4] | A6 | COL[5] | COL[4] |
| A5 | COL[4] | COL[3] | A5 | COL[4] | COL[3] |
| A4 | COL[3] | COL[2] | A4 | COL[3] | COL[2] |
| A3 | COL[2] | COL[1] | A3 | COL[2] | COL[1] |
| A2 | COL[1] | COL[0] | A2 | COL[1] | COL[0] |
| A1 | COL[0] | — | A1 | COL[0] | — |
| A0 | — | — | A0 | — | — |

> **NOTE | 注** In cases where this is an access to a non-initialized or disconnected chip select, behavior may be unexpected.
> 在访问未初始化或断开连接的片选的情况下,行为可能不符合预期。

#### 35.4.4.2 Chip select settings | 35.4.4.2 片选设置

MMDC drives the incoming access to either CS0 or CS1 by comparing the 7 most significant address bits (ARADDR[31:25]/AWADDR[31:25]) with MDASP[CS0_END].
MMDC通过将7个最高地址位(ARADDR[31:25]/AWADDR[31:25])与MDASP[CS0_END]进行比较,将输入访问发送到CS0或CS1。

Generally, the total density per chip-select must be a power of two and the total density must be the same for each chip-select.
通常,每个片选的总密度必须是2的幂,且每个片选的总密度必须相同。

Creating 4 Gbyte address space with 2 Gbyte CS density and Creating 2 Gbyte address spaces with 1 Gbyte CS density show how to create a continous address space and configure the MMDC accordingly.
创建4 Gbyte地址空间(2 Gbyte CS密度)和创建2 Gbyte地址空间(1 Gbyte CS密度)展示了如何创建连续地址空间并相应配置MMDC。

##### 35.4.4.2.1 Creating 4 Gbyte address space with 2 Gbyte CS density | 35.4.4.2.1 创建4 Gbyte地址空间(2 Gbyte CS密度)

If the DDR memory space allocation is 4 Gbytes, only one configuration of chip select partition is allowed. The register MDASP[CS0_END] should be set to 2 Gbytes partition (16Gb).
如果DDR存储器空间分配为4 Gbytes,则只允许一种片选分区配置。寄存器MDASP[CS0_END]应设置为2 Gbytes分区(16Gb)。

The figure below shows the associated memory space.
下图显示了相关的存储器空间。

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/63ce86576320fd9875718188a22c1645e2ac0a67a8fcd25c160aad1b76e98ec3.jpg)

**Figure 35-2. Chip select partion—2 Gbytes per chip select | 图35-2. 片选分区—每片选2 Gbytes**

##### 35.4.4.2.2 Creating 2 Gbyte address spaces with 1 Gbyte CS density | 35.4.4.2.2 创建2 Gbyte地址空间(1 Gbyte CS密度)

If the DDR memory space allocation is 2 Gbytes, there are three options for configuring the chip select partition:MDASP[CS0_END] to 001_1111 (1 Gbyte), MDASP[CS0_END] to 011_1111 (2 Gbytes), and MDASP[CS0_END] to 101_1111 (3 Gbytes).
如果DDR存储器空间分配为2 Gbytes,则有三种选项来配置片选分区:MDASP[CS0_END]设置为001_1111(1 Gbyte)、MDASP[CS0_END]设置为011_1111(2 Gbytes)和MDASP[CS0_END]设置为101_1111(3 Gbytes)。

If DDR memory space allocation is 2 Gbytes, there are three options for configuring the chip select partition:
如果DDR存储器空间分配为2 Gbytes,则有三种选项来配置片选分区:

• MDASP[CS0_END] to 001_1111 (1 Gbyte) | MDASP[CS0_END]设为001_1111(1 Gbyte)
• MDASP[CS0_END] to 011_1111 (2 Gbytes) | MDASP[CS0_END]设为011_1111(2 Gbytes)
• MDASP[CS0_END] to 101_1111 (3 Gbytes) | MDASP[CS0_END]设为101_1111(3 Gbytes)

The figure below shows the associated memory space:
下图显示了相关的存储器空间:

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/e355b01792121d2ba52900d3754bb248ea1e7ca344aebe6f412b70f1fd524074.jpg)

**Figure 35-3. Chip select partion—1 Gbyte per chip select | 图35-3. 片选分区—每片选1 Gbyte**

#### 35.4.4.3 Translation of AXI accesses to DDR accessess | 35.4.4.3 AXI访问到DDR访问的转换

##### 35.4.4.3.1 Example 1 | 示例1

Assume the AXI read access has the following attributes:
假设AXI读访问具有以下属性:

• Wrap (arburst[1:0] = 10b) | 包装突发(arburst[1:0] = 10b)
• AXI size of 128 bits (arsize[2:0] = 100b) | AXI大小128位(arsize[2:0] = 100b)
• AXI length of 8 (arlen[3:0] = 0111b) | AXI长度8(arlen[3:0] = 0111b)
• AXI address with suffix B0h (non-aligned to AXI wrap boundary which is 16Bx8=128B = 0x80) | AXI地址后缀B0h(未对齐到AXI包装边界16Bx8=128B = 0x80)

Toward DDR3(MDMISC[DDR_TYPE] = 00b) with the following attributes:
针对DDR3(MDMISC[DDR_TYPE] = 00b),具有以下属性:

• x32 (MDCTL[DSIZ] = 01b) | x32(MDCTL[DSIZ] = 01b)
• burst length of 8 (MDCTL[BL] = 1b) | 突发长度8(MDCTL[BL] = 1b)

In this case, the AXI wrap boundary is every 16Bx8=128B (0x80) and the DDR wrap boundary is every 4Bx8=32B (0x20).
在这种情况下,AXI包装边界为每16Bx8=128B(0x80),DDR包装边界为每4Bx8=32B(0x20)。

The master expects to fetch the data that is associated with the following addresses: 0xB0, 0xC0, 0xD0, 0xE0, 0xF0, 0x80, 0x90, 0xA0.
主设备期望获取与以下地址关联的数据:0xB0、0xC0、0xD0、0xE0、0xF0、0x80、0x90、0xA0。

The first aligned AXI address that is associated with suffix 0xB0 is with suffix 0x80, and the last wrap AXI address is with suffux 0xFF. Because the AXI master expects to get the first data from AXI address with suffix 0xB0, the MMDC issues the following accesses toward the DDR:
与后缀0xB0关联的第一个对齐AXI地址是后缀0x80,最后一个包装AXI地址是后缀0xFF。因为AXI主设备期望从后缀为0xB0的AXI地址获取第一个数据,所以MMDC向DDR发出以下访问:

• Read access toward logic address with suffix 0xA0 (DDR boundary is 0x20 and 0xA0 is the closest to 0xB0)
• 访问逻辑地址后缀0xA0(DDR边界为0x20,0xA0最接近0xB0)

> **NOTE | 注** Logic address is the address of the column normalized to 1 byte.
> 逻辑地址是归一化为1字节的列地址。

• Read access toward logic address with suffix 0xC0 | 访问逻辑地址后缀0xC0
• Read access toward logic address with suffix 0xE0 | 访问逻辑地址后缀0xE0
• Read access toward logic address with suffix 0x80 | 访问逻辑地址后缀0x80

The MMDC breaks the AXI access into four DDR accesses and returns the read data associated with address 0xB0 to the master first. The read data fetched from address 0xA0 is stored in the internal buffers and is driven back to the master at the end.
MMDC将AXI访问分解为四个DDR访问,并首先将与地址0xB0关联的读数据返回给主设备。从地址0xA0获取的读数据存储在内部缓冲区中,并在最后驱动回主设备。

##### 35.4.4.3.2 Example 2 | 示例2

Assume the AXI write access has the following attributes:
假设AXI写访问具有以下属性:

• Increment (awburst[1:0]=2'b01) | 增量(awburst[1:0]=2'b01)
• AXI size of 64bits (awsize[2:0]=3'b011) | AXI大小64位(awsize[2:0]=3'b011)
• AXI length of 8 (awlen[3:0]=4'b0111) | AXI长度8(awlen[3:0]=4'b0111)
• AXI address with suffix 0xB0 (aligned as the size of the increment is 8B) | AXI地址后缀0xB0(由于增量大小为8B而对齐)

Toward DDR3(MDMISC[DDR_TYPE]=2'b00) with the following attributes:
针对DDR3(MDMISC[DDR_TYPE]=2'b00),具有以下属性:

• x64 (MDCTL[DSIZ]=2'b10) | x64(MDCTL[DSIZ]=2'b10)
• burst length of 8 (MDCTL[BL]=1'b1) | 突发长度8(MDCTL[BL]=1'b1)

In this case, the AXI alignment is every 8B and the DDR boundary is every 8Bx8=64B (0x40).
在这种情况下,AXI对齐为每8B,DDR边界为每8Bx8=64B(0x40)。

The master expects to write the data to the following addresses: 0xB0, 0xB8, 0xC0, 0xC8, 0xD0, 0xD8, 0xE0, 0xE8.
主设备期望将数据写入以下地址:0xB0、0xB8、0xC0、0xC8、0xD0、0xD8、0xE0、0xE8。

The MMDC will issue the following accesses toward the DDR:
MMDC将向DDR发出以下访问:

• Write access toward logic address with suffix 0x80 (DDR boundary is 0x40 and 0x80 is the closest to 0xB0) while address 0x80 to 0xAF are masked by DM (data masking signal).
• 访问逻辑地址后缀0x80(DDR边界为0x40,0x80最接近0xB0),而地址0x80到0xAF被DM(数据掩码信号)掩码。

> **NOTE | 注** Logic address is the address of the column normalized to 1 byte.
> 逻辑地址是归一化为1字节的列地址。

• Write access toward logic address with suffix 0xC0 while addresses 0xF0 through 0xFF are masked by DM (data masking signal)
• 访问逻辑地址后缀0xC0,同时地址0xF0到0xFF被DM(数据掩码信号)掩码

The MMDC will break the AXI access into two DDR accesses.
MMDC将把AXI访问分成两个DDR访问。

##### 35.4.4.3.3 Example 3 | 示例3

Assume the AXI write access has the following attributes:
假设AXI写访问具有以下属性:

• Wrap (awburst[1:0]=2'b10) | 包装突发(awburst[1:0]=2'b10)
• AXI size of 128bits (awsize[2:0] = 3'b100) | AXI大小128位(awsize[2:0] = 3'b100)
• AXI length of 4 (awlen[3:0]=4'b0011) | AXI长度4(awlen[3:0]=4'b0011)
• AXI address with suffix 0x80 (aligned) | AXI地址后缀0x80(对齐)

Toward DDR3(MDMISC[DDR_TYPE]=2'b00) with the following attributes:
针对DDR3(MDMISC[DDR_TYPE]=2'b00),具有以下属性:

• x64 (MDCTL[DSIZ]=2'b10) | x64(MDCTL[DSIZ]=2'b10)
• burst length of 8 (MDCTL[BL]=1'b1) | 突发长度8(MDCTL[BL]=1'b1)

In this case, the AXI wrap boundary is every 16Bx4=64B (0x40) and the DDR wrap boundary is every 8x8=64B (0x40).
在这种情况下,AXI包装边界为每16Bx4=64B(0x40),DDR包装边界为每8x8=64B(0x40)。

The master expects to write the data to the following addresses: 0x80, 0x90, 0xA0, 0xB0.
主设备期望将数据写入以下地址:0x80、0x90、0xA0、0xB0。

Because the AXI wrap boundary and DDR wrap boundary are similar and the starting AXI address is aligned, the MMDC will issue only one access toward the DDR as follows:
因为AXI包装边界和DDR包装边界相似且起始AXI地址是对齐的,所以MMDC将只向DDR发出一个访问,如下所示:

• Write access towards logic address with suffix 0x80 | 访问逻辑地址后缀0x80

> **NOTE | 注** Logic address is the address of the column normalized to 1 byte.
> 逻辑地址是归一化为1字节的列地址。

##### 35.4.4.3.4 Example 4 | 示例4

Assume the AXI write access has the following attributes:
假设AXI写访问具有以下属性:

• Increment (awburst[1:0]=2'b01) | 增量(awburst[1:0]=2'b01)
• AXI size of 64bits (awsize[2:0]=3'b011) | AXI大小64位(awsize[2:0]=3'b011)
• AXI length of 2 (awlen[3:0]=4'b0001) | AXI长度2(awlen[3:0]=4'b0001)
• AXI address with suffix 0x5 (non aligned) | AXI地址后缀0x5(未对齐)

Toward DDR3(MDMISC[DDR_TYPE]=2'b00) with the following attributes:
针对DDR3(MDMISC[DDR_TYPE]=2'b00),具有以下属性:

• x32 (MDCTL[DSIZ]=2'b10) | x32(MDCTL[DSIZ]=2'b10)
• burst length of 8 (MDCTL[BL]=1'b1) | 突发长度8(MDCTL[BL]=1'b1)

In this case the AXI alignment is every 8B (0x8) and the DDR boundary is every 4Bx8=32B (0x20).
在这种情况下,AXI对齐为每8B(0x8),DDR边界为每4Bx8=32B(0x20)。

The master expects to write the data to the following addresses: 0x5 (with WSTRB=0xE0), 0x8 (till 0xF).
主设备期望将数据写入以下地址:0x5(带WSTRB=0xE0)、0x8(直到0xF)。

The MMDC will issue one access toward the DDR as follows:
MMDC将向DDR发出一个访问,如下所示:

Write access toward logic address with suffix 0x0 (DDR boundary is 0x20 and 0x0 is the closest to 0x0) while address 0x0 till 0x4 are masked by DM (data masking signal) and address 0x10 till 0x1F are also masked by DM.
访问逻辑地址后缀0x0(DDR边界为0x20,0x0最接近0x0),同时地址0x0到0x4被DM(数据掩码信号)掩码,地址0x10到0x1F也被DM掩码。

##### 35.4.4.3.5 Example 5 | 示例5

Assume AXI write access has the following attributes:
假设AXI写访问具有以下属性:

• Increment (awburst[1:0]=2'b01) | 增量(awburst[1:0]=2'b01)
• AXI size of 64bits (awsize[2:0]=3'b011) | AXI大小64位(awsize[2:0]=3'b011)
• AXI length of 7 (awlen[3:0]=4'b0001) | AXI长度7(awlen[3:0]=4'b0001)
• AXI address with suffix 0x10 (aligned) | AXI地址后缀0x10(对齐)

Toward DDR3 (MDMISC[DDR_TYPE]=2'b00) with the following attributes:
针对DDR3(MDMISC[DDR_TYPE]=2'b00),具有以下属性:

• x64 (MDCTL[DSIZ]=2'b10) | x64(MDCTL[DSIZ]=2'b10)
• burst length of 8 (MDCTL[BL]=1'b1) | 突发长度8(MDCTL[BL]=1'b1)

In this case the AXI alignment is every 8B (0x8) and the DDR boundary is every 8Bx8=64B (0x40).
在这种情况下,AXI对齐为每8B(0x8),DDR边界为每8Bx8=64B(0x40)。

The master expects to write the data to the following addresses: 0x10, 0x18, 0x20, 0x28, 0x30, 0x38, 0x40, 0x48.
主设备期望将数据写入以下地址:0x10、0x18、0x20、0x28、0x30、0x38、0x40、0x48。

Because the AXI access is not aligned to DDR boundary, which is every 0x40, the MMDC will issue two accesses toward the DDR as follows:
因为AXI访问未对齐DDR边界(每0x40),所以MMDC将向DDR发出两个访问,如下所示:

• Write access toward logic address with suffix 0x0 while address 0x0 till 0xF are masked by DM (data masking signal).
• 访问逻辑地址后缀0x0,同时地址0x0到0xF被DM(数据掩码信号)掩码。

> **NOTE | 注** Logic address is the address of the column normalized to 1 byte.
> 逻辑地址是归一化为1字节的列地址。

• Write access towards logic address with suffix 0x40 while addresses 0x50 till 0x7F are masked by DM (data masking signal).
• 访问逻辑地址后缀0x40,同时地址0x50到0x7F被DM(数据掩码信号)掩码。

#### 35.4.4.4 Address mirroring | 35.4.4.4 地址镜像

When enabling this feature, address bits DRAM_A3, DRAM_A4, DRAM_A5, DRAM_A6, DRAM_A7, DRAM_A8, DRAM_SDBA0, and DRAM_SDBA1 behave differently according to the associated chip select.
启用此功能时,地址位DRAM_A3、DRAM_A4、DRAM_A5、DRAM_A6、DRAM_A7、DRAM_A8、DRAM_SDBA0和DRAM_SDBA1根据相关的片选表现不同。

This feature facilitates PCB board routing for devices on chip select 1, which are typically populated on the opposite side of the PCB from the devices on chip select 0.
此功能便于片选1上的器件的PCB板布线,这些器件通常与片选0上的器件在PCB的另一侧。

> **NOTE | 注** This feature will not be supported for DDR3 since only a single chip select is supported for DDR3.
> 此功能在DDR3中不支持,因为DDR3仅支持单个片选。

The following table specifies the address mirroring options:
下表指定了地址镜像选项:

**Table 35-6. Address mirroring options | 表35-6. 地址镜像选项**

| MMDC pin | Chip select 0 pin | Chip select 1 pin | MMDC引脚 | 片选0引脚 | 片选1引脚 |
|----------|------------------|------------------|----------|-----------|-----------|
| DRAM_A3 | DRAM_A3 | DRAM_A4 | DRAM_A3 | DRAM_A3 | DRAM_A4 |
| DRAM_A4 | DRAM_A4 | DRAM_A3 | DRAM_A4 | DRAM_A4 | DRAM_A3 |
| DRAM_A5 | DRAM_A5 | DRAM_A6 | DRAM_A5 | DRAM_A5 | DRAM_A6 |
| DRAM_A6 | DRAM_A6 | DRAM_A5 | DRAM_A6 | DRAM_A6 | DRAM_A5 |
| DRAM_A7 | DRAM_A7 | DRAM_A8 | DRAM_A7 | DRAM_A7 | DRAM_A8 |
| DRAM_A8 | DRAM_A8 | DRAM_A7 | DRAM_A8 | DRAM_A8 | DRAM_A7 |
| DRAM_SDBA0 | DRAM_SDBA0 | DRAM_SDBA1 | DRAM_SDBA0 | DRAM_SDBA0 | DRAM_SDBA1 |
| DRAM_SDBA1 | DRAM_SDBA1 | DRAM_SDBA0 | DRAM_SDBA1 | DRAM_SDBA1 | DRAM_SDBA0 |

### 35.4.5 LPDDR2 and DDR3 pin mux mapping | 35.4.5 LPDDR2和DDR3引脚复用映射

The following table shows the pin mux mapping between LPDDR2 and DDR3. The i.MX DDR I/O pads corresponds with the DDR3 standard.
下表显示了LPDDR2和DDR3之间的引脚复用映射。i.MX DDR I/O引脚与DDR3标准对应。

• In DDR3, all DRAM_DATA, DRAM_SDQS, and DRAM_DQM data lines work with channel 0.
• 在DDR3中,所有DRAM_DATA、DRAM_SDQS和DRAM_DQM数据线工作在通道0。

• In LPDDR2, DRAM_DDQS[3:0], DRAM_DATA[31:0] and DRAM_DQM[3:0] work with channel 0. DRAM_SDQS[7:4], DRAM_DATA[63:32], and DRAM_DQM[7:4] work with channel 1.
• 在LPDDR2中,DRAM_DDQS[3:0]、DRAM_DATA[31:0]和DRAM_DQM[3:0]工作在通道0。DRAM_SDQS[7:4]、DRAM_DATA[63:32]和DRAM_DQM[7:4]工作在通道1。

**Table 35-7. LPDDR2 and DRAM pin mux mapping | 表35-7. LPDDR2和DRAM引脚复用映射**

| DRAM I/O pad | LPDDR2 I/O pad | DRAM I/O引脚 | LPDDR2 I/O引脚 |
|--------------|----------------|--------------|----------------|
| DRAM_ADDR00 | LPDDR2_CA0 | DRAM_ADDR00 | LPDDR2_CA0 |
| DRAM_ADDR01 | LPDDR2_CA1 | DRAM_ADDR01 | LPDDR2_CA1 |
| DRAM_ADDR02 | LPDDR2_CA2 | DRAM_ADDR02 | LPDDR2_CA2 |
| DRAM_ADDR03 | LPDDR2_CA3 | DRAM_ADDR03 | LPDDR2_CA3 |
| DRAM_ADDR04 | LPDDR2_CA4 | DRAM_ADDR04 | LPDDR2_CA4 |
| DRAM_ADDR05 | LPDDR2_CA5 | DRAM_ADDR05 | LPDDR2_CA5 |
| DRAM_ADDR06 | LPDDR2_CA6 | DRAM_ADDR06 | LPDDR2_CA6 |
| DRAM_ADDR07 | LPDDR2_CA7 | DRAM_ADDR07 | LPDDR2_CA7 |
| DRAM_ADDR08 | LPDDR2_CA8 | DRAM_ADDR08 | LPDDR2_CA8 |
| DRAM_ADDR09 | LPDDR2_CA9 | DRAM_ADDR09 | LPDDR2_CA9 |
| DRAM_ADDR10 | — | DRAM_ADDR10 | — |
| DRAM_ADDR11 | — | DRAM_ADDR11 | — |
| DRAM_ADDR12 | — | DRAM_ADDR12 | — |
| DRAM_ADDR13 | — | DRAM_ADDR13 | — |
| DRAM_ADDR14 | — | DRAM_ADDR14 | — |
| DRAM_ADDR15 | — | DRAM_ADDR15 | — |
| DRAM_CAS_B | — | DRAM_CAS_B | — |
| DRAM_RAS_B | — | DRAM_RAS_B | — |
| DRAM_WE_B | — | DRAM_WE_B | — |
| DRAM_SDCKE0 | LPDDR2_CKE0 | DRAM_SDCKE0 | LPDDR2_CKE0 |
| DRAM_SDCKE1 | LPDDR2_CKE1 | DRAM_SDCKE1 | LPDDR2_CKE1 |
| DRAM_CS_B0 | LPDDR2_CS_B0 | DRAM_CS_B0 | LPDDR2_CS_B0 |
| DRAM_CS_B1 | LPDDR2_CS_B1 | DRAM_CS_B1 | LPDDR2_CS_B1 |
| DRAM_ODT0 | LPDDR2_ODT0 | DRAM_ODT0 | LPDDR2_ODT0 |
| DRAM_ODT1 | LPDDR2_ODT1 | DRAM_ODT1 | LPDDR2_ODT1 |
| DRAM_SDCLK0_P | LPDDR2_CK0 | DRAM_SDCLK0_P | LPDDR2_CK0 |
| DRAM_SDCLK1 | LPDDR2_CK1 | DRAM_SDCLK1 | LPDDR2_CK1 |
| DRAM_BA0 | — | DRAM_BA0 | — |
| DRAM_BA1 | — | DRAM_BA1 | — |
| DRAM_BA2 | — | DRAM_BA2 | — |

### 35.4.6 Power Saving and Clock Frequency Change modes | 35.4.6 功耗管理和时钟频率变化模式

#### 35.4.6.1 Power saving general | 35.4.6.1 功耗管理概述

MMDC supports multiple DDR power saving modes.
MMDC支持多种DDR功耗管理模式。

> **NOTE | 注** At default, the power saving modes are disabled. These modes may dramatically decrease the power consumption of DDR memories.
> 默认情况下,功耗管理模式被禁用。这些模式可以显著降低DDR存储器的功耗。

1. Self-refresh entry to the entire DDR device (for both chip select 0 and 1) can be activated through two mechanisms:
1. 可以通过两种机制激活对整个DDR设备的自刷新进入(对于片选0和1):

• LPMD (Low Power Mode) | LPMD(低功耗模式)

• Hardware handshaking (LPMD/LPACK) with the clock module in the system | 与系统中的时钟模块进行硬件握手(LPMD/LPACK)

• Software handshaking by setting the field MAPSR[LPMD] and polling MAPSR[LPACK] | 通过设置MAPSR[LPMD]字段和轮询MAPSR[LPACK]进行软件握手

• Automatic entry by configuring the amount of idle cycle for triggering selfrefresh entry through MAPSR[PST] and by clearing MAPSR[PSD] | 通过MAPSR[PST]配置空闲周期数来触发自刷新进入,并通过清除MAPSR[PSD]来实现自动进入

• DVFS (Dynamic Voltage and Frequency Change) | DVFS(动态电压和频率变化)

• Hardware handshaking (DVFS/DVACK) with the clock module in the system | 与系统中的时钟模块进行硬件握手(DVFS/DVACK)

• Software handshaking by setting the field MAPSR[DVFS] and polling MAPSR[DVACK] | 通过设置MAPSR[DVFS]字段和轮询MAPSR[DVACK]进行软件握手

> **NOTE | 注** If hardware or software requests for self-refresh entry were detected by the MMDC (even before the assertion of the LPACK), no write or read accesses will be acknowledged until the deassertion of those requests.
> 如果MMDC检测到硬件或软件自刷新进入请求(甚至在LPACK断言之前),则在解除这些请求之前不会确认任何写或读访问。

2. Automatic active/precharge power down entry to a specific chip select can be activated by configuring the ESDPDC register:
2. 可以通过配置ESDPDC寄存器来激活对特定片选的自动激活/预充电掉电进入:

• PWDT_0/PWDT_1 - define the number of idle cycles before entering power down, can be different value per chip select.
• PWDT_0/PWDT_1 - 定义进入掉电前的空闲周期数,每个片选可以不同。

• SLOW_PD - In case of DDR3 memory is configured to use slow precharge power down then this bit should be set as well.
• SLOW_PD - 如果DDR3存储器配置为使用慢预充电掉电,则也应设置此位。

• BOTH_CS_PS - The MMDC can either set each chip select independently to power down, according to its idle state, or set both chip selects to power down only if both in idle state for the configured period.
• BOTH_CS_PS - MMDC可以独立设置每个片选根据其空闲状态进入掉电,或者仅当两个片选在配置期间都处于空闲状态时才设置两个片选进入掉电。

• Few parameters must be configured in addition: | 还需要配置一些参数:

• Timing parameters at MDCFG0[tXP and tXPDLL]. | MDCFG0中的时序参数[tXP和tXPDLL]。

• ODT timing at MDOTC[tAOFPD, tAONPD, tANPD and tAXPD] | MDOTC中的ODT时序[tAOFPD、tAONPD、tANPD和tAXPD]

> **NOTE | 注** It is possible to enter certain chip selects to low power consumption while the second chip select is activated.
> 可以使某些片选进入低功耗,而第二个片选保持激活。

3. Automatic precharge of all DDR banks to a specific chip select. Can be activated by configuring ESDPDC fields: PRCT_0 and PRCT_1. Each field determines a value loaded to a different chip select.
3. 自动预充电所有DDR bank到特定片选。可以通过配置ESDPDC字段PRCT_0和PRCT_1来激活。每个字段确定加载到不同片选的值。

#### 35.4.6.2 Self refresh and Frequency change entry/exit | 35.4.6.2 自刷新和频率变化进入/退出

As described in Power saving general, the MMDC supports two mechanisms that will cause the DDR device to enter self-refresh mode:
如功耗管理概述中所述,MMDC支持两种导致DDR设备进入自刷新模式的机制:

• LPMD (Low Power Mode) - For power saving purposes | LPMD(低功耗模式) - 用于省电

• DVFS (Dynamic Voltage and Frequency Change) - For clock frequency changes | DVFS(动态电压和频率变化) - 用于时钟频率变化

While the DDR device is in self-refresh mode, there is no need to provide periodic refresh commands.
当DDR设备处于自刷新模式时,不需要提供周期性刷新命令。

The MMDC treats hardware/software handshaking of LPMD/DVFS in the same manner:
MMDC以相同方式处理LPMD/DVFS的硬件/软件握手:

• Upon the assertion of LPMD/DVFS request, the following is done:
• 断言LPMD/DVFS请求时,执行以下操作:

• The MMDC blocks any further AXI accesses even before the acknowledge is asserted | MMDC甚至在确认信号断言之前就阻止任何进一步的AXI访问

• Completes all opened AXI accesses | 完成所有打开的AXI访问

• Closes (precharge) all banks in the appropriate timing | 在适当的时序中关闭(预充电)所有bank

• Drives self-refresh command by deasserting clock enable signal (DRAM_SDCKE is driven to "0") together with a refresh command. This occurs after satisfying tRP/tRPA from the precharge all command.
• 通过解除时钟使能信号(DRAM_SDCKE被驱动到"0")以及刷新命令来驱动自刷新命令。这发生在满足预充电所有命令的tRP/tRPA之后发生。

• Deasserts the clock (CK) that is driven to the DDR device | 解除驱动到DDR设备的时钟(CK)

• Asserts LPMD/DVFS acknowledge (LPACK/DVACK) | 断言LPMD/DVFS确认(LPACK/DVACK)

• Allows deassertion of the operating clock of the MMDC (AXI clock) | 允许解除MMDC的工作时钟(AXI时钟)

• Upon the deassertion of LPMD/DVFS request, the following is done:
• 解除LPMD/DVFS请求时,执行以下操作:

• Operating clock of the MMDC must be turned on before LPMD/DVFS is deasserted | MMDC的工作时钟必须在LPMD/DVFS解除之前打开

• Starts driving the clock (CK) to the DDR device | 开始驱动时钟(CK)到DDR设备

• After satisfying tCKSRX from clock renewal the clock enable signal (DRAM_SDCKE) is asserted | 时钟重新激活满足tCKSRX后,时钟使能信号(DRAM_SDCKE)被断言

• LPMD/DVFS acknowledge (LPACK/DVACK) is deasserted | LPMD/DVFS确认(LPACK/DVACK)被解除

• After satisfying tXS from the assertion of DRAM_SDCKE, a refresh command is driven to the DDR device.
• 从DRAM_SDCKE断言满足tXS后,刷新命令被驱动到DDR设备。

• If ZQ calibration is enabled then tRFC is satisfied from the refresh command and a long ZQ command is driven.
• 如果ZQ校准被启用,则从刷新命令满足tRFC,并驱动长ZQ命令。

• tZQoper idle cycles are counted after the ZQ command.
• ZQ命令后计算tZQoper空闲周期。

• After satisfying tDLLK from the assertion DRAM_SDCKE, the MMDC returns to normal operation.
• 从DRAM_SDCKE断言满足tDLLK后,MMDC返回正常操作。

The figure below shows the timing diagram of the hardware/software handshaking of LPMD/DVFS:
下图显示了LPMD/DVFS硬件/软件握手的时序图:

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/992dc6e3050a7b3e7c1a13bf942bc250f90ebd776f8578611b5b028a747cbd66.jpg)

**Figure 35-4. LPMD/DVFS Hardware/Software Handshaking | 图35-4. LPMD/DVFS硬件/软件握手**

Note for self-refresh:
自刷新注意事项:

• As soon as LPMD or DVFS requests are detected by either hardware or software handshaking, the MMDC will deassert the AXI ARREADY/AWREADY signals immediately to block further requests from the system.
• 一旦硬件或软件握手检测到LPMD或DVFS请求,MMDC将立即解除AXI ARREADY/AWREADY信号以阻止来自系统的进一步请求。

• In case of automatic self-refresh, the internal operating clock will be negated to save power.
• 在自动自刷新的情况下,内部工作时钟将被置反以节省功耗。

### 35.4.7 Reset | 35.4.7 复位

#### 35.4.7.1 Hard reset | 35.4.7.1 硬复位

When hard reset is asserted (aresetn is driven to "0") while warm reset is deasserted (warm_reset is driven to "0"), the entire MMDC will be initialized, including configuration/status registers and state machines.
当硬复位被断言(aresetn被驱动到"0")而暖复位被解除(warm_reset被驱动到"0")时,整个MMDC将被初始化,包括配置/状态寄存器和状态机。

In order to access the DDR device, the MMDC will then have to be reconfigured.
为了访问DDR设备,必须重新配置MMDC。

#### 35.4.7.2 Warm reset | 35.4.7.2 暖复位

The MMDC supports warm reset signal. The warm reset signal must envelop the hard reset signal and then the MMDC will reset all the internal registers. The only registers that are not reset are those that are essential for returning it to normal operation without repeating the initialization sequence and without losing data stored in the memory (configuration/status registers won't be initialized).
MMDC支持暖复位信号。暖复位信号必须包围硬复位信号,然后MMDC将重置所有内部寄存器。唯一不被重置的寄存器是那些对于恢复正常操作而不重复初始化序列和不丢失存储在存储器中的数据必不可少的寄存器(配置/状态寄存器不会被初始化)。

For the successful operation of warm reset, the following steps must be performed:
要成功执行暖复位,必须执行以下步骤:

• The MMDC must enter self-refresh mode. This can be achieved by either LPMD or DFVS requests | MMDC必须进入自刷新模式。这可以通过LPMD或DFVS请求实现

• Wait for LPMD or DVFS acknowledge | 等待LPMD或DVFS确认

• Assert warm reset signal (i.e. drive warm_reset to "1") | 断言暖复位信号(即驱动warm_reset到"1")

• Assert hard reset signal (i.e. drive aresetn to "0") | 断言硬复位信号(即驱动aresetn到"0")

• Deassert hard reset signal | 解除硬复位信号

• Deassert warm reset | 解除暖复位

• Get out of the LPMD/DVFS mode | 退出LPMD/DVFS模式

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/540c8d7db3a3fca3e890853e9fea499f18e4d39ee54b1ef773ed9e7fc6478236.jpg)

**Figure 35-5. Warm Reset Diagram | 图35-5. 暖复位图**

#### 35.4.7.3 Software reset | 35.4.7.3 软件复位

The MMDC supports software reset. When software reset is configured then the MMDC will reset all the internal registers except those that are essential for returning to normal operation without repeating the initialization sequence or without losing data stored in the memory (configuration/status registers won't be initialized).
MMDC支持软件复位。当配置软件复位时,MMDC将重置所有内部寄存器,那些对于恢复正常操作而不重复初始化序列和不丢失存储在存储器中的数据必不可少的寄存器除外(配置/状态寄存器不会被初始化)。

The following steps should be performed for successful operation of software reset:
成功执行软件复位应执行以下步骤:

• The MMDC should enter self-refresh mode. This can be achieved by either LPMD or DFVS request.
• MMDC应进入自刷新模式。这可以通过LPMD或DFVS请求实现。

• Wait for LPMD or DVFS acknowledge | 等待LPMD或DVFS确认

• Assert software reset, by setting MDMISC[RST] | 通过设置MDMISC[RST]来断言软件复位

• Get out of the LPMD/DVFS mode | 退出LPMD/DVFS模式

Normal operation can be resumed.
可以恢复正常操作。

### 35.4.8 Refresh Scheme | 35.4.8 刷新方案

The MMDC supports various automatic refresh options which can be configured via the MDREF register.
MMDC支持多种可通过MDREF寄存器配置的自动刷新选项。

The periodic auto refresh can be triggered by the following clocks:
周期性自动刷新可以通过以下时钟触发:

• 32 kHz clock | 32 kHz时钟
• 64 kHz clock | 64 kHz时钟
• MMDC operating clock | MMDC工作时钟

The refresh scheme of the MMDC is flexible and allows the system to configure the desired AXI accesses delay/latency in each refresh cycle.
MMDC的刷新方案是灵活的,允许系统在每个刷新周期中配置所需的AXI访问延迟/等待时间。

The table below shows an example of four configurations of the refresh cycles that will be handled by the MMDC. Each configuration meets a refresh rate of 3.9μs (tREFI, refresh command every 3.9μs).
下表显示了MMDC将处理的刷新周期的四种配置示例。每种配置都满足3.9μs的刷新率(tREFI,每3.9μs刷新命令)。

**Table 35-8. MMDC Refresh Scheme | 表35-8. MMDC刷新方案**

| Option number | Description | REFR | REF_SEL | REF_CNT | DDR hang time | 选项号 | 描述 | REFR | REF_SEL | REF_CNT | DDR挂起时间 |
|---------------|-------------|------|---------|---------|---------------|--------|------|------|---------|---------|-------------|
| 1 | Issue 8 refresh commands every 31,250 ns | 0x7 (8 refreshes) | 0x0 (64 kHz) | not needed | tRFC x 8 | 1 | 每31,250 ns发出8个刷新命令 | 0x7 (8次刷新) | 0x0 (64 kHz) | 不需要 | tRFC x 8 |
| 2 | Issue 4 refresh commands every 15,625ns | 0x3 (4 refreshes) | 0x1(32 kHz) | not needed | tRFC x 4 | 2 | 每15,625 ns发出4个刷新命令 | 0x3 (4次刷新) | 0x1(32 kHz) | 不需要 | tRFC x 4 |
| 3 | Issue 2 refresh commands every 7800ns | 0x1(2 refreshes) | 0x2 (REF_CNT) | 7800/2.5 = 3120 (0xC30) | tRFC x 2 | 3 | 每7800 ns发出2个刷新命令 | 0x1(2次刷新) | 0x2 (REF_CNT) | 7800/2.5 = 3120 (0xC30) | tRFC x 2 |
| 4 | Issue 1 refresh command every 3900 ns | 0x0 (1 refresh) | 0x2 (REF_CNT) | 3900/2.5 = 1560(0x618) | tRFC | 4 | 每3900 ns发出1个刷新命令 | 0x0 (1次刷新) | 0x2 (REF_CNT) | 3900/2.5 = 1560(0x618) | tRFC |

### 35.4.9 Burst Length options towards DDR | 35.4.9 DDR突发长度选项

The MMDC supports burst lengths which can be configured through MD+CTL[BL] as follows:
MMDC支持可通过MD+CTL[BL]配置的突发长度,如下:

• In DDR3 mode, only burst length 8 can be used.
• 在DDR3模式下,只能使用突发长度8。

• In LPDDR2 mode, only burst length 4 can be used.
• 在LPDDR2模式下,只能使用突发长度4。

In DDR3 mode read/write accesses to the DDR are always 8 words (x16) and aligned in according to JEDEC standards.
在DDR3模式下,对DDR的读/写访问始终为8个字(x16),并按照JEDEC标准对齐。

In case of AXI INCREMENT, accesses that are not aligned the irrelevant data is masked in write accesses and ignored in read accesses. In case of AXI WRAP accesses, even if the access is not aligned, then the MMDC provides an internal optimization mechanism for better efficiency of the DDR data bus.
对于AXI INCREMENT访问,未对齐的无关数据在写访问中被掩码,在读访问中被忽略。对于AXI WRAP访问,即使访问未对齐,MMDC也提供内部优化机制以提高DDR数据总线的效率。

### 35.4.10 Exclusive accesses handling | 35.4.10 独占访问处理

The MMDC contains four exclusive monitors, each for dedicated ID as configured in MAEXIDR0 and MAEXIDR1.
MMDC包含四个独占监视器,每个监视器用于在MAEXIDR0和MAEXIDR1中配置专用ID。

• If legal read exclusive is received by the MMDC, the associated monitor is turned on.
• 如果MMDC接收到合法的读独占,则相关的监视器被打开。

• While the monitor is turned on upon legal write exclusive, the monitor will be turned off and the write will be completed successfully with EXOKAY.
• 当监视器在合法写独占时被打开时,监视器将被关闭,写操作将成功完成并返回EXOKAY。

• The following rules must be met for successful exclusive access:
• 必须满足以下规则才能成功进行独占访问:

• Aligned access (the AXI address is aligned to the AXI size) | 对齐访问(AXI地址对齐到AXI大小)

• AXI single access (AXI burst length isn't greater than 1) | AXI单次访问(AXI突发长度不大于1)

• AXI size of up to 64 bits | AXI大小最高64位

• AXI non-cachable access | AXI非缓存访问

• AXI ID that matches one of the four exclusive IDs | 与四个独占ID之一匹配的AXI ID

Exclusive read behavior (first bullet also correct for non-exclusive accesses):
独占读行为(第一点也适用于非独占访问):

• In case of security violation, the read is blocked and is not sent to DDR. There are two options for response:
• 如果安全违规,读被阻止,不发送到DDR。有两种响应选项:

• If ARCR_SEC_ERR_EN (MAARCR[30]) is high, SLV error is issued towards the Master, otherwise OKAY response is sent to the Master.
• 如果ARCR_SEC_ERR_EN(MAARCR[30])为高,则向主设备发出SLV错误,否则向主设备发送OKAY响应。

• If AXI exclusive rules violation occurs (as described above), the read access is not blocked and is sent to DDR. The data will be fetched and be driven to the master, but the type of response may be unpredicted.
• 如果发生AXI独占规则违规(如上所述),读访问不被阻止并被发送到DDR。数据将被获取并驱动到主设备,但响应类型可能不可预测。

• If none of the above occurs, the read is sent to the DDR. The exclusive monitor will be turned on and the response is EXOKAY.
• 如果以上都不发生,则读访问被发送到DDR。独占监视器将被打开,响应为EXOKAY。

• If additional legal AXI read exclusive is received with the same ID before the AXI exclusive write, the monitor will be updated with the latest attributes.
• 如果在AXI独占写之前收到具有相同ID的其他合法AXI读独占,监视器将使用最新属性更新。

Exclusive write behavior (first bullet also correct for non-exclusive accesses):
独占写行为(第一点也适用于非独占访问):

• In case of security violation, the write is blocked and is not sent to DDR, but the monitor will be kept on. There are two options for response:
• 如果安全违规,写被阻止,不发送到DDR,但监视器将保持打开。有两种响应选项:

• If ARCR_SEC_ERR_EN (MAARCR[30]) is high then SLV error is issued towards the Master, otherwise OKAY response is sent to the Master.
• 如果ARCR_SEC_ERR_EN(MAARCR[30])为高,则向主设备发出SLV错误,否则向主设备发送OKAY响应。

• In case of AXI exclusive rules violation (as described above), the write is blocked and is not sent to DDR. In that case the type of response may be unpredicted.
• 如果发生AXI独占规则违规(如上所述),写被阻止,不发送到DDR。在这种情况下,响应类型可能不可预测。

• In case the exclusive write access has different AXI attributes, but the same ID as the read exclusive access, the write is blocked and is not sent to DDR and the monitor will be turned off. There are two options for response.
• 如果独占写访问具有不同的AXI属性,但与读独占访问具有相同的ID,则写被阻止,不发送到DDR,监视器将被关闭。有两种响应选项。

• If ARCR_EXC_ERR_EN (MAARCR[28]) is high then SLV error is issued towards the Master, otherwise OKAY response is sent to the Master.
• 如果ARCR_EXC_ERR_EN(MAARCR[28])为高,则向主设备发出SLV错误,否则向主设备发送OKAY响应。

• In case of regular (non exclusive) write access is received to the same address or overlapping addresses then the write will be sent to the DDR and the monitor will be turned off.
• 如果收到对相同地址或重叠地址的常规(非独占)写访问,则写操作将被发送到DDR,监视器将被关闭。

• In case of legal write exclusive access is received with the same attributes as the read exclusive access while the monitor is on (no write accesses occured to the same address between the read exclusive and write exclusive), then the write is sent to DDR and the response is EXOKAY. But, if the legal write exclusive is received while the monitor is off, the write is blocked and there are two options for response.
• 如果在监视器打开时收到具有与读独占访问相同属性的合法写独占访问(在读独占和写独占之间没有发生对相同地址的写访问),则写操作被发送到DDR,响应为EXOKAY。但是,如果在监视器关闭时收到合法的写独占访问,则写操作被阻止,有两种响应选项。

• If ARCR_EXC_ERR_EN (MAARCR[28]) is high then SLV error is issued towards the Master, otherwise OKAY response is sent to the Master.
• 如果ARCR_EXC_ERR_EN(MAARCR[28])为高,则向主设备发出SLV错误,否则向主设备发送OKAY响应。

### 35.4.11 AXI Error Handling | 35.4.11 AXI错误处理

The MMDC supports the AXI responses listed here.
MMDC支持列出的AXI响应。

• In case of AXI exclusive violation there are two options for response:
• 如果AXI独占违规,有两种响应选项:

• If MAARCR[28] is high then SLV Error is issued towards the Master, Otherwise OKAY response is sent to the Master.
• 如果MAARCR[28]为高,则向主设备发出SLV错误,否则向主设备发送OKAY响应。

> **NOTE | 注** In case of read error MMDC drives zeros on the read data bus.
> 如果读错误,MMDC在读数据总线上驱动零。

---
*End of Chapter 35.1-35.4 Translation | 第35.1-35.4章翻译结束*