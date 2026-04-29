# 第35章 多模式DDR控制器 (MMDC)

# 35.1 概述

MMDC 是一种多模式 DDR 控制器，支持 DDR3/DDR3L x16 和 LPDDR2 x16 存储器类型。MMDC 具有可配置、高性能和优化的特点。下图展示了 MMDC 的框图。

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/38b044e75ed1b59d806a215d31c9ae0ade0dbf737840b05492e7c8cf9170bdb3.jpg)

Figure 35-1. MMDC 框图

MMDC 包含一个内核（MMDC_CORE）和一个 PHY（MMDC_PHY）。

i.MX 6ULL 应用处理器参考手册，Rev. 1，11/2017

# 概述

• 内核负责通过 AXI 接口与系统通信、DDR 命令生成、DDR 命令优化以及读/写数据通路。

• PHY 负责时序调整；它使用特殊的校准机制来确保在高达 400 MHz 的时钟频率下的数据捕获裕量。

MMDC 的内部存储器映射（配置寄存器）可通过 IP 通道（IP0）进行配置。

# 35.1.1 MMDC 特性汇总

下表汇总了 MMDC 的特性。

Table 35-1. MMDC 特性汇总

<table><tr><td>特性</td><td>详情</td></tr><tr><td>DDR 标准</td><td>• DDR3L, DDR3 x16
• LPDDR2 x16
• 不支持 LPDDR1、MDDR 或 DDR2</td></tr><tr><td>DDR 接口</td><td>• x16 数据总线宽度
• 每个 DDR 器件密度为 256 Mbits-8 Gbits，支持以下列和行组合：
• 列地址大小为 8-12 位
• 行地址大小为 11-16 位
• 两个片选（DDR3/DDR3L、LPDDR2 使用一个片选）
• 最大 4 Gbytes 地址空间，可在 CS0 和 CS1 之间可配置分区（对于 LPDDR2 2ch x32，每个通道最大 2 Gbytes）
• 支持 DDR3 的突发长度为 8（对齐）
• 支持 LPDDR2 的突发长度为 4</td></tr><tr><td>DDR 性能</td><td>• MMDC 最高运行在 400 MHz（800MT/s），实际支持的时钟频率请参见 CCM 模块。
• 通过来自芯片的 QoS 旁带优先级信号支持实时优先级，可在重排序机制中实现多种优先级等级：实时、延迟敏感、普通优先级。
• 页命中/页未命中优化
• 连续读/写访问优化
• 支持深度读和写请求队列以实现 Bank 预测。
• 从 DDR 器件接收到关键字后立即驱动回读事务（无需等待整个数据阶段完成）。
• 持续跟踪打开的内存页面
• 支持 Bank 交错
• 在 DDR3 模式下（突发长度 8）针对非对齐回卷访问的特殊优化
注意：由于重排序和优化机制（基于不同的 AXI 标识符（ID）），发往 DDR 器件的事务可能以与 AXI 主设备接收时不同的 ID 顺序被驱动。类似地，写响应、读响应或读数据也可能以不同的 ID 顺序被驱动回 AXI 主设备。</td></tr><tr><td>AXI 接口</td><td>• 符合 AXI 总线规范
• 支持 8、16、64 位总线传输（单次访问和突发），运行频率为 400 MHz。</td></tr><tr><td></td><td>支持最大 16 的 AXI 突发长度支持 WRAP、INCR 和 FIXED 突发类型支持 16 位 AXI ID写数据交错深度为 1（不支持写数据交错）支持先写数据后地址支持缓冲/非缓冲访问（AWCACHED[0] = 0b 表示不可缓冲访问，AWCACHED[0] = 1b 表示可缓冲访问）。其余 Cache 选项不支持为保持同一主设备读写访问之间的数据一致性，响应信号按以下方式发送：可缓冲写访问 — 当访问的最后数据进入 MMDC 时发送 BRESP。不可缓冲写访问 — 当数据被物理写入外部存储器器件时发送 BRESP。支持每个可配置 ID 最多四个独占监视器，仅用于最大 64 位的单次访问支持以下 AXI 响应：Okay — 访问成功或独占访问失败Slave error — 安全性违规Exclusive okay — 独占访问的读或写部分成功</td></tr><tr><td>DDR 校准和延迟线。</td><td>支持多种校准过程，可自动（硬件）或手动（软件）对 CS0 或 CS1 执行。（过程结束时，延迟线将使用一组结果工作。）支持以下校准过程：外部 DDR 器件的 ZQ 校准（DDR3 通过 ZQ 校准命令，LPDDR2 通过 MRW 命令）可自动处理 ZQ Short（周期性的）和 ZQ Long（退出自刷新时）可手动处理 ZQ INIT用于校准 DDR 驱动强度的 DDR I/O 焊盘 ZQ 校准序列可由硬件自动处理序列可由软件逐步手动处理读数据校准。调整读 DQS 与读数据字节。仅适用于 DDR3 的读 DQS 门控校准。调整 DQS 门控与读前导码窗口。写数据校准。调整写 DQS 与写数据字节。写电平校准。调整写 DQS 与 CK（DDR 差分时钟）。读微调。每个读数据位最多调整 7 个延迟线单元。写微调。每个读数据位最多调整 3 个延迟线单元。周期性延迟线测量以在刷新间隔内保持其精度。额外的微调延迟线用于调整 DDR 时钟延迟、DDR 时钟占空比、DQS 占空比。</td></tr><tr><td>省电</td><td>支持通过硬件和软件与系统协商（请求/应答握手）实现动态电压、频率变化和自刷新模式进入在硬件或软件自刷新请求断言后，进一步 AXI 请求将被阻塞（甚至在应答断言之前）。在自刷新模式下，系统可以取消断言 MMDC 的工作时钟以节省功耗。在自刷新模式下，驱动到 DDR 器件的时钟（CK）将被门控以节省功耗。支持自动自刷新和电源下关进入与退出在自动自刷新中，内部工作时钟将被门控以节省功耗。</td></tr><tr><td></td><td>支持 DDR3 的快速和慢速预充电电源关每个片选的自动激活和预充电电源关定时器（一个片选可以进入电源关而另一个仍在工作）当 CS（片选）处于非活动状态（高电平）时，命令和地址总线不切换以节省功耗。</td></tr><tr><td>DDR 通用</td><td>可配置的时序参数可配置的刷新方案页边界跨跃支持自动生成预充电命令并激活下一行支持多种 ODT 控制方案每个读或写访问以及活动或非活动 CS（片选）的 ODT 控制断言或取消断言支持 LPDDR2 的 MRW 和 MRR 命令在 LPDDR2 模式下软件控制切换到降额时序参数和/或根据温度传感器更新刷新率调试和分析能力</td></tr></table>

# 35.2 外部信号

下表描述了 MMDC 的外部信号。

Table 35-2. MMDC 外部信号

<table><tr><td>信号</td><td>描述</td><td>焊盘</td><td>模式</td><td>方向</td></tr><tr><td>DRAM_ADDR[15:0]</td><td>地址总线信号</td><td>DRAM_A[15:0]</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_CAS</td><td>列地址选通信号</td><td>DRAM_CAS</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_CS[1:0]</td><td>片选信号</td><td>DRAM_CS[1:0]</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_DATA[31:0]</td><td>数据总线信号</td><td>DRAM_D[31:0]</td><td>无复用</td><td>I/O</td></tr><tr><td>DRAM_DQM[1:0]</td><td>数据掩码信号</td><td>DRAM_DQM[1:0]</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_ODT[1:0]</td><td>片上端接信号</td><td>DRAM_SDODT[1:0]</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_RAS</td><td>行地址选通信号</td><td>DRAM_RAS</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_RESET</td><td>复位信号</td><td>DRAM_RESET</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_SDBA[2:0]</td><td>Bank 选择信号</td><td>DRAM_SDBA[2:0]</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_SDCKE[1:0]</td><td>时钟使能信号</td><td>DRAM_SDCKE[1:0]</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_SDCLK0_N</td><td>负时钟信号</td><td>DRAM_SDCLK_1:0]</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_SDCLK0_P</td><td>正时钟信号</td><td>DRAM_SDCLK_1:0]</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_SDQS[1:0]_N</td><td>负 DQS 信号</td><td>DRAM_SDQS[1:0]_N</td><td>无复用</td><td>I/O</td></tr><tr><td>DRAM_SDQS[1:0]_P</td><td>正 DQS 信号</td><td>DRAM_SDQS[1:0]_P</td><td>无复用</td><td>I/O</td></tr><tr><td>DRAM_SDWE</td><td>写使能信号</td><td>DRAM_SDWE</td><td>无复用</td><td>O</td></tr><tr><td>DRAM_ZQPAD</td><td>ZQ 信号</td><td>DRAM_ZQPAD</td><td>无复用</td><td>O</td></tr></table>

# 35.3 时钟

下表描述了 MMDC 的时钟源。

有关时钟设置、配置和门控信息，请参见时钟控制器模块（CCM）。

# 注意

术语"时钟"和"周期"可互换使用，均指主 DDR 时钟（mmdc_axi_clk_root）的时钟周期，通常称为 DDR 频率。

Table 35-3. MMDC 时钟

<table><tr><td>时钟名称</td><td>时钟根</td><td>描述</td></tr><tr><td>aclk_fast_core_p0</td><td>mmdc_axi_clk_root</td><td>快速时钟（通道 1）</td></tr><tr><td>ipg_clk_p0</td><td>ipg_clk_root</td><td>外设时钟（通道 1）</td></tr><tr><td>aclk_fast_phy_p0</td><td>mmdc_axi_clk_root</td><td>快速时钟（通道 1 - PHY）</td></tr></table>

# 35.4 功能描述

本节提供该模块的完整功能描述。

# 35.4.1 写/读数据流

# 35.4.1.1 写数据流

1. 写请求被接收进一个 8 深的请求 FIFO。仅当至少有两个可用条目时才会接收访问。每个条目保存所有 AXI 属性。

• 如果突发长度大于 8，访问将拆分为两次访问：一次突发长度为 8，另一次为剩余部分。

• 访问可以在相关写请求的整个数据阶段完成（所有数据节拍已接收）后立即执行。

2. 在待处理的读和写访问之间执行简单的轮询仲裁，并将此阶段的胜出访问指针发送到重排序缓冲器。

3. 激活重排序机制以查找胜出访问 — 即根据动态得分最能充分利用 DDR 总线的访问。更多信息请参见动态评分模式（仲裁获胜条件）。

4. 上一阶段的胜出写访问被接收并保持，等待分派到 DDR 逻辑。

5. 当 DDR 命令控制单元准备好接受写请求时，根据 Bank 模型的状态和定时器参数，向 DDR 器件发出（如果需要）预充电/激活命令。

6. DDR 逻辑通过 DDR PHY 将相关数据驱动到 DDR 器件。

# 35.4.1.2 读数据流

1. 如果 MMDC 中至少有两个可用条目，读请求被接收进一个 16 深的请求 FIFO。每个条目保存所有 AXI 属性。

# 注意

如果突发长度大于 8，访问将拆分为 2 次访问（一次突发长度为 8，另一次为剩余部分）。

2. 在待处理的读和写访问之间执行简单的轮询仲裁，并将此阶段的胜出访问指针发送到重排序缓冲器。

3. 激活重排序机制以查找胜出访问 — 即根据动态得分最能充分利用 DDR 总线的访问。更多信息请参见动态评分模式（仲裁获胜条件）。

4. 上一阶段的胜出读访问被采样并保持，等待分派到 DDR 逻辑。当读数据缓冲器中至少有一个空闲槽位用于存储数据时，该读访问将被分派。

5. 当 DDR 命令控制单元准备好接受读请求时，根据 Bank 模型的状态和定时器参数，向 DDR 器件发出（如果需要）预充电/激活命令。

6. MMDC PHY 采样读数据，DDR 逻辑将数据传输到读数据缓冲器中的相应槽位。

7. MMDC 将数据传回主设备。

# 35.4.2 MMDC 初始化

由于芯片退出复位时 MMDC 处于禁用状态，因此没有时钟驱动到 DDR 器件，整个面向 DDR 器件的接口处于非活动状态。需要以下步骤来正确激活 MMDC。

# 注意

为保证 DRAM_RESET 和 DRAM_SDCKE 信号在芯片上电和复位序列期间保持低电平（根据 JEDEC 定义），必须将这些信号连接到下拉电阻。

1. 设置 MDSCR[CON_REQ]，即设置配置请求；注意，由于 MMDC 被禁用，无需轮询 MDSCR[CON_ACK] 上的配置应答位。

2. 在 MDCFG0、MDCFG1、MDOTC 和 MDCFG2 寄存器中配置所需的时序参数。

3. 在 MDMISC 寄存器中配置 DDR 类型和其他杂项参数。

4. 在 MDOR 寄存器中配置退出复位所需的延迟。

5. 在 MDCTL 寄存器中配置 DDR 物理参数（密度和突发长度）。

6. 执行 MMDC 模块的 ZQ 校准，以正确初始化驱动强度。

7. 在 MDCTL[SDE_0]（片选 0）和 MDCTL[SDE_1]（片选 1）上使能所需的片选来启用 MMDC。此时，MMDC 启动与 DRAM_RESET/DRAM_SDCKE 相关的复位和初始化序列，按 JEDEC 定义。

8. 通过发出 MRS/MRW 命令（用于 ZQ、ODT、PRE 等）完成 JEDEC 定义的初始化序列。要发出这些命令，请在 MDSCR 寄存器中配置相应的命令和地址。

9. 通过在 MDSCR 寄存器中配置相应的命令和地址来编程 DDR 模式寄存器。

10. 在 MDPDC 和 MAPSR 寄存器中配置电源关和自刷新进入与退出参数。

11. 在 MPZQHWCTRL 和 MPZQLP2CTL 寄存器中配置 ZQ 方案。

12. 在 MDREF 寄存器中配置并激活周期性刷新方案。

13. 通过清除 MDSCR[CON_REQ] 取消配置请求。

# 注意

步骤 1 到 6 是非阻塞的，可以按任意顺序执行。

完成这些步骤后，MMDC 即可开始工作并处理 AXI 访问。

# 注意

为获得更好的时序和精度，建议用户通过运行自动或手动校准过程来配置 MMDC PHY 延迟参数。在开始任何校准过程之前，必须先禁用周期性刷新方案（MDREF[REF_SEL] $= 1 1$），然后通过将 MDSCR[CMD] 配置为 2h 来发出手动刷新命令。更多信息，请参见校准过程。

# 35.4.3 配置 MMDC 寄存器

为安全修改 MMDC 的内部配置寄存器，必须将 MMDC 置于配置模式。

使用以下步骤进入配置模式。

1. 通过设置 MDSCR[CON_REQ] 发出配置请求。

2. 轮询配置应答，直到 MDSCR[CON_ACK] 被置位。

此时，MMDC 进入配置模式，允许访问 MMDC 寄存器。

# 注意

在配置模式下，MMDC 阻止进一步的 AXI 访问被确认。

取消断言 MDSCR[CON_REQ] 后，MMDC 退出配置模式，AXI 访问开始被处理。

# 35.4.4 MMDC 地址空间

# 35.4.4.1 地址解码

MMDC 支持最多两个连续的片选，每个片选具有相同的密度。

可以通过 MDASP[CS0_END] 选择性地配置片选之间的分区。

输入的 AXI 地址总线为 32 位。MMDC 按如下方式解码每个访问：

1. 片选
2. Bank 号
3. 行号
4. 列号

MMDC 中的以下寄存器定义了 DDR 地址空间：

• MDMISC[DDR_4_BANK] — 定义 DDR 器件中的 Bank 数为 4 或 8
• MDCTL[DSIZ] — 定义 DDR 数据总线宽度为 x16
• MDMISC[BI] — 定义 Bank 交错是开启还是关闭
• MDCTL[COL] — 定义 DDR 器件的列大小
• MDCTL[ROW] — 定义 DDR 器件的行大小

以下表格展示了在 Bank 交错开启和关闭时，x16 位 DDR 器件的地址解码示例。假设配置如下：8 个 Bank（3 位），行分配 15 位，列分配 10 位。总密度为 256 MWords（x16 位时为 512 Mbytes）。

# 注意

片选通过将 7 个最高有效地址位（ARADDR[31:25]/AWADDR[31:25]）与 MDASP[CS0_END] 进行比较来完成。

Table 35-4. 地址解码 — Bank 交错关闭

<table><tr><td>AXI 地址</td><td>x16 DDR</td><td>x32 DDR</td></tr><tr><td>A29</td><td>—</td><td>BANK[2]</td></tr><tr><td>A28</td><td>BANK[2]</td><td>BANK[1]</td></tr><tr><td>A27</td><td>BANK[1]</td><td>BANK[0]</td></tr><tr><td>A26</td><td>BANK[0]</td><td>ROW[14]</td></tr><tr><td>A25</td><td>ROW[14]</td><td>ROW[13]</td></tr><tr><td>A24</td><td>ROW[13]</td><td>ROW[12]</td></tr><tr><td>A23</td><td>ROW[12]</td><td>ROW[11]</td></tr><tr><td>A22</td><td>ROW[11]</td><td>ROW[10]</td></tr><tr><td>A21</td><td>ROW[10]</td><td>ROW[9]</td></tr><tr><td>A20</td><td>ROW[9]</td><td>ROW[8]</td></tr><tr><td>A19</td><td>ROW[8]</td><td>ROW[7]</td></tr><tr><td>A18</td><td>ROW[7]</td><td>ROW[6]</td></tr><tr><td>A17</td><td>ROW[6]</td><td>ROW[5]</td></tr><tr><td>A16</td><td>ROW[5]</td><td>ROW[4]</td></tr><tr><td>A15</td><td>ROW[4]</td><td>ROW[3]</td></tr><tr><td>A14</td><td>ROW[3]</td><td>ROW[2]</td></tr><tr><td>A13</td><td>ROW[2]</td><td>ROW[1]</td></tr><tr><td>A12</td><td>ROW[1]</td><td>ROW[0]</td></tr><tr><td>A11</td><td>ROW[0]</td><td>COL[9]</td></tr><tr><td>A10</td><td>COL[9]</td><td>COL[8]</td></tr><tr><td>A9</td><td>COL[8]</td><td>COL[7]</td></tr><tr><td>A8</td><td>COL[7]</td><td>COL[6]</td></tr><tr><td>A7</td><td>COL[6]</td><td>COL[5]</td></tr><tr><td>A6</td><td>COL[5]</td><td>COL[4]</td></tr><tr><td>A5</td><td>COL[4]</td><td>COL[3]</td></tr><tr><td>A4</td><td>COL[3]</td><td>COL[2]</td></tr><tr><td>A3</td><td>COL[2]</td><td>COL[1]</td></tr><tr><td>A2</td><td>COL[1]</td><td>COL[0]</td></tr><tr><td>A1</td><td>COL[0]</td><td>—</td></tr><tr><td>A0</td><td>—</td><td>—</td></tr></table>

Table 35-5. 地址解码 — Bank 交错开启

<table><tr><td>AXI 地址</td><td>x16 DDR</td><td>x32 DDR</td></tr><tr><td>A29</td><td>—</td><td>ROW[14]</td></tr><tr><td>A28</td><td>ROW[14]</td><td>ROW[13]</td></tr><tr><td>A27</td><td>ROW[13]</td><td>ROW[12]</td></tr><tr><td>A26</td><td>ROW[12]</td><td>ROW[11]</td></tr><tr><td>A25</td><td>ROW[11]</td><td>ROW[10]</td></tr><tr><td>A24</td><td>ROW[10]</td><td>ROW[9]</td></tr><tr><td>A23</td><td>ROW[9]</td><td>ROW[8]</td></tr><tr><td>A22</td><td>ROW[8]</td><td>ROW[7]</td></tr><tr><td>A21</td><td>ROW[7]</td><td>ROW[6]</td></tr><tr><td>A20</td><td>ROW[6]</td><td>ROW[5]</td></tr><tr><td>A19</td><td>ROW[5]</td><td>ROW[4]</td></tr><tr><td>A18</td><td>ROW[4]</td><td>ROW[3]</td></tr><tr><td>A17</td><td>ROW[3]</td><td>ROW[2]</td></tr><tr><td>A16</td><td>ROW[2]</td><td>ROW[1]</td></tr><tr><td>A15</td><td>ROW[1]</td><td>ROW[0]</td></tr><tr><td>A14</td><td>ROW[0]</td><td>BANK[2]</td></tr><tr><td>A13</td><td>BANK[2]</td><td>BANK[1]</td></tr><tr><td>A12</td><td>BANK[1]</td><td>BANK[0]</td></tr><tr><td>A11</td><td>BANK[0]</td><td>COL[9]</td></tr><tr><td>A10</td><td>COL[9]</td><td>COL[8]</td></tr><tr><td>A9</td><td>COL[8]</td><td>COL[7]</td></tr><tr><td>A8</td><td>COL[7]</td><td>COL[6]</td></tr><tr><td>A7</td><td>COL[6]</td><td>COL[5]</td></tr><tr><td>A6</td><td>COL[5]</td><td>COL[4]</td></tr><tr><td>A5</td><td>COL[4]</td><td>COL[3]</td></tr><tr><td>A4</td><td>COL[3]</td><td>COL[2]</td></tr><tr><td>A3</td><td>COL[2]</td><td>COL[1]</td></tr><tr><td>A2</td><td>COL[1]</td><td>COL[0]</td></tr><tr><td>A1</td><td>COL[0]</td><td>—</td></tr><tr><td>A0</td><td>—</td><td>—</td></tr></table>

# 注意

如果访问未初始化或未连接的片选，行为可能不可预期。

# 35.4.4.2 片选设置

MMDC 通过将 7 个最高有效地址位（ARADDR[31:25]/AWADDR[31:25]）与 MDASP[CS0_END] 进行比较，将输入的访问驱动到 CS0 或 CS1。

通常，每个片选的总密度必须为 2 的幂，且每个片选的总密度必须相同。

使用 2 Gbyte CS 密度创建 4 Gbyte 地址空间 和 使用 1 Gbyte CS 密度创建 2 Gbyte 地址空间 展示了如何创建连续地址空间并相应配置 MMDC。

# 35.4.4.2.1 使用 2 Gbyte CS 密度创建 4 Gbyte 地址空间

如果 DDR 内存空间分配为 4 Gbytes，则只允许一种片选分区配置。寄存器 MDASP[CS0_END] 应设置为 2 Gbytes 分区（16Gb）。

下图显示了相应的内存空间。

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/63ce86576320fd9875718188a22c1645e2ac0a67a8fcd25c160aad1b76e98ec3.jpg)

Figure 35-2. 片选分区 — 每个片选 2 Gbytes

# 35.4.4.2.2 使用 1 Gbyte CS 密度创建 2 Gbyte 地址空间

如果 DDR 内存空间分配为 2 Gbytes，有三种配置片选分区的选项：MDASP[CS0_END] 设置为 001_1111（1 Gbyte）、MDASP[CS0_END] 设置为 011_1111（2 Gbytes）和 MDASP[CS0_END] 设置为 101_1111（3 Gbytes）。

如果 DDR 内存空间分配为 2 Gbytes，有三种配置片选分区的选项：

• MDASP[CS0_END] 设置为 001_1111（1 Gbyte）
• MDASP[CS0_END] 设置为 011_1111（2 Gbytes）
• MDASP[CS0_END] 设置为 101_1111（3 Gbytes）

下图显示了相应的内存空间：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/e355b01792121d2ba52900d3754bb248ea1e7ca344aebe6f412b70f1fd524074.jpg)

Figure 35-3. 片选分区 — 每个片选 1 Gbyte

# 35.4.4.3 AXI 访问到 DDR 访问的转换

# 35.4.4.3.1 示例 1

假设 AXI 读访问具有以下属性：

• 回卷（arburst $[ 1 { : } 0 ] = 1 0 \mathrm { b }$）
• AXI 大小为 128 位（arsize $[ 2 ; 0 ] = 1 0 0 0$）
• AXI 长度为 8（arlen[3:0] = 0111b）
• AXI 地址后缀为 B0h（未对齐到 AXI 回卷边界，该边界为 $1 6 \mathbf { B } \mathbf { x } 8 = 1 2 8 \mathbf { B } = 0 \mathbf { x } 8 0$）

面向具有以下属性的 DDR3（MDMISC[DDR_TYPE] = 00b）：

• x32（MDCTL[DSIZ] = 01b）
• 突发长度为 8（MDCTL[BL] = 1b）

在此情况下，AXI 回卷边界为每 16Bx8=128B（0x80），DDR 回卷边界为每 $4 \mathbf { B } \mathbf { x } 8 { = } 3 2 \mathbf { B } ( 0 \mathbf { x } 2 0 )$。

主设备期望获取与以下地址相关联的数据：0xB0、0xC0、0xD0、0xE0、0xF0、0x80、0x90、0xA0。

与后缀 0xB0 对齐的第一个 AXI 地址是后缀为 $0 \mathrm { { x } 8 0 }$ 的地址，最后一个回卷 AXI 地址是后缀为 0xFF 的地址。由于 AXI 主设备期望从后缀为 0xB0 的 AXI 地址获取第一个数据，MMDC 向 DDR 发出以下访问：

• 对后缀为 0xA0 的逻辑地址进行读访问（DDR 边界为 $0 \times 2 0$，0xA0 最接近 0xB0）

# 注意

逻辑地址是列地址归一化到 1 字节的地址。

• 对后缀为 0xC0 的逻辑地址进行读访问
• 对后缀为 0xE0 的逻辑地址进行读访问
• 对后缀为 0x80 的逻辑地址进行读访问

MMDC 将 AXI 访问分解为四次 DDR 访问，并首先将与地址 0xB0 关联的读数据返回给主设备。从地址 0xA0 获取的读数据存储在内部缓冲器中，最后再驱动回主设备。

# 35.4.4.3.2 示例 2

假设 AXI 写访问具有以下属性：

• 递增（awburst[1:0]=2'b01）
• AXI 大小为 64 位（awsize[2:0]=3'b011）
• AXI 长度为 8（awlen[3:0]=4'b0111）
• AXI 地址后缀为 0xB0（对齐，因为递增大小为 8B）

面向具有以下属性的 DDR3（MDMISC[DDR_TYPE]=2'b00）：

• x64（MDCTL[DSIZ]=2'b10）
• 突发长度为 8（MDCTL[BL]=1'b1）

在此情况下，AXI 对齐为每 8B，DDR 边界为每 $8 \mathrm { B x } 8 { = } 6 4 \mathrm { B } ( 0 \mathrm { x } 4 0 )$。

主设备期望将数据写入以下地址：0xB0、0xB8、0xC0、0xC8、0xD0、0xD8、0xE0、0xE8。

MMDC 将向 DDR 发出以下访问：

• 对后缀为 0x80 的逻辑地址进行写访问（DDR 边界为 0x40，$0 \mathrm { { x } 8 0 }$ 最接近 0xB0），同时地址 $0 \times 8 0$ 到 0xAF 被 DM（数据掩码信号）屏蔽。

# 注意

逻辑地址是列地址归一化到 1 字节的地址。

• 对后缀为 0xC0 的逻辑地址进行写访问，同时地址 0xF0 到 0xFF 被 DM（数据掩码信号）屏蔽。

MMDC 将 AXI 访问分解为两次 DDR 访问。

# 35.4.4.3.3 示例 3

假设 AXI 写访问具有以下属性：

• 回卷（awburst[1:0]=2'b10）
• AXI 大小为 128 位（awsize[2:0] $=$ 3'b100）
• AXI 长度为 4（awlen[3:0]=4'b0011）
• AXI 地址后缀为 0x80（对齐）

面向具有以下属性的 DDR3（MDMISC[DDR_TYPE]=2'b00）：

• x64（MDCTL[DSIZ]=2'b10）
• 突发长度为 8（MDCTL[BL]=1'b1）

在此情况下，AXI 回卷边界为每 16Bx4=64B（0x40），DDR 回卷边界为每 $8 \mathrm { x } 8 { = } 6 4 \mathrm { B } ( 0 \mathrm { x } 4 0 )$。

主设备期望将数据写入以下地址：0x80、0x90、0xA0、0xB0。

由于 AXI 回卷边界和 DDR 回卷边界相同，且起始 AXI 地址已对齐，MMDC 将只向 DDR 发出一次访问，如下所示：

• 对后缀为 0x80 的逻辑地址进行写访问

# 注意

逻辑地址是列地址归一化到 1 字节的地址。

# 35.4.4.3.4 示例 4

假设 AXI 写访问具有以下属性：

• 递增（awburst[1:0]=2'b01）
• AXI 大小为 64 位（awsize[2:0]=3'b011）
• AXI 长度为 2（awlen[3:0]=4'b0001）
• AXI 地址后缀为 0x5（未对齐）

面向具有以下属性的 DDR3（MDMISC[DDR_TYPE]=2'b00）：

• x32（MDCTL[DSIZ]=2'b10）
• 突发长度为 8（MDCTL[BL]=1'b1）

在此情况下，AXI 对齐为每 8B（0x8），DDR 边界为每 $4 \mathbf { B } \mathbf { x } 8 { = } 3 2 \mathbf { B } ( 0 \mathbf { x } 2 0 )$。

主设备期望将数据写入以下地址：0x5（WSTRB=0xE0）、0x8（到 0xF）。

MMDC 将向 DDR 发出一次访问，如下所示：

对后缀为 0x0 的逻辑地址进行写访问（DDR 边界为 $0 \times 2 0$，$0 \mathrm { x 0 }$ 最接近 0x0），同时地址 0x0 到 0x4 被 DM（数据掩码信号）屏蔽，地址 0x10 到 0x1F 也被 DM 屏蔽。

# 35.4.4.3.5 示例 5

假设 AXI 写访问具有以下属性：

• 递增（awburst[1:0]=2'b01）
• AXI 大小为 64 位（awsize[2:0]=3'b011）
• AXI 长度为 7（awlen[3:0]=4'b0001）
• AXI 地址后缀为 0x10（对齐）

面向具有以下属性的 DDR3（MDMISC[DDR_TYPE]=2'b00）：

• x64（MDCTL[DSIZ]=2'b10）
• 突发长度为 8（MDCTL[BL]=1'b1）

在此情况下，AXI 对齐为每 8B（0x8），DDR 边界为每 $8 \mathrm { B x } 8 { = } 6 4 \mathrm { B } ( 0 \mathrm { x } 4 0 )$。

主设备期望将数据写入以下地址：0x10、0x18、0x20、0x28、0x30、0x38、0x40、0x48。

由于 AXI 访问未对齐到 DDR 边界（每 0x40），MMDC 将向 DDR 发出两次访问，如下所示：

• 对后缀为 0x0 的逻辑地址进行写访问，同时地址 0x0 到 0xF 被 DM（数据掩码信号）屏蔽。

# 注意

逻辑地址是列地址归一化到 1 字节的地址。

• 对后缀为 0x40 的逻辑地址进行写访问，同时地址 0x50 到 0x7F 被 DM（数据掩码信号）屏蔽。

# 35.4.4.4 地址镜像

使能此功能时，地址位 DRAM_A3、DRAM_A4、DRAM_A5、DRAM_A6、DRAM_A7、DRAM_A8、DRAM_SDBA0 和 DRAM_SDBA1 根据相关联的片选表现出不同的行为。

此功能便于片选 1 上器件的 PCB 板级布线，这些器件通常位于 PCB 上与片选 0 器件相对的一侧。

# 注意

DDR3 不支持此功能，因为 DDR3 仅支持单个片选。

下表指定了地址镜像选项：

Table 35-6. 地址镜像选项

<table><tr><td>MMDC 引脚</td><td>片选 0 引脚</td><td>片选 1 引脚</td></tr><tr><td>DRAM_A3</td><td>DRAM_A3</td><td>DRAM_A4</td></tr><tr><td>DRAM_A4</td><td>DRAM_A4</td><td>DRAM_A3</td></tr><tr><td>DRAM_A5</td><td>DRAM_A5</td><td>DRAM_A6</td></tr><tr><td>DRAM_A6</td><td>DRAM_A6</td><td>DRAM_A5</td></tr><tr><td>DRAM_A7</td><td>DRAM_A7</td><td>DRAM_A8</td></tr><tr><td>DRAM_A8</td><td>DRAM_A8</td><td>DRAM_A7</td></tr><tr><td>DRAM_SDBA0</td><td>DRAM_SDBA0</td><td>DRAM_SDBA1</td></tr><tr><td>DRAM_SDBA1</td><td>DRAM_SDBA1</td><td>DRAM_SDBA0</td></tr></table>

# 35.4.5 LPDDR2 和 DDR3 引脚复用映射

下表显示了 LPDDR2 和 DDR3 之间的引脚复用映射。i.MX DDR I/O 焊盘符合 DDR3 标准。

• 在 DDR3 中，所有 DRAM_DATA、DRAM_SDQS 和 DRAM_DQM 数据线都在通道 0 上工作。
• 在 LPDDR2 中，DRAM_DDQS[3:0]、DRAM_DATA[31:0] 和 DRAM_DQM[3:0] 在通道 0 上工作。DRAM_SDQS[7:4]、DRAM_DATA[63:32] 和 DRAM_DQM[7:4] 在通道 1 上工作。

Table 35-7. LPDDR2 和 DRAM 引脚复用映射

<table><tr><td>DRAM I/O 焊盘</td><td>LPDDR2 I/O 焊盘</td></tr><tr><td>DRAM_ADDR00</td><td>LPDDR2_CA0</td></tr><tr><td>DRAM_ADDR01</td><td>LPDDR2_CA1</td></tr><tr><td>DRAM_ADDR02</td><td>LPDDR2_CA2</td></tr><tr><td>DRAM_ADDR03</td><td>LPDDR2_CA3</td></tr><tr><td>DRAM_ADDR04</td><td>LPDDR2_CA4</td></tr><tr><td>DRAM_ADDR05</td><td>LPDDR2_CA5</td></tr><tr><td>DRAM_ADDR06</td><td>LPDDR2_CA6</td></tr><tr><td>DRAM_ADDR07</td><td>LPDDR2_CA7</td></tr><tr><td>DRAM_ADDR08</td><td>LPDDR2_CA8</td></tr><tr><td>DRAM_ADDR09</td><td>LPDDR2_CA9</td></tr><tr><td>DRAM_ADDR10</td><td>—</td></tr><tr><td>DRAM_ADDR11</td><td>—</td></tr><tr><td>DRAM_ADDR12</td><td>—</td></tr><tr><td>DRAM_ADDR13</td><td>—</td></tr><tr><td>DRAM_ADDR14</td><td>—</td></tr><tr><td>DRAM_ADDR15</td><td>—</td></tr><tr><td>DRAM_CAS_B</td><td>—</td></tr><tr><td>DRAM_RAS_B</td><td>—</td></tr><tr><td>DRAM_WE_B</td><td>—</td></tr><tr><td>DRAM_SDCKE0</td><td>LPDDR2_CKE0</td></tr><tr><td>DRAM_SDCKE1</td><td>LPDDR2_CKE1</td></tr><tr><td>DRAM_CS_B0</td><td>LPDDR2_CS_B0</td></tr><tr><td>DRAM_CS_B1</td><td>LPDDR2_CS_B1</td></tr><tr><td>DRAM_ODT0</td><td>LPDDR2_ODT0</td></tr><tr><td>DRAM_ODT1</td><td>LPDDR2_ODT1</td></tr><tr><td>DRAM_SDCLK0_P</td><td>LPDDR2_CK0</td></tr><tr><td>DRAM_SDCLK1</td><td>LPDDR2_CK1</td></tr><tr><td>DRAM_BA0</td><td>—</td></tr><tr><td>DRAM_BA1</td><td>—</td></tr><tr><td>DRAM_BA2</td><td>—</td></tr></table>

# 35.4.6 省电和时钟频率变化模式

# 35.4.6.1 省电概述

MMDC 支持多种 DDR 省电模式。

# 注意

在默认情况下，省电模式是禁用的。这些模式可以显著降低 DDR 存储器的功耗。

1. 整个 DDR 器件（片选 0 和 1）的自刷新进入可通过两种机制激活：

• LPMD（低功耗模式）
• 与系统中的时钟模块进行硬件握手（LPMD/LPACK）
• 通过设置 MAPSR[LPMD] 字段并轮询 MAPSR[LPACK] 进行软件握手
• 通过 MAPSR[PST] 配置触发自刷新进入的空闲周期数，并清除 MAPSR[PSD] 进行自动进入
• DVFS（动态电压和频率变化）
• 与系统中的时钟模块进行硬件握手（DVFS/DVACK）
• 通过设置 MAPSR[DVFS] 字段并轮询 MAPSR[DVACK] 进行软件握手

# 注意

如果 MMDC 检测到硬件或软件的自刷新进入请求（甚至在 LPACK 断言之前），在取消这些请求之前，不会确认任何写或读访问。

2. 特定片选的自动激活/预充电电源关进入可通过配置 ESDPDC 寄存器来激活：

• PWDT_0/PWDT_1 — 定义进入电源关前的空闲周期数，每个片选可设置不同值。
• SLOW_PD — 如果 DDR3 存储器配置为使用慢速预充电电源关，则也应设置此位。
• BOTH_CS_PS — MMDC 可以根据空闲状态独立设置每个片选进入电源关，或者仅当两个片选在配置的时间内都处于空闲状态时才将两个片选都设置为电源关。
• 还需配置以下参数：
• MDCFG0 中的时序参数 [tXP 和 tXPDLL]。
• MDOTC 中的 ODT 时序 [tAOFPD, tAONPD, tANPD 和 tAXPD]

# 注意

可以在第二个片选激活时，使某些片选进入低功耗状态。

3. 特定片选所有 DDR Bank 的自动预充电。可通过配置 ESDPDC 字段来激活：PRCT_0 和 PRCT_1。每个字段确定加载到不同片选的值。

# 35.4.6.2 自刷新和频率变化进入/退出

如省电概述中所述，MMDC 支持两种使 DDR 器件进入自刷新模式的机制：

• LPMD（低功耗模式）— 用于省电目的
• DVFS（动态电压和频率变化）— 用于时钟频率变化

当 DDR 器件处于自刷新模式时，无需提供周期性刷新命令。

MMDC 以相同方式处理 LPMD/DVFS 的硬件/软件握手：

• 在 LPMD/DVFS 请求断言时，执行以下操作：
• MMDC 阻止任何进一步的 AXI 访问，甚至在应答断言之前
• 完成所有已打开的 AXI 访问
• 以适当的时序关闭（预充电）所有 Bank
• 通过取消断言时钟使能信号（DRAM_SDCKE 驱动为"0"）并同时发出刷新命令来驱动自刷新命令。这发生在完成全部预充电命令的 tRP/tRPA 之后。
• 取消断言驱动到 DDR 器件的时钟（CK）
• 断言 LPMD/DVFS 应答（LPACK/DVACK）
• 允许取消断言 MMDC 的工作时钟（AXI 时钟）
• 在 LPMD/DVFS 请求取消断言时，执行以下操作：
• 在 LPMD/DVFS 取消断言之前，MMDC 的工作时钟必须开启
• 开始向 DDR 器件驱动时钟（CK）
• 在满足时钟恢复后的 tCKSRX 后，时钟使能信号（DRAM_SDCKE）被断言
• LPMD/DVFS 应答（LPACK/DVACK）被取消断言
• 在满足 DRAM_SDCKE 断言后的 tXS 后，向 DDR 器件驱动刷新命令。
• 如果 ZQ 校准已使能，则从刷新命令开始满足 tRFC，然后发出长 ZQ 命令。
• ZQ 命令后计数 tZQoper 空闲周期。
• 在满足 DRAM_SDCKE 断言后的 tDLLK 后，MMDC 恢复正常操作。

下图显示了 LPMD/DVFS 硬件/软件握手的时序图：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/992dc6e3050a7b3e7c1a13bf942bc250f90ebd776f8578611b5b028a747cbd66.jpg)

Figure 35-4. LPMD/DVFS 硬件/软件握手

关于自刷新的说明：

• 只要通过硬件或软件握手检测到 LPMD 或 DVFS 请求，MMDC 将立即取消断言 AXI ARREADY/AWREADY 信号，以阻止系统发出进一步的请求。
• 在自动自刷新的情况下，内部工作时钟将被取消以使能省电。

# 35.4.7 复位

# 35.4.7.1 硬复位

当硬复位被断言（aresetn 驱动为"0"）而热复位被取消断言（warm_reset 驱动为"0"）时，整个 MMDC 将被初始化，包括配置/状态寄存器和状态机。

为了访问 DDR 器件，随后需要重新配置 MMDC。

# 35.4.7.2 热复位

MMDC 支持热复位信号。热复位信号必须覆盖硬复位信号，然后 MMDC 将复位所有内部寄存器。唯一不复位的寄存器是那些在不重复初始化序列和不丢失存储器中存储的数据的情况下恢复正常操作所必需的寄存器（配置/状态寄存器不会被初始化）。

对于热复位的成功操作，必须执行以下步骤：

• MMDC 必须进入自刷新模式。这可以通过 LPMD 或 DFVS 请求实现
• 等待 LPMD 或 DVFS 应答
• 断言热复位信号（即将 warm_reset 驱动为"1"）
• 断言硬复位信号（即将 aresetn 驱动为"0"）
• 取消断言硬复位信号
• 取消断言热复位
• 退出 LPMD/DVFS 模式

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/540c8d7db3a3fca3e890853e9fea499f18e4d39ee54b1ef773ed9e7fc6478236.jpg)

Figure 35-5. 热复位图

# 35.4.7.3 软件复位

MMDC 支持软件复位。当配置软件复位时，MMDC 将复位所有内部寄存器，除了那些在不重复初始化序列和不丢失存储器中存储的数据的情况下恢复正常操作所必需的寄存器（配置/状态寄存器不会被初始化）。

对于软件复位的成功操作，应执行以下步骤：

• MMDC 应进入自刷新模式。这可以通过 LPMD 或 DFVS 请求实现。
• 等待 LPMD 或 DVFS 应答
• 通过设置 MDMISC[RST] 断言软件复位
• 退出 LPMD/DVFS 模式

可以恢复正常操作。

# 35.4.8 刷新方案

MMDC 支持多种自动刷新选项，可通过 MDREF 寄存器进行配置。

周期性自动刷新可以由以下时钟触发：

• 32 kHz 时钟
• 64 kHz 时钟
• MMDC 工作时钟

MMDC 的刷新方案是灵活的，允许系统在每个刷新周期中配置所需的 AXI 访问延迟/等待时间。

下表显示了 MMDC 将处理的四种刷新周期配置示例。每种配置都满足 3.9μs 的刷新率（tREFI，每 $3 . 9 \mu \mathrm { s }$ 一次刷新命令）。

Table 35-8. MMDC 刷新方案

<table><tr><td>选项编号</td><td>描述</td><td>REFR</td><td>REF_SEL</td><td>REF_CNT</td><td>DDR 挂起时间</td></tr><tr><td>1</td><td>每 31,250 ns 发出 8 次刷新命令</td><td>0x7 (8 次刷新)</td><td>0x0 (64 kHz)</td><td>不需要</td><td>tRFC x 8</td></tr><tr><td>2</td><td>每 15,625ns 发出 4 次刷新命令</td><td>0x3 (4 次刷新)</td><td>0x1(32 kHz)</td><td>不需要</td><td>tRFC x 4</td></tr><tr><td>3</td><td>每 7800ns 发出 2 次刷新命令</td><td>0x1(2 次刷新)</td><td>0x2 (REF_CNT)</td><td>7800/2.5 = 3120 (0xC30)</td><td>tRFC x 2</td></tr><tr><td>4</td><td>每 3900 ns 发出 1 次刷新命令</td><td>0x0 (1 次刷新)</td><td>0x2 (REF_CNT)</td><td>3900/2.5 = 1560(0x618)</td><td>tRFC</td></tr></table>

# 35.4.9 DDR 突发长度选项

MMDC 支持可通过 MDCTL[BL] 配置的突发长度，如下所示：

• 在 DDR3 模式下，只能使用突发长度 8。
• 在 LPDDR2 模式下，只能使用突发长度 4。

在 DDR3 模式下，对 DDR 的读/写访问始终为 8 字（x16），并根据 JEDEC 标准对齐。

对于 AXI 递增访问，未对齐的访问中无关数据在写访问中被掩码，在读访问中被忽略。对于 AXI 回卷访问，即使访问未对齐，MMDC 也提供内部优化机制以提高 DDR 数据总线的效率。

# 35.4.10 独占访问处理

MMDC 包含四个独占监视器，每个用于在 MAEXIDR0 和 MAEXIDR1 中配置的专用 ID。

• 如果 MMDC 接收到合法的读独占，相应的监视器被打开。
• 当在合法的写独占上监视器被打开时，监视器将被关闭，写操作将以 EXOKAY 成功完成。
• 成功的独占访问必须满足以下规则：
• 对齐访问（AXI 地址对齐到 AXI 大小）
• AXI 单次访问（AXI 突发长度不大于 1）
• AXI 大小最大为 64 位
• AXI 非缓存访问（即 ARCACHE[1]/AWCACHE[1] 等于"0"，或 ARCACHE[1]/AWCACHE[1] 等于"1"而 ARCACHE[3:2]/AWCACHE[3:2] 等于"00"）
• AXI ID 匹配四个独占 ID 之一

独占读行为（第一条也适用于非独占访问）：

• 在安全性违规的情况下，读操作被阻止，不会发送到 DDR。响应的两种选项：
• 如果 ARCR_SEC_ERR_EN（MAARCR[30]）为高，则向主设备发出 SLV 错误，否则向主设备发送 OKAY 响应。
• 如果发生 AXI 独占规则违规（如上所述），读操作不会被阻止，会发送到 DDR。数据将被获取并驱动到主设备，但响应类型可能不可预知。
• 如果上述情况均未发生，读操作被发送到 DDR。独占监视器将被打开，响应为 EXOKAY
• 如果在 AXI 独占写之前接收到具有相同 ID 的额外合法 AXI 读独占，监视器将使用最新属性更新。

独占写行为（第一条也适用于非独占访问）：

• 在安全性违规的情况下，写操作被阻止，不会发送到 DDR，但监视器将保持打开。响应的两种选项：
• 如果 ARCR_SEC_ERR_EN（MAARCR[30]）为高，则向主设备发出 SLV 错误，否则向主设备发送 OKAY 响应。
• 在 AXI 独占规则违规的情况下（如上所述），写操作被阻止，不会发送到 DDR。在这种情况下，响应类型可能不可预知。
• 如果独占写访问具有不同的 AXI 属性，但与读独占访问具有相同的 ID，则写操作被阻止，不会发送到 DDR，监视器将被关闭。响应的两种选项：
• 如果 ARCR_EXC_ERR_EN（MAARCR[28]）为高，则向主设备发出 SLV 错误，否则向主设备发送 OKAY 响应。
• 如果接收到常规（非独占）写访问到相同地址或重叠地址，则写操作将被发送到 DDR，监视器将被关闭。
• 如果接收到合法的写独占访问，且具有与读独占访问相同的属性，同时监视器已打开（在读独占和写独占之间没有发生对同一地址的写访问），则写操作被发送到 DDR，响应为 EXOKAY。但是，如果在监视器关闭时接收到合法的写独占，则写操作被阻止，响应的两种选项：
• 如果 ARCR_EXC_ERR_EN（MAARCR[28]）为高，则向主设备发出 SLV 错误，否则向主设备发送 OKAY 响应。

# 35.4.11 AXI 错误处理

MMDC 支持此处列出的 AXI 响应。

• 在 AXI 独占违规的情况下，响应的两种选项：
• 如果 MAARCR[28] 为高，则向主设备发出 SLV 错误，否则向主设备发送 OKAY 响应

# 注意

在读错误的情况下，MMDC 在读数据总线上驱动零值

# 35.5 性能

# 35.5.1 仲裁和重排序机制

# 35.5.1.1 仲裁概述

以下说明 MMDC 中面向 DDR 的仲裁和重排序流程。

• AXI 读和写访问在相应的队列中被采样。
• 处理读/写仲裁以选择胜出访问。
• 胜出访问被采样到重排序队列中
• 在重排序队列中的有效请求之间执行重排序机制，以选择将分派到 DDR 的访问。
• 执行重排序以优化访问并最大化 DDR 总线的利用率
• 一旦重排序的访问完成（由响应或数据阶段结束指示），它就会从相应的队列中删除，MMDC 准备好从主设备接收下一个可用访问

通常，重排序/仲裁机制基于动态优先级机制，该机制比较重排序队列中有效条目之间的动态优先级，并向 DDR 逻辑发出具有最高动态优先级的条目。

胜出访问的选择基于两种模式，这两种模式可以同时激活，如下所示：

• 实时通道模式：
• 具有 $\mathrm { Q o S = ^ { \prime } f ^ { \prime } }$（即 awqos[3:0]/arqos[3:0] = "f"）的访问将绕过所有其他面向 DDR 的请求
• 动态评分模式：
• 仲裁机制基于动态优先级。适用于 QoS 小于 'f' 的访问或实时通道模式禁用时。

# 注意

由于重排序和优化机制（基于不同的 AXI ID），发往 DDR 的事务可能以与 AXI 主设备接收时不同的 ID 顺序被驱动。类似地，写响应、读响应或读数据也可能以不同的 ID 顺序被驱动到 AXI 主设备。

# 35.5.1.2 实时通道模式

当实时模式使能时（即 MAARCR[ARCR_RCH_EN] = "1"），所有具有 $\mathrm { Q o S = ^ { \prime } f ^ { \prime } }$（即 awqos[3:0]/aqqos[3:0] = "f"）的请求将绕过所有其他面向 DDR 的待处理访问。此模式默认使能。

# 35.5.1.3 动态评分模式（仲裁获胜条件）

MMDC 中待处理访问之间的仲裁根据每个访问的动态优先级进行处理。

动态优先级（也可称为得分）根据一些因素的之和（final_score[3:0]）计算，其中部分因素可以动态更新。以下说明每个评分因素：

• MAARCR[ARCR_PAG_HIT]（页命中得分）— 当待处理访问具有页命中时考虑的静态得分
• MAARCR[ARCR_ACC_HIT]（访问命中得分）— 当当前访问类型（读/写）与之前已分派到 DDR 的访问类型相同时考虑的静态得分
• MAARCR[ARCR_DYN_JMP]（动态跳变得分）— 当待处理访问在仲裁中未被选中时给予的动态得分。动态跳变计数器受限于 MAARCR[ARCR_DYN_MAX] 中设置的最大值。
• 通过旁带 4 位 AXI 信号（awqos[3:0]/aqqos[3:0]）指示并由 AXI 主设备每个访问驱动的 QoS 得分

# 注意

为防止总得分总和溢出，当总得分总和大于 'f' 时执行裁剪并选择最大得分值 'f'。

下图显示了动态得分计算

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/bbab9aedafc5b2ea86a75221c517199ba1ffb7f7e332791eeb79c47c16dedf75.jpg)

Figure 35-6. 动态得分/优先级计算

# 35.5.1.4 保护（老化）机制

保护机制（也可称为老化）用于防止访问饥饿。

当动态跳变得分达到其最大值（MAARCR[ARCR_DYN_MAX]）时，每次待处理请求在仲裁中未被选中，"保护"计数器就增加 1。当"保护"计数器达到其在 MAARCR[ARCR_GUARD] 中设置的预定义值时，相关请求获得最高优先级，并将在下一个面向 DDR 的仲裁周期中被选中，除非有实时通道到达（即具有 $\mathrm { Q o S } = " \mathrm { f " }$ 的访问）。

注意：如果实时通道到达，非实时通道的动态得分将不会增加，以防止多个访问的"保护"计数器达到其限制的情况。

# 35.5.2 预测机制

当预测机制使能时（即通过配置 MDMISC[MIF3_MODE]），MMDC 在访问物理分派到 DDR 器件之前预测将要发往 DDR 的片选、Bank 地址和行地址。

该机制使 DDR 器件能够为未来的访问做好准备，从而提高整体 DDR 性能。

该预测机制与重排序机制并行运行，可以基于 3 个级别的待处理访问产生预测：

1. 流水线第一阶段的访问。
2. AXI 总线（读通道或写通道）上的有效访问。
3. 来自仲裁的特殊总线上的有效访问 — 该访问被仲裁选为其缓冲器中的下一个未命中访问

# 35.5.3 DDR3 访问的特殊优化

如果在 DDR3 模式下确认了一个 AXI 读/写回卷非对齐访问，其回卷边界与 DDR 回卷边界相同，则 MMDC 将进行优化，只向 DDR 发出一次访问，尽管所有对 DDR3 的访问必须对齐。

例如：AXI 写访问，大小为 128 位（awsize[2:0] $\left| = 3 \right.$ 'b100），长度为 4（awlen[3:0]=4'b0011），面向 DDR3 x64（突发长度 8）。在这种情况下，AXI 回卷边界为 $1 6 \mathrm { { B x } } 4 = 6 4 \mathrm { { B } }$（0x40），DDR3 回卷边界为 $8 \mathrm { B x } 8 { = } 6 4 \mathrm { B }$（0x40）。例如，如果 AXI 访问面向后缀为 0x10（未对齐到 64B 边界）的 AXI 地址，则 MMDC 将从 AXI 主设备获取与地址 0x10、0x20、0x30、0x0 相关联的数据。MMDC 将在内部重新排列数据以匹配 DDR3 对齐：0x0、0x10、0x20、0x30，并通过一次面向 DDR 的访问驱动到地址 0x0。替代方案是向 DDR 发出两次访问，地址为 0x0，使用不同的数据掩码。

# 注意

在读回卷访问中，执行相同的优化，而当从 DDR 获取到关键的 AXI 字时，它会立即驱动到 AXI 主设备，无需缓冲。基于上述示例，主设备期望首先获取与地址 0x10 关联的数据。因此，MMDC 将从 DDR 地址 0x0 发出读访问，一旦接收到与地址 0x10 关联的数据，它将立即驱动回主设备，甚至在获取更远地址的数据之前。

# 35.6 MMDC 调试

# 35.6.1 硬件调试监视器

MMDC 具有硬件调试机制，监视驱动到 MMDC 的每个访问。每次此机制使能时（将 MADPCR0[DBG_EN] 设置为 "1"），每个将分派到 DDR 的访问也会在 I/O 焊盘上被观察到（即通过 ipp_do_ddr_debug[50:0]）。该总线的内容如下表所述。

Table 35-9. 硬件监视器调试

<table><tr><td>信号名称</td><td>位数</td><td>描述</td></tr><tr><td>acc_addr</td><td>[31:0]</td><td>所选访问的 AXI 地址</td></tr><tr><td>acc_type</td><td>1</td><td>所选访问的访问类型。"0"表示写。"1"表示读。</td></tr><tr><td>acc_id</td><td>[15:0]</td><td>所选访问的 AXI 事务 ID</td></tr><tr><td>valid_strobe</td><td>1</td><td>有效请求指示。此信号将断言 1 个时钟周期</td></tr></table>

上述字段按以下方式组织：

MMDC_DEBUG[50:0] = {1'b0,valid_strobe,acc_id,access_type,addr}

这些信号发送到 IOMUX，在 IOMUX 中用户可以配置将其从芯片输出以供调试使用。

# 35.6.2 逐步（SBS）软件监视器

MMDC 具有逐步（SBS）软件调试机制，监视驱动到 MMDC 的每个访问。每次触发此机制时，一个 AXI 访问将被分派到 DDR，同时其属性将在状态寄存器中被观察到。

一旦"逐步"使能（即 MADPCR0[SBS_EN] 为 "1"），则所有对 DDR 器件的访问将被暂停。此 SBS 功能在 DDR SDCLK 频率缩放期间使用，以防止在转换期间对 DDR 器件进行任何访问。将 MADPCR0[SBS] 设置为 "1" 将分派在 MMDC 队列头部等待的访问（读或写）。每次设置 MADPCR0[SBS] 时：

• 访问的 AXI 属性将被采样到相关的 MASBS0 和 MASBS1 字段中
• MADPCR0[SBS] 将自动清零。

再次将 MADPCR0[SBS] 设置为 "1" 将分派 MMDC 队列中的下一个待处理访问。

# 注意

在 MMDC0_MAARCR 寄存器中设置 ARCR_ARB_REO_DIS 位将禁用 SBS 功能。

# 35.7 MMDC 性能分析

性能分析机制提供计算 DDR 利用率以及给定时间段内向 DDR 的读写访问统计信息的能力。

MMDC 支持以下性能分析计数器：

• MADPSR0（总周期计数）— 指示性能分析周期的总周期数（最多 $2 ^ { \wedge } 3 2$ 个周期）
• MADPSR1（忙周期计数）— 指示性能分析期间的总忙周期数。忙周期是指内部状态机非空闲的任何 MMDC 时钟周期。如果 FIFO 中有任何读或写请求待处理，MMDC 就不是空闲的。
• MADPSR2（总读访问计数）— 指示性能分析期间对 MMDC 的总读访问数
• MADPSR3（总写访问计数）— 指示性能分析期间对 MMDC 的总写访问数
• MADPSR4（总读字节计数）— 指示性能分析期间从 MMDC 读取的总字节数
• MADPSR5（总写字节计数）— 指示性能分析期间写入 MMDC 的总字节数

上述所有性能分析项目默认禁用。以下说明如何控制性能分析机制：

• MADPCR0[DBG_EN] 使能性能分析。
• MADPCR0[PRF_FRZ] 停止/冻结性能分析，例如用户希望对特定任务执行 DDR 性能分析时。要恢复性能分析，应清除 MADPCR0[PRF_FRZ]。
• MADPCR0[DBG_RST] 清除所有性能分析计数器
• MADPCR0[CYC_OVF] 指示总周期计数器是否发生溢出（即总周期数大于 $2 ^ { \land } 3 2$）。此字段只能通过写入 '0' 来清除。

可以按特定 AXI ID（16 位）收集读/写统计信息。MADPCR1 寄存器中的以下字段确定要监视的 AXI-ID 或 AXI-ID：

• PRF_AXI_ID 定义哪些 AXI ID 用于性能分析。默认值为 16'h0。
• PRF_AXI_ID_MASK 定义 PRF_AXI_ID 中的哪些位将与读/写访问的 AXI ID 进行比较。"1"表示监视相关位，"0"表示不关心。默认值为 16'h0000，表示所有 ID 都不被监视

因此，要监视的 AXI-ID 根据以下等式计算：

(AXI-ID & PRF_AXI_ID_MASK) Xnor (PRF_AXI_ID & PRF_AXI_ID_MASK)

例如，如果希望监视 A100 到 A1FF 之间的 AXI ID，则应配置：

• PRF_AXI_ $\mathrm { I D } = \mathrm { A } 1 0 0$
• PRF_AXI_ID_MASK = FF00

# 35.8 LPDDR2 刷新率更新和时序降额

LPDDR2 器件可能具有温度传感器，用于确定适当的刷新率以及是否需要 AC 时序降额。温度传感器的状态可以通过从 LPDDR2 MR4 寄存器的 MRR 命令读取。

MMDC 支持实时刷新更新和时序降额机制。以下步骤说明如何使用该机制：

• 使用 MRR 命令定期轮询 MR4 LPDDR2 寄存器
• 读取 MDMRR 寄存器并分析 MR4 指示
• 如果需要刷新率更新和/或 AC 时序降额，则需要更新 MDREF 和/或 MDMR4[tRCD_DE, tRC_DE, tRAS_DE, tRP_DE, tRRD_DE] 参数

# 注意

MDMR4[tRCD_DE, tRC_DE, tRAS_DE, tRP_DE, tRRD_DE] 引用在 MDCFG3LP[tRC_LP, tRP_LP, tRCD_LP]、MDCFG1[tRAS]、MDCFG2[tRRD] 配置的相关值。

• 断言 MDMR4[UPDATE_DE_REQ]
• 当 MMDC 切换到新值时，将在 MDMR4[UPDATE_DE_ACK] 上指示应答

使能的省电功能可能会干扰 MR4 读取。当这些功能使能时，MMDC 将自动进入自刷新，从而阻止 MR4 读取。因此，当 SW 执行 MR4 读取时，应禁用省电和刷新功能。

要禁用"电源关"模式，将 MAPSR（0x021B0404）的位 0 设置为 1'b。要禁用"自刷新电源关定时器"模式，将 MDPDC（0x021B0004）的位 [15:8] 设置为 0x00。

执行 MR4 读取的完整序列

1. 设置 MAPSR 为 0x00010107
2. 设置 MDPDC 为 0x00020076
3. MRR 命令读取 MR4
4. 写入 MDPDC 为 0x00025576 以重新使能此功能
5. 写入 MAPSR 为 0x00010106 以重新使能此功能

# 35.9 DLL 切换

# 35.9.1 DLL 关闭模式

DLL 关闭模式仅在 DDR3 中支持，允许 DDR 在低频下运行（即低于 JEDEC 标准定义的 125 MHz）。

更多详情请参见标准中的 DLL-off 模式章节。

从 DLL 开启切换到 DLL 关闭模式应执行以下步骤：

• 断言 CON_REQ 信号并等待 CON_ACK 断言。
• 禁用可能与此序列冲突的电源关定时器，例如：MAPSR[PSD]、MDPDC[PWDT_1]、MDPDC[PWDT_0]、MDPDC[PRCT_0]、MDPDC[PRCT_1]。
• 执行所有 Bank 预充电命令（通过 MDSCR）。
• 执行 MRW 命令到 MR1，禁用 RTT Nom（A9,A6,A2 =0）并使能 DLL ON（$\mathrm { A } 0 = 1$）。
• 执行 MRW 命令到 MR2，将 CWL 更新为 6。
• 执行 MRW 命令到 MR0，将 CL 更新为 6。
• 取消断言 CON_REQ 信号。
• 进入自刷新模式。更多信息请参见自刷新和频率变化进入/退出。
• 在自刷新进入应答时，更改到所需频率。
• 退出自刷新模式。
• 断言 CON_REQ 并等待 CON_ACK 断言。
• 在 DQS 上使能下拉电阻（通过 I/O-MUX）。
• 按如下方式配置 MMDC 寄存器：
• 更新 tCWL ${ = } 6$ 和 tCL ${ = } 6$ 以满足在 DDR 器件中配置的值。（MDCGFG0, MDCFG1）
• 禁用 ODT 电阻（即设置 MPODTCTRL 为 "0"）。
• 禁用 DQS 门控（即设置 MPDGCTRL0[DG_DIS] 为 "1"）。
• 使能所需的前述禁用的电源关定时器，例如：MAPSR[PSD]、MDPDC[PWDT_1]、MDPDC[PWDT_0]、MDPDC[PRCT_0]、MDPDC[PRCT_1]。
• 取消断言 CON_REQ 并等待 CON_ACK 取消断言。

从 DLL 关闭切换到 DLL 开启应执行以下步骤：

• 执行所有 Bank 预充电命令（通过 MDSCR）。
• 进入自刷新模式。更多信息请参见自刷新和频率变化进入/退出。
• 在自刷新进入应答时，更改到所需频率。
• 退出自刷新模式
• 断言 CON_REQ 并等待 CON_ACK 断言。
• 禁用可能与此序列冲突的电源关定时器，例如：MAPSR[PSD]、MDPDC[PWDT_1]、MDPDC[PWDT_0]、MDPDC[PRCT_0]、MDPDC[PRCT_1]。
• 执行 MRW 命令到 MR1，使能 RTT Nom（A9,A6,A2）和 DLL ON（$\mathrm { A } 0 = 0$）。
• 执行 MRW 命令到 MR0 以复位 DLL（A8）并更新 CL 值
• 执行 MRW 命令到 MR2 以更新 CWL 值。
• 执行 ZQ 命令。
• 重新配置 MMDC 模块
• 更新 tCWL 和 tCL 以满足配置到存储器的值。（MDCGFG0, MDCFG1）
• 使能 ODT 电阻（即 MPODTCTRL 寄存器）
• 使能 DQS 门控（即设置 MPDGCTRL0[DG_DIS] 为 "0"）。
• 在 DQS 上禁用下拉电阻（通过 I/O-MUX）。
• 使能所需的前述禁用的电源关定时器，例如：MAPSR[PSD]、MDPDC[PWDT_1]、MDPDC[PWDT_0]、MDPDC[PRCT_0]、MDPDC[PRCT_1]。
• 取消断言 CON_REQ 并等待 CON_ACK 取消断言。

# 35.10 ODT 配置

MMDC 在 DDR3 模式下支持一个 DRAM_ODT 信号（每个 DRAM_CS 对应一个 DRAM_ODT），以允许 DDR 器件打开/关闭其端接电阻。MMDC 提供多种用于断言 ODT 信号的配置以及若干时序相关的配置。

MDOTC 寄存器控制 DRAM_ODT 信号断言的时序。

# 注意

tODTLon 决定 DRAM_ODT 信号与相关 RTT 之间的延迟，根据 JEDEC 标准，它等于 WL（写延迟）- 2。因此，配置到 MDOTC[tODTLon] 字段的值应与配置到 MDCGFG1[tCWL] 的值对应。

在预充电电源关模式下，当所有 Bank 关闭时，ODT 的断言对应于在 MDOTC 寄存器中配置的 tAOFPD 和 tAONPD。

下图显示了 MPODTCTRL[0] 设置为 "1"（即在写访问命令中向非活动 DRAM_CS 断言 DRAM_ODT）且 MDOTC[tODTLon] 设置为 4 时的 DRAM_ODT 和 RTT 信号时序图。

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/10688ff6e898be428da516e0d585073c9a3c19dabd9e84d80c33707ce530bc92.jpg)

Figure 35-7. ODT — DDR3 时序图 WL $\mathtt { \pmb { \mathscr { = } } 6 }$，BL=8

# 35.11 校准过程

MMDC 提供多种校准过程，用于获得更好的时序精度、板级偏移补偿和 I/O 焊盘驱动强度调整。每个校准过程可以自动（硬件）或手动（软件）执行，但手动方法通常保留用于调试目的。支持以下校准过程：

# 注意

在校准过程开始前应禁用省电功能。（例如：MDPDC[PWDTn]、MDPDC[PRCTn]、MAPSR[PSD]）

• 外部 DDR 器件的 ZQ 校准（DDR3 通过 ZQ 校准命令，LPDDR2/LPDDR3 通过 MRW 命令）
• 可自动处理 ZQ Short（周期性）和 ZQ Long（退出自刷新时）
• 可手动处理 ZQ INIT
• 用于校准 DDR 驱动强度的 i.MX DDR I/O 焊盘的 ZQ 校准
• 序列可由硬件自动处理
• 序列可由软件逐步手动处理
• 仅适用于 DDR3 的读 DQS 门控校准。调整 DQS 门控与读前导码窗口。更多信息请参见读 DQS 门控校准
• LPDDR2/LPDDR3 不支持读 DQS 门控校准
• 读数据校准。调整读 DQS 与读数据字节。更多信息请参见读校准
• 写数据校准。调整写 DQS 与写数据字节。更多信息请参见写校准
• 写电平校准。调整写 DQS 与 CK（DDR 差分时钟）。更多信息请参见写电平校准
• 读微调。每个读数据位最多调整 7 个延迟线单元。
• 写微调。每个写数据位最多调整 3 个延迟线单元。

# 注意

在开始任何涉及 DDR3 器件 MPR 模式或写电平校准的校准过程之前，应完成以下操作：

• 禁用周期性刷新方案（即设置 MDREF[REF_SEL] = "11"），然后通过配置 MDSCR[CMD]= 0x2 发出手动刷新命令突发。在校准结束时，需要使能周期性刷新方案。
• 禁用自动省电模式（即设置 MAPSR[PSD] = "1"）。

# 35.11.1 延迟线

每个校准过程控制多个延迟线，用于对齐数据和选通信号。

默认情况下，延迟线配置为产生 1/4 时钟周期的延迟。

此外，当工作时钟处于特性列表中出现的最大允许频率时，延迟线能够发出高达 1/2 时钟周期的可配置延迟。

# 注意

在校准过程开始时，延迟线的初始值必须是有效值（即选通信号必须位于相关数据窗口内的某处），尽管可能不是最佳值。延迟线校准应在读 DQS 门控和写电平校准之后完成。

为了在 MMDC 正常运行期间产生足够的延迟，延迟线在 DDR 器件的刷新周期期间经历自动测量过程。

# 35.11.2 ZQ 校准

MMDC 支持 ZQ 校准过程，用于校准 DDR I/O 焊盘的驱动强度以及驱动 ZQ 命令以校准外部 DDR 器件的驱动强度。

第一次 ZQ 校准（在处理器启动后）在开启 MMDC 之前执行。后续的 ZQ 校准可以与 DDR ZQ 校准并行执行。MMDC 支持 2 种 ZQ 校准命令：short 和 long。

ZQ long 校准在上电序列期间、退出自刷新模式时或退出慢速预充电电源关时执行（DLL 锁定可以并行完成）。ZQ short 校准根据 MPZQHWCTRL[ZQ_HW_PER] 定义的可配置定时器周期性执行。

字段 MPZQHWCTRL[ZQ_MODE] 决定 MMDC 是否将对 DDR I/O 焊盘执行 ZQ 校准和/或向 DDR 器件发出 ZQ short/long 命令。

MMDC 支持 DDR I/O 焊盘的自动（硬件）和手动（软件）ZQ 校准过程。

可以通过断言 MPZQHWCTRL[ZQ_HW_FOR] 仅执行一次自动（硬件）ZQ 校准（即非周期性）。

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/d755f2a2b0fac3a5f973df018f09c0066ff2217948289a74fa8e2044f7f3b24e.jpg)

Figure 35-8. MMDC ZQ 接口与焊盘

# 35.11.2.1 ZQ 自动（硬件）校准过程

ZQ 自动校准通过多个步骤进行，分为上拉电阻校准和下拉电阻校准，如下所示。

# 35.11.2.1.1 ZQ 自动上拉校准

MMDC 自动与 ZQ 校准焊盘执行握手机制，如下所示：

1. MMDC 将 zq_comparator_en 驱动为 "1"
2. MMDC 根据 MPZQHWCTRL[ZQ_EARLY_COMPARATOR_EN_TIMER] 等待几个周期
3. MMDC 将 zq_pu_pd_sel 驱动为 "1" 表示上拉校准，并将 zq_pu_val[4:0] $=$ 5'b00000
4. MMDC 将 zq_pu_val[4] 驱动为 "1"
5. MMDC 断言 zq_compare_en
6. MMDC 根据 MPZQSWCTRL[ZQ_CMP_OUT_SMP] 等待几个周期，然后采样比较器输出（即 zq_comp_out）。如果 zq_comp_out 为 "1"，则表示输出电压大于 Vdd/2（即内部电阻小于 240 ohm），并将位 zq_pu_val[4] 驱动为 "1"，否则将 zq_pu_val[4] 驱动为 "0"
7. MMDC 取消断言 zq_compare_en
8. MMDC 对 zq_pu_val 位 3 到 0 重复步骤 4-7
9. MMDC 将 ZQ 校准结果驱动到 MPZQHWCTRL[ZQ_HW_PU_RES]
10. MMDC 进入下拉校准

# 35.11.2.1.2 ZQ 自动下拉校准

1. MMDC 将 zq_pu_pd_sel 驱动为 "0" 表示下拉校准，并将 zq_pd_val[4:0] $=$ 5'b00000
2. MMDC 将 zq_pd_val[4] 驱动为 "1"
3. MMDC 断言 zq_compare_en
4. MMDC 根据 MPZQSWCTRL[ZQ_CMP_OUT_SMP] 等待几个周期，然后采样比较器输出（即 zq_comp_out）。如果 zq_comp_out 为 "1"，则表示输出电压大于 Vdd/2（即内部电阻小于 240 ohm），并将位 zq_pd_val[4] 驱动为 "0"，否则将 zq_pd_val[4] 驱动为 "1"
5. MMDC 取消断言 zq_compare_en
6. MMDC 对 zq_pd_val 位 3 到 0 重复步骤 2-5
7. MMDC 将 ZQ 校准结果驱动到 MPZQHWCTRL[ZQ_HW_PD_RES]
8. MMDC 取消断言 zq_comparator_en 以指示 ZQ 校准完成

# 35.11.2.2 ZQ 软件校准过程

ZQ 校准也可以由软件完成。但由于软件 ZQ 校准比硬件校准慢得多，应主要用于调试。

软件应配置 ZQ 校准参数（上拉或下拉及其值），然后断言 MPZQSWCTRL[ZQ_SW_FOR] 位。然后软件应等待直到 ZQ_SW_FOR 被取消断言，并使用 ZQ_SW_RES 状态位来计算下一个 ZQ 校准参数。

# 35.11.2.3 ZQ 校准命令

在 MMDC 可以向存储器发出 ZQCL/ZQCS 命令之前，它应预充电所有存储 Bank 并等待 tRP 周期。只要器件不共享同一个 ZQ 电阻，就可以向所有器件发出单个 ZQ 命令。

当 MMDC 发出 ZQ 命令时，它还应该驱动 A10（长或短命令）和 CS（0、1 或两者）。

MMDC 必须在 Jedec 定义的 ZQ 校准时间内保持存储器线路静默（CK 除外）（复位后 ZQCL 为 512 个周期，其他 ZQCL 为 256 个周期，ZQCS 为 64 个周期）。

# 35.11.3 读 DQS 门控校准

读 DQS 门控校准用于调整读 DQS 门控与读 DQS 前导码的中间位置。DQS 门控包括最多 7 个周期的延迟（延迟根据两个字段 MPDGCTRLn[DG_HC_DELn] 和 MPDGCTRLn[DG_DL_ABS_OFFSETn] 选择）。

每个 DQS 有自己的延迟线。DQS 门控过程可以对所有 DQS 并行完成。

# 注意

在 LPDDR2/LPDDR3 模式下，应禁用硬件读 DQS 门控，DQS/DQSn 上的上拉/下拉电阻应使能，而 ODT 电阻必须断开。

# 注意

在 DDR3_x64 模式下，通过设置 MPDGCTRL0[HW_DG_EN] 激活校准。

# 35.11.3.1 硬件 DQS 门控校准

• 有两种操作模式：
• 使用 MPR（多功能寄存器）校准
• 使用 MMDC 预定义值校准

# 35.11.3.1.1 使用 MPR 的硬件 DQS 校准

应执行以下步骤：

1. 预充电所有活动 Bank（可通过 MDSCR 完成），按标准要求。
2. 通过 MRS 命令将 DDR 器件进入 MPR 模式
3. 通过断言 MPPDCMPR2[MPR_CMP] 配置 MMDC 以使用 MPR 模式工作
4. 确保每个字节的读延迟线绝对偏移中配置的初始值（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）将读 DQS 放置在读 DQ 窗口内的某处
5. 通过断言 MPDGCTRL0[HW_DG_EN] 启动校准过程

# 35.11.3.1.2 使用预定义值的硬件 DQS 校准

如果使用预定义模式（即 MPPDCMPR2[MPR_CMP] 被清除），则应执行以下步骤：

1. 预充电所有活动 Bank（可通过 MDSCR 完成），按标准要求。
2. 将预定义值（该值反映将通过读校准写入和比较的值）配置到 MPPDCMPR1[PDV1, PDV2]
3. 通过设置 MPSWDAR0[SW_DUMMY_WR] = 1 向外部 DDR 器件发出写访问（MMDC 将在内部生成对 Bank 0、行 0、列 0 的写访问，无需系统干预）
4. 确保每个字节的读延迟线绝对偏移中配置的初始值（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）将读 DQS 放置在读 DQ 窗口内的某处
5. 通过断言 MPDGCTRL0[HW_DG_EN] 启动校准过程

对于两种模式（MPR 和预定义值），MMDC 将自动执行以下步骤：

6. MMDC 等待，直到读 DQS 延迟线更新为所有字节的绝对延迟值（在 MPDGCTRLn[DG_HC_DELn] 和 MPDGCTRLn[DG_DL_ABS_OFFSETn] 中），并满足 Tmod + 4 要求

# 校准过程

7. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。

8. MMDC 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则表明读 DQS 门控在非法时间点断言。如果比较通过，则 MMDC 进入步骤 14。

9. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。

10. MMDC 将每个字节的读 DQS 门控延迟递增半个周期（即 MPDGCTRLn[DG_HC_DELn] + 1）。

11. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。

12. MMDC 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。

13. 如果比较失败，则表明读 DQS 门控在非法时间点断言，需要重复步骤 9-12。如果比较通过，则 MMDC 存储临时下边界值并进入下一步。

14. MMDC 将每个字节的读 DQS 门控延迟线递增半个周期（即 MPDGCTRLn[DG_HC_DELn] + 1），并启动读 DQS 门控延迟线的测量过程以使用新值更新自身。

15. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。

16. MMDC 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。

17. 如果比较通过，则表明读 DQS 门控在读前导码窗口内断言，需要重复步骤 14-16。如果比较失败，则 MMDC 存储临时上边界值，并开始搜索合适的低边界和高边界。

18. MMDC 返回到临时下边界减去半个周期，并启动读 DQS 门控延迟线的测量过程以使用新值更新自身。

19. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。

20. MMDC 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。

21. 如果比较失败，则表明读 DQS 门控在非法时间点断言，需要重复步骤 22-23。如果比较通过，则 MMDC 存储合适的低边界值并进入步骤 24。

22. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。

23. MMDC 将每个字节的读 DQS 门控延迟递增 1（即 MPDGCTRLn[DG_DL_ABS_OFFSETn] + 1），并启动读 DQS 门控延迟线的测量过程以使用新值更新自身，然后进入步骤 19。

24. MMDC 返回到临时上边界减去半个周期，并启动读 DQS 门控延迟线的测量过程以使用新值更新自身。

25. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。

26. MMDC 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。

27. 如果比较通过，则表明读 DQS 门控在读前导码窗口内断言，需要重复步骤 28-29。如果比较失败，则 MMDC 存储减 1 后的合适上边界值并进入步骤 30。

28. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。

29. MMDC 将每个字节的读 DQS 门控延迟递增 1（即 MPDGCTRLn[DG_DL_ABS_OFFSETn] + 1），并启动读 DQS 门控延迟线的测量过程以使用新值更新自身，然后进入步骤 25。

30. 在 MMDC 找到每个读数据字节的窗口边界（下边界和上边界）后，它将下边界和上边界之间的平均值存储到相应的 MPDGCTRLn[DG_DL_ABS_OFFSETn] 中，并启动读 DQS 延迟线的测量过程以使用新值更新自身。

31. MMDC 通过设置 MPDGCTRL0[HW_DG_EN] = 0 指示读 DQS 门控校准已完成。

32. 通过 MRS 命令将 DDR 器件退出 MPR 模式。

33. 读取找到的上边界：MPDGHWSTn[HW_DG_UPn]。该字段为 11 位，低 7 位对应 MPDGCTRLn[DG_DL_ABS_OFFSETn] 的上限值，高 4 位对应 MPDGCTRLn[DG_HC_DELn] 的上限值。

34. 将 MPDGHWSTn[HW_DG_UPn][6:0] 设置到 MPDGCTRLn[DG_DL_ABS_OFFSETn]。

# 校准过程

35. 将 (MPDGHWSTn[HW_DG_UPn][10:7] - 1) 设置到 MPDGCTRLn[DG_HC_DELn]。（将 DQS 门控值设置为上限值减半个周期）

# 35.11.3.2 SW 读 DQS 门控校准

有两种操作模式：

• 使用 MPR（多功能寄存器）校准
• 使用 MMDC 预定义值校准

# 35.11.3.2.1 使用 MPR 的 SW 读校准

执行以下步骤：

1. 预充电所有活动 Bank（可通过 MDSCR 完成），按标准要求。
2. 通过 MRS 命令将 DDR 器件进入 MPR 模式。
3. 通过断言 MPPDCMPR2[MPR_CMP] 配置 MMDC 以使用 MPR 模式工作。
4. 确保每个字节的读延迟线绝对偏移中配置的初始值（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）将读 DQS 放置在读 DQ 窗口内的某处。

# 35.11.3.2.2 使用预定义值的 SW 读校准

如果使用预定义模式（即 MPPDCMPR2[MPR_CMP] 被清除），则应执行以下步骤：

1. 预充电所有活动 Bank（可通过 MDSCR 完成），按标准要求。
2. 将预定义值（该值反映将通过读校准写入和比较的值）配置到 MPPDCMPR1[PDV1, PDV2]。
3. 向外部 DDR 器件发出写访问（使用任何合法的 DDR 地址）。
4. 确保每个字节的读延迟线绝对偏移中配置的初始值（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）将读 DQS 放置在读 DQ 窗口内的某处。

对于两种模式（MPR 和预定义值），MMDC 将自动执行以下步骤：

1. 通过设置 MPDGCTRLn[DG_DL_ABS_OFFSETn] = 0 和 MPDGCTRLn[DG_HC_DELn] = 0 将读 DQS 延迟线配置为产生零延迟。
2. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的读延迟。
3. 等待 16 个 DDR 周期，直到读 DQS 延迟线更新为所有字节的绝对延迟值。
4. 从外部 DDR 器件发出读命令（使用步骤 3 中选择的合法 DDR 地址）。
5. 等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。
6. 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则表明读 DQS 门控在非法时间点断言。如果比较通过，则进入步骤 11。
7. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。
8. 将每个字节的读 DQS 门控延迟递增半个周期（即 MPDGCTRLn[DG_HC_DELn] + 1）。
9. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。
10. 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则表明读 DQS 门控在非法时间点断言，需要重复步骤 7-10。如果比较通过，则进入步骤 11。
11. 存储临时下边界并开始搜索临时上边界。
12. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。
13. 将每个字节的读 DQS 门控延迟递增半个周期（即 MPDGCTRLn[DG_HC_DELn] + 1）。
14. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。
15. 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。
16. 如果比较通过，则表明读 DQS 门控在读前导码窗口内断言，需要重复步骤 12-15。如果比较失败，则需要存储临时上边界值，并开始搜索合适的低边界和高边界。
17. 将临时下边界减半个周期加载到相应的 MPDGCTRLn[DG_HC_DELn]。
18. 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。

# 校准过程

19. 将每个字节的读 DQS 门控延迟递增 1（即 MPDGCTRLn[DG_DL_ABS_OFFSETn] + 1），并通过配置 MPMUR0[FRC_MSR] = 1 强制延迟线测量自身并发出请求的读 DQS 延迟。
20. 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。
21. 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。
22. 如果比较失败，则表明读 DQS 门控在非法时间点断言，需要重复步骤 18-22。如果比较通过，则进入下一步。
23. 存储合适的低边界。
24. 将临时上边界减半个周期加载到相应的 MPDGCTRLn[DG_HC_DELn]。
25. 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。
26. 将每个字节的读 DQS 门控延迟递增 1（即 MPDGCTRLn[DG_DL_ABS_OFFSETn] + 1），并通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的读 DQS 延迟。
27. 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPDGCTRL0[DG_CMP_CYC]），假定数据已从 DDR 器件到达。
28. 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。
29. 如果比较通过，则需要重复步骤 25-28。如果比较失败，则进入下一步。
30. 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。
31. 存储合适的边界。
32. 保持 MPDGCTRLn[DG_DL_ABS_OFFSETn] 的值作为上限值。
33. 设置 MPDGCTRLn[DG_HC_DELn] = (MPDGCTRLn[DG_HC_DELn] - 1)。（将 DQS 门控值设置为上限值减半个周期）
34. 通过配置 MPMUR[FRC_MSR] = 1 发出请求的读 DQS 延迟。
35. 通过 MRS 命令将 DDR 器件退出 MPR 模式。

# 35.11.4 读校准

读校准用于调整读 DQS 与读数据字节。假设读 DQS 门控校准过程在读校准之前完成。

# 注意

在 DDR3 模式下，通过设置 MPRDDLHWCTL[HW_RD_DL_EN] 激活校准。

# 注意

在 LP2_x16 模式下，通过设置 MPRDDLHWCTL[HW_RD_DL_EN] 激活校准。

# 35.11.4.1 硬件（自动）读校准

有两种操作模式：

• 使用 MPR（多功能寄存器）/DQ 校准（LPDDR2）校准
• 使用 MMDC 预定义值校准

# 35.11.4.1.1 使用 MPR/DQ 校准的硬件（自动）校准

执行以下步骤：

1. 预充电所有活动 Bank（可通过 MDSCR 完成），按标准要求。
2. 通过 MRS/MRW 命令将 DDR 器件进入 MPR/DQ 校准模式。
3. 通过断言 MPPDCMPR2[MPR_CMP] 配置 MMDC 以使用 MPR/DQ 校准模式工作。
4. 确保每个字节的读延迟线绝对偏移中配置的初始值（MPRDDLCTL[RD_DL_ABS_OFFSET#]）将读 DQS 放置在读 DQ 窗口内的某处。
5. 通过断言 MPRDDLHWCTL[HW_RD_DL_EN] 启动校准过程。

# 35.11.4.1.2 使用预定义值的硬件（自动）校准

如果使用预定义模式（即 MPPDCMPR2[MPR_CMP] 被清除），则应执行以下步骤：

1. 预充电所有活动 Bank（可通过 MDSCR 完成），按标准要求。
2. 将预定义值（该值反映将通过读校准写入和比较的值）配置到 MPPDCMPR1[PDV1, PDV2]。
3. 通过设置 MPSWDAR0[SW_DUMMY_WR] = 1 向外部 DDR 器件发出写访问（MMDC 将在内部生成对 Bank 0、行 0、列 0 的写访问，无需系统干预）。
4. 确保每个字节的读延迟线绝对偏移中配置的初始值（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）将读 DQS 放置在读 DQ 窗口内的某处。

# 校准过程

5. 通过断言 MPRDDLHWCTL[HW_RD_DL_EN] 启动校准过程。

对于两种模式（MPR 和预定义值），MMDC 将自动执行以下步骤：

1. MMDC 等待，直到读延迟线更新为所有字节的绝对延迟值（在 MPRDDLCTL[RD_DL_ABS_OFFSETn] 中），并满足 Tmod + 4 要求。
2. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPRDDLHWCTL[HW_RD_DL_CMP_CYC]），假定数据已从 DDR 器件到达。
3. MMDC 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则表明初始读 DQS 不在读 DQ 窗口内，MMDC 在 MPRDDLHWCTL[HW_RD_DL_ERRn] 中为相应字节生成错误。如果比较通过，则 MMDC 进入下一步。
4. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。
5. MMDC 将每个字节的读延迟线绝对偏移递减 1（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]），并启动读延迟线的测量过程以使用新值更新自身。
6. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPRDDLHWCTL[HW_RD_DL_CMP_CYC]），假定数据已从 DDR 器件到达。
7. MMDC 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则将每个字节的读低边界存储在 MPRDDLHWST0/1[HW_RD_DL_LOWn] 中。如果比较通过，则 MMDC 重复步骤 4-6。如果所有读数据比较都失败，则 MMDC 进入下一步。
8. MMDC 开始寻找上边界，将每个字节的读延迟线绝对偏移设置为步骤 4 中确定的初始值加 1，并启动读延迟线的测量过程以使用新值更新自身。
9. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义值）及其指针。
10. MMDC 向外部 DDR 器件发出读命令，并等待 16 或 32 个周期（根据 MPRDDLHWCTL[HW_RD_DL_CMP_CYC]），假定数据已从 DDR 器件到达。
11. MMDC 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则将每个字节的读上边界存储在 MPRDDLHWST0/1[HW_RD_DL_UPn] 中。如果比较通过，则 MMDC 将每个字节的读延迟线绝对偏移递增 1（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]），并启动读延迟线的测量过程以使用新值更新自身。
12. 如果所有读数据比较都失败，则 MMDC 进入下一步。否则，MMDC 重复步骤 9-11。
13. 在 MMDC 找到每个读数据字节的窗口边界（下边界和上边界）后，它将下边界和上边界之间的平均值存储到相应的 MPRDDLCTL[RD_DL_ABS_OFFSETn] 中，并启动读延迟线的测量过程以使用新值更新自身。
14. MMDC 通过设置 MPRDDLHWCTL[HW_RD_DL_EN] = 0 指示读数据校准已完成。
15. 通过 MRS/MRW 命令将 DDR 器件退出 MPR/DQ 校准模式。

# 35.11.4.2 SW 读校准

有两种操作模式：

• 使用 MPR（多功能寄存器）/DQ 校准（LPDDR2）校准
• 使用 MMDC 预定义值校准

# 35.11.4.2.1 使用 MPR/DQ 校准的校准

执行以下步骤：

1. 预充电所有活动 Bank（可通过 MDSCR 完成），按标准要求。
2. 通过 MRS/MRW 命令将 DDR 器件进入 MPR/DQ 校准模式。
3. 通过断言 MPPDCMPR2[MPR_CMP] 配置 MMDC 以使用 MPR/DQ 校准模式工作。
4. 确保每个字节的读延迟线绝对偏移中配置的初始值（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）将读 DQS 放置在读 DQ 窗口内的某处。

# 35.11.4.2.2 使用预定义值的校准

如果使用预定义模式（即 MPPDCMPR2[MPR_CMP] 被清除），则应执行以下步骤：

1. 预充电所有活动 Bank（可通过 MDSCR 完成），按标准要求。
2. 将预定义值（该值反映将通过读校准写入和比较的值）配置到 MPPDCMPR1[PDV1, PDV2]。

# 校准过程

3. 向外部 DDR 器件发出写访问（使用任何合法的 DDR 地址）。
4. 确保每个字节的读延迟线绝对偏移中配置的初始值（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）将读 DQS 放置在读 DQ 窗口内的某处。

对于两种模式（MPR/DQ 校准和预定义值），将由 SW 手动执行以下步骤：

1. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的读延迟。
2. 等待 16 个 DDR 周期，直到读延迟线更新为所有字节的绝对延迟值。
3. 从外部 DDR 器件发出读命令（使用任何合法的 DDR 地址）。
4. 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则表明初始读 DQS 不在读 DQ 窗口内。如果比较通过，则进入下一步。
5. 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。
6. 将每个字节的读延迟线绝对偏移递减 1（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）。
7. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的读延迟。
8. 从外部 DDR 器件发出读命令（使用步骤 7 中选择的合法 DDR 地址），并等待 16 或 32 个周期（根据 MPRDDLHWCTL[HW_RD_DL_CMP_CYC]），假定数据已从 DDR 器件到达。
9. 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则需要存储每个字节的读低边界。如果比较通过，则重复步骤 5-8。如果所有读数据比较都失败，则进入下一步。
10. 开始寻找上边界，将每个字节的读延迟线绝对偏移设置为步骤 4 中确定的初始值加 1。
11. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的读延迟。
12. 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义/MPR 值）及其指针。
13. 从外部 DDR 器件发出读命令（使用步骤 7 中选择的合法 DDR 地址）。
14. 将读数据字节与预定义/MPR 值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则需要存储每个字节的读上边界。如果比较通过，则将每个字节的读延迟线绝对偏移递增 1（即 MPRDDLCTL[RD_DL_ABS_OFFSETn]）。
15. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的读延迟。
16. 如果所有读数据比较都失败，则进入下一步；否则重复步骤 12-15。
17. 在找到每个读数据字节的窗口边界（下边界和上边界）后，计算下边界和上边界之间的平均值，并将相应的平均值存储到 MPRDDLCTL[RD_DL_ABS_OFFSETn] 中。
18. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的读延迟。
19. 通过 MRS/MRW 命令将 DDR 器件退出 MPR/DQ 校准模式。

# 35.11.5 写校准

写校准用于调整写 DQS 与写数据字节。假设读校准过程在写校准之前完成。

# 注意

在 DDR3_x64 和 LP2_1ch_x64 模式下，通过设置 MPWRDLHWCTL0[HW_WR_DL_EN] 激活校准。

# 注意

在 LP2_x16、LP2_x32 模式下，每个通道的校准通过设置 MPWRDLHWCTL0[HW_WR_DL_EN] 激活。

# 35.11.5.1 HW（自动）写校准

应执行以下步骤：

1. 确保每个字节的写延迟线绝对偏移中配置的初始值（即 MPWRDLCTL[WR_DL_ABS_OFFSET#]）将写 DQS 放置在写 DQ 窗口内的某处。
2. 将预定义值（该值反映将通过写校准写入和比较的值）配置到 MPPDCMPR1[PDV1, PDV2]。

# 校准过程

3. 断言 MPWRDLHWCTL0[HW_WR_DL_EN]。

将自动执行以下步骤：

4. MMDC 等待，直到写延迟线更新为所有字节的绝对延迟值（在 MPWRDCTL[WR_DL_ABS_OFFSET#] 中）。
5. MMDC 向外部 DDR 器件发出写命令（到 Bank 0 地址 0），并等待 16 或 32 个周期（根据 MPWRDLHWCTL[HW_WR_DL_CMP_CYC]），假定数据已到达 DDR 器件。
6. MMDC 从外部 DDR 器件向同一地址发出读命令。
7. MMDC 将读数据字节与预定义值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则表明初始写 DQS 不在写 DQ 窗口内，MMDC 在 MPWRDLHWCTL[HW_WR_DL_ERR#] 中为相应字节生成错误。如果比较通过，则 MMDC 进入下一步。
8. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义值）及其指针。
9. MMDC 将每个字节的写延迟线绝对偏移递减 1（即 MPWRDLCTL[WR_DL_ABS_OFFSET#]），并启动写延迟线的测量过程以使用新值更新自身。
10. MMDC 向外部 DDR 器件发出写命令（到 Bank 0 地址 0），并等待 16 或 32 个周期（根据 MPWRDLHWCTL[HW_WR_DL_CMP_CYC]），假定数据已到达 DDR 器件。
11. MMDC 从外部 DDR 器件向同一地址发出读命令。
12. MMDC 将读数据字节与预定义值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则将每个字节的写低边界存储在 MPWRDLHWST0/1[HW_WR_DL_LOW#] 中。如果比较通过，则 MMDC 重复步骤 8-11。如果所有数据比较都失败，则 MMDC 进入下一步。
13. MMDC 开始寻找上边界，将每个字节的写延迟线绝对偏移设置为步骤 4 中确定的初始值加 1，并启动写延迟线的测量过程以使用新值更新自身。
14. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义值）及其指针。
15. MMDC 向外部 DDR 器件发出写命令（到 Bank 0 地址 0），并等待 16 或 32 个周期（根据 MPWRDLHWCTL[HW_WR_DL_CMP_CYC]），假定数据已到达 DDR 器件。
16. MMDC 从外部 DDR 器件向同一地址发出读命令。
17. MMDC 将读数据字节与预定义值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则将每个字节的写上边界存储在 MPWRDLHWST0/1[HW_WR_DL_UP#] 中。如果比较通过，则 MMDC 将每个字节的写延迟线绝对偏移递增 1（即 MPWRDLCTL[WR_DL_ABS_OFFSET#]），并启动写延迟线的测量过程以使用新值更新自身。
18. MMDC 重复步骤 14-17。如果所有数据比较都失败，则 MMDC 进入下一步。
19. 在 MMDC 找到每个写数据字节的窗口边界（下边界和上边界）后，它将下边界和上边界之间的平均值存储到相应的 MPWRDLCTL[WR_DL_ABS_OFFSET#] 中，并启动写延迟线的测量过程以使用新值更新自身。
20. MMDC 通过设置 MPWRDLHWCTL[HW_WR_DL_EN] = 0 指示写数据校准已完成。

# 35.11.5.2 SW 写校准

应执行以下步骤：

# 注意

建议使用 HW 方法进行写校准。SW 方法仅用于调试目的。

1. 确保每个字节的写延迟线绝对偏移中配置的初始值（即 MPWRDLCTL[WR_DL_ABS_OFFSETn]）将写 DQS 放置在写 DQ 窗口内的某处。
2. 将预定义值（该值反映将通过写校准写入和比较的值）配置到 MPPDCMPR1[PDV1, PDV2]。
3. 通过配置 MPMUR0[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写延迟。
4. 等待 16 个 DDR 周期，直到写延迟线更新为所有字节的绝对延迟值。
5. 向外部 DDR 器件的任意合法 DDR 地址发出写命令。
6. 从外部 DDR 器件向之前写入的地址发出读命令。
7. 将读数据字节与预定义值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则表明初始写 DQS 不在写 DQ 窗口内。如果比较通过，则进入下一步。
8. MMDC 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义值）及其指针。

# 校准过程

9. 将每个字节的写延迟线绝对偏移递减 1（即 MPWRDLCTL[WR_DL_ABS_OFFSETn]）。
10. 通过配置 MPMUR0[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写延迟。
11. 向外部 DDR 器件的任意合法 DDR 地址发出写命令。
12. 从外部 DDR 器件向之前写入的地址发出读命令。
13. 将读数据字节与预定义值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则需要将每个字节的写低边界存储在 MPWRDLHWST0/1[HW_WR_DL_LOWn] 中。如果比较通过，则重复步骤 8-12。如果所有数据比较都失败，则进入下一步。
14. 开始寻找上边界，将每个字节的写延迟线绝对偏移设置为初始值加 1。
15. 通过配置 MPMUR0[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写延迟。
16. 通过设置 MPDGCTRL[RST_RD_FIFO] = 1 复位读 FIFO（反相的预定义值）及其指针。
17. 向外部 DDR 器件的任意合法 DDR 地址发出写命令。
18. 从外部 DDR 器件向之前写入的地址发出读命令。
19. 将读数据字节与预定义值中的相应字节进行比较（针对 DDR 突发中的所有字节，突发长度 4 或 8）。如果比较失败，则需要将每个字节的写上边界存储在 MPWRDLHWST0/1[HW_WR_DL_UPn] 中。如果比较通过，则将每个字节的写延迟线绝对偏移递增 1。
20. 通过配置 MPMUR0[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写延迟。
21. 如果所有读数据比较都失败，则进入下一步；否则重复步骤 16-20。
22. 在找到每个写数据字节的窗口边界（下边界和上边界）后，计算下边界和上边界之间的平均值，并将相应的平均值存储到 MPWRDLCTL[WR_DL_ABS_OFFSETn] 中。
23. 通过配置 MPMUR0[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写延迟。

# 35.11.6 写电平校准

写电平校准可以产生时钟与相关 DQS 之间最多 3 个周期的延迟，计算方式如下：(WL_DL_ABS_OFFSET/256*cycle) + (WL_HC_DEL*半周期) + (WL_CYC_DEL*周期)。写电平校准可以自动（HW）或手动（SW）执行。

自动校准过程只能检测到 1 个周期内的最佳 DQS 到时钟延迟。在极端情况下（DDR3 存储器远离微控制器，即地址/命令/时钟走线较长），DQS 与时钟之间的偏移可能超过 1 个周期。如果发生这种情况，用户需要理解其设计导致 DQS 到时钟偏移超过 1 个周期，并在 MPWLDECTRL0/1[WL_CYC_DEL#] 中手动指示。强烈建议将 DDR3 存储器尽可能靠近微控制器放置，尤其是在嵌入式系统设计中。当使用菊花链拓扑时，用户应计算时钟信号到最远 DDR3 存储器的 PCB 飞行时间，以确保 DQS 与时钟之间的偏移小于 1 个周期。

# 注意

在 LPDDR2 模式下，应禁用写电平校准。

# 35.11.6.1 硬件写电平校准

应执行以下步骤：

1. 通过 MRS 命令配置外部 DDR 器件进入写电平模式。
2. 通过设置 MDSCR[WL_EN] 激活 DQS 输出使能。
3. 通过设置 MPWLGCR[HW_WL_EN] 激活自动校准。

MMDC 将自动执行以下步骤：

4. MMDC 进入写电平模式，计数 25 + 15 个周期，将 DQS 焊盘驱动为输出，而 DQ 焊盘保持输入。同时，MMDC 将写电平延迟线配置为"0"（即 MPWLDECTRL0[WL_DL_ABS_OFFSET#] = 0），并启动写电平延迟线的测量过程以使用新值更新自身。
5. MMDC 向外部 DDR 器件驱动一个 DQS 脉冲。
6. MMDC 等待 16 个周期（以确保 DQ 原始数据稳定），然后采样相应的原始 DQ 位（例如对于 DQS1，MMDC 采样 DQ[8]）。
7. MMDC 将写电平延迟线递增 1/8 周期，并执行测量过程以将更新后的值加载到相应的延迟线。

# 校准过程

8. MMDC 重复步骤 5-7，直到写电平延迟达到 1 个周期。
9. MMDC 检查每个 DQS 的 8 位原始 DQ 结果，并找到从 0 到 1 的第一次跳变。如果未找到跳变，则 MMDC 在 MPWLGCR[HW_WL_ERR#] 中指示错误。
10. MMDC 存储跳变前在原始 DQ 上产生最后一个"0"的值，并将其加载到写电平延迟线。MMDC 启动微调过程，将延迟线值递增 1 步（即 1/256 周期），直到检测到最精确的从 0 到 1 的跳变。
11. 此过程完成后，MMDC 取消断言 MPWLGCR[HW_WL_EN]，并将最精确的延迟线值更新到相应的 MPWLDECTRL#[WL_DL_ABS_OFFSET#] 中。
12. MMDC 执行测量过程，以将最精确的值加载到相应的延迟线。
13. 用户应发出 MRS 命令以退出写电平模式。
14. 用户应读取相应延迟线的结果（MPWLDECTRL#[WL_DL_ABS_OFFSET#]），如果用户估计合理延迟可能超过 1 个周期，则应在 MPWLDECTRL#[WL_CYC_DEL#] 中指示。此外，用户还应在 MDMISC[WALAT] 字段中指示。例如，如果写电平校准的结果是 100/256 周期，但用户估计延迟超过 2 个周期，则应将 MPWLDECTRL#[WL_CYC_DEL#] 配置为 2，因此总延迟为 2 又 100/256 周期。
15. 通过取消断言 MDSCR[WL_EN] 将 DQS 输出使能返回到功能模式。

# 35.11.6.2 SW 写电平校准

应执行以下步骤：

# 注意

建议使用 HW 方法进行写校准。SW 方法仅用于调试目的。

1. 通过 MRS 命令配置外部 DDR 器件进入写电平模式。
2. 通过设置 MDSCR[WL_EN] 激活 DQS 输出使能。
3. 通过配置 MPWLDECTRL0[WL_DL_ABS_OFFSET#] = 0 将写电平延迟线偏移设置为"0"。
4. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写电平延迟。
5. 通过设置 MPWLGCR[SW_WL_EN] = 1 和 MPWLGCR[SW_WL_CNT_EN] = 1 激活 SW 写电平校准并发出一个 DQS 脉冲。
6. 从 MPWLGCR 发出 IP 读命令。如果 MPWLGCR[SW_WL_EN] = 0，则 SW 写电平结果在 MPWLGCR[WL_SW_RES#] 中有效。
7. 将写电平延迟线递增 1/8 周期——即将 0x20 加到 {MPWLDECTRL0[WL_HC_DEL#], MPWLDECTRL0[WL_DL_ABS_OFFSET#]}。
8. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写电平延迟。
9. 通过设置 MPWLGCR[SW_WL_EN] = 1 激活 SW 写电平校准并发出一个 DQS 脉冲。
10. 重复步骤 6-9，直到检测到 CK 的边沿（即写电平结果从"0"切换到"1"）。
11. 存储跳变前在原始 DQ 上产生最后一个"0"的值，将其加载到写电平延迟线，并开始微调过程以检测从"0"到"1"的精确切换点。
12. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写电平延迟。
13. 通过设置 MPWLGCR[SW_WL_EN] = 1 激活 SW 写电平校准并发出一个 DQS 脉冲。
14. 从 MPWLGCR 发出 IP 读命令。如果 MPWLGCR[SW_WL_EN] = 0，则 SW 写电平结果在 MPWLGCR[WL_SW_RES#] 中有效。
15. 将写电平延迟线递增 1 步（即将 0x01 加到 MPWLDECTRL0[WL_DL_ABS_OFFSET#]）。
16. 通过配置 MPMUR[FRC_MSR] = 1 强制延迟线测量自身并发出请求的写电平延迟。
17. 从 MPWLGCR 发出 IP 读命令。如果 MPWLGCR[SW_WL_EN] = 0，则 SW 写电平结果在 MPWLGCR[WL_SW_RES#] 中有效。
18. 通过设置 MPWLGCR[SW_WL_EN] = 1 激活 SW 写电平校准并发出一个 DQS 脉冲。
19. 重复步骤 15-18，直到检测到 CK 的精确边沿（即写电平结果从"0"切换到"1"）。
20. 发出 MRS 命令以退出写电平模式。
21. 通过取消断言 MDSCR[WL_EN] 将 DQS 输出使能返回到功能模式。

# 35.11.7 写微调

写微调是一个附加电路，可对每个 DQ/DM 位（相对于 DQS）的时序进行最多 100 ps 的微调。要使用写微调，选择每个 DQ/DM I/O 中的延迟单元数（最多 3 个延迟单元，每个约 30-35 ps）。延迟可以独立配置。此配置由 MPWRDQBYnDL 寄存器控制。

# 35.11.8 读微调

读微调是一个附加电路，可对每个输入 DQ 位（相对于输入 DQS）的时序进行最多 +/-100 ps 的微调。通过将输入 rd_dqs 的延迟减少 100 ps 并为每个 DQ 输入添加最多 200 ps 的可配置延迟（6 个延迟单元，每个约 30-35 ps）来实现。延迟可以独立配置。由 MPRDDQBY#DL 寄存器控制。

# 35.11.9 ZQ 微调

可以在 ZQ 校准过程确定的 PU/PD 值上添加一个偏移量。偏移范围可从 -7 到 +7，由 MMDC_MPPDCMPR2[ZQ_PU_OFFSET] 和 MMDC_MPPDCMPR2[ZQ_PD_OFFSET] 字段控制。由 MMDC_MPPDCMPR2[ZQ_OFFSET_EN] 使能/禁用。

# 35.11.10 占空比调整

可以对 SDCLKx 和 SDQSx 信号进行占空比调整，详见 MMDCx_MPDCCR 寄存器。

# 35.12 MMDC 内存映射/寄存器定义

内存映射如下所示。

# 注意

术语"时钟"和"周期"可互换使用，均指主 DDR 时钟（mmdc_axi_clk_root）的时钟周期，通常称为 DDR 频率。

MMDC 内存映射

<table><tr><td>绝对地址（十六进制）</td><td>寄存器名称</td><td>宽度（位）</td><td>访问</td><td>复位值</td><td>章节/页</td></tr><tr><td>21B_0000</td><td>MMDC 内核控制寄存器 (MMDC_MDCTL)</td><td>32</td><td>R/W</td><td>0311_0000h</td><td>35.12.1/2263</td></tr><tr><td>21B_0004</td><td>MMDC 内核电源关控制寄存器 (MMDC_MDPDC)</td><td>32</td><td>R/W</td><td>0003_0012h</td><td>35.12.2/2264</td></tr><tr><td>21B_0008</td><td>MMDC 内核 ODT 时序控制寄存器 (MMDC_MDOTC)</td><td>32</td><td>R/W</td><td>1227_2000h</td><td>35.12.3/2267</td></tr><tr><td>21B_000C</td><td>MMDC 内核时序配置寄存器 0 (MMDC_MDCFG0)</td><td>32</td><td>R/W</td><td>3236_22D3h</td><td>35.12.4/2269</td></tr><tr><td>21B_0010</td><td>MMDC 内核时序配置寄存器 1 (MMDC_MDCFG1)</td><td>32</td><td>R/W</td><td>B6B1_8A23h</td><td>35.12.5/2270</td></tr><tr><td>21B_0014</td><td>MMDC 内核时序配置寄存器 2 (MMDC_MDCFG2)</td><td>32</td><td>R/W</td><td>00C7_0092h</td><td>35.12.6/2273</td></tr><tr><td>21B_0018</td><td>MMDC 内核杂项寄存器 (MMDC_MDMISC)</td><td>32</td><td>R/W</td><td>0000_1600h</td><td>35.12.7/2275</td></tr><tr><td>21B_001C</td><td>MMDC 内核特殊命令寄存器 (MMDC_MDSCR)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.8/2278</td></tr><tr><td>21B_0020</td><td>MMDC 内核刷新控制寄存器 (MMDC_MDREF)</td><td>32</td><td>R/W</td><td>0000_C000h</td><td>35.12.9/2281</td></tr><tr><td>21B_002C</td><td>MMDC 内核读/写命令延迟寄存器 (MMDC_MDRWD)</td><td>32</td><td>R/W</td><td>0F9F_26D2h</td><td>35.12.10/2283</td></tr><tr><td>21B_0030</td><td>MMDC 内核退出复位延迟寄存器 (MMDC_MDOR)</td><td>32</td><td>R/W</td><td>009F_0E0Eh</td><td>35.12.11/2285</td></tr><tr><td>21B_0034</td><td>MMDC 内核 MRR 数据寄存器 (MMDC_MDMRR)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.12/2286</td></tr><tr><td>21B_0038</td><td>MMDC 内核时序配置寄存器 3 (MMDC_MDCFG3LP)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.13/2287</td></tr><tr><td>21B_003C</td><td>MMDC 内核 MR4 降额寄存器 (MMDC_MDMR4)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.14/2289</td></tr><tr><td>21B_0040</td><td>MMDC 内核地址空间分区寄存器 (MMDC_MDASP)</td><td>32</td><td>R/W</td><td>0000_003Fh</td><td>35.12.15/2291</td></tr><tr><td>21B_0400</td><td>MMDC 内核 AXI 重排序控制寄存器 (MMDC_MAARCR)</td><td>32</td><td>R/W</td><td>5142_01F0h</td><td>35.12.16/2292</td></tr><tr><td>21B_0404</td><td>MMDC 内核省电控制和状态寄存器 (MMDC_MAPSR)</td><td>32</td><td>R/W</td><td>0000_1007h</td><td>35.12.17/2294</td></tr><tr><td>21B_0408</td><td>MMDC 内核独占 ID 监视器寄存器 0 (MMDC_MAEXIDR0)</td><td>32</td><td>R/W</td><td>0020_0000h</td><td>35.12.18/2296</td></tr><tr><td>21B_040C</td><td>MMDC 内核独占 ID 监视器寄存器 1 (MMDC_MAEXIDR1)</td><td>32</td><td>R/W</td><td>0060_0040h</td><td>35.12.19/2297</td></tr><tr><td>21B_0410</td><td>MMDC 内核调试和性能分析控制寄存器 0 (MMDC_MADPCR0)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.20/2298</td></tr><tr><td>21B_0414</td><td>MMDC 内核调试和性能分析控制寄存器 1 (MMDC_MADPCR1)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.21/2299</td></tr><tr><td>21B_0418</td><td>MMDC 内核调试和性能分析状态寄存器 0 (MMDC_MADPSR0)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.22/2300</td></tr><tr><td>21B_041C</td><td>MMDC 内核调试和性能分析状态寄存器 1 (MMDC_MADPSR1)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.23/2300</td></tr><tr><td>21B_0420</td><td>MMDC 内核调试和性能分析状态寄存器 2 (MMDC_MADPSR2)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.24/2301</td></tr><tr><td>21B_0424</td><td>MMDC 内核调试和性能分析状态寄存器 3 (MMDC_MADPSR3)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.25/2301</td></tr><tr><td>21B_0428</td><td>MMDC 内核调试和性能分析状态寄存器 4 (MMDC_MADPSR4)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.26/2302</td></tr><tr><td>21B_042C</td><td>MMDC 内核调试和性能分析状态寄存器 5 (MMDC_MADPSR5)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.27/2302</td></tr><tr><td>21B_0430</td><td>MMDC 内核逐步地址寄存器 (MMDC_MASBS0)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.28/2303</td></tr><tr><td>21B_0434</td><td>MMDC 内核逐步地址属性寄存器 (MMDC_MASBS1)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.29/2303</td></tr><tr><td>21B_0440</td><td>MMDC 内核通用寄存器 (MMDC_MAGENP)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.30/2304</td></tr><tr><td>21B_0800</td><td>MMDC PHY ZQ 硬件控制寄存器 (MMDC_MPZQHWCTRL)</td><td>32</td><td>R/W</td><td>A138_0000h</td><td>35.12.31/2305</td></tr><tr><td>21B_0804</td><td>MMDC PHY ZQ 软件控制寄存器 (MMDC_MPZQSWCTRL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.32/2308</td></tr><tr><td>21B_0808</td><td>MMDC PHY 写电平配置和错误状态寄存器 (MMDC_MPWLGCR)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.33/2310</td></tr><tr><td>21B_080C</td><td>MMDC PHY 写电平延迟控制寄存器 0 (MMDC_MPWLDECTRL0)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.34/2313</td></tr><tr><td>21B_0810</td><td>MMDC PHY 写电平延迟控制寄存器 1 (MMDC_MPWLDECTRL1)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.35/2315</td></tr><tr><td>21B_0814</td><td>MMDC PHY 写电平延迟线状态寄存器 (MMDC_MPWLDLST)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.36/2318</td></tr><tr><td>21B_0818</td><td>MMDC PHY ODT 控制寄存器 (MMDC_MPODTCTRL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.37/2319</td></tr><tr><td>21B_081C</td><td>MMDC PHY 读 DQ 字节 0 延迟寄存器 (MMDC_MPRDDQBY0DL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.38/2321</td></tr><tr><td>21B_0820</td><td>MMDC PHY 读 DQ 字节 1 延迟寄存器 (MMDC_MPRDDQBY1DL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.39/2324</td></tr><tr><td>21B_082C</td><td>MMDC PHY 写 DQ 字节 0 延迟寄存器 (MMDC_MPWRDQBY0DL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.40/2327</td></tr><tr><td>21B_0830</td><td>MMDC PHY 写 DQ 字节 1 延迟寄存器 (MMDC_MPWRDQBY1DL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.41/2329</td></tr><tr><td>21B_0834</td><td>MMDC PHY 写 DQ 字节 2 延迟寄存器 (MMDC_MPWRDQBY2DL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.42/2331</td></tr><tr><td>21B_0838</td><td>MMDC PHY 写 DQ 字节 3 延迟寄存器 (MMDC_MPWRDQBY3DL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.43/2333</td></tr><tr><td>21B_083C</td><td>MMDC PHY 读 DQS 门控控制寄存器 0 (MMDC_MPDGCTRL0)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.44/2336</td></tr><tr><td>21B_0840</td><td>MMDC PHY 读 DQS 门控控制寄存器 1 (MMDC_MPDGCTRL1)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.45/2338</td></tr><tr><td>21B_0844</td><td>MMDC PHY 读 DQS 门控延迟线状态寄存器 (MMDC_MPDLST0)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.46/2340</td></tr><tr><td>21B_0848</td><td>MMDC PHY 读延迟线配置寄存器 (MMDC_MPRDDLCTL)</td><td>32</td><td>R/W</td><td>4040_4040h</td><td>35.12.47/2342</td></tr><tr><td>21B_084C</td><td>MMDC PHY 读延迟线状态寄存器 (MMDC_MPRDDLST)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.48/2344</td></tr><tr><td>21B_0850</td><td>MMDC PHY 写延迟线配置寄存器 (MMDC_MPWRDLCTL)</td><td>32</td><td>R/W</td><td>4040_4040h</td><td>35.12.49/2346</td></tr><tr><td>21B_0854</td><td>MMDC PHY 写延迟线状态寄存器 (MMDC_MPWRDLST)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.50/2348</td></tr><tr><td>21B_0858</td><td>MMDC PHY CK 控制寄存器 (MMDC_MPSDCTRL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.51/2349</td></tr><tr><td>21B_085C</td><td>MMDC ZQ LPDDR2 硬件控制寄存器 (MMDC_MPZQLP2CTL)</td><td>32</td><td>R/W</td><td>1B5F_0109h</td><td>35.12.52/2350</td></tr><tr><td>21B_0860</td><td>MMDC PHY 读延迟硬件校准控制寄存器 (MMDC_MPRDDLHWCTL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.53/2352</td></tr><tr><td>21B_0864</td><td>MMDC PHY 写延迟硬件校准控制寄存器 (MMDC_MPWRDLHWCTL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.54/2355</td></tr><tr><td>21B_0868</td><td>MMDC PHY 读延迟硬件校准状态寄存器 0 (MMDC_MPRDDLHWST0)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.55/2357</td></tr><tr><td>21B_0870</td><td>MMDC PHY 写延迟硬件校准状态寄存器 0 (MMDC_MPWRDLHWST0)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.56/2358</td></tr><tr><td>21B_0878</td><td>MMDC PHY 写电平硬件错误寄存器 (MMDC_MPWLHWERR)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.57/2359</td></tr><tr><td>21B_087C</td><td>MMDC PHY 读 DQS 门控硬件状态寄存器 0 (MMDC_MPDLGWST0)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.58/2359</td></tr><tr><td>21B_0880</td><td>MMDC PHY 读 DQS 门控硬件状态寄存器 1 (MMDC_MPDLGWST1)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.59/2360</td></tr><tr><td>21B_0884</td><td>MMDC PHY 读 DQS 门控硬件状态寄存器 2 (MMDC_MPDGHWST2)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.60/2360</td></tr><tr><td>21B_0888</td><td>MMDC PHY 读 DQS 门控硬件状态寄存器 3 (MMDC_MPDGHWST3)</td><td>32</td><td>R</td><td>0000_0000h</td><td>35.12.61/2361</td></tr><tr><td>21B_088C</td><td>MMDC PHY 预定义比较寄存器 1 (MMDC_MPPDCMPR1)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.62/2361</td></tr><tr><td>21B_0890</td><td>MMDC PHY 预定义比较和 CA 延迟线配置寄存器 (MMDC_MPPDCMPR2)</td><td>32</td><td>R/W</td><td>0040_0000h</td><td>35.12.63/2363</td></tr><tr><td>21B_0894</td><td>MMDC PHY 软件伪访问寄存器 (MMDC_MPSWDAR0)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.64/2366</td></tr><tr><td>21B_0898</td><td>MMDC PHY 软件伪读数据寄存器 0 (MMDC_MPSWDRDR0)</td><td>32</td><td>R</td><td>FFFF_FFFFh</td><td>35.12.65/2368</td></tr><tr><td>21B_089C</td><td>MMDC PHY 软件伪读数据寄存器 1 (MMDC_MPSWDRDR1)</td><td>32</td><td>R</td><td>FFFF_FFFFh</td><td>35.12.66/2368</td></tr><tr><td>21B_08A0</td><td>MMDC PHY 软件伪读数据寄存器 2 (MMDC_MPSWDRDR2)</td><td>32</td><td>R</td><td>FFFF_FFFFh</td><td>35.12.67/2369</td></tr><tr><td>21B_08A4</td><td>MMDC PHY 软件伪读数据寄存器 3 (MMDC_MPSWDRDR3)</td><td>32</td><td>R</td><td>FFFF_FFFFh</td><td>35.12.68/2369</td></tr><tr><td>21B_08A8</td><td>MMDC PHY 软件伪读数据寄存器 4 (MMDC_MPSWDRDR4)</td><td>32</td><td>R</td><td>FFFF_FFFFh</td><td>35.12.69/2369</td></tr><tr><td>21B_08AC</td><td>MMDC PHY 软件伪读数据寄存器 5 (MMDC_MPSWDRDR5)</td><td>32</td><td>R</td><td>FFFF_FFFFh</td><td>35.12.70/2370</td></tr><tr><td>21B_08B0</td><td>MMDC PHY 软件伪读数据寄存器 6 (MMDC_MPSWDRDR6)</td><td>32</td><td>R</td><td>FFFF_FFFFh</td><td>35.12.71/2370</td></tr><tr><td>21B_08B4</td><td>MMDC PHY 软件伪读数据寄存器 7 (MMDC_MPSWDRDR7)</td><td>32</td><td>R</td><td>FFFF_FFFFh</td><td>35.12.72/2371</td></tr><tr><td>21B_08B8</td><td>MMDC PHY 测量单元寄存器 (MMDC_MPMUR0)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.73/2371</td></tr><tr><td>21B_08BC</td><td>MMDC 写 CA 延迟线控制器 (MMDC_MPWRCADL)</td><td>32</td><td>R/W</td><td>0000_0000h</td><td>35.12.74/2372</td></tr><tr><td>21B_08C0</td><td>MMDC 占空比控制寄存器 (MMDC_MPDCCR)</td><td>32</td><td>R/W</td><td>2492_2492h</td><td>35.12.75/2374</td></tr></table>

# 35.12.1 MMDC 内核控制寄存器 (MMDC_MDCTL)

地址: 21B_0000h 基址 + 0h 偏移 = 21B_0000h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/cfa64d8d207a1c77424164536b28dfeddd4d4702288c550505bd0728ecff3590.jpg)

# MMDC_MDCTL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 SDE_0</td><td>MMDC 使能 CS0。该位使能/禁止 MMDC 对片选 0 的访问。该位的复位值为"0"（即不会向存储器驱动时钟和时钟使能）。在使能点时，MMDC 将对两个片选执行初始化过程（包括 RESET 和/或 CKE 上的延迟）。初始化长度取决于配置的存储器类型。0 禁用；1 使能</td></tr><tr><td>30 SDE_1</td><td>MMDC 使能 CS1。该位使能/禁止 MMDC 对片选 1 的访问。该位的复位值为"0"（即不会向存储器驱动时钟和时钟使能）。在使能点时，MMDC 将对两个片选执行初始化过程（包括 RESET 和/或 CKE 上的延迟）。初始化长度取决于配置的存储器类型。0 禁用；1 使能</td></tr><tr><td>29-27 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>26-24 ROW</td><td>行地址宽度。该字段指定存储器阵列使用的行地址数。它将影响传入地址的解码方式。设置 110-111 为保留。000 11 位行地址；001 12 位行地址；010 13 位行地址；011 14 位行地址；100 15 位行地址；101 16 位行地址</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>22-20 COL</td><td>列地址宽度。该字段指定存储器阵列使用的列地址数。它将决定传入地址的解码方式。0x0 9位列地址；0x1 10位列地址；0x2 11位列地址；0x3 8位列地址；0x4 12位列地址；0x5-0xF 保留</td></tr><tr><td>19 BL</td><td>突发长度。该字段决定 DDR 器件的突发长度。在 LPDDR2 模式下，MMDC 支持突发长度 4。在 DDR3 模式下，MMDC 支持突发长度 8。0 使用突发长度 4；1 使用突发长度 8</td></tr><tr><td>18 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>17-16 DSIZ</td><td>DDR 数据总线宽度。该字段决定 DDR 存储器的数据总线大小。0 16 位数据总线；1 保留；2-3 保留</td></tr><tr><td>15-0 保留</td><td>此只读字段保留，始终读为 0。</td></tr></table>

# 35.12.2 MMDC 内核电源关控制寄存器 (MMDC_MDPDC)

表 35-10. PRCT 字段编码

<table><tr><td>PRCT[2:0]</td><td>预充电定时器</td></tr><tr><td>000</td><td>禁用（位字段复位值）</td></tr><tr><td>001</td><td>2 个时钟</td></tr><tr><td>010</td><td>4 个时钟</td></tr><tr><td>011</td><td>8 个时钟</td></tr><tr><td>100</td><td>16 个时钟</td></tr><tr><td>101</td><td>32 个时钟</td></tr><tr><td>110</td><td>64 个时钟</td></tr><tr><td>111</td><td>128 个时钟</td></tr></table>

表 35-11. PWDT 字段编码

<table><tr><td>PWDT[3:0]</td><td>电源关超时</td></tr><tr><td>0000</td><td>禁用（位字段复位值）</td></tr><tr><td>0001</td><td>16 个周期</td></tr><tr><td>0010</td><td>32 个周期</td></tr><tr><td>0011</td><td>64 个周期</td></tr><tr><td>0100</td><td>128 个周期</td></tr><tr><td>0101</td><td>256 个周期</td></tr><tr><td>0110</td><td>512 个周期</td></tr><tr><td>0111</td><td>1024 个周期</td></tr><tr><td>1000</td><td>2048 个周期</td></tr><tr><td>1001</td><td>4096 个周期</td></tr><tr><td>1010</td><td>8196 个周期</td></tr><tr><td>1011</td><td>16384 个周期</td></tr><tr><td>1100</td><td>32768 个周期</td></tr><tr><td>1101-1111</td><td>保留</td></tr></table>

地址: 21B_0000h 基址 + 4h 偏移 = 21B_0004h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/abe9107b21b8bf2e968521420650aaf252def4166e1e2522f5d4b85d44aa8834.jpg)

# MMDC_MDPDC 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-28 PRCT_1</td><td>预充电定时器 - 片选 1。该字段决定片选 1 自动预充电前的空闲周期数。周期数根据上述 PRCT 字段编码表确定。</td></tr><tr><td>27 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>26-24 PRCT_0</td><td>预充电定时器 - 片选 0。该字段决定片选 0 自动预充电前的空闲周期数。周期数根据下表确定。</td></tr><tr><td>23-19 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>18-16 tCKE</td><td>CKE 最小脉冲宽度。该字段决定 CKE 的最小脉冲宽度。0x0 1 个周期；0x1 2 个周期；0x6 7 个周期；0x7 8 个周期</td></tr><tr><td>15-12 PWDT_1</td><td>电源关定时器 - 片选 1。该字段决定片选 1 自动进入预充电/活动电源关前的空闲周期数。周期数根据上述 PWDT 字段编码表确定。</td></tr><tr><td>11-8 PWDT_0</td><td>电源关定时器 - 片选 0。该字段决定片选 0 自动进入预充电/活动电源关前的空闲周期数。周期数根据上述 PWDT 字段编码表确定。</td></tr><tr><td>7 SLOW_PD</td><td>慢速/快速电源关。在 DDR3 模式下，该字段指慢速预充电电源关。LPDDR2 模式：该字段不相关，应保持默认复位值。注意：存储器应配置相同。0 快速模式；1 慢速模式</td></tr><tr><td>6 BOTH_CS_PD</td><td>两个片选并行进入电源关。当两个片选都使用电源关定时器时（即 PWDT_0 和 PWDT1 不等于"0"），如果该位使能，MMDC 仅在两个片选都达到空闲周期数时进入电源关。0 每个片选可根据其配置独立进入电源关；1 仅当两个片选都达到空闲周期数时才可进入电源关</td></tr><tr><td>5-3 tCKSRX</td><td>自刷新退出前的有效时钟周期数。该字段决定自刷新退出前的时钟周期数。0x0 0 个周期；0x1 1 个周期；0x6 6 个周期；0x7 7 个周期</td></tr><tr><td>2-0 tCKSRE</td><td>自刷新进入后的有效时钟周期数。该字段决定自刷新进入后的时钟周期数。0x0 0 个周期；0x1 1 个周期；0x6 6 个周期；0x7 7 个周期</td></tr></table>

# 35.12.3 MMDC 内核 ODT 时序控制寄存器 (MMDC_MDOTC)

更多信息请参见 ODT 配置。

地址: 21B_0000h 基址 + 8h 偏移 = 21B_0008h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/624a439b775fcd2f24c0de4cb494d899569e1de54634652aaec88114d3db5efc.jpg)

# MMDC_MDOTC 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-30 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>29-27 tAOFPD</td><td>异步 RTT 关断延迟（DLL 冻结时的电源关）。该字段决定端接电路开始关闭 ODT 电阻到端接达到高阻抗之间的时间。LPDDR2 模式：该字段不相关，应保持默认复位值。0x0 1 个周期；0x1 2 个周期；0x6 7 个周期；0x7 8 个周期</td></tr><tr><td>26-24 tAONPD</td><td>异步 RTT 开启延迟（DLL 冻结时的电源关）。该字段决定端接电路退出高阻抗并开始开启到 ODT 电阻完全开启之间的时间。LPDDR2 模式：该字段不相关，应保持默认复位值。0x0 1 个周期；0x1 2 个周期；0x6 7 个周期；0x7 8 个周期</td></tr><tr><td>23-20 tANPD</td><td>异步 ODT 到电源关进入延迟。在 DDR3 中应设置为 tCWL-1。LPDDR2 模式：该字段不相关，应保持默认复位值。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0xE 15 个时钟；0xF 16 个时钟</td></tr><tr><td>19-16 tAXPD</td><td>异步 ODT 到电源关退出延迟。在 DDR3 中应设置为 tCWL-1。LPDDR2 模式：该字段不相关，应保持默认复位值。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0xE 15 个时钟；0xF 16 个时钟</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-12 tODTLon</td><td>ODT 开启延迟。该字段决定 ODT 信号与相关 RTT 之间的延迟，根据 JEDEC 标准等于 WL - 2。因此 tODTLon 的值应与 MDCGFG1[tCWL] 对应。LPDDR2 模式：不相关。0x0-0x1 保留；0x2 2 个周期；0x3 3 个周期；0x4 4 个周期；0x5 5 个周期；0x6 6 个周期；0x7 保留</td></tr><tr><td>11-9 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>8-4 tODT_idle_off</td><td>ODT 关断延迟。决定关闭存储器 ODT 前的空闲周期数。注意：LPDDR2 模式：不相关。0x0 0 个周期（最早可能的时间）；0x1 1 个周期；0x2 2 个周期；0x1E 30 个周期；0x1F 31 个周期</td></tr><tr><td>3-0 保留</td><td>此只读字段保留，始终读为 0。</td></tr></table>

# 35.12.4 MMDC 内核时序配置寄存器 0 (MMDC_MDCFG0)

地址: 21B_0000h 基址 + Ch 偏移 = 21B_000Ch

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>RW</td><td colspan="8">tRFC</td><td colspan="9">tXS</td><td colspan="2">tXP</td><td colspan="4">tXPDLL</td><td colspan="6">tFAW</td><td colspan="4">tCL</td></tr><tr><td>复位</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td></tr></table>

# MMDC_MDCFG0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-24 tRFC</td><td>刷新命令到激活或刷新命令的时间。详见 DDR3 SDRAM 规范 JESD79-3E 和 LPDDR2 SDRAM 规范 JESD209-2B。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0xFE 255 个时钟；0xFF 256 个时钟</td></tr><tr><td>23-16 tXS</td><td>退出自刷新到非读命令。在 LPDDR2 中称为 tXSR（自刷新退出到下一个有效命令延迟）。详见 DDR3/LPDDR2 SDRAM 规范。0x0-0x15 保留；0x16 23 个时钟；0x17 24 个时钟；0xFE 255 个时钟；0xFF 256 个时钟</td></tr><tr><td>15-13 tXP</td><td>退出 DLL 开启的电源关到任意有效命令。LPDDR2/LPDDR3 中指退出电源关到下一个有效命令延迟。0x0 1 个周期；0x1 2 个周期；0x6 7 个周期；0x7 8 个周期</td></tr><tr><td>12-9 tXPDLL</td><td>退出 DLL 冻结的预充电电源关到需要 DLL 的命令。LPDDR2 模式：不相关。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0xE 15 个时钟；0xF 16 个时钟</td></tr><tr><td>8-4 tFAW</td><td>四激活窗口（所有 Bank）。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0x1E 31 个时钟；0x1F 32 个时钟</td></tr><tr><td>3-0 tCL</td><td>CAS 读延迟。DDR3 中指 CL，LPDDR2 中指 RL。注意 LPDDR2/LPDDR3 只允许 MR2 中指定的 RL/WL 配对。0x0 3 个周期；0x1 4 个周期；0x2 5 个周期；0x3 6 个周期；0x4 7 个周期；0x5 8 个周期；0x6 9 个周期；0x7 10 个周期；0x8 11 个周期；0x9-0xF 保留</td></tr></table>

# 35.12.5 MMDC 内核时序配置寄存器 1 (MMDC_MDCFG1)

地址: 21B_0000h 基址 + 10h 偏移 = 21B_0010h

<table><tr><td rowspan="2">位 R W</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td></tr><tr><td colspan="3">tRCD</td><td colspan="3">tRP</td><td colspan="5">tRC</td><td colspan="5">tRAS</td></tr><tr><td>复位</td><td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td></tr><tr><td rowspan="3">位 R W</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>tRPA</td><td colspan="3">0</td><td rowspan="2" colspan="3">tWR</td><td rowspan="2" colspan="4">tMRD</td><td colspan="2">0</td><td rowspan="2" colspan="3">tCWL</td></tr><tr><td colspan="4"></td><td colspan="2"></td></tr><tr><td>复位</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td></tr></table>

# MMDC_MDCFG1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-29 tRCD</td><td>激活命令到内部读或写延迟时间（同 Bank）。仅对 DDR2/DDR3 有效。LPDDR2/LPDDR3 应在 tRCD_LP 中配置。0x0-0x7 对应 1-8 个时钟</td></tr><tr><td>28-26 tRP</td><td>预充电命令周期（同 Bank）。仅对 DDR2/DDR3 有效。LPDDR2 应在 tRPpb_LP 中配置。0x0-0x7 对应 1-8 个时钟</td></tr><tr><td>25-21 tRC</td><td>激活到激活或刷新命令周期（同 Bank）。仅对 DDR2/DDR3 有效。LPDDR2/LPDDR3 应在 tRC_LP 中配置。0x0-0x1F 对应 1-32 个时钟</td></tr><tr><td>20-16 tRAS</td><td>激活到预充电命令周期（同 Bank）。0x0-0x1E 对应 1-31 个时钟；0x1F 保留</td></tr><tr><td>15 tRPA</td><td>预充电所有命令周期。仅对 DDR2/DDR3 有效。0 等于 tRP；1 等于 tRP+1</td></tr><tr><td>14-12 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>11-9 tWR</td><td>写恢复时间（同 Bank）。0x0-0x7 对应 1-8 个周期</td></tr><tr><td>8-5 tMRD</td><td>模式寄存器设置命令周期（所有 Bank）。DDR3 应设为 max(tMRD,tMOD)。LPDDR2/LPDDR3 应设为 max(tMRR,tMRW)。0x0-0xF 对应 1-16 个时钟</td></tr><tr><td>4-3 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>2-0 tCWL</td><td>CAS 写延迟。DDR3 中指 CWL，LPDDR2/LPDDR3 中指 WL。0x0=2/1周期；0x1=3/2；0x2=4/3；0x3=5/4；0x4=6/5；0x5=7/6；0x6=8/7；0x7 保留（DDR2/DDR3 / LPDDR2/LPDDR3）</td></tr></table>

# 35.12.6 MMDC 内核时序配置寄存器 2 (MMDC_MDCFG2)

地址: 21B_0000h 基址 + 14h 偏移 = 21B_0014h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td colspan="7">0</td><td rowspan="2" colspan="9">tDLLK</td><td colspan="6">0</td><td rowspan="2" colspan="2">tRTP</td><td rowspan="2" colspan="2">tWTR</td><td rowspan="2" colspan="6">tRRD</td></tr><tr><td>W</td><td colspan="7"></td><td colspan="6"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td></tr></table>

# MMDC_MDCFG2 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-25 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>24-16 tDLLK</td><td>DLL 锁定时间。LPDDR2 模式：不相关。0x0 1 个周期；0x1 2 个周期；0x2 3 个周期；0xC7 200 个周期；0x1FE 511 个周期；0x1FF 512 个周期（DDR3 JEDEC 值）</td></tr><tr><td>15-9 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>8-6 tRTP</td><td>内部读命令到预充电命令延迟（同 Bank）。0x0-0x7 对应 1-8 个周期</td></tr><tr><td>5-3 tWTR</td><td>内部写到读命令延迟（同 Bank）。0x0-0x7 对应 1-8 个周期</td></tr><tr><td>2-0 tRRD</td><td>激活到激活命令周期（所有 Bank）。0x0-0x6 对应 1-7 个周期；0x7 保留</td></tr></table>

# 35.12.7 MMDC 内核杂项寄存器 (MMDC_MDMISC)

地址: 21B_0000h 基址 + 18h 偏移 = 21B_0018h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/ca4564d17bfb263f0736943911f7fb6bbcdcfe1094bc92faa1e154ef8f7954d7.jpg)

# MMDC_MDMISC 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 CS0_RDY</td><td>CS0 上外部状态器件。只读状态位，指示外部存储器是否处于唤醒周期。0 器件处于唤醒周期；1 器件已准备好初始化</td></tr><tr><td>30 CS1_RDY</td><td>CS1 上外部状态器件。只读状态位，指示外部存储器是否处于唤醒周期。0 器件处于唤醒周期；1 器件已准备好初始化</td></tr><tr><td>29-22 保留</td><td>保留</td></tr><tr><td>21 CK1_GATING</td><td>门控辅助 DDR 时钟。断言时 MMDC 将禁用辅助 DDR 时钟。0 MMDC 向 DDR 存储器驱动两个时钟；1 MMDC 只向 DDR 存储器驱动一个时钟（CK0）</td></tr><tr><td>20 CALIB_PER_CS</td><td>校准过程的片选编号。决定相关校准目标片选索引。适用于读、写、写电平和读 DQS 门控校准。0 校准目标为 CS0；1 校准目标为 CS1</td></tr><tr><td>19 ADDR_MIRROR</td><td>地址镜像。注意：LPDDR2/LPDDR3 不支持此功能。仅 DDR2/DDR3。0 地址镜像禁用；1 地址镜像使能</td></tr><tr><td>18 LHD</td><td>延迟隐藏禁用。调试功能。设为"1"时 MMDC 一次只处理一个读/写访问。0 延迟隐藏开启；1 延迟隐藏禁用</td></tr><tr><td>17-16 WALAT</td><td>写附加延迟。如果写电平校准指示 CK 与 DQS 之间的延迟超过 1/8 时钟周期，则必须相应配置此字段。0x0 无附加延迟；0x1 1 个周期附加延迟；0x2 2 个周期；0x3 3 个周期</td></tr><tr><td>15-13 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>12 BI_ON</td><td>Bank 交错使能。控制 Bank、行和列地址位的组织方式。0 Bank 不交错，地址解码为 Bank-行-列；1 Bank 交错，地址解码为行-Bank-列</td></tr><tr><td>11 LPDDR2_S2</td><td>LPDDR2 S2 器件类型指示。使用 LPDDR2 时（DDR_TYPE=0x1），指示使用 S2 还是 S4 器件。DDR3 模式下应清零。0x0 LPDDR2-S4；0x1 LPDDR2-S2</td></tr><tr><td>10-9 MIF3_MODE</td><td>命令预测工作模式。决定 MMDC 使用的命令预测级别。00 禁用预测；01 基于第一流水线级有效访问使能预测；10 基于第一流水线级有效访问和 AXI 总线有效访问使能预测；11 基于第一流水线级有效访问、AXI 总线有效访问和访问队列下次未命中使能预测</td></tr><tr><td>8-6 RALAT</td><td>读附加延迟。决定添加到 CAS 延迟和内部延迟的附加读延迟。用于补偿板级/芯片延迟。注意：LPDDR2 模式下内部会额外增加 2 个周期以补偿 tDQSCK 延迟。0x0-0x7 对应 0-7 个周期附加延迟</td></tr><tr><td>5 DDR_4_BANK</td><td>每个 DDR 器件的 Bank 数。设为"1"时 MMDC 使用 4 Bank DDR 器件。0 使用 8 Bank 器件（默认）；1 使用 4 Bank 器件</td></tr><tr><td>4-3 DDR_TYPE</td><td>DDR 类型。决定外部 DDR 器件的类型。0x0 DDR3；0x1 LPDDR2；0x2-0x3 保留</td></tr><tr><td>2 保留</td><td>保留</td></tr><tr><td>1 RST</td><td>软件复位。断言时 MMDC 的内部状态机和寄存器将被初始化。注意：该位断言后自动取消断言。0 无操作；1 向 MMDC 断言复位</td></tr><tr><td>0 保留</td><td>此只读字段保留，始终读为 0。</td></tr></table>

# 35.12.8 MMDC 内核特殊命令寄存器 (MMDC_MDSCR)

该寄存器用于向外部 DDR 器件手动发出特殊命令（如加载模式寄存器、手动自刷新、手动预充电等）。每次写入该寄存器将被解释为一个命令，读取该寄存器将显示最后执行的命令。

每次写入该寄存器将产生一个特殊命令，IP 总线将在特殊命令执行期间断言 ips_xfr_wait。

地址: 21B_0000h 基址 + 1Ch 偏移 = 21B_001Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/4f63025746222820a0b3c72e0ae002a9eeda19d0eae79fd56ccdb455436aa2f3.jpg)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/9294a924ada44489efd7120e567aca00b09afdebeff9eceb709a691fa6ed9ffc.jpg)

# MMDC_MDSCR 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-24 CMD_ADDR_MSB_MR_OP</td><td>命令/地址 MSB。指示命令/地址的高位。在 LPDDR2/LPDDR3 中指示 MRW 操作数</td></tr><tr><td>23-16 CMD_ADDR_LSB_MR_ADDR</td><td>命令/地址 LSB。指示命令/地址的低位。在 LPDDR2/LPDDR3 中指示 MRR/MRW 地址</td></tr><tr><td>15 CON_REQ</td><td>配置请求。设置时 MMDC 将清除待处理的 AXI 访问并阻止进一步 AXI 访问被确认。设置后需轮询 CON_ACK 直到其为"1"。配置完成后必须取消断言此位以处理后续 AXI 访问。注意：该位在复位序列结束时被断言，表示 MMDC 在接受 AXI 访问前等待配置和初始化外部存储器。0 无请求；1 请求配置 MMDC</td></tr><tr><td>14 CON_ACK</td><td>配置应答。设置时允许配置 MMDC IP 寄存器。0 禁止配置 MMDC 寄存器；1 允许配置 MMDC 寄存器</td></tr><tr><td>13-11 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>10 MRR_READ_DATA_VALID</td><td>MRR 读数据有效。指示 MDMRR 寄存器的读数据有效。仅 LPDDR2/LPDDR3 相关。0 MRR 命令断言时清除；1 MRR 数据有效并存储到 MDMRR 寄存器</td></tr><tr><td>9 WL_EN</td><td>DQS 焊盘方向。在写电平校准过程中控制 DQS 焊盘方向。开始前应设为"1"，发送退出命令时应设为"0"。0 退出写电平模式或保持正常模式；1 已发送写电平进入命令</td></tr><tr><td>8-7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-4 CMD</td><td>命令。包含要执行的命令。命令发送到 DDR 存储器后自动清除。注意：应使用 0x5 预充电所有命令，使用 0x1 命令时存储器操作不可预测。0x0 正常操作；0x1 预充电所有（独立于 Bank 状态发送）；0x2 自动刷新命令；0x3 加载模式寄存器命令（DDR2/DDR3）或 MRW 命令（LPDDR2/LPDDR3）；0x4 ZQ 校准；0x5 仅当 Bank 打开时预充电所有；0x6 MRR 命令（LPDDR2/LPDDR3）；0x7 保留</td></tr><tr><td>3 CMD_CS</td><td>片选。决定命令目标片选。0 片选 0；1 片选 1</td></tr><tr><td>2-0 CMD_BA</td><td>Bank 地址。决定所选片选中目标命令的 Bank 地址。0x0-0x7 对应 Bank 地址 0-7</td></tr></table>

# 35.12.9 MMDC 内核刷新控制寄存器 (MMDC_MDREF)

该寄存器决定向 DDR 器件执行的刷新方案。指定刷新周期发生的频率以及每个刷新周期执行的刷新命令数。

表 35-12. REF_SEL = 0 时的刷新率示例

<table><tr><td>REFR[2:0]</td><td>每 64KHz 的刷新命令数</td><td>平均周期刷新率 (tREFI)</td><td>系统刷新周期</td></tr><tr><td>0x0</td><td>1</td><td>15.6 μs</td><td>tRFC</td></tr><tr><td>0x1</td><td>2</td><td>7.8 μs</td><td>2*tRFC</td></tr><tr><td>0x3</td><td>4</td><td>3.9μs</td><td>4*tRFC</td></tr><tr><td>0x7</td><td>8</td><td>1.95 μs</td><td>8*tRFC</td></tr></table>

表 35-13. REF_SEL = 1 时的刷新率示例

<table><tr><td>REFR[2:0]</td><td>每 32KHz 的刷新命令数</td><td>平均周期刷新率 (tREFI)</td><td>系统刷新周期</td></tr><tr><td>0x1</td><td>2</td><td>15.6 μs</td><td>2*tRFC</td></tr><tr><td>0x3</td><td>4</td><td>7.8 μs</td><td>4*tRFC</td></tr><tr><td>0x7</td><td>8</td><td>3.9μs</td><td>8*tRFC</td></tr></table>

表 35-14. REF_SEL = 2 @ 400MHz 时的刷新率示例

<table><tr><td>REFR[2:0]</td><td>每刷新周期的刷新命令数</td><td>REF_CNT</td><td>平均周期刷新率 (tREFI)</td><td>系统刷新周期</td></tr><tr><td>0x0</td><td>1</td><td>0x618</td><td>3.9 μs</td><td>tRFC</td></tr><tr><td>0x1</td><td>2</td><td>0xC30</td><td>3.9 μs</td><td>2*tRFC</td></tr><tr><td>0x2</td><td>3</td><td>0x1248</td><td>3.9μs</td><td>3*tRFC</td></tr><tr><td>0x3</td><td>4</td><td>0x1860</td><td>3.9 μs</td><td>4*tRFC</td></tr></table>

也允许其他刷新配置，上表中的值仅为获得所需平均周期刷新率的示例。只要保持所需的平均周期刷新率（tREFI），所有行将在每个刷新窗口中被刷新。

地址: 21B_0000h 基址 + 20h 偏移 = 21B_0020h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/50ed5ed71d5e1906be7b7004831e490671022d7047112c596a62ffa48545b331.jpg)

# MMDC_MDREF 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-16 REF_CNT</td><td>DDR 时钟周期的刷新计数器。如果 REF_SEL 等于'2'，则每经过本字段配置的 DDR 周期数启动一次刷新周期。0x0 保留；0x1 1 个周期；0xFFFFE 65534 个周期；0xFFFF 65535 个周期</td></tr><tr><td>15-14 REF_SEL</td><td>刷新选择器。选择触发每个刷新周期的时钟源。0 以 64KHz 频率触发周期刷新；1 以 32KHz 频率触发周期刷新；2 每 REF_CNT 字段配置的周期数触发周期刷新；3 不触发刷新周期</td></tr><tr><td>13-11 REFR</td><td>刷新率。决定每个刷新周期发出的刷新命令数。每次刷新命令后 MMDC 在满足 tRFC 周期前不会向 DDR 器件驱动任何命令。0x0-0x7 对应 1-8 次刷新</td></tr><tr><td>10-1 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>0 START_REF</td><td>手动启动刷新周期。设为'1'时 MMDC 根据'REFR'字段配置的刷新命令数立即启动刷新周期。该位自动归零。0 无操作；1 启动刷新周期</td></tr></table>

# 35.12.10 MMDC 内核读/写命令延迟寄存器 (MMDC_MDRWD)

该寄存器决定连续读和写访问之间的延迟。寄存器复位值设置为所需的最小值。

注意：默认值已设为达到最佳效果，不建议修改。

地址: 21B_0000h 基址 + 2Ch 偏移 = 21B_002Ch

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td></tr><tr><td>R</td><td colspan="3">0</td><td rowspan="2" colspan="13">tDAI</td></tr><tr><td>W</td><td colspan="3"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td></tr></table>

<table><tr><td>位</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td>0</td><td rowspan="2" colspan="2">RTW_SAME</td><td rowspan="2" colspan="2">WTR_DIFF</td><td rowspan="2" colspan="3">WTW_DIFF</td><td rowspan="2" colspan="2">RTW_DIFF</td><td rowspan="2" colspan="6">RTR_DIFF</td></tr><tr><td>W</td><td></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td></tr></table>

# MMDC_MDRWD 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-29 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>28-16 tDAI</td><td>器件自动初始化周期（最大值）。注意：仅 LPDDR2 模式相关。0x0 1 个周期；0xF9F 4000 个周期（默认，LPDDR2 的 JEDEC 值，400MHz 时对应 10μs）；0x1FFF 8192 个周期</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-12 RTW_SAME</td><td>相同片选的读到写延迟。控制相同片选读命令到写命令之间的延迟。总延迟：BL/2 + RTW_SAME + (tCL-tCWL) + RALAT。0x0-0x7 对应 0-7 个周期</td></tr><tr><td>11-9 WTR_DIFF</td><td>不同片选的写到读延迟。控制不同片选写命令到读命令之间的延迟。总延迟：BL/2 + WTR_DIFF + (tCL-tCWL) + RALAT。0x0-0x7 对应 0-7 个周期</td></tr><tr><td>8-6 WTW_DIFF</td><td>不同片选的写到写延迟。控制不同片选写命令到写命令之间的延迟。总延迟：BL/2 + WTW_DIFF。0x0-0x7 对应 0-7 个周期</td></tr><tr><td>5-3 RTW_DIFF</td><td>不同片选的读到写延迟。控制不同片选读命令到写命令之间的延迟。总延迟：BL/2 + RTW_DIFF + (tCL-tCWL) + RALAT。0x0-0x7 对应 0-7 个周期</td></tr><tr><td>2-0 RTR_DIFF</td><td>不同片选的读到读延迟。控制不同片选读命令到读命令之间的延迟。总延迟：BL/2 + RTR_DIFF。0x0-0x7 对应 0-7 个周期</td></tr></table>

# 35.12.11 MMDC 内核退出复位延迟寄存器 (MMDC_MDOR)

该寄存器定义 MMDC 退出复位时必须保持的延迟。

地址: 21B_0000h 基址 + 30h 偏移 = 21B_0030h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td colspan="8">0</td><td rowspan="2" colspan="8">tXPR</td><td colspan="2">0</td><td rowspan="2" colspan="5">SDE_to_RST</td><td colspan="2">0</td><td rowspan="2" colspan="8">RST_to_CKE</td></tr><tr><td>W</td><td colspan="8"></td><td colspan="2"></td><td colspan="2"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td><td>1</td><td>0</td></tr></table>

# MMDC_MDOR 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-24 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>23-16 tXPR</td><td>LPDDR2：与此模式无关，应保持默认复位值。DDR3：按时序参数表定义。0x0 保留；0x1 2 个周期；0x2 3 个周期；0xFE 255 个周期；0xFF 256 个周期</td></tr><tr><td>15-14 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>13-8 SDE_to_RST</td><td>DDR3 模式：从 SDE 使能到 DDR reset# 为高的时间。LPDDR2 模式：不相关。注意：该字段每个周期为 15.258 μs。0x0-0x2 保留；0x3 1 个周期；0x4 2 个周期；0x10 14 个周期（DDR3 JEDEC 值，总计 200μs）；0x3E 60 个周期；0x3F 61 个周期</td></tr><tr><td>7-6 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>5-0 RST_to_CKE</td><td>DDR3：从 SDE 使能到 CKE 上升的时间。若 DDR reset# 为低，将等待其变高后再等待此周期直到 CKE 上升（JEDEC 值为 500μs）。LPDDR2：首次 CKE 断言后的空闲时间（JEDEC 值为 200μs）。注意：每个周期为 15.258 μs。0x0-0x2 保留；0x3 1 个周期；0x10 14 个周期（LPDDR2 JEDEC 值，200μs）；0x23 33 个周期（DDR3 JEDEC 值，500μs）；0x3E 60 个周期；0x3F 61 个周期</td></tr></table>

# 35.12.12 MMDC 内核 MRR 数据寄存器 (MMDC_MDMRR)

该寄存器包含发出 MRR 命令后收集的数据。仅当 MDSCR[MRR_READ_DATA_VALID] 为"1"时数据有效。仅 LPDDR2 模式相关。

地址: 21B_0000h 基址 + 34h 偏移 = 21B_0034h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td rowspan="2" colspan="8">保留</td><td rowspan="2" colspan="8">保留</td><td colspan="7">MRR_READ_DATA1</td><td colspan="9">MRR_READ_DATA0</td></tr><tr><td>W</td><td colspan="7"></td><td colspan="8"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MDMRR 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-16 保留</td><td>保留</td></tr><tr><td>15-8 MRR_READ_DATA1</td><td>在 DQ[15:8] 上到达的 MRR 数据</td></tr><tr><td>7-0 MRR_READ_DATA0</td><td>在 DQ[7:0] 上到达的 MRR 数据</td></tr></table>

# 35.12.13 MMDC 内核时序配置寄存器 3 (MMDC_MDCFG3LP)

该寄存器仅 LPDDR2 模式相关。

地址: 21B_0000h 基址 + 38h 偏移 = 21B_0038h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td colspan="10">0</td><td rowspan="2" colspan="7">RC_LP</td><td colspan="4">0</td><td rowspan="2" colspan="3">tRCD_LP</td><td rowspan="2" colspan="3">tRPpb_LP</td><td rowspan="2" colspan="6">tRPab_LP</td></tr><tr><td>W</td><td colspan="10"></td><td colspan="4"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MDCFG3LP 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-22 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>21-16 RC_LP</td><td>激活到激活或刷新命令周期（同 Bank）。仅 LPDDR2 有效。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0x3E 63 个时钟；0x3F 保留</td></tr><tr><td>15-12 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>11-8 tRCD_LP</td><td>激活命令到内部读或写延迟时间（同 Bank）。仅 LPDDR2 有效。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0xE 15 个时钟；0xF 保留</td></tr><tr><td>7-4 tRPpb_LP</td><td>预充电（每 Bank）命令周期（同 Bank）。仅 LPDDR2 有效。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0xE 15 个时钟；0xF 保留</td></tr><tr><td>3-0 tRPab_LP</td><td>预充电（所有 Bank）命令周期。仅 LPDDR2 有效。0x0 1 个时钟；0x1 2 个时钟；0x2 3 个时钟；0xE 15 个时钟；0xF 保留</td></tr></table>

# 35.12.14 MMDC 内核 MR4 降额寄存器 (MMDC_MDMR4)

仅 LPDDR2 模式相关。用于根据 MR4 读取结果（基于存储器温度传感器结果）动态更改某些值。

地址: 21B_0000h 基址 + 3Ch 偏移 = 21B_003Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/2a981aba230803f2b8c9c045174ebdfa1c0b54a2598f619a26ff2c7d518dce4e.jpg)

# MMDC_MDMR4 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-9 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>8 tRRD_DE</td><td>tRRD 降额值。0 使用原始 tRRD；1 tRRD 降额 1 个周期</td></tr><tr><td>7 tRP_DE</td><td>tRP 降额值。0 使用原始 tRP；1 tRP 降额 1 个周期</td></tr><tr><td>6 tRAS_DE</td><td>tRAS 降额值。0 使用原始 tRAS；1 tRAS 降额 1 个周期</td></tr><tr><td>5 tRC_DE</td><td>tRC 降额值。0 使用原始 tRC；1 tRC 降额 1 个周期</td></tr><tr><td>4 tRCD_DE</td><td>tRCD 降额值。0 使用原始 tRCD；1 tRCD 降额 1 个周期</td></tr><tr><td>3-2 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>1 UPDATE_DE_ACK</td><td>更新降额值应答。该只读位在 UPDATE_DE_REQ 断言时清除，在新值生效后设置。</td></tr><tr><td>0 UPDATE_DE_REQ</td><td>更新降额值请求。该读-修改-写字段在请求发出后自动清除。0 无操作；1 请求更新以下值：tRRD、tRCD、tRP、tRC、tRAS 和刷新相关字段（MDREF 寄存器）：REF_CNT、REF_SEL、REFR</td></tr></table>

# 35.12.15 MMDC 内核地址空间分区寄存器 (MMDC_MDASP)

该寄存器定义片选 0 和片选 1 之间的分区。

地址: 21B_0000h 基址 + 40h 偏移 = 21B_0040h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/6bd1f0fe6e32d8c9c2c75b8c53f5ce285c6d5cbe4b7eb06c97158619fc4041bf.jpg)

# MMDC_MDASP 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 CS0_END</td><td>定义与 CS0 关联的绝对最后地址，以 256Mb 为增量。CS0_END = AXI_ADDRESS[31:25] 位。MMDC0_MDASP[CS0_END] 应设置为 DDR_CS_SIZE/32M + 0x3f（通道 0 基址始于 0x80000000）</td></tr></table>

# 35.12.16 MMDC 内核 AXI 重排序控制寄存器 (MMDC_MAARCR)

该寄存器确定用于重排序仲裁引擎的权重值。

地址: 21B_0000h 基址 + 400h 偏移 = 21B_0400h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/4afcc45bcfaee395e63ed665a21ad2e79a26168c8a67952304822853946e5134.jpg)

# MMDC_MAARCR 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 ARCR_SEC_ERR_LOCK</td><td>设置后锁定 ARCR_SEC_ERR_EN 并阻止其更新。只能通过复位清除。默认值 0x0（未锁定）。0 ARCR_SEC_ERR_EN 未锁定，可随时更新；1 ARCR_SEC_ERR_EN 已锁定，无法更新</td></tr><tr><td>30 ARCR_SEC_ERR_EN</td><td>定义安全读/写访问冲突导致 SLV 错误响应还是 OKAY 响应。默认值 0x1（SLV 错误）。0 安全冲突产生 OKAY 响应；1 安全冲突产生 SLV 错误响应</td></tr><tr><td>29 保留</td><td>保留</td></tr><tr><td>28 ARCR_EXC_ERR_EN</td><td>定义 AXI 6.2.4 规则的独占读/写访问冲突导致 SLV 错误还是 OKAY 响应。默认值 0x1（SLV 错误）。0 冲突产生 OKAY 响应；1 冲突产生 SLV 错误响应</td></tr><tr><td>27-25 保留</td><td>保留</td></tr><tr><td>24 ARCR_RCH_EN</td><td>定义实时通道是否激活并绕过所有其他待处理访问。QoS='F'的访问将在优化/重排序机制中获得最高优先级。默认值 0x1（使能）。0 正常优先级，无旁路；1 QoS='F'的访问绕过仲裁</td></tr><tr><td>23 保留</td><td>保留</td></tr><tr><td>22-20 ARCR_PAG_HIT</td><td>ARCR 页面命中率。优化/重排序机制将此值加到目标为打开 DDR 行的待处理访问中。默认值 0x100（编码 4）。</td></tr><tr><td>19 保留</td><td>保留</td></tr><tr><td>18-16 ARCR_ACC_HIT</td><td>ARCR 访问命中率。优化/重排序机制将此值加到与先前访问具有相同访问类型（读/写）的待处理访问中。默认值 0x010（编码 2）。</td></tr><tr><td>15-12 保留</td><td>保留</td></tr><tr><td>11-8 ARCR_DYN_JMP</td><td>ARCR 动态跳跃。每次访问未被优化/重排序机制选中时，其动态分数将增加 ARCR_DYN_JMP 值。注意：设置此值可能导致低优先级访问饥饿。ARCR_DYN_JMP 必须小于 ARCR_DYN_MAX。默认值 0x0001（编码 1）。</td></tr><tr><td>7-4 ARCR_DYN_MAX</td><td>ARCR 动态最大值。优化/重排序机制中每个访问可获得的最大动态分数值。0000 0；1111 15（默认）</td></tr><tr><td>3-0 ARCR_guard</td><td>ARCR 保护。访问达到最大动态分数值后，将等待额外的 ARCR_guard 仲裁周期，然后获得优化/重排序机制中的最高优先级。0000 15（默认）；0001 16；1111 30</td></tr></table>

# 35.12.17 MMDC 内核省电控制和状态寄存器 (MMDC_MAPSR)

MAPSR 决定 MMDC 的省电功能。

注意：请参见芯片特定信息以了解在您器件上的实现。

地址: 21B_0000h 基址 + 404h 偏移 = 21B_0404h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/66416d1ceb85b6bcfb6ff59a48f648a03d725756c015be0996cd6a154ab413bc.jpg)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/177f21892dabdb09af4cb1e4945f17e3c6a9df80f203689c11ca03c31d9cbc07.jpg)

# MMDC_MAPSR 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-26 保留</td><td>保留</td></tr><tr><td>25 DVACK</td><td>DVFS/自刷新应答。只读位，指示 DVFS/自刷新应答是否已断言以及 MMDC 是否处于自刷新模式。</td></tr><tr><td>24 LPACK</td><td>通用低功耗应答。只读位，指示低功耗应答是否已断言以及 MMDC 是否处于自刷新模式。</td></tr><tr><td>23-22 保留</td><td>保留</td></tr><tr><td>21 DVFS</td><td>DVFS/自刷新请求。软件请求 DVFS/自刷新。断言此位将启动自刷新进入序列。0 无 DVFS/自刷新进入请求；1 DVFS/自刷新进入请求</td></tr><tr><td>20 LPMD</td><td>通用 LPMD 请求。软件请求 LPMD。断言此位将产生自刷新进入序列。0 无 lpmd 请求；1 lpmd 请求</td></tr><tr><td>19-16 保留</td><td>保留</td></tr><tr><td>15-8 PST</td><td>自动省电定时器。仅当 PSD 设为"0"时生效。MMDC 空闲达到该字段指定的周期数后，DDR 器件将自动进入自刷新模式。实际使用的值为寄存器值乘以 64。00000000 保留（禁止）；00000001 64 个时钟周期；00000010 128 个时钟周期；00010000（默认）1024 个时钟周期；11111111 16320 个时钟周期</td></tr><tr><td>7 保留</td><td>保留</td></tr><tr><td>6 WIS</td><td>写空闲状态。只读位，指示写请求缓冲器是否空闲（空）。0 非空闲；1 空闲</td></tr><tr><td>5 RIS</td><td>读空闲状态。只读位，指示读请求缓冲器是否空闲（空）。0 非空闲；1 空闲</td></tr><tr><td>4 PSS</td><td>省电状态。只读位，指示 MMDC 是否处于自动省电模式。0 非省电模式；1 省电模式</td></tr><tr><td>3-1 保留</td><td>保留</td></tr><tr><td>0 PSD</td><td>自动省电禁用。PSD 为"0"时（即自动省电使能），PST 激活，MMDC 在达到空闲周期数后自动进入自刷新。注意：校准过程中必须禁用此位（即设为"1"）。0 省电使能；1 省电禁用（默认）</td></tr></table>

# 35.12.18 MMDC 内核独占 ID 监视器寄存器 0 (MMDC_MAEXIDR0)

该寄存器定义要监视的 ID，用于监视器 0 和监视器 1 的独占访问。

地址: 21B_0000h 基址 + 408h 偏移 = 21B_0408h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>RW</td><td colspan="17">EXC_ID_MONITOR1</td><td colspan="16">EXC_ID_MONITOR0</td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MAEXIDR0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-16 EXC_ID_MONITOR1</td><td>定义独占监视器#1 的 ID。默认值 0x0020</td></tr><tr><td>15-0 EXC_ID_MONITOR0</td><td>定义独占监视器#0 的 ID。默认值 0x0000</td></tr></table>

# 35.12.19 MMDC 内核独占 ID 监视器寄存器 1 (MMDC_MAEXIDR1)

该寄存器定义要监视的 ID，用于监视器 2 和监视器 3 的独占访问。

地址: 21B_0000h 基址 + 40Ch 偏移 = 21B_040Ch

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>RW</td><td colspan="17">EXC_ID_MONITOR3</td><td colspan="16">EXC_ID_MONITOR2</td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MAEXIDR1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-16 EXC_ID_MONITOR3</td><td>定义独占监视器#3 的 ID。默认值 0x0060</td></tr><tr><td>15-0 EXC_ID_MONITOR2</td><td>定义独占监视器#2 的 ID。默认值 0x0040</td></tr></table>

# 35.12.20 MMDC 内核调试和性能分析控制寄存器 0 (MMDC_MADPCR0)

地址: 21B_0000h 基址 + 410h 偏移 = 21B_0410h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/d7ac336fabdfcc687e1b55a822955fba1d97196f79b7eaccebe66140f03e1bcf.jpg)

# MMDC_MADPCR0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-10 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>9 SBS</td><td>逐步触发。如果 SBS_EN 设为"1"，则仅当该位设为"1"时才会将 AXI 待处理访问发送到 DDR，否则不会发送任何访问。该位在待处理访问已发向 DDR 器件时清除。1 启动 AXI 待处理访问到 DDR；0 不启动任何访问到 DDR</td></tr><tr><td>8 SBS_EN</td><td>逐步调试使能。使能逐步模式。每次使能此机制时，设置 SBS 为"1"将发送一个待处理 AXI 访问到 DDR，同时其属性将在状态寄存器（MASBS0 和 MASBS1）中观察。0 禁用；1 使能</td></tr><tr><td>7-4 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>3 CYC_OVF</td><td>总性能分析周期计数溢出。性能分析机制使能时（DBG_EN 设为"1"），CYC_COUNT 溢出时断言此位。写 1 清除。0 无溢出；1 溢出</td></tr><tr><td>2 PRF_FRZ</td><td>性能分析冻结。断言时性能分析机制冻结，相关状态寄存器（MADPSR0-MADPSR5）保持当前性能分析值。0 性能分析计数器未冻结；1 性能分析计数器冻结</td></tr><tr><td>1 DBG_RST</td><td>调试和性能分析复位。复位所有调试和性能分析计数器及组件。0 不复位；1 复位</td></tr><tr><td>0 DBG_EN</td><td>调试和性能分析使能。使能调试和性能分析机制。断言时 MMDC 将基于 MADPCR1 中配置的 ID 执行性能分析。PRF_FRZ 断言时性能分析冻结，结果采样到状态寄存器（MADPSR0-MADPSR5）。0 禁用（默认）；1 使能</td></tr></table>

# 35.12.21 MMDC 内核调试和性能分析控制寄存器 1 (MMDC_MADPCR1)

地址: 21B_0000h 基址 + 414h 偏移 = 21B_0414h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R W</td><td colspan="16">PRF_AXI_ID_MASK</td><td colspan="17">PRF_AXI_ID</td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MADPCR1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-16 PRF_AXI_ID_MASK</td><td>性能分析 AXI ID 掩码。此值掩码的 AXI ID 位被选中用于性能分析。1 选中 AXI ID 特定位用于性能分析；0 忽略 AXI ID 特定位（不关心）</td></tr><tr><td>15-0 PRF_AXI_ID</td><td>性能分析 AXI ID。与 PRF_AXI_ID_MASK 进行按位与逻辑运算匹配的 AXI ID 被选中用于性能分析。默认值 0x0，选择所有 ID 进行性能分析</td></tr></table>

# 35.12.22 MMDC 内核调试和性能分析状态寄存器 0 (MMDC_MADPSR0)

地址: 21B_0000h 基址 + 418h 偏移 = 21B_0418h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/34d83b98bf966b33348b7fa2629d36d86d8f71a60280820cc99db9f5cfba8924.jpg)

# MMDC_MADPSR0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 CYC_COUNT</td><td>总性能分析周期计数。反映从 DBG_EN 断言到 PRF_FRZ 断言期间的总周期数（性能分析机制使能时）</td></tr></table>

# 35.12.23 MMDC 内核调试和性能分析状态寄存器 1 (MMDC_MADPSR1)

反映 MMDC 状态机忙碌的总周期数（包括写和读）。可用于 DDR 利用率计算。

地址: 21B_0000h 基址 + 41Ch 偏移 = 21B_041Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/79f327131b948c8efa88dfc113365dfe3d56aaa02023fb22136c61e7eef3ea84.jpg)

# MMDC_MADPSR1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 BUSY_COUNT</td><td>性能分析忙碌周期计数。反映性能分析期间 MMDC 读写状态机忙碌的总周期数。可用于 DDR 利用率计算。忙碌周期指内部状态机非空闲的任何 MMDC 时钟周期。如果 FIFO 中有任何待处理的读或写请求，MMDC 非空闲。</td></tr></table>

# 35.12.24 MMDC 内核调试和性能分析状态寄存器 2 (MMDC_MADPSR2)

反映发向 MMDC 的读访问总数（按 AXI ID）。

地址: 21B_0000h 基址 + 420h 偏移 = 21B_0420h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/c084e8dc5b51973416947ce0981c2249bdf1410bd4de9639eb3aa15d775f31c2.jpg)

# MMDC_MADPSR2 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 RD_ACC_COUNT</td><td>性能分析读访问计数。反映发向 MMDC 的读访问总数（按 AXI ID）。</td></tr></table>

# 35.12.25 MMDC 内核调试和性能分析状态寄存器 3 (MMDC_MADPSR3)

反映发向 MMDC 的写访问总数（按 AXI ID）。

地址: 21B_0000h 基址 + 424h 偏移 = 21B_0424h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/1d4b70a37b677a39fb1e0d976ca887b9b0d8765503656486bfc948cefdab09d9.jpg)

# MMDC_MADPSR3 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 WR_ACC_COUNT</td><td>性能分析写访问计数。反映发向 MMDC 的写访问总数（按 AXI ID）。</td></tr></table>

# 35.12.26 MMDC 内核调试和性能分析状态寄存器 4 (MMDC_MADPSR4)

反映发向 MMDC 的读访问期间传输的字节总数（按 AXI ID）。

地址: 21B_0000h 基址 + 428h 偏移 = 21B_0428h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/ec9234587942d00b0432b63632a0e2623fdfd4550e04bfbbdc3d6f19b63b6567.jpg)

# MMDC_MADPSR4 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 RD_BYTE_COUNT</td><td>性能分析读字节计数。反映发向 MMDC 的读访问期间传输的字节总数（按 AXI ID）。</td></tr></table>

# 35.12.27 MMDC 内核调试和性能分析状态寄存器 5 (MMDC_MADPSR5)

反映发向 MMDC 的写访问期间传输的字节总数（按 AXI ID）。

地址: 21B_0000h 基址 + 42Ch 偏移 = 21B_042Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/89556dd017568c4c72a4895cec1a688369797f64cc5daa42d4ef361a0ddefcd4.jpg)

# MMDC_MADPSR5 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 WR_BYTE_COUNT</td><td>性能分析写字节计数。反映发向 MMDC 的写访问期间传输的字节总数（按 AXI ID）。</td></tr></table>

# 35.12.28 MMDC 内核逐步地址寄存器 (MMDC_MASBS0)

地址: 21B_0000h 基址 + 430h 偏移 = 21B_0430h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/1256bf9fd30dba5ea5f5e34172d76c0b9fc4b99fb3a733341db39157d8cbe597.jpg)

# MMDC_MASBS0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 SBS_ADDR</td><td>逐步地址。在逐步模式下反映待处理请求的地址。</td></tr></table>

# 35.12.29 MMDC 内核逐步地址属性寄存器 (MMDC_MASBS1)

地址: 21B_0000h 基址 + 434h 偏移 = 21B_0434h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/1218427fee0f959191affb7c611b4e9095c34b3191c5109049ec8ecd6c4710aa.jpg)

# MMDC_MASBS1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-16 SBS_AXI_ID</td><td>逐步 AXI ID。在逐步模式下反映待处理请求的 AXI ID。</td></tr><tr><td>15-13 SBS_LEN</td><td>逐步长度。在逐步模式下反映待处理请求的 AXI 长度。000 突发长度 1；001 突发长度 2；111 突发长度 8</td></tr><tr><td>12 SBS_BUFF</td><td>逐步缓冲。在逐步模式下反映待处理请求的 AXI Cache[0]。仅写请求相关。</td></tr><tr><td>11-10 SBS_BURST</td><td>逐步突发类型。反映 AXI 突发类型。00 FIXED；01 INCR 突发；10 WRAP 突发；11 保留</td></tr><tr><td>9-7 SBS_SIZE</td><td>逐步大小。反映 AXI 大小。000 8 位；001 16 位；010 32 位；011 64 位；100 128 位；101-111 保留</td></tr><tr><td>6-4 SBS_PROT</td><td>逐步保护。反映待处理请求的 AXI PROT。</td></tr><tr><td>3-2 SBS_LOCK</td><td>逐步锁定。反映待处理请求的 AXI LOCK。</td></tr><tr><td>1 SBS_TYPE</td><td>逐步请求类型。反映待处理请求的类型（读/写）。0 写；1 读</td></tr><tr><td>0 SBS_VLD</td><td>逐步有效。反映逐步模式下是否有待处理请求。0 无效；1 有效</td></tr></table>

# 35.12.30 MMDC 内核通用寄存器 (MMDC_MAGENP)

32 位通用读/写寄存器。

地址: 21B_0000h 基址 + 440h 偏移 = 21B_0440h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R W</td><td colspan="32">GP31_GP0</td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MAGENP 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 GP31_GP0</td><td>通用读/写位。</td></tr></table>

# 35.12.31 MMDC PHY ZQ 硬件控制寄存器 (MMDC_MPZQHWCTRL)

地址: 21B_0000h 基址 + 800h 偏移 = 21B_0800h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td></tr><tr><td>R</td><td rowspan="2" colspan="5">ZQ_EARLY_COMPARATOR_EN_TIMER</td><td rowspan="2">0</td><td rowspan="2" colspan="3">TZQ_CS</td><td rowspan="2" colspan="3">TZQ_OPEN</td><td rowspan="2" colspan="3">TZQ_INIT</td><td rowspan="2">ZQ_HW_FOR</td></tr><tr><td>W</td></tr><tr><td>复位</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td></tr><tr><td>位</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td colspan="5">ZQ_HW_PD_RES</td><td colspan="5">ZQ_HW_PU_RES</td><td rowspan="2" colspan="4">ZQ_HW_PER</td><td rowspan="2" colspan="2">ZQ_MODE</td></tr><tr><td>W</td><td colspan="5"></td><td colspan="5"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPZQHWCTRL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-27 ZQ_EARLY_COMPARATOR_EN_TIMER</td><td>ZQ 早期比较器使能定时器。该定时器定义 i.MX ZQ 校准焊盘比较器预热与 ZQ 校准过程开始之间的间隔。0x0 - 0x6 保留；0x7 8 个周期；0x14 21 个周期（默认）；0x1E 31 个周期；0x1F 32 个周期</td></tr><tr><td>26 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>25-23 TZQ_CS</td><td>器件 ZQ 短校准时间。该字段保存外部 DDR 器件执行 ZQ 短校准所需的周期数。向 DDR 器件发送命令后，在满足该时间之前不会向 DDR 器件发出进一步访问。注意：在 LPDDR2 中，ZQ 短校准时间取自 MPZQLP2CTL[ZQ_LP2_HW_ZQCS]。注意：此字段不应在 ZQ 校准期间更新。000 保留；001 保留；010 128 个周期（默认）；011 256 个周期；100 512 个周期；101 1024 个周期；110-111 保留</td></tr><tr><td>22-20 TZQ_OPEN</td><td>器件 ZQ 长/操作时间。该字段保存外部 DDR 器件执行 ZQ 长校准所需的周期数（复位后发送的第一个 ZQ 长命令除外）。向 DDR 器件发送命令后，在满足该时间之前不会向 DDR 器件发出进一步访问。注意：在 LPDDR2 中，ZQ 操作时间取自 MPZQLP2CTL[ZQ_LP2_HW_ZQCL]。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPZQHWCTRL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>注意：此字段不应在 ZQ 校准期间更新。</td></tr><tr><td></td><td>000 保留</td></tr><tr><td></td><td>001 保留</td></tr><tr><td></td><td>010 128 个周期</td></tr><tr><td></td><td>011 256 个周期 - 默认（DDR3 的 JEDEC 值）</td></tr><tr><td></td><td>100 512 个周期</td></tr><tr><td></td><td>101 1024 个周期</td></tr><tr><td></td><td>110-111 保留</td></tr><tr><td>19-17 TZQ_INIT</td><td>器件 ZQ 长/初始化时间。该字段保存复位后外部 DDR 器件执行 ZQ 长校准所需的周期数。向 DDR 器件发送命令后，在满足该时间之前不会向 DDR 器件发出进一步访问。</td></tr><tr><td></td><td>注意：在 LPDDR2 中，ZQ 初始化时间取自 MPZQLP2CTL[ZQ_LP2_HW_ZQINIT]。</td></tr><tr><td></td><td>注意：此字段不应在 ZQ 校准期间更新。</td></tr><tr><td></td><td>000 保留</td></tr><tr><td></td><td>001 保留</td></tr><tr><td></td><td>010 128 个周期</td></tr><tr><td></td><td>011 256 个周期</td></tr><tr><td></td><td>100 512 个周期 - 默认（DDR3 的 JEDEC 值）</td></tr><tr><td></td><td>101 1024 个周期</td></tr><tr><td></td><td>110-111 保留</td></tr><tr><td>16 ZQ_HW_FOR</td><td>强制使用 i.MX ZQ 校准焊盘进行 ZQ 自动校准过程。当该位置位时，MMDC 将使用 i.MX ZQ 校准焊盘发起一次 ZQ 自动校准过程。用户有责任在使用 CON_REQ/CON_ACK 机制置位该位之前确保所有对 DDR 的访问已完成。硬件将在 ZQ 校准过程完成后清除该位。该位清除后，ZQ HW 校准上拉和下拉结果（分别为 ZQ_HW_PU_RES 和 ZQ_HW_PD_RES）有效。</td></tr><tr><td></td><td>注意：为使能该位，ZQ_MODE 必须设置为 "1" 或 "3"。</td></tr><tr><td>15-11 ZQ_HW_PD_RES</td><td>ZQ HW 校准下拉结果。该字段保存在使用 i.MX ZQ 校准焊盘的 ZQ 自动校准过程结束时计算出的下拉电阻值。</td></tr><tr><td></td><td>注意：可对此结果应用偏移量，请参见 MMDC_MPPDCMPR2[ZQ_PD_OFFSET]。</td></tr><tr><td></td><td>00000 最大电阻。</td></tr><tr><td></td><td>11111 最小电阻。</td></tr><tr><td>10-6 ZQ_HW_PU_RES</td><td>ZQ 自动校准上拉结果。该字段保存在使用 i.MX ZQ 校准焊盘的 ZQ 自动校准过程结束时计算出的上拉电阻值。</td></tr><tr><td></td><td>注意：可对此结果应用偏移量，请参见 MMDC_MPPDCMPR2[ZQ_PU_OFFSET]。</td></tr><tr><td></td><td>00000 最小电阻。</td></tr><tr><td></td><td>11111 最大电阻。</td></tr><tr><td>5-2 ZQ_HW_PER</td><td>ZQ 周期性校准时间。该字段确定执行周期性 ZQ 校准的频率。该字段适用于 ZQ 短校准和使用 i.MX ZQ 校准焊盘的 ZQ 自动校准过程。每当该定时器到期时，根据 ZQ_MODE，将发起使用 i.MX ZQ 校准焊盘的 ZQ 自动校准过程和/或向外部 DDR 器件发送短/长命令。</td></tr><tr><td></td><td>如果 ZQ_MODE 等于 "00"，则忽略此字段。</td></tr><tr><td></td><td>0000 每 1 毫秒执行一次 ZQ 校准。</td></tr><tr><td></td><td>0001 每 2 毫秒执行一次 ZQ 校准。</td></tr><tr><td></td><td>0010 每 4 毫秒执行一次 ZQ 校准。</td></tr><tr><td></td><td>1010 每 1 秒执行一次 ZQ 校准。</td></tr><tr><td></td><td>1110 每 16 秒执行一次 ZQ 校准。</td></tr><tr><td></td><td>1111 每 32 秒执行一次 ZQ 校准。</td></tr><tr><td>1-0 ZQ_MODE</td><td>ZQ 校准模式：</td></tr><tr><td></td><td>0x0 不发起 ZQ 校准。（默认）</td></tr><tr><td></td><td>0x1 仅在退出自刷新时向 i.MX ZQ 校准焊盘发起 ZQ 校准，同时向外部 DDR 器件发起 ZQ 长命令。</td></tr><tr><td></td><td>0x2 仅周期性地和退出自刷新时向外部 DDR 器件发起 ZQ 校准命令长/短。</td></tr><tr><td></td><td>0x3 周期性地和退出自刷新时向 i.MX ZQ 校准焊盘发起 ZQ 校准，同时向外部 DDR 器件发起 ZQ 校准命令长/短。</td></tr></table>

# 35.12.32 MMDC PHY ZQ 软件控制寄存器 (MMDC_MPZQSWCTRL)

地址: 21B_0000h 基址 + 804h 偏移 = 21B_0804h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/1c5d1a13d17d5c689f2d69aba84ed1764954b860ee6f420c2a0f463cf45c0241.jpg)

# MMDC_MPZQSWCTRL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-18 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>17-16 ZQ_CMP_OUT_SMP</td><td>定义从驱动 ZQ 信号到 ZQ 焊盘到采样比较器使能输出之间的周期数，在执行使用 i.MX ZQ 校准焊盘的 ZQ 校准过程时使用。</td></tr><tr><td></td><td>00 7 个周期</td></tr><tr><td></td><td>01 15 个周期</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPZQSWCTRL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>10 23 个周期；11 31 个周期</td></tr><tr><td>15-14 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>13 USE_ZQ_SW_VAL</td><td>使用软件 ZQ 配置值控制 I/O 焊盘电阻。该位选择是 ZQ SW 值还是 ZQ HW 值将被驱动到 I/O 焊盘电阻控制端。默认情况下该位清零，MMDC 将 HW ZQ 状态位驱动到 I/O 焊盘的电阻控制端。注意：此位不应在 ZQ 校准期间更新。0 字段 ZQ_HW_PD_VAL 和 ZQ_HW_PU_VAL 将被驱动到 I/O 焊盘电阻控制端。1 字段 ZQ_HW_PD_VAL 和 ZQ_SW_PU_VAL 将被驱动到 I/O 焊盘电阻控制端。</td></tr><tr><td>12 ZQ_SW_PD</td><td>ZQ 软件 PU/PD 校准。该位确定校准阶段（PU 或 PD）。0 PU 电阻校准；1 PD 电阻校准</td></tr><tr><td>11-7 ZQ_SW_PD_VAL</td><td>ZQ 软件下拉电阻。该字段确定软件 ZQ 校准期间 PD 电阻的值。00000 最大电阻；11111 最小电阻。</td></tr><tr><td>6-2 ZQ_SW_PU_VAL</td><td>ZQ 软件上拉电阻。该字段确定软件 ZQ 校准期间 PU 电阻的值。00000 最小电阻；11111 最大电阻。</td></tr><tr><td>1 ZQ_SW_RES</td><td>ZQ 软件校准结果。该位反映 ZQ 校准电压比较器的值。0 当前 ZQ 校准电压小于 VDD/2。1 当前 ZQ 校准电压大于 VDD/2。</td></tr><tr><td>0 ZQ_SW_FOR</td><td>ZQ SW 校准使能。该位置位时使能 ZQ SW 校准。硬件在 ZQ SW 校准完成后清除该位。该位清除后，ZQ SW 校准结果（即 ZQ_SW_RES）有效。</td></tr></table>

# 35.12.33 MMDC PHY 写均衡配置和错误状态寄存器 (MMDC_MPWLGCR)

地址: 21B_0000h 基址 + 808h 偏移 = 21B_0808h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/781883882f5f777302d40d8dd8ac22013752210e82ca7c8ff57b1c1bf933593f.jpg)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/99b3b95adff8f89e69c64413c14d01af541550f3d4bc1252b23118433cdc8b7f.jpg)

# MMDC_MPWLGCR 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-12 -</td><td>此字段保留。保留</td></tr><tr><td>11 -</td><td>此字段保留。保留</td></tr><tr><td>10 -</td><td>此字段保留。保留</td></tr><tr><td>9 WL_HW_ERR1</td><td>字节1写均衡硬件校准错误。当在写均衡硬件校准期间在字节1上发现错误时，该位置位。该位仅在写均衡硬件校准完成后有效（即 HW_WL_EN 位被清零）。0 写均衡硬件校准期间在字节1上未发现错误。1 写均衡硬件校准期间在字节1上发现错误。</td></tr><tr><td>8 WL_HW_ERR0</td><td>字节0写均衡硬件校准错误。当在写均衡硬件校准期间在字节0上发现错误时，该位置位。该位仅在写均衡硬件校准完成后有效（即 HW_WL_EN 位被清零）。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWLGCR 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>0 写均衡硬件校准期间在字节0上未发现错误。1 写均衡硬件校准期间在字节0上发现错误。</td></tr><tr><td>7 -</td><td>此字段保留。保留</td></tr><tr><td>6 -</td><td>此字段保留。保留</td></tr><tr><td>5 WL_SW_RES1</td><td>字节1写均衡软件结果。该位反映软件写均衡期间 DDR 器件在 DQ8 上驱动的值。0 软件写均衡期间 DQS1 采样到 CK 为低。1 软件写均衡期间 DQS1 采样到 CK 为高。</td></tr><tr><td>4 WL_SW_RES0</td><td>字节0写均衡软件结果。该位反映软件写均衡期间 DDR 器件在 DQ0 上驱动的值。0 软件写均衡期间 DQS0 采样到 CK 为低。1 软件写均衡期间 DQS0 采样到 CK 为高。</td></tr><tr><td>3 -</td><td>此字段保留。保留</td></tr><tr><td>2 SW_WL_CNT_EN</td><td>软件写均衡倒计时使能。该位置位时，在设置 SW_WL_EN 之后向 DDR 器件驱动 DQS 之前设置（25+15）个周期的固定延迟。应在第一次软件写均衡请求之前并在发出写均衡 MRS 命令之后置位该位。0 MMDC 在发出写均衡 DQS 之前不计数 25+15 个周期。1 MMDC 在发出写均衡 DQS 之前计数 25+15 个周期。</td></tr><tr><td>1 SW_WL_EN</td><td>写均衡软件使能。如果该位置位，则 MMDC 将向 DDR 器件执行一次写均衡迭代（假设已通过 MRS 命令在 DDR 器件中使能了写均衡过程）。硬件在软件写均衡完成后清除该位。该位清除也表示写均衡软件校准结果有效。注意：如果该位和 SW_WL_CNT_EN 都使能，MMDC 在发出软件写均衡 DQS 之前计数 25+15 个周期。</td></tr><tr><td>0 HW_WL_EN</td><td>写均衡硬件（自动）使能。如果该位置位，则 MMDC 将向 DDR 器件执行整个写均衡序列（假设已通过 MRS 命令在 DDR 器件中使能了写均衡过程）。硬件在硬件写均衡完成后清除该位。该位清除也表示写均衡硬件校准结果有效。注意：在发出第一个 DQS 之前，MMDC 自动计数标准要求的 25+15 个周期。</td></tr></table>

# 35.12.34 MMDC PHY 写均衡延迟控制寄存器 0 (MMDC_MPWLDECTRL0)

地址: 21B_0000h 基址 + 80Ch 偏移 = 21B_080Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/1889dbad5307a80795505b56b169bf0044aad138ecbe337ceef02fe98c0598de.jpg)

# MMDC_MPWLDECTRL0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-27 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>26-25 WL_CYC_DEL1</td><td>字节1写均衡周期延迟。该字段指示在相关的 WR_DL_ABS_OFFSET 和 WL_HC_DEL 所指示的延迟基础上，是否增加 1 或 2 个周期的 CK 与写 DQS 之间的延迟。因此总延迟为 (WL_DL_ABS_OFFSET/256*周期) + (WL_HC_DEL*半个周期) + (WL_CYC_DEL*周期)。当软件写均衡使能（即 SW_WL_EN = 1）或硬件写均衡使能（即 HW_WL_EN = 1）时，该值将被直接采用并添加到 WL_DL_OFFSET 和 WL_HC_DEL 所配置的相关延迟中。注意：在硬件写均衡中，此字段不用于指示（如 WL_DL_OFFSET 和 WL_HC_DEL），而是用于配置。0 不添加延迟。1 添加 1 个周期延迟。2 添加 2 个周期延迟。3 保留。</td></tr><tr><td>24 WL_HC_DEL1</td><td>字节1写均衡半周期延迟。该字段指示在相关的 WR_DL_ABS_OFFSET 和 WL_CYC_DEL 所指示的延迟基础上，是否增加半个周期的 CK 与写 DQS 之间的延迟。因此总延迟为 (WL_DL_ABS_OFFSET/256*周期) + (WL_HC_DEL*半个周期) + (WL_CYC_DEL*周期)。当软件写均衡使能（即 SW_WL_EN = 1）时，该值将被直接采用并添加到 WL_DL_OFFSET 和 WL_CYC_DEL 所配置的延迟中。当硬件写均衡使能（即 HW_WL_EN = 1）时，该值将指示（状态）是否向相关的 WL_DL_OFFSET 和 WL_CYC_DEL 添加了半周期延迟。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWLDECTRL0 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>0 不添加延迟。1 添加半周期延迟。</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>22-16 WL_DL_ABS_OFFSET1</td><td>字节1绝对写均衡延迟偏移。该字段指示字节1的 CK 与写 DQS 之间的绝对延迟，精度为时钟周期的分数，最高到半周期。该值与工艺和频率无关。延迟值可使用以下公式计算：(WR_DL_ABS_OFFSET1 / 256) * 时钟周期。当软件写均衡使能（即 SW_WL_EN = 1）时，该值将被直接用于相关的延迟线。当硬件写均衡使能（即 HW_WL_EN = 1）时，该值将指示（状态）写均衡校准结束时相关延迟线的值。注意：延迟线的分辨率可能因器件而异，因此在某些情况下，延迟增加 1 步可能小于延迟线的分辨率。</td></tr><tr><td>15-11 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>10-9 WL_CYC_DEL0</td><td>字节0写均衡周期延迟。该字段指示在相关的 WR_DL_ABS_OFFSET 和 WL_HC_DEL 所指示的延迟基础上，是否增加 1 或 2 个周期的 CK 与写 DQS 之间的延迟。因此总延迟为 (WL_DL_ABS_OFFSET/256*周期) + (WL_HC_DEL*半个周期) + (WL_CYC_DEL*周期)。当软件写均衡使能（即 SW_WL_EN = 1）或硬件写均衡使能（即 HW_WL_EN = 1）时，该值将被直接采用并添加到 WL_DL_OFFSET 和 WL_HC_DEL 所配置的相关延迟中。注意，在硬件写均衡中，此字段不用于指示（如 WL_DL_OFFSET 和 WL_HC_DEL），而是用于配置。0 不添加延迟。1 添加 1 个周期延迟。2 添加 2 个周期延迟。3 保留。</td></tr><tr><td>8 WL_HC_DEL0</td><td>字节0写均衡半周期延迟。该字段指示在相关的 WR_DL_ABS_OFFSET 和 WL_CYC_DEL 所指示的延迟基础上，是否增加半个周期的 CK 与写 DQS 之间的延迟。因此总延迟为 (WL_DL_ABS_OFFSET/256*周期) + (WL_HC_DEL*半个周期) + (WL_CYC_DEL*周期)。当软件写均衡使能（即 SW_WL_EN = 1）时，该值将被直接采用并添加到 WL_DL_OFFSET 和 WL_CYC_DEL 所配置的延迟中。当硬件写均衡使能（即 HW_WL_EN = 1）时，该值将指示（状态）是否向相关的 WL_DL_OFFSET 和 WL_CYC_DEL 添加了半周期延迟。0 不添加延迟。1 添加半周期延迟。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 WL_DL_ABS_OFFSET0</td><td>字节0绝对写均衡延迟偏移。该字段指示字节0的 CK 与写 DQS 之间的绝对延迟，精度为时钟周期的分数，最高到半周期。该值与工艺和频率无关。延迟值可使用以下公式计算：(WR_DL_ABS_OFFSET0 / 256) * 时钟周期。</td></tr><tr><td rowspan="2"></td><td>当软件写均衡使能（即 SW_WL_EN = 1）时，该值将被直接用于相关的延迟线。当硬件写均衡使能（即 HW_WL_EN = 1）时，该值将指示（状态）写均衡校准结束时相关延迟线的值。</td></tr><tr><td>注意：延迟线的分辨率可能因器件而异，因此在某些情况下，延迟增加 1 步可能小于延迟线的分辨率。</td></tr></table>

# 35.12.35 MMDC PHY 写均衡延迟控制寄存器 1 (MMDC_MPWLDECTRL1)

地址: 21B_0000h 基址 + 810h 偏移 = 21B_0810h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/514853f13c21421d463b3aa9da0dd15c54186be743604d05f323cb20ab5ded14.jpg)

# MMDC_MPWLDECTRL1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-27 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>26-25 WL_CYC_DEL3</td><td>字节3写均衡周期延迟。该字段指示在相关的 WL_DL_ABS_OFFSET 和 WL_HC_DEL 所指示的延迟基础上，是否增加 1 或 2 个周期的 CK 与写 DQS 之间的延迟。因此总延迟为 (WL_DL_ABS_OFFSET/256*周期) + (WL_HC_DEL*半个周期) + (WL_CYC_DEL*周期)。当软件写均衡使能（即 SW_WL_EN = 1）或硬件写均衡使能（即 HW_WL_EN = 1）时，该值将被直接采用并添加到 WL_DL_OFFSET 和 WL_HC_DEL 所配置的相关延迟中。注意：在硬件写均衡中，此字段不用于指示（如 WL_DL_OFFSET 和 WL_HC_DEL），而是用于配置。0 不添加延迟。1 添加 1 个周期延迟。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWLDECTRL1 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>2 添加 2 个周期延迟。3 保留。</td></tr><tr><td>24 WL_HC_DEL3</td><td>字节3写均衡半周期延迟。该字段指示在相关的 WL_DL_ABS_OFFSET 和 WL_CYC_DEL 所指示的延迟基础上，是否增加半个周期的 CK 与写 DQS 之间的延迟。因此总延迟为 (WL_DL_ABS_OFFSET/256*周期) + (WL_HC_DEL*半个周期) + (WL_CYC_DEL*周期)。当软件写均衡使能（即 SW_WL_EN = 1）时，该值将被直接采用并添加到 WL_DL_OFFSET 和 WL_CYC_DEL 所配置的延迟中。当硬件写均衡使能（即 HW_WL_EN = 1）时，该值将指示（状态）是否向相关的 WL_DL_OFFSET 和 WL_CYC_DEL 添加了半周期延迟。0 不添加延迟。1 添加半周期延迟。</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>22-16 WL_DL_ABS_OFFSET3</td><td>字节3绝对写均衡延迟偏移。该字段指示字节3的 CK 与写 DQS 之间的绝对延迟，精度为时钟周期的分数，最高到半周期。该值与工艺和频率无关。延迟值可使用以下公式计算：(WL_DL_ABS_OFFSET3 / 256) * 时钟周期。当软件写均衡使能（即 SW_WL_EN = 1）时，该值将被直接用于相关的延迟线。当硬件写均衡使能（即 HW_WL_EN = 1）时，该值将指示（状态）写均衡校准结束时相关延迟线的值。注意：延迟线的分辨率可能因器件而异，因此在某些情况下，延迟增加 1 步可能小于延迟线的分辨率。</td></tr><tr><td>15-11 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>10-9 WL_CYC_DEL2</td><td>字节2写均衡周期延迟。该字段指示在相关的 WR_DL_ABS_OFFSET 和 WL_HC_DEL 所指示的延迟基础上，是否增加 1 或 2 个周期的 CK 与写 DQS 之间的延迟。因此总延迟为 (WL_DL_ABS_OFFSET/256*周期) + (WL_HC_DEL*半个周期) + (WL_CYC_DEL*周期)。当软件写均衡使能（即 SW_WL_EN = 1）或硬件写均衡使能（即 HW_WL_EN = 1）时，该值将被直接采用并添加到 WL_DL_OFFSET 和 WL_HC_DEL 所配置的相关延迟中。注意：在硬件写均衡中，此字段不用于指示（如 WL_DL_OFFSET 和 WL_HC_DEL），而是用于配置。0 不添加延迟。1 添加 1 个周期延迟。2 添加 2 个周期延迟。3 保留。</td></tr><tr><td>8 WL_HC_DEL2</td><td>字节2写均衡半周期延迟。该字段指示在相关的 WR_DL_ABS_OFFSET 和 WL_CYC_DEL 所指示的延迟基础上，是否增加半个周期的 CK 与写 DQS 之间的延迟。因此总延迟为 (WL_DL_ABS_OFFSET/256*周期) + (WL_HC_DEL*半个周期) + (WL_CYC_DEL*周期)。当软件写均衡使能（即 SW_WL_EN = 1）时，该值将被直接采用并添加到 WL_DL_OFFSET 和 WL_CYC_DEL 所配置的延迟中。当硬件写均衡使能（即 HW_WL_EN = 1）时，该值将指示（状态）是否向相关的 WL_DL_OFFSET 和 WL_CYC_DEL 添加了半周期延迟。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWLDECTRL1 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>0 不添加延迟。1 添加半周期延迟。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 WL_DL_ABS_OFFSET2</td><td>字节2绝对写均衡延迟偏移。该字段指示字节2的 CK 与写 DQS 之间的绝对延迟，精度为时钟周期的分数，最高到半周期。该值与工艺和频率无关。延迟值可使用以下公式计算：(WR_DL_ABS_OFFSET2 / 256) * 时钟周期。当软件写均衡使能（即 SW_WL_EN = 1）时，该值将被直接用于相关的延迟线。当硬件写均衡使能（即 HW_WL_EN = 1）时，该值将指示（状态）写均衡校准结束时相关延迟线的值。注意：延迟线的分辨率可能因器件而异，因此在某些情况下，延迟增加 1 步可能小于延迟线的分辨率。</td></tr></table>

# 35.12.36 MMDC PHY 写均衡延迟线状态寄存器 (MMDC_MPWLDLST)

该寄存器保存四条写均衡延迟线的状态。

地址: 21B_0000h 基址 + 814h 偏移 = 21B_0814h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/5f7dcc64686a9dfb3dc237f7a9db6f62fbfc5c80dba26af8239d50c907ffb205.jpg)

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

# MMDC_MPWLDLST 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31</td><td>此字段保留。保留</td></tr><tr><td>30-24</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>23</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>22-16</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>15</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>14-8</td><td rowspan="2">该字段反映写均衡延迟线1实际使用的延迟单元数量。</td></tr><tr><td>WL_DL_UNIT_NUM1</td></tr><tr><td>7</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>6-0 WL_DL_UNIT_NUM0</td><td>该字段反映写均衡延迟线0实际使用的延迟单元数量。</td></tr></table>

# 35.12.37 MMDC PHY ODT 控制寄存器 (MMDC_MPODTCTRL)

# 注意

在 LPDDR2 模式下，此寄存器应清零，这样将不会激活端接。

地址: 21B_0000h 基址 + 818h 偏移 = 21B_0818h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/f36dccb47d49b134c8db035266ef8f8c9aaf4b3ebcbc070d07f93303f1bce1ec.jpg)

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

# MMDC_MPODTCTRL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-19 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>18-16 - 保留</td><td>此字段保留。保留</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-12 - 保留</td><td>此字段保留。保留</td></tr><tr><td>11 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>10-8 ODT1_INT_RES</td><td>片内 ODT 字节1电阻 - 该字段确定读访问期间片内 ODT 字节1的 Rtt_Nom。000 Rtt_Nom 禁用；001 Rtt_Nom 120 欧姆；010 Rtt_Nom 60 欧姆；011 Rtt_Nom 40 欧姆；100 Rtt_Nom 30 欧姆；101 Rtt_Nom 24 欧姆；110 Rtt_Nom 20 欧姆；111 Rtt_Nom 17 欧姆</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-4 ODT0_INT_RES</td><td>片内 ODT 字节0电阻 - 该字段确定读访问期间片内 ODT 字节0的 Rtt_Nom。000 Rtt_Nom 禁用；001 Rtt_Nom 120 欧姆；010 Rtt_Nom 60 欧姆；011 Rtt_Nom 40 欧姆；100 Rtt_Nom 30 欧姆；101 Rtt_Nom 24 欧姆；110 Rtt_Nom 20 欧姆；111 Rtt_Nom 17 欧姆</td></tr><tr><td>3 ODT_RD_ACT_EN</td><td>活跃读 CS ODT 使能。该位确定在读访问期间是否将断言活跃 CS 的 ODT 引脚。0 读访问期间活跃 CS ODT 引脚禁用。1 读访问期间活跃 CS ODT 引脚使能。</td></tr><tr><td>2 ODT_RD_PAS_EN</td><td>非活跃读 CS ODT 使能。该位确定在读访问期间是否将断言非活跃 CS 的 ODT 引脚。0 对其他 CS 的读访问期间非活跃 CS ODT 引脚禁用。1 对其他 CS 的读访问期间非活跃 CS ODT 引脚使能。</td></tr><tr><td>1 ODT_WR_ACT_EN</td><td>活跃写 CS ODT 使能。该位确定在写访问期间是否将断言活跃 CS 的 ODT 引脚。</td></tr><tr><td></td><td>0 写访问期间活跃 CS ODT 引脚禁用。1 写访问期间活跃 CS ODT 引脚使能。</td></tr><tr><td>0 ODT_WR_PAS_EN</td><td>非活跃写 CS ODT 使能。该位确定在写访问期间是否将断言非活跃 CS 的 ODT 引脚。0 对其他 CS 的写访问期间非活跃 CS ODT 引脚禁用。1 对其他 CS 的写访问期间非活跃 CS ODT 引脚使能。</td></tr></table>

# 35.12.38 MMDC PHY 读 DQ 字节0延迟寄存器 (MMDC_MPRDDQBY0DL)

该寄存器用于对读 DQ 字节0中相对于读 DQS 的每个比特进行微调调整。此延迟是对读数据校准的补充。如果工作在 64 位模式，则在第二个基地址处映射了一个相同的寄存器。

地址: 21B_0000h 基址 + 81Ch 偏移 = 21B_081Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/2eec15d61afcad77c92288dc510f5425107e284caf91f51825982e1fadb077c7.jpg)

# MMDC_MPRDDQBY0DL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-28 rd_dq7_del</td><td>读 dqs0 到 dq7 延迟微调。该字段保存添加到 dq7（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>000 dq7 延迟不变</td></tr><tr><td></td><td>001 添加 dq7 延迟 1 个延迟单元</td></tr><tr><td></td><td>010 添加 dq7 延迟 2 个延迟单元</td></tr><tr><td></td><td>011 添加 dq7 延迟 3 个延迟单元</td></tr><tr><td></td><td>100 添加 dq7 延迟 4 个延迟单元</td></tr><tr><td></td><td>101 添加 dq7 延迟 5 个延迟单元</td></tr><tr><td></td><td>110 添加 dq7 延迟 6 个延迟单元</td></tr><tr><td></td><td>111 添加 dq7 延迟 7 个延迟单元</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPRDDQBY0DL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td>27 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>26-24 rd_dq6_del</td><td>读 dqs0 到 dq6 延迟微调。该字段保存添加到 dq6（相对于 dqs0）的延迟单元数量。000 dq6 延迟不变；001 添加 dq6 延迟 1 个延迟单元；010 添加 dq6 延迟 2 个延迟单元；011 添加 dq6 延迟 3 个延迟单元；100 添加 dq6 延迟 4 个延迟单元；101 添加 dq6 延迟 5 个延迟单元；110 添加 dq6 延迟 6 个延迟单元；111 添加 dq6 延迟 7 个延迟单元。</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>22-20 rd_dq5_del</td><td>读 dqs0 到 dq5 延迟微调。该字段保存添加到 dq5（相对于 dqs0）的延迟单元数量。000 dq5 延迟不变；001 添加 dq5 延迟 1 个延迟单元；010 添加 dq5 延迟 2 个延迟单元；011 添加 dq5 延迟 3 个延迟单元；100 添加 dq5 延迟 4 个延迟单元；101 添加 dq5 延迟 5 个延迟单元；110 添加 dq5 延迟 6 个延迟单元；111 添加 dq5 延迟 7 个延迟单元。</td></tr><tr><td>19 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>18-16 rd_dq4_del</td><td>读 dqs0 到 dq4 延迟微调。该字段保存添加到 dq4（相对于 dqs0）的延迟单元数量。000 dq4 延迟不变；001 添加 dq4 延迟 1 个延迟单元；010 添加 dq4 延迟 2 个延迟单元；011 添加 dq4 延迟 3 个延迟单元；100 添加 dq4 延迟 4 个延迟单元；101 添加 dq4 延迟 5 个延迟单元；110 添加 dq4 延迟 6 个延迟单元；111 添加 dq4 延迟 7 个延迟单元。</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-12 rd_dq3_del</td><td>读 dqs0 到 dq3 延迟微调。该字段保存添加到 dq3（相对于 dqs0）的延迟单元数量。000 dq3 延迟不变；001 添加 dq3 延迟 1 个延迟单元；010 添加 dq3 延迟 2 个延迟单元；011 添加 dq3 延迟 3 个延迟单元。</td></tr><tr><td></td><td>100 添加 dq3 延迟 4 个延迟单元。</td></tr><tr><td></td><td>101 添加 dq3 延迟 5 个延迟单元。</td></tr><tr><td></td><td>110 添加 dq3 延迟 6 个延迟单元。</td></tr><tr><td></td><td>111 添加 dq3 延迟 7 个延迟单元。</td></tr><tr><td>11 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>10-8 rd_dq2_del</td><td>读 dqs0 到 dq2 延迟微调。该字段保存添加到 dq2（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>000 dq2 延迟不变</td></tr><tr><td></td><td>001 添加 dq2 延迟 1 个延迟单元</td></tr><tr><td></td><td>010 添加 dq2 延迟 2 个延迟单元</td></tr><tr><td></td><td>011 添加 dq2 延迟 3 个延迟单元</td></tr><tr><td></td><td>100 添加 dq2 延迟 4 个延迟单元</td></tr><tr><td></td><td>101 添加 dq2 延迟 5 个延迟单元</td></tr><tr><td></td><td>110 添加 dq2 延迟 6 个延迟单元</td></tr><tr><td></td><td>111 添加 dq2 延迟 7 个延迟单元</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-4 rd_dq1_del</td><td>读 dqs0 到 dq1 延迟微调。该字段保存添加到 dq1（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>000 dq1 延迟不变</td></tr><tr><td></td><td>001 添加 dq1 延迟 1 个延迟单元</td></tr><tr><td></td><td>010 添加 dq1 延迟 2 个延迟单元</td></tr><tr><td></td><td>011 添加 dq1 延迟 3 个延迟单元</td></tr><tr><td></td><td>100 添加 dq1 延迟 4 个延迟单元</td></tr><tr><td></td><td>101 添加 dq1 延迟 5 个延迟单元</td></tr><tr><td></td><td>110 添加 dq1 延迟 6 个延迟单元</td></tr><tr><td></td><td>111 添加 dq1 延迟 7 个延迟单元</td></tr><tr><td>3 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>2-0 rd_dq0_del</td><td>读 dqs0 到 dq0 延迟微调。该字段保存添加到 dq0（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>000 dq0 延迟不变</td></tr><tr><td></td><td>001 添加 dq0 延迟 1 个延迟单元</td></tr><tr><td></td><td>010 添加 dq0 延迟 2 个延迟单元</td></tr><tr><td></td><td>011 添加 dq0 延迟 3 个延迟单元</td></tr><tr><td></td><td>100 添加 dq0 延迟 4 个延迟单元</td></tr><tr><td></td><td>101 添加 dq0 延迟 5 个延迟单元</td></tr><tr><td></td><td>110 添加 dq0 延迟 6 个延迟单元</td></tr><tr><td></td><td>111 添加 dq0 延迟 7 个延迟单元</td></tr></table>

# 35.12.39 MMDC PHY 读 DQ 字节1延迟寄存器 (MMDC_MPRDDQBY1DL)

该寄存器用于对读 DQ 字节1中相对于读 DQS 的每个比特进行微调调整。

地址: 21B_0000h 基址 + 820h 偏移 = 21B_0820h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/74c102b327050fd7ea7a0ff2e9e947cea2a575efcd60a1c20cfbf3e6a9020d0b.jpg)

# MMDC_MPRDDQBY1DL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-28 rd_dq15_del</td><td>读 dqs1 到 dq15 延迟微调。该字段保存添加到 dq15（相对于 dqs1）的延迟单元数量。000 dq15 延迟不变；001 添加 dq15 延迟 1 个延迟单元；010 添加 dq15 延迟 2 个延迟单元；011 添加 dq15 延迟 3 个延迟单元；100 添加 dq15 延迟 4 个延迟单元；101 添加 dq15 延迟 5 个延迟单元；110 添加 dq15 延迟 6 个延迟单元；111 添加 dq15 延迟 7 个延迟单元。</td></tr><tr><td>27 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>26-24 rd_dq14_del</td><td>读 dqs1 到 dq14 延迟微调。该字段保存添加到 dq14（相对于 dqs1）的延迟单元数量。000 dq14 延迟不变；001 添加 dq14 延迟 1 个延迟单元；010 添加 dq14 延迟 2 个延迟单元；011 添加 dq14 延迟 3 个延迟单元；100 添加 dq14 延迟 4 个延迟单元；101 添加 dq14 延迟 5 个延迟单元；110 添加 dq14 延迟 6 个延迟单元；111 添加 dq14 延迟 7 个延迟单元。</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>22-20 rd_dq13_del</td><td>读 dqs1 到 dq13 延迟微调。该字段保存添加到 dq13（相对于 dqs1）的延迟单元数量。000 dq13 延迟不变；001 添加 dq13 延迟 1 个延迟单元；010 添加 dq13 延迟 2 个延迟单元；011 添加 dq13 延迟 3 个延迟单元；100 添加 dq13 延迟 4 个延迟单元；101 添加 dq13 延迟 5 个延迟单元；110 添加 dq13 延迟 6 个延迟单元；111 添加 dq13 延迟 7 个延迟单元。</td></tr><tr><td>19 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>18-16 rd_dq12_del</td><td>读 dqs1 到 dq12 延迟微调。该字段保存添加到 dq12（相对于 dqs1）的延迟单元数量。000 dq12 延迟不变；001 添加 dq12 延迟 1 个延迟单元；010 添加 dq12 延迟 2 个延迟单元；011 添加 dq12 延迟 3 个延迟单元；100 添加 dq12 延迟 4 个延迟单元；101 添加 dq12 延迟 5 个延迟单元；110 添加 dq12 延迟 6 个延迟单元；111 添加 dq12 延迟 7 个延迟单元。</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-12 rd_dq11_del</td><td>读 dqs1 到 dq11 延迟微调。该字段保存添加到 dq11（相对于 dqs1）的延迟单元数量。000 dq11 延迟不变；001 添加 dq11 延迟 1 个延迟单元；010 添加 dq11 延迟 2 个延迟单元；011 添加 dq11 延迟 3 个延迟单元；100 添加 dq11 延迟 4 个延迟单元；101 添加 dq11 延迟 5 个延迟单元；110 添加 dq11 延迟 6 个延迟单元；111 添加 dq11 延迟 7 个延迟单元。</td></tr><tr><td>11 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>10-8 rd_dq10_del</td><td>读 dqs1 到 dq10 延迟微调。该字段保存添加到 dq10（相对于 dqs1）的延迟单元数量。000 dq10 延迟不变；001 添加 dq10 延迟 1 个延迟单元；010 添加 dq10 延迟 2 个延迟单元；011 添加 dq10 延迟 3 个延迟单元。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPRDDQBY1DL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>100 添加 dq10 延迟 4 个延迟单元。</td></tr><tr><td></td><td>101 添加 dq10 延迟 5 个延迟单元</td></tr><tr><td></td><td>110 添加 dq10 延迟 6 个延迟单元。</td></tr><tr><td></td><td>111 添加 dq10 延迟 7 个延迟单元。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-4 rd_dq9_del</td><td>读 dqs1 到 dq9 延迟微调。该字段保存添加到 dq9（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>000 dq9 延迟不变</td></tr><tr><td></td><td>001 添加 dq9 延迟 1 个延迟单元</td></tr><tr><td></td><td>010 添加 dq9 延迟 2 个延迟单元</td></tr><tr><td></td><td>011 添加 dq9 延迟 3 个延迟单元</td></tr><tr><td></td><td>100 添加 dq9 延迟 4 个延迟单元</td></tr><tr><td></td><td>101 添加 dq9 延迟 5 个延迟单元</td></tr><tr><td></td><td>110 添加 dq9 延迟 6 个延迟单元</td></tr><tr><td></td><td>111 添加 dq9 延迟 7 个延迟单元</td></tr><tr><td>3 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>2-0 rd_dq8_del</td><td>读 dqs1 到 dq8 延迟微调。该字段保存添加到 dq8（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>000 dq8 延迟不变</td></tr><tr><td></td><td>001 添加 dq8 延迟 1 个延迟单元</td></tr><tr><td></td><td>010 添加 dq8 延迟 2 个延迟单元</td></tr><tr><td></td><td>011 添加 dq8 延迟 3 个延迟单元</td></tr><tr><td></td><td>100 添加 dq8 延迟 4 个延迟单元</td></tr><tr><td></td><td>101 添加 dq8 延迟 5 个延迟单元</td></tr><tr><td></td><td>110 添加 dq8 延迟 6 个延迟单元</td></tr><tr><td></td><td>111 添加 dq8 延迟 7 个延迟单元</td></tr></table>

# 35.12.40 MMDC PHY 写 DQ 字节0延迟寄存器 (MMDC_MPWRDQBY0DL)

该寄存器用于对写 DQ 字节0中相对于写 DQS 的每个比特进行微调调整。

地址: 21B_0000h 基址 + 82Ch 偏移 = 21B_082Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/6daff70b415555af72e4eadcffeb3d6f472551a834e0872eb654708286e91260.jpg)

# MMDC_MPWRDQBY0DL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td rowspan="5">31-30 wr_dm0_del</td><td>写 dm0 延迟微调。该字段保存添加到 dm0（相对于 dqs0）的延迟单元数量。</td></tr><tr><td>00 dm0 延迟不变</td></tr><tr><td>01 添加 dm0 延迟 1 个延迟单元</td></tr><tr><td>10 添加 dm0 延迟 2 个延迟单元</td></tr><tr><td>11 添加 dm0 延迟 3 个延迟单元</td></tr><tr><td rowspan="5">29-28 wr_dq7_del</td><td>写 dq7 延迟微调。该字段保存添加到 dq7（相对于 dqs0）的延迟单元数量。</td></tr><tr><td>00 dq7 延迟不变</td></tr><tr><td>01 添加 dq7 延迟 1 个延迟单元</td></tr><tr><td>10 添加 dq7 延迟 2 个延迟单元</td></tr><tr><td>11 添加 dq7 延迟 3 个延迟单元</td></tr><tr><td>27-26 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td rowspan="5">25-24 wr_dq6_del</td><td>写 dq6 延迟微调。该字段保存添加到 dq6（相对于 dqs0）的延迟单元数量。</td></tr><tr><td>00 dq6 延迟不变</td></tr><tr><td>01 添加 dq6 延迟 1 个延迟单元</td></tr><tr><td>10 添加 dq6 延迟 2 个延迟单元</td></tr><tr><td>11 添加 dq6 延迟 3 个延迟单元</td></tr><tr><td>23-22 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>21-20 wr_dq5_del</td><td>写 dq5 延迟微调。该字段保存添加到 dq5（相对于 dqs0）的延迟单元数量。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWRDQBY0DL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>00 dq5 延迟不变</td></tr><tr><td></td><td>01 添加 dq5 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq5 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq5 延迟 3 个延迟单元</td></tr><tr><td>19-18 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>17-16 wr_dq4_del</td><td>写 dq4 延迟微调。该字段保存添加到 dq4（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>00 dq4 延迟不变</td></tr><tr><td></td><td>01 添加 dq4 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq4 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq4 延迟 3 个延迟单元</td></tr><tr><td>15-14 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>13-12 wr_dq3_del</td><td>写 dq3 延迟微调。该字段保存添加到 dq3（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>00 dq3 延迟不变</td></tr><tr><td></td><td>01 添加 dq3 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq3 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq3 延迟 3 个延迟单元</td></tr><tr><td>11-10 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>9-8 wr_dq2_del</td><td>写 dq2 延迟微调。该字段保存添加到 dq2（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>00 dq2 延迟不变</td></tr><tr><td></td><td>01 添加 dq2 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq2 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq2 延迟 3 个延迟单元</td></tr><tr><td>7-6 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>5-4 wr_dq1_del</td><td>写 dq1 延迟微调。该字段保存添加到 dq1（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>00 dq1 延迟不变</td></tr><tr><td></td><td>01 添加 dq1 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq1 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq1 延迟 3 个延迟单元</td></tr><tr><td>3-2 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>1-0 wr_dq0_del</td><td>写 dq0 延迟微调。该字段保存添加到 dq0（相对于 dqs0）的延迟单元数量。</td></tr><tr><td></td><td>00 dq0 延迟不变</td></tr><tr><td></td><td>01 添加 dq0 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq0 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq0 延迟 3 个延迟单元</td></tr></table>

# 35.12.41 MMDC PHY 写 DQ 字节1延迟寄存器 (MMDC_MPWRDQBY1DL)

该寄存器用于对写 DQ 字节1中相对于写 DQS 的每个比特进行微调调整。

地址: 21B_0000h 基址 + 830h 偏移 = 21B_0830h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/bd9a9dc12d4a77c8aaffb8a53693a31599ef47ac9798ca65d55de4c2159c8646.jpg)

# MMDC_MPWRDQBY1DL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-30 wr_dm1_del</td><td>写 dm1 延迟微调。该字段保存添加到 dm1（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>00 dm1 延迟不变</td></tr><tr><td></td><td>01 添加 dm1 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dm1 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dm1 延迟 3 个延迟单元</td></tr><tr><td>29-28 wr_dq15_del</td><td>写 dq15 延迟微调。该字段保存添加到 dq15（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>00 dq15 延迟不变</td></tr><tr><td></td><td>01 添加 dq15 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq15 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq15 延迟 3 个延迟单元</td></tr><tr><td>27-26 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>25-24 wr_dq14_del</td><td>写 dq14 延迟微调。该字段保存添加到 dq14（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>00 dq14 延迟不变</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWRDQBY1DL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>01 添加 dq14 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq14 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq14 延迟 3 个延迟单元</td></tr><tr><td>23-22 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>21-20 wr_dq13_del</td><td>写 dq13 延迟微调。该字段保存添加到 dq13（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>00 dq13 延迟不变</td></tr><tr><td></td><td>01 添加 dq13 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq13 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq13 延迟 3 个延迟单元</td></tr><tr><td>19-18 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>17-16 wr_dq12_del</td><td>写 dq12 延迟微调。该字段保存添加到 dq12（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>00 dq12 延迟不变</td></tr><tr><td></td><td>01 添加 dq12 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq12 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq12 延迟 3 个延迟单元</td></tr><tr><td>15-14 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>13-12 wr_dq11_del</td><td>写 dq11 延迟微调。该字段保存添加到 dq11（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>00 dq11 延迟不变</td></tr><tr><td></td><td>01 添加 dq11 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq11 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq11 延迟 3 个延迟单元</td></tr><tr><td>11-10 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>9-8 wr_dq10_del</td><td>写 dq10 延迟微调。该字段保存添加到 dq10（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>00 dq10 延迟不变</td></tr><tr><td></td><td>01 添加 dq10 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq10 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq10 延迟 3 个延迟单元</td></tr><tr><td>7-6 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>5-4 wr_dq9_del</td><td>写 dq9 延迟微调。该字段保存添加到 dq9（相对于 dqs1）的延迟单元数量。</td></tr><tr><td></td><td>00 dq9 延迟不变</td></tr><tr><td></td><td>01 添加 dq9 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq9 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq9 延迟 3 个延迟单元</td></tr><tr><td>3-2 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>1-0 wr_dq8_del</td><td>写 dq8 延迟微调。该字段保存添加到 dq8（相对于 dqs1）的延迟单元数量。00 dq8 延迟不变；01 添加 dq8 延迟 1 个延迟单元；10 添加 dq8 延迟 2 个延迟单元；11 添加 dq8 延迟 3 个延迟单元。</td></tr></table>

# 35.12.42 MMDC PHY 写 DQ 字节2延迟寄存器 (MMDC_MPWRDQBY2DL)

该寄存器用于对写 DQ 字节2中相对于写 DQS 的每个比特进行微调调整。

地址: 21B_0000h 基址 + 834h 偏移 = 21B_0834h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/3bf79f9e95bb0d0380be3376953959ce42d10e0f4876ec2286fb49a7ad132595.jpg)

# MMDC_MPWRDQBY2DL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-30 wr_dm2_del</td><td>写 dm2 延迟微调。该字段保存添加到 dm2（相对于 dqs2）的延迟单元数量。</td></tr><tr><td></td><td>00 dm2 延迟不变</td></tr><tr><td></td><td>01 添加 dm2 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dm2 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dm2 延迟 3 个延迟单元</td></tr><tr><td>29-28 wr_dq23_del</td><td>写 dq23 延迟微调。该字段保存添加到 dq23（相对于 dqs2）的延迟单元数量。</td></tr><tr><td></td><td>00 dq23 延迟不变</td></tr><tr><td></td><td>01 添加 dq23 延迟 1 个延迟单元</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWRDQBY2DL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>10 添加 dq23 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq23 延迟 3 个延迟单元</td></tr><tr><td>27-26 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>25-24 wr_dq22_del</td><td>写 dq22 延迟微调。该字段保存添加到 dq22（相对于 dqs2）的延迟单元数量。</td></tr><tr><td></td><td>00 dq22 延迟不变</td></tr><tr><td></td><td>01 添加 dq22 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq22 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq22 延迟 3 个延迟单元</td></tr><tr><td>23-22 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>21-20 wr_dq21_del</td><td>写 dq21 延迟微调。该字段保存添加到 dq21（相对于 dqs2）的延迟单元数量。</td></tr><tr><td></td><td>00 dq21 延迟不变</td></tr><tr><td></td><td>01 添加 dq21 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq21 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq21 延迟 3 个延迟单元</td></tr><tr><td>19-18 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>17-16 wr_dq20_del</td><td>写 dq20 延迟微调。该字段保存添加到 dq20（相对于 dqs2）的延迟单元数量。</td></tr><tr><td></td><td>00 dq20 延迟不变</td></tr><tr><td></td><td>01 添加 dq20 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq20 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq20 延迟 3 个延迟单元</td></tr><tr><td>15-14 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>13-12 wr_dq19_del</td><td>写 dq19 延迟微调。该字段保存添加到 dq19（相对于 dqs2）的延迟单元数量。</td></tr><tr><td></td><td>00 dq19 延迟不变</td></tr><tr><td></td><td>01 添加 dq19 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq19 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq19 延迟 3 个延迟单元</td></tr><tr><td>11-10 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>9-8 wr_dq18_del</td><td>写 dq18 延迟微调。该字段保存添加到 dq18（相对于 dqs2）的延迟单元数量。</td></tr><tr><td></td><td>00 dq18 延迟不变</td></tr><tr><td></td><td>01 添加 dq18 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq18 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq18 延迟 3 个延迟单元</td></tr><tr><td>7-6 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td rowspan="5">5-4 wr_dq17_del</td><td>写 dq17 延迟微调。该字段保存添加到 dq17（相对于 dqs2）的延迟单元数量。</td></tr><tr><td>00 dq17 延迟不变</td></tr><tr><td>01 添加 dq17 延迟 1 个延迟单元</td></tr><tr><td>10 添加 dq17 延迟 2 个延迟单元</td></tr><tr><td>11 添加 dq17 延迟 3 个延迟单元</td></tr><tr><td>3-2 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td rowspan="5">1-0 wr_dq16_del</td><td>写 dq16 延迟微调。该字段保存添加到 dq16（相对于 dqs2）的延迟单元数量。</td></tr><tr><td>00 dq16 延迟不变</td></tr><tr><td>01 添加 dq16 延迟 1 个延迟单元</td></tr><tr><td>10 添加 dq16 延迟 2 个延迟单元</td></tr><tr><td>11 添加 dq16 延迟 3 个延迟单元</td></tr></table>

# 35.12.43 MMDC PHY 写 DQ 字节3延迟寄存器 (MMDC_MPWRDQBY3DL)

该寄存器用于对写 DQ 字节3中相对于写 DQS 的每个比特进行微调调整。

地址: 21B_0000h 基址 + 838h 偏移 = 21B_0838h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/a232e11a55ed7805884bd7c45be810f9cddbabecda69fd6e9b0d8b59cb19dc5c.jpg)

# MMDC_MPWRDQBY3DL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-30 wr_dm3_del</td><td>写 dm3 延迟微调。该字段保存添加到 dm3（相对于 dqs3）的延迟单元数量。00 dm3 延迟不变；01 添加 dm3 延迟 1 个延迟单元。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWRDQBY3DL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>10 添加 dm3 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dm3 延迟 3 个延迟单元</td></tr><tr><td>29-28 wr_dq31_del</td><td>写 dq31 延迟微调。该字段保存添加到 dq31（相对于 dqs3）的延迟单元数量。</td></tr><tr><td></td><td>00 dq31 延迟不变</td></tr><tr><td></td><td>01 添加 dq31 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq31 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq31 延迟 3 个延迟单元</td></tr><tr><td>27-26 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>25-24 wr_dq30_del</td><td>写 dq30 延迟微调。该字段保存添加到 dq30（相对于 dqs3）的延迟单元数量。</td></tr><tr><td></td><td>00 dq30 延迟不变</td></tr><tr><td></td><td>01 添加 dq30 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq30 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq30 延迟 3 个延迟单元</td></tr><tr><td>23-22 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>21-20 wr_dq29_del</td><td>写 dq29 延迟微调。该字段保存添加到 dq29（相对于 dqs3）的延迟单元数量。</td></tr><tr><td></td><td>00 dq29 延迟不变</td></tr><tr><td></td><td>01 添加 dq29 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq29 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq29 延迟 3 个延迟单元</td></tr><tr><td>19-18 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>17-16 wr_dq28_del</td><td>写 dq28 延迟微调。该字段保存添加到 dq28（相对于 dqs3）的延迟单元数量。</td></tr><tr><td></td><td>00 dq28 延迟不变</td></tr><tr><td></td><td>01 添加 dq28 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq28 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq28 延迟 3 个延迟单元</td></tr><tr><td>15-14 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>13-12 wr_dq27_del</td><td>写 dq27 延迟微调。该字段保存添加到 dq27（相对于 dqs3）的延迟单元数量。</td></tr><tr><td></td><td>00 dq27 延迟不变</td></tr><tr><td></td><td>01 添加 dq27 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 dq27 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 dq27 延迟 3 个延迟单元</td></tr><tr><td>11-10 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>9-8 wr_dq26_del</td><td>写 dq26 延迟微调。该字段保存添加到 dq26（相对于 dqs3）的延迟单元数量。00 dq26 延迟不变；01 添加 dq26 延迟 1 个延迟单元；10 添加 dq26 延迟 2 个延迟单元；11 添加 dq26 延迟 3 个延迟单元。</td></tr><tr><td>7-6 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>5-4 wr_dq25_del</td><td>写 dq25 延迟微调。该字段保存添加到 dq25（相对于 dqs3）的延迟单元数量。00 dq25 延迟不变；01 添加 dq25 延迟 1 个延迟单元；10 添加 dq25 延迟 2 个延迟单元；11 添加 dq25 延迟 3 个延迟单元。</td></tr><tr><td>3-2 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>1-0 wr_dq24_del</td><td>写 dq24 延迟微调。该字段保存添加到 dq24（相对于 dqs3）的延迟单元数量。00 dq24 延迟不变；01 添加 dq24 延迟 1 个延迟单元；10 添加 dq24 延迟 2 个延迟单元；11 添加 dq24 延迟 3 个延迟单元。</td></tr></table>

# 35.12.44 MMDC PHY 读 DQS 门控控制寄存器 0 (MMDC_MPDGCTRL0)

地址: 21B_0000h 基址 + 83Ch 偏移 = 21B_083Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/7a4df5b3bb4e4302407a450b5a532ec1123391d67edb695a6ab9e71536731512.jpg)

# MMDC_MPDGCTRL0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 RST_RD_FIFO</td><td>复位读数据 FIFO 及关联指针。如果该位置位，MMDC 将复位读数据 FIFO 及关联指针。该位在 FIFO 复位完成后自清除。</td></tr><tr><td>30 DG_CMP_CYC</td><td>读 DQS 门控采样周期。如果该位置位，MMDC 在比较读数据之前等待 32 个周期，否则等待 16 个 DDR 周期。0 MMDC 等待 16 个 DDR 周期；1 MMDC 等待 32 个 DDR 周期</td></tr><tr><td>29 DG_DIS</td><td>读 DQS 门控禁用。如果该位置位，MMDC 禁用读 DQS 门控机制。如果该位置位（读 DQS 门控禁用），则 DQS 和 DQS# 应分别使用上拉和下拉电阻。0 读 DQS 门控机制使能；1 读 DQS 门控机制禁用</td></tr><tr><td>28 HW_DG_EN</td><td>使能自动读 DQS 门控校准。如果该位置位，MMDC 执行自动读 DQS 门控校准。硬件在自动读 DQS 门控完成后清除该位。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPDGCTRL0 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>注意：在发出第一个读命令之前，MMDC 计数 12 个周期。在 LPDDR2 模式下，自动（HW）读 DQS 门控应禁用，DQS/DQS# 上的上拉/下拉电阻应使能，同时 ODT 电阻必须断开。0 禁用自动读 DQS 门控校准；1 启动自动读 DQS 门控校准</td></tr><tr><td>27-24 DG_HC_DEL1</td><td>字节1的读 DQS 门控半周期延迟。该字段指示读 DQS 门控与字节1读 DQS 前导码中点之间的半周期延迟。此延迟添加到读 DQS1 门控延迟线生成的延迟，因此总读 DQS 门控延迟为 (DG_HC_DEL#)*0.5*周期 + (DG_DL_ABS_OFFSET#)*1/256*周期。自动读 DQS 门控校准完成后，该字段获得 ((HW_DG_LOW1 + HW_DG_UP1) /2) 的 4 位 MSB 值。0000 0 个周期延迟；0001 半周期延迟；0010 1 个周期延迟；1101 6.5 个周期延迟；1110 保留；1111 保留</td></tr><tr><td>23 DG_EXT_UP</td><td>DG 扩展上边界。默认情况下，DQS 门控硬件校准的上边界根据至少一次通过比较后的第一次失败比较设置。如果该位置位，则上边界根据最后一次通过比较设置。</td></tr><tr><td>22-16 DG_DL_ABS_OFFSET1</td><td>字节1绝对读 DQS 门控延迟偏移。该字段指示读 DQS 门控与字节1读 DQS 前导码中点之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (DG_DL_ABS_OFFSET1 / 256) * MMDC AXI 时钟（快时钟）。该字段也可由硬件写入。自动读 DQS 门控校准完成后，该字段获得 ((HW_DG_LOW1 + HW_DG_UP1) /2) 的 7 位 LSB 值。注意：并非所有更改都会对实际延迟产生影响。如果请求的更改小于延迟线的分辨率，则不会发生更改。</td></tr><tr><td>15-13 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>12 HW_DG_ERR</td><td>HW DQS 门控错误。该位在读 DQS 门控硬件校准过程中发现错误时置位。当硬件校准中未找到有效值时可能发生错误。该位仅在 HW_DG_EN 被清零后有效。0 DQS 门控硬件校准过程中未发现错误。1 DQS 门控硬件校准过程中发现错误。</td></tr><tr><td>11-8 DG_HC_DEL0</td><td>字节0的读 DQS 门控半周期延迟。该字段指示读 DQS 门控与字节0/4读 DQS 前导码中点之间的半周期延迟。此延迟添加到读 DQS1 门控延迟线生成的延迟，因此总读 DQS 门控延迟为 (DG_HC_DEL#)*0.5*周期 + (DG_DL_ABS_OFFSET#)*1/256*周期。自动读 DQS 门控校准完成后，该字段获得 ((HW_DG_LOW1 + HW_DG_UP1) /2) 的 4 位 MSB 值。0000 2 个周期延迟；0001 半周期延迟。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPDGCTRL0 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>0010 1 个周期延迟</td></tr><tr><td></td><td>1101 6.5 个周期延迟</td></tr><tr><td></td><td>1110 保留</td></tr><tr><td></td><td>1111 保留</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 DG_DL_ABS_OFFSET0</td><td>字节0绝对读 DQS 门控延迟偏移。该字段指示读 DQS 门控与字节0读 DQS 前导码中点之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (DG_DL_ABS_OFFSET0 / 256) * MMDC AXI 时钟（快时钟）。该字段也可由硬件写入。自动读 DQS 门控校准完成后，该字段获得 ((HW_DG_LOW0 + HW_DG_UP0) /2) 的 7 位 LSB 值。注意：并非所有更改都会对实际延迟产生影响。如果请求的更改小于延迟线的分辨率，则不会发生更改。</td></tr></table>

# 35.12.45 MMDC PHY 读 DQS 门控控制寄存器 1 (MMDC_MPDGCTRL1)

地址: 21B_0000h 基址 + 840h 偏移 = 21B_0840h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/113b76011a26f3706001e9e33de7a84af34ddb23477a88a99806a996fa84037d.jpg)

# MMDC_MPDGCTRL1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-28 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>27-24 DG_HC_DEL3</td><td>字节3的读 DQS 门控半周期延迟。该字段指示读 DQS 门控与字节3/7读 DQS 前导码中点之间的半周期延迟。此延迟添加到读 DQS1 门控延迟线生成的延迟，因此总读 DQS 门控延迟为 (DG_HC_DEL#)*0.5*周期 + (DG_DL_ABS_OFFSET#)*1/256*周期。自动读 DQS 门控校准完成后，该字段获得 ((HW_DG_LOW3 + HW_DG_UP3) /2) 的 4 位 MSB 值。0000 0 个周期延迟；0001 半周期延迟。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPDGCTRL1 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>0010 1 个周期延迟</td></tr><tr><td></td><td>1101 6.5 个周期延迟</td></tr><tr><td></td><td>1110 保留</td></tr><tr><td></td><td>1111 保留</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>22-16 DG_DL_ABS_OFFSET3</td><td>字节3绝对读 DQS 门控延迟偏移。该字段指示读 DQS 门控与字节3读 DQS 前导码中点之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (DG_DL_ABS_OFFSET3 / 256) * MMDC AXI 时钟（快时钟）。该字段也可由硬件写入。自动读 DQS 门控校准完成后，该字段获得 ((HW_DG_LOW3 + HW_DG_UP3) /2) 的 7 位 LSB 值。注意：并非所有更改都会对实际延迟产生影响。如果请求的更改小于延迟线的分辨率，则不会发生更改。</td></tr><tr><td>15-12 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>11-8 DG_HC_DEL2</td><td>字节2的读 DQS 门控半周期延迟。该字段指示读 DQS 门控与字节2/5读 DQS 前导码中点之间的半周期延迟。此延迟添加到读 DQS1 门控延迟线生成的延迟，因此总读 DQS 门控延迟为 (DG_HC_DEL#)*0.5*周期 + (DG_DL_ABS_OFFSET#)*1/256*周期。自动读 DQS 门控校准完成后，该字段获得 ((HW_DG_LOW2 + HW_DG_UP2) /2) 的 4 位 MSB 值。0000 0 个周期延迟；0001 半周期延迟；0010 1 个周期延迟；1101 6.5 个周期延迟；1110 保留；1111 保留</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 DG_DL_ABS_OFFSET2</td><td>字节2绝对读 DQS 门控延迟偏移。该字段指示读 DQS 门控与字节2读 DQS 前导码中点之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (DG_DL_ABS_OFFSET2 / 256) * MMDC AXI 时钟（快时钟）。该字段也可由硬件写入。自动读 DQS 门控校准完成后，该字段获得 ((HW_DG_LOW2 + HW_DG_UP2) /2) 的 7 位 LSB 值。注意：并非所有更改都会对实际延迟产生影响。如果请求的更改小于延迟线的分辨率，则不会发生更改。</td></tr></table>

# 35.12.46 MMDC PHY 读 DQS 门控延迟线状态寄存器 (MMDC_MPDGDLST0)

该寄存器保存 4 条 DQS 门控延迟线的状态。

地址: 21B_0000h 基址 + 844h 偏移 = 21B_0844h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/e78951027d37870e1bdb550bea0566331cec08b403ccd7a8e8a90db888ed32ff.jpg)

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

# MMDC_MPDGDLST0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31</td><td>此字段保留。保留</td></tr><tr><td>30-24</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>23</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>22-16</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>15</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>14-8</td><td rowspan="2">该字段反映读 DQS 门控延迟线1实际使用的延迟单元数量。</td></tr><tr><td>DG_DL_UNIT_NUM1</td></tr><tr><td>7</td><td rowspan="2">此字段保留。保留</td></tr><tr><td>-</td></tr><tr><td>6-0 DG_DL_UNIT_NUM0</td><td>该字段反映读 DQS 门控延迟线0实际使用的延迟单元数量。</td></tr></table>

# 35.12.47 MMDC PHY 读延迟线配置寄存器 (MMDC_MPRDDLCTL)

该寄存器控制读延迟线功能；它确定 DQS 相对于相关 DQ 读访问的延迟。延迟线补偿工艺变化，并产生与工艺、温度和电压无关的恒定延迟。

地址: 21B_0000h 基址 + 848h 偏移 = 21B_0848h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/b1514fc99d3a0182b5fffaccf67343d711dbcc79d4d66f9fae1c35414843f807.jpg)

# MMDC_MPRDDLCTL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-24 -</td><td>此字段保留。保留</td></tr><tr><td>23 -</td><td>此字段保留。保留</td></tr><tr><td>22-16 -</td><td>此字段保留。保留</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPRDDLCTL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td>14-8 RD_DL_ABS_OFFSET1</td><td>字节1绝对读延迟偏移。该字段指示读 DQS 选通与字节1读数据之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (RD_DL_ABS_OFFSET1 / 256) * MMDC AXI 时钟（快时钟）。因此对于默认值 64，获得四分之一周期延迟。该字段也可由硬件写入。读延迟线硬件校准完成后，该字段获得 (HW_RD_DL_LOW1 + HW_RD_DL_UP1) /2 的值。注意：并非所有更改都会对实际延迟产生影响。如果请求的更改小于延迟线的分辨率，则不会发生更改。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 RD_DL_ABS_OFFSET0</td><td>字节0绝对读延迟偏移。该字段指示读 DQS 选通与字节0读数据之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (RD_DL_ABS_OFFSET0 / 256) * MMDC AXI 时钟（快时钟）。因此对于默认值 64，获得四分之一周期延迟。该字段也可由硬件写入。读延迟线硬件校准完成后，该字段获得 (HW_RD_DL_LOW0 + HW_RD_DL_UP0) /2 的值。注意：并非所有更改都会对实际延迟产生影响。如果请求的更改小于延迟线的分辨率，则不会发生更改。</td></tr></table>

# 35.12.48 MMDC PHY 读延迟线状态寄存器 (MMDC_MPRDDLST)

该寄存器保存 4 条读延迟线的状态。

地址: 21B_0000h 基址 + 84Ch 偏移 = 21B_084Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/dd47e7eadf0bc34d991386382638588f73672e5902a6a3e101b89402fa99d8e7.jpg)

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

# MMDC_MPRDDLST 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-24 -</td><td>此字段保留。保留</td></tr><tr><td>23 -</td><td>此字段保留。保留</td></tr><tr><td>22-16 -</td><td>此字段保留。保留</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-8 RD_DL_UNIT_NUM1</td><td>该字段反映读延迟线1实际使用的延迟单元数量。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 RD_DL_UNIT_NUM0</td><td>该字段反映读延迟线0实际使用的延迟单元数量。</td></tr></table>

# 35.12.49 MMDC PHY 写延迟线配置寄存器 (MMDC_MPWRDLCTL)

该寄存器控制写延迟线功能，它确定写访问中 DQ/DM 相对于相关 DQS 的延迟。延迟线补偿工艺变化，并产生与工艺、温度和电压无关的恒定延迟。

地址: 21B_0000h 基址 + 850h 偏移 = 21B_0850h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/ec6cbf56d8b62ff678d8b2d222651a78cfc1f2cc49664b55176c55d8b192a582.jpg)

# MMDC_MPWRDLCTL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-24 -</td><td>此字段保留。保留</td></tr><tr><td>23 -</td><td>此字段保留。保留</td></tr><tr><td>22-16 -</td><td>此字段保留。保留</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWRDLCTL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td>14-8 WR_DL_ABS_OFFSET1</td><td>字节1绝对写延迟偏移。该字段指示写 DQS 选通与字节1写数据之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (WR_DL_ABS_OFFSET1 / 256) * MMDC AXI 时钟（快时钟）。因此对于默认值 64，获得四分之一周期延迟。该字段也可由硬件写入。写延迟线硬件校准完成后，该字段获得 (HW_WR_DL_LOW1 + HW_WR_DL_UP1) /2 的值。注意：并非此值的所有更改都会影响实际延迟。如果请求的更改小于延迟线的分辨率，则不会发生更改。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 WR_DL_ABS_OFFSET0</td><td>字节0绝对写延迟偏移。该字段指示写 DQS 选通与字节0写数据之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (WR_DL_ABS_OFFSET0 / 256) * MMDC AXI 时钟（快时钟）。因此对于默认值 64，获得四分之一周期延迟。该字段也可由硬件写入。写延迟线硬件校准完成后，该字段获得 (HW_WR_DL_LOW0 + HW_WR_DL_UP0) /2 的值。注意：并非此值的所有更改都会影响实际延迟。如果请求的更改小于延迟线的分辨率，则不会发生更改。</td></tr></table>

# 35.12.50 MMDC PHY 写延迟线状态寄存器 (MMDC_MPWRDLST)

该寄存器保存 4 条写延迟线的状态。

地址: 21B_0000h 基址 + 854h 偏移 = 21B_0854h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/17e5118b0b3b15c6d496277747f79365c05bdb6a86ac2529b0e47aa1af24a141.jpg)

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

# MMDC_MPWRDLST 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-24 -</td><td>此字段保留。保留</td></tr><tr><td>23 -</td><td>此字段保留。保留</td></tr><tr><td>22-16 -</td><td>此字段保留。保留</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-8 WR_DL_UNIT_NUM1</td><td>该字段反映写延迟线1实际使用的延迟单元数量。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 WR_DL_UNIT_NUM0</td><td>该字段反映写延迟线0实际使用的延迟单元数量。</td></tr></table>

# 35.12.51 MMDC PHY CK 控制寄存器 (MMDC_MPSDCTRL)

该寄存器控制主时钟（CK0）的微调。

地址: 21B_0000h 基址 + 858h 偏移 = 21B_0858h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/4a397c9a557a16c10432b17756bdba352be5446617ff4921ce56d69c568410d3.jpg)

# MMDC_MPSDCTRL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-10 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>9-8 SDclk0_del</td><td>DDR 时钟0延迟微调。该字段保存添加到 DDR 时钟（CK0）的延迟单元数量。00 DDR 时钟0延迟不变；01 添加 DDR 时钟0延迟 1 个延迟单元。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPSDCTRL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>10 添加 DDR 时钟0延迟 2 个延迟单元；11 添加 DDR 时钟0延迟 3 个延迟单元。</td></tr><tr><td>7-0 保留</td><td>此只读字段保留，始终读为 0。</td></tr></table>

# 35.12.52 MMDC ZQ LPDDR2 硬件控制寄存器 (MMDC_MPZQLP2CTL)

该寄存器控制 LPDDR2 器件执行 ZQ 校准所需的空闲时间。

地址: 21B_0000h 基址 + 85Ch 偏移 = 21B_085Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/0c4c0d588676cfb5a3cd36629c57aa6002d49c06bfa66c9bc500ae26a197bdf6.jpg)

# MMDC_MPZQLP2CTL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-24 ZQ_LP2_HW_ZQCS</td><td>该寄存器定义存储器器件执行短 ZQ 校准所需的周期数。这是 MMDC 在发送短 ZQ 校准后、发送其他命令之前必须等待的时间。如果发送 ZQ 复位，也将使用此延迟。0x0-0x1A 保留；0x1B 112 个周期（默认）；0x1C 116 个周期；0x7E 508 个周期；0x7F 512 个周期</td></tr><tr><td>23-16 ZQ_LP2_HW_ZQCL</td><td>该寄存器定义存储器器件执行长 ZQ 校准所需的周期数。这是 MMDC 在发送长 ZQ 校准后、发送其他命令之前必须等待的时间。0x0-0x36 保留；0x37 112 个周期</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPZQLP2CTL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>0x38 114 个周期；0x5F 192 个周期（默认，JEDEC 值，tZQCL，适用于 LPDDR2，360ns @ 时钟频率 533MHz）；0xFE 510 个周期；0xFF 512 个周期</td></tr><tr><td>15-9 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>8-0 ZQ_LP2_HW_ZQINIT</td><td>该寄存器定义存储器器件执行初始化 ZQ 校准所需的周期数。这是 MMDC 在发送初始化 ZQ 校准后、发送其他命令之前必须等待的时间。0x0-0x36 保留；0x37 112 个周期；0x38 114 个周期；0x109 532 个周期（默认，JEDEC 值，tZQINIT，适用于 LPDDR2，1us @ 时钟频率 533MHz）；0x1FE 1022 个周期；0x1FF 1024 个周期</td></tr></table>

# 35.12.53 MMDC PHY 读延迟硬件校准控制寄存器 (MMDC_MPRDDLHWCTL)

地址: 21B_0000h 基址 + 860h 偏移 = 21B_0860h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/be5b9f10b4a00de43370423a33d73597e095a04f72676642067afcbada3334af.jpg)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/5ff8c23ef64c9bb978c4e6b454e3b09db523c6d641a190b7305aab58ba49c14b.jpg)

# MMDC_MPRDDLHWCTL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-6 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>5 HW_RD_DL_CMP_CYC</td><td>自动（HW）读采样周期。如果该位置位，MMDC 将在发送读命令使能脉冲后 32 个周期比较读数据，否则在 16 个周期后比较数据。</td></tr><tr><td>4 HW_RD_DL_EN</td><td>使能自动（HW）读校准。如果该位置位，MMDC 将执行自动读校准。硬件应在校准完成后清除该位。该位清除也表示读校准结果有效。注意：在发出第一个读命令之前，MMDC 计数 12 个周期。</td></tr><tr><td>3 -</td><td>此字段保留。保留</td></tr><tr><td>2 -</td><td>此字段保留。保留</td></tr><tr><td>1 HW_RD_DL_ERR1</td><td>字节1自动（HW）读校准错误。如果该位置位，表示在读延迟线1的硬件校准过程中发现错误。如果校准过程结束时该位为零，则边界结果可在 MPRDDLHWST0 寄存器中找到。该位仅在 HW_RD_DL_EN 被清零后有效。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPRDDLHWCTL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>0 读延迟线1的自动（HW）读校准过程中未发现错误。</td></tr><tr><td></td><td>1 读延迟线1的自动（HW）读校准过程中发现错误。</td></tr><tr><td>0 HW_RD_DL_ERR0</td><td>字节0自动（HW）读校准错误。如果该位置位，表示在读延迟线0的硬件校准过程中发现错误。如果校准过程结束时该位为零，则边界结果可在 MPRDDLHWST0 寄存器中找到。该位仅在 HW_RD_DL_EN 被清零后有效。</td></tr><tr><td></td><td>0 读延迟线0的自动（HW）读校准过程中未发现错误。</td></tr><tr><td></td><td>1 读延迟线0的自动（HW）读校准过程中发现错误。</td></tr></table>

# 35.12.54 MMDC PHY 写延迟硬件校准控制寄存器 (MMDC_MPWRDLHWCTL)

地址: 21B_0000h 基址 + 864h 偏移 = 21B_0864h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/cb62b86354a6f50560a02a62bc1ae86979154b56a38b9eb7e6f26cbca015a987.jpg)

MMDC 内存映射/寄存器定义

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/e9cabc6b334ea09af1492e72ec8bd9648db7f91ab43a70ce652d1c5b5f16bd45.jpg)

# MMDC_MPWRDLHWCTL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-6 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>5 HW_WR_DL_CMP_CYC</td><td>写采样周期。如果该位置位，MMDC 将在发送读命令使能脉冲后 32 个周期比较数据，否则在 16 个周期后比较数据。</td></tr><tr><td>4 HW_WR_DL_EN</td><td>使能自动（HW）写校准。如果该位置位，MMDC 将执行自动写校准。硬件应在校准完成后清除该位。该位清除也表示写校准结果有效。注意：在发出第一个读命令之前，MMDC 计数 12 个周期。</td></tr><tr><td>3 -</td><td>此字段保留。保留</td></tr><tr><td>2 -</td><td>此字段保留。保留</td></tr><tr><td>1 HW_WR_DL_ERR1</td><td>字节1自动（HW）写校准错误。如果该位置位，表示在写延迟线1的硬件校准过程中发现错误。如果校准过程结束时该位为零，则边界结果可在 MPWRDLHWST0 寄存器中找到。该位仅在 HW_WR_DL_EN 被清零后有效。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWRDLHWCTL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>0 写延迟线1的自动（HW）写校准过程中未发现错误。1 写延迟线1的自动（HW）写校准过程中发现错误。</td></tr><tr><td>0 HW_WR_DL_ERR0</td><td>字节0自动（HW）写校准错误。如果该位置位，表示在写延迟线0的硬件校准过程中发现错误。如果校准过程结束时该位为零，则边界结果可在 MPWRDLHWST0 寄存器中找到。该位仅在 HW_WR_DL_EN 被清零后有效。0 写延迟线0的自动（HW）写校准过程中未发现错误。1 写延迟线0的自动（HW）写校准过程中发现错误。</td></tr></table>

# 35.12.55 MMDC PHY 读延迟硬件校准状态寄存器 0 (MMDC_MPRDDLHWST0)

地址: 21B_0000h 基址 + 868h 偏移 = 21B_0868h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td></tr><tr><td>R</td><td>0</td><td colspan="7">HW_RD_DL_UP1</td><td>0</td><td colspan="7">HW_RD_DL_LOW1</td></tr><tr><td>W</td><td></td><td colspan="7"></td><td></td><td colspan="7"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr><tr><td>位</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td>0</td><td colspan="7">HW_RD_DL_UP0</td><td>0</td><td colspan="7">HW_RD_DL_LOW0</td></tr><tr><td>W</td><td></td><td colspan="7"></td><td></td><td colspan="7"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPRDDLHWST0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-24 HW_RD_DL_UP1</td><td>字节1上边界的自动（HW）读校准结果。该字段保存字节1上边界的自动（HW）读校准结果。</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>22-16 HW_RD_DL_LOW1</td><td>字节1下边界的自动（HW）读校准结果。该字段保存字节1下边界的自动（HW）读校准结果。</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-8 HW_RD_DL_UP0</td><td>字节0上边界的自动（HW）读校准结果。该字段保存字节0上边界的自动（HW）读校准结果。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPRDDLHWST0 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td>6-0 HW_RD_DL_LOW0</td><td>字节0下边界的自动（HW）读校准结果。该字段保存字节0下边界的自动（HW）读校准结果。</td></tr></table>

# 35.12.56 MMDC PHY 写延迟硬件校准状态寄存器 0 (MMDC_MPWRDLHWST0)

地址: 21B_0000h 基址 + 870h 偏移 = 21B_0870h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td></tr><tr><td>R</td><td>0</td><td colspan="7">HW_WR_DL_UP1</td><td>0</td><td colspan="7">HW_WR_DL_LOW1</td></tr><tr><td>W</td><td></td><td colspan="7"></td><td></td><td colspan="7"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr><tr><td>位</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td>0</td><td colspan="7">HW_WR_DL_UP0</td><td>0</td><td colspan="7">HW_WR_DL_LOW0</td></tr><tr><td>W</td><td></td><td colspan="7"></td><td></td><td colspan="7"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPWRDLHWST0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-24 HW_WR_DL_UP1</td><td>字节1上边界的自动（HW）写校准结果。该字段保存字节1上边界的自动（HW）写校准结果。</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>22-16 HW_WR_DL_LOW1</td><td>字节1下边界的自动（HW）写校准结果。该字段保存字节1下边界的自动（HW）写校准结果。</td></tr><tr><td>15 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>14-8 HW_WR_DL_UP0</td><td>字节0上边界的自动（HW）写校准结果。该字段保存字节0上边界的自动（HW）写校准结果。</td></tr><tr><td>7 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>6-0 HW_WR_DL_LOW0</td><td>字节0下边界的自动（HW）写校准结果。该字段保存字节0下边界的自动（HW）写校准结果。</td></tr></table>

# 35.12.57 MMDC PHY 写均衡硬件错误寄存器 (MMDC_MPWLHWERR)

地址: 21B_0000h 基址 + 878h 偏移 = 21B_0878h

<table><tr><td rowspan="2">位</td><td rowspan="2">保留</td><td>保留</td><td>HW_WL1_DQ</td><td>HW_WL0_DQ</td></tr><tr><td></td><td></td><td></td></tr><tr><td>复位</td><td>0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0</td><td>0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 16</td><td>15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0</td><td></td></tr></table>

# MMDC_MPWLHWERR 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-24 -</td><td>此字段保留。保留</td></tr><tr><td>23-16 -</td><td>此字段保留。保留</td></tr><tr><td>15-8 HW_WL1_DQ</td><td>字节1硬件写均衡校准结果。该字段保存字节1所有 8 个写均衡步骤的结果。即位 0 保存 0 延迟的写均衡校准结果，位 1 保存 1/8 延迟的写均衡校准结果，直到位 7 保存 7/8 延迟的写均衡校准结果。</td></tr><tr><td>7-0 HW_WL0_DQ</td><td>字节0硬件写均衡校准结果。该字段保存字节0所有 8 个写均衡步骤的结果。即位 0 保存 0 延迟的写均衡校准结果，位 1 保存 1/8 延迟的写均衡校准结果，直到位 7 保存 7/8 延迟的写均衡校准结果。</td></tr></table>

# 35.12.58 MMDC PHY 读 DQS 门控硬件状态寄存器 0 (MMDC_MPDGHWST0)

地址: 21B_0000h 基址 + 87Ch 偏移 = 21B_087Ch

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td rowspan="2" colspan="5">保留</td><td colspan="11">HW_DG_UP0</td><td rowspan="2" colspan="5">保留</td><td colspan="11">HW_DG_LOW0</td></tr><tr><td>W</td><td colspan="11"></td><td colspan="11"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPDGHWST0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-27 -</td><td>此字段保留。保留</td></tr><tr><td>26-16 HW_DG_UP0</td><td>字节0上边界的硬件 DQS 门控校准结果。该字段保存字节0上边界的硬件 DQS 门控校准结果。</td></tr><tr><td>15-11 -</td><td>此字段保留。保留</td></tr><tr><td>10-0 HW_DG_LOW0</td><td>字节0下边界的硬件 DQS 门控校准结果。该字段保存字节0下边界的硬件 DQS 门控校准结果。</td></tr></table>

# 35.12.59 MMDC PHY 读 DQS 门控硬件状态寄存器 1 (MMDC_MPDGHWST1)

地址: 21B_0000h 基址 + 880h 偏移 = 21B_0880h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td rowspan="2" colspan="5">保留</td><td colspan="11">HW_DG_UP1</td><td rowspan="2" colspan="5">保留</td><td colspan="11">HW_DG_LOW1</td></tr><tr><td>W</td><td colspan="11"></td><td colspan="11"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPDGHWST1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-27 -</td><td>此字段保留。保留</td></tr><tr><td>26-16 HW_DG_UP1</td><td>字节1上边界的硬件 DQS 门控校准结果。该字段保存字节1上边界的硬件 DQS 门控校准结果。</td></tr><tr><td>15-11 -</td><td>此字段保留。保留</td></tr><tr><td>10-0 HW_DG_LOW1</td><td>字节1下边界的硬件 DQS 门控校准结果。该字段保存字节1下边界的硬件 DQS 门控校准结果。</td></tr></table>

# 35.12.60 MMDC PHY 读 DQS 门控硬件状态寄存器 2 (MMDC_MPDGHWST2)

地址: 21B_0000h 基址 + 884h 偏移 = 21B_0884h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td rowspan="2" colspan="5">保留</td><td colspan="11">HW_DG_UP2</td><td rowspan="2" colspan="5">保留</td><td colspan="11">HW_DG_LOW2</td></tr><tr><td>W</td><td colspan="11"></td><td colspan="11"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPDGHWST2 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-27 -</td><td>此字段保留。保留</td></tr><tr><td>26-16 HW_DG_UP2</td><td>字节2上边界的硬件 DQS 门控校准结果。该字段保存字节2上边界的硬件 DQS 门控校准结果。</td></tr><tr><td>15-11 -</td><td>此字段保留。保留</td></tr><tr><td>10-0 HW_DG_LOW2</td><td>字节2下边界的硬件 DQS 门控校准结果。该字段保存字节2下边界的硬件 DQS 门控校准结果。</td></tr></table>

# 35.12.61 MMDC PHY 读 DQS 门控硬件状态寄存器 3 (MMDC_MPDGHWST3)

地址: 21B_0000h 基址 + 888h 偏移 = 21B_0888h

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td rowspan="2" colspan="5">保留</td><td colspan="11">HW_DG_UP3</td><td rowspan="2" colspan="5">保留</td><td colspan="11">HW_DG_LOW3</td></tr><tr><td>W</td><td colspan="11"></td><td colspan="11"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPDGHWST3 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-27 -</td><td>此字段保留。保留</td></tr><tr><td>26-16 HW_DG_UP3</td><td>字节3上边界的硬件 DQS 门控校准结果。该字段保存字节3上边界的硬件 DQS 门控校准结果。</td></tr><tr><td>15-11 -</td><td>此字段保留。保留</td></tr><tr><td>10-0 HW_DG_LOW3</td><td>字节3下边界的硬件 DQS 门控校准结果。该字段保存字节3下边界的硬件 DQS 门控校准结果。</td></tr></table>

# 35.12.62 MMDC PHY 预定义比较寄存器 1 (MMDC_MPPDCMPR1)

该寄存器保存 MMDC 预定义比较值，将在自动读、读 DQS 门控和写校准过程中使用。比较值可以是 MPR 值（如 JEDEC 所定义），也可以由 PDV1 和 PDV2 字段编程。在 DDR3（BL=8）情况下，MMDC 将复制 PDV1、PDV2 并将该数据驱动到同一字节的 Beat4-7 上。

地址: 21B_0000h 基址 + 88Ch 偏移 = 21B_088Ch

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R W</td><td colspan="17">PDV2</td><td colspan="15">PDV1</td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPPDCMPR1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-16 PDV2</td><td rowspan="2">MMDC 预定义比较值2。该字段保存将在自动读、读 DQS 门控和写校准过程中驱动到 DDR 器件的数据的 2 个 MSB，当 MPR（DDR3）/ DQ 校准（LPDDR2/LPDDR3）模式禁用时（MPR_CMP 禁用）。校准期间的读访问中，MMDC 将读数据与此字段中存储的数据进行比较。</td></tr><tr><tr><td></td><td>注意：在发出读访问之前，MMDC 将反转该字段的值并将其驱动到读比较 FIFO 中的相关条目。更多信息请参见第 19.14.3.1.2 节 "使用预定义值的校准"、第 19.14.4.1.2 节 "使用预定义值的校准"和第 19.14.5.1 节 "HW（自动）写校准"。</td></tr><tr><td>15-0 PDV1</td><td>MMDC 预定义比较值1。该字段保存将在自动读、读 DQS 门控和写校准过程中驱动到 DDR 器件的数据的 2 个 LSB，当 MPR（DDR3）/ DQ 校准（LPDDR2/LPDDR3）模式禁用时（MPR_CMP 禁用）。校准期间的读访问中，MMDC 将读数据与此字段中存储的数据进行比较。</td></tr><tr><td></td><td>注意：在发出读访问之前，MMDC 将反转该字段的值并将其驱动到读比较 FIFO 中的相关条目。</td></tr></table>

# 35.12.63 MMDC PHY 预定义比较和 CA 延迟线配置寄存器 (MMDC_MPPDCMPR2)

地址: 21B_0000h 基址 + 890h 偏移 = 21B_0890h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/b7e64a0f0864fa2f20a74f52a693e32ce280c0d94ac881e9fe93cef7eda64803.jpg)

# MMDC_MPPDCMPR2 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>30-24 PHY_CA_DL_UNIT</td><td>该字段反映 CA（LPDDR2 的命令/地址）延迟线实际使用的延迟单元数量。</td></tr><tr><td>23 保留</td><td>此只读字段保留，始终读为 0。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPPDCMPR2 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td>22-16 CA_DL_ABS_OFFSET</td><td>绝对 CA（LPDDR2 的命令/地址）偏移。该字段指示 CA（命令/地址）总线与 DDR 时钟（CK）之间的绝对延迟，精度为时钟周期的分数，最高到半周期。分数值与工艺和频率无关。延迟线的延迟为 (CA_DL_ABS_OFFSET / 256) * MMDC AXI 时钟（快时钟）。因此对于默认值 64，获得四分之一周期延迟。</td></tr><tr><td>15-12 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>11-8 ZQ_PU_OFFSET</td><td>可编程偏移量（-7 到 7），当 ZQ_OFFSET_EN 使能时添加到 MMDC_MPZQHWCTRL[ZQ_HW_PU_RES] 字段。位[11]确定方向：'b0 = 偏移量加到 ZQ_HW_PU_RES 字段；'b1 = 偏移量从 ZQ_HW_PU_RES 字段减去。位[10:8] = 要应用的变化量。0000 0 — 偏移量加到 ZQ_HW_PU_RES 字段；0001 1 — 偏移量加到 ZQ_HW_PU_RES 字段；... 1111 7 — 偏移量从 ZQ_HW_PU_RES 字段减去。</td></tr><tr><td>7-4 ZQ_PD_OFFSET</td><td>可编程偏移量（-7 到 7），当 ZQ_OFFSET_EN 使能时添加到 MMDC_MPZQHWCTRL[ZQ_HW_PD_RES] 字段。位[7]确定方向：'b0 = 偏移量加到 ZQ_HW_PD_RES 字段；'b1 = 偏移量从 ZQ_HW_PD_RES 字段减去。位[6:4] = 要应用的变化量。</td></tr><tr><td></td><td>0000 0 — 偏移量加到 ZQ_HW_PD_RES 字段；0001 1 — 偏移量加到 ZQ_HW_PD_RES 字段；... 1111 7 — 偏移量从 ZQ_HW_PD_RES 字段减去。</td></tr><tr><td>3 ZQ_OFFSET_EN</td><td>0 硬件 ZQ 偏移禁用；1 硬件 ZQ 偏移使能</td></tr><tr><td>2 READ_LEVEL_PATTERN</td><td>MPR（DDR3）/ DQ 校准（LPDDR2/LPDDR3）读比较模式。如果在校准过程中使用 MPR（DDR3）/ DQ 校准（LPDDR2/LPDDR3）模式（MPR_CMP 置位），则该字段指示比较的读模式。0 与读模式 1010 比较；1 与读模式 0011 比较（仅在 LPDDR2/LPDDR3 模式下使用）</td></tr><tr><td>1 MPR_FULL_CMP</td><td>MPR（DDR3）/ DQ 校准（LPDDR2/LPDDR3）全比较使能。如果在校准过程中使用 MPR（DDR3）/ DQ 校准（LPDDR2/LPDDR3）模式（MPR_CMP 置位），则该字段指示 MMDC 是否将从 DDR 器件读取的数据的所有位与 MPR 预定义模式进行比较。当该位清零时，仅比较每个字节的 LSB。</td></tr><tr><td>0 MPR_CMP</td><td>MPR（DDR3）/ DQ 校准（LPDDR2/LPDDR3）比较使能。该位指示 MMDC 在自动读和读 DQS 校准过程中是将读数据与 DDR 器件驱动的预定义模式（由 JEDEC 定义的 READ_LEVEL_PATTERN）进行比较，还是与存储在 PDV1 和 PDV2 中的通用预定义值进行比较。当该位禁用时，数据与预定义比较值字段的数据进行比较。更多信息请参见读 DQS 门控校准和读校准。</td></tr></table>

# 35.12.64 MMDC PHY 软件虚拟访问寄存器 (MMDC_MPSWDAR0)

地址: 21B_0000h 基址 + 894h 偏移 = 21B_0894h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/44fbefd608c44a7c3dbaceecdb5d026f7ce75c310b3463b82946a94b54dda893.jpg)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/8d0ea53638877f0ebd914d7a0274bf04f769034188edfeb5076c4d017472a8e5.jpg)

# MMDC_MPSWDAR0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-6 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>5 -</td><td>此字段保留。保留</td></tr><tr><td>4 -</td><td>此字段保留。保留</td></tr><tr><td>3 SW_DUM_CMP1</td><td>软件虚拟读字节1比较结果。该位指示 SW_DUMMY_RD 完成时字节1读数据比较的结果。该位仅在 SW_DUMMY_RD 被清零后有效。0 虚拟读失败；1 虚拟读通过</td></tr><tr><td>2 SW_DUM_CMP0</td><td>软件虚拟读字节0比较结果。该位指示 SW_DUMMY_RD 完成时字节0读数据比较的结果。该位仅在 SW_DUMMY_RD 被清零后有效。0 虚拟读失败；1 虚拟读通过</td></tr><tr><td>1 SW_DUMMY_RD</td><td>软件虚拟读。当该位置位时，MMDC 将在内部生成对 bank 0、row 0、column 0 的读访问，无需系统干预。如果 MPR_CMP = 1，则读数据将与 MPPDCMPR2[READ_LEVEL.Pattern] 比较。如果 MPR_CMP = 0，则读数据将与</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPSWDAR0 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>MPPDCMPR1[PDV1]、MPPDCMPR1[PDV2] 比较。访问完成后该位自动清零，读数据和比较结果分别在 MPSWDAR0[SW_DUM_CMP#] 和 MPSWDRDR0-MPSWDRDR7 中有效。</td></tr><tr><td>0 SW_DUMMY_WR</td><td>软件虚拟写。当该位置位时，MMDC 将在内部生成对 bank 0、row 0、column 0 的写访问，无需系统干预，数据来自 MPPDCMPR1[PDV1] 和 MPPDCMPR1[PDV2]。访问完成后该位自动清零。</td></tr></table>

# 35.12.65 MMDC PHY 软件虚拟读数据寄存器 0 (MMDC_MPSWDRDR0)

地址: 21B_0000h 基址 + 898h 偏移 = 21B_0898h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/27b4079382abf3530a7e6eddcec624a9053df2b12a26f712b245beb71b3acc11.jpg)

# MMDC_MPSWDRDR0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 DUM_RD0</td><td>虚拟读数据0。该字段保存软件虚拟读访问期间从 DDR 读取的第一个数据（即 SW_DUMMY_RD = 1 时）。该字段仅在 SW_DUMMY_RD 被清零后有效。</td></tr></table>

# 35.12.66 MMDC PHY 软件虚拟读数据寄存器 1 (MMDC_MPSWDRDR1)

地址: 21B_0000h 基址 + 89Ch 偏移 = 21B_089Ch

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/657476f6af22cedc85ea5118e4ec6eea6b6f4819ffddfe9fcccef2627a7632ab.jpg)

# MMDC_MPSWDRDR1 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 DUM_RD1</td><td>虚拟读数据1。该字段保存软件虚拟读访问期间从 DDR 读取的第二个数据（即 SW_DUMMY_RD = 1 时）。该字段仅在 SW_DUMMY_RD 被清零后有效。</td></tr></table>

# 35.12.67 MMDC PHY 软件虚拟读数据寄存器 2 (MMDC_MPSWDRDR2)

地址: 21B_0000h 基址 + 8A0h 偏移 = 21B_08A0h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/41794be166297c8c096ae797b7a189948cde4e66d9153cc53560e263b835906c.jpg)

# MMDC_MPSWDRDR2 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 DUM_RD2</td><td>虚拟读数据2。该字段保存软件虚拟读访问期间从 DDR 读取的第三个数据（即 SW_DUMMY_RD = 1 时）。该字段仅在 SW_DUMMY_RD 被清零后有效。</td></tr></table>

# 35.12.68 MMDC PHY 软件虚拟读数据寄存器 3 (MMDC_MPSWDRDR3)

地址: 21B_0000h 基址 + 8A4h 偏移 = 21B_08A4h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/ee1bd1c0ed995f5b2a09a323ca2d3f54fdab065fac3fbf333053d11576f37f75.jpg)

# MMDC_MPSWDRDR3 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 DUM_RD3</td><td>虚拟读数据3。该字段保存软件虚拟读访问期间从 DDR 读取的第四个数据（即 SW_DUMMY_RD = 1 时）。该字段仅在 SW_DUMMY_RD 被清零后有效。</td></tr></table>

# 35.12.69 MMDC PHY 软件虚拟读数据寄存器 4 (MMDC_MPSWDRDR4)

地址: 21B_0000h 基址 + 8A8h 偏移 = 21B_08A8h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/c43f1d0751bdc490260d3d32024fc48f8e95fef62adfb614c02c171d8e732ecf.jpg)

# MMDC_MPSWDRDR4 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 DUM_RD4</td><td>虚拟读数据4。该字段保存软件虚拟读访问期间从 DDR 读取的第五个数据（仅在突发长度为 8（BL=1）时）。该字段仅在 SW_DUMMY_RD 被清零后有效。</td></tr></table>

# 35.12.70 MMDC PHY 软件虚拟读数据寄存器 5 (MMDC_MPSWDRDR5)

地址: 21B_0000h 基址 + 8ACh 偏移 = 21B_08ACh

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/39f0386dcbf1cd78a4c9ffc1b4e676bebc0e951fda9977cd5006907f08dca52e.jpg)

# MMDC_MPSWDRDR5 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 DUM_RD5</td><td>虚拟读数据5。该字段保存软件虚拟读访问期间从 DDR 读取的第六个数据（仅在突发长度为 8（BL=1）时）。该字段仅在 SW_DUMMY_RD 被清零后有效。</td></tr></table>

# 35.12.71 MMDC PHY 软件虚拟读数据寄存器 6 (MMDC_MPSWDRDR6)

地址: 21B_0000h 基址 + 8B0h 偏移 = 21B_08B0h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/5e5918b5fcb335b9a3b4a74be3ec58c40acafb106b064260013a6b501de6c706.jpg)

# MMDC_MPSWDRDR6 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 DUM_RD6</td><td>虚拟读数据6。该字段保存软件虚拟读访问期间从 DDR 读取的第七个数据（仅在突发长度为 8（BL=1）时）。该字段仅在 SW_DUMMY_RD 被清零后有效。</td></tr></table>

# 35.12.72 MMDC PHY 软件虚拟读数据寄存器 7 (MMDC_MPSWDRDR7)

地址: 21B_0000h 基址 + 8B4h 偏移 = 21B_08B4h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/d9885d1f65fdfc452c28607c10a36c6d5e6961f47fef61e67ca92ed507003615.jpg)

# MMDC_MPSWDRDR7 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-0 DUM_RD7</td><td>虚拟读数据7。该字段保存软件虚拟读访问期间从 DDR 读取的第八个数据（仅在突发长度为 8（BL=1）时）。该字段仅在 SW_DUMMY_RD 被清零后有效。</td></tr></table>

# 35.12.73 MMDC PHY 测量单元寄存器 (MMDC_MPMUR0)

地址: 21B_0000h 基址 + 8B8h 偏移 = 21B_08B8h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/f8cb2bf6a0d843808392e23d10b2600f7fc50352bf43a37480e2aa37ab6a5812.jpg)

# MMDC_MPMUR0 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-26 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>25-16 MU_UNIT_DEL_NUM</td><td>每周期测量的延迟单元数量。该字段用于调试模式，保存测量单元每 DDR 时钟周期测量的延迟单元数量。每个校准过程中使用的延迟线使用该数量生成所需延迟。</td></tr><tr><td>15-12 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>11 FRC_MSB</td><td>强制测量延迟线。当该位置位时，将执行测量过程，完成后延迟线将发出所需延迟。测量过程完成后，测量单元和延迟线将返回功能模式。该位自清除。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPMUR0 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>注意：该位应仅在手动（SW）校准期间使用，不应在 DDR 功能正常（被访问）时使用。初始校准完成后，硬件执行周期性测量以跟踪任何工作条件变化。因此，不应使用强制测量（FRC_MSB）。更多信息请参见校准过程。</td></tr><tr><td></td><td>注意：用户应确保在置位该位之前没有对 DDR 的活跃访问。</td></tr><tr><td></td><td>0 不执行测量</td></tr><tr><td></td><td>1 执行测量过程</td></tr><tr><td>10 MU_BYP_EN</td><td>测量单元旁路使能。该字段用于调试模式，置位时延迟线将使用 MU_BYP_VAL 指示的延迟单元数量，否则延迟线将使用测量单元测量的并在 MU_UNIT_DEL_NUM 中指示的延迟单元数量。</td></tr><tr><td></td><td>0 延迟线使用 MU_UNIT_DEL_NUM 指示的延迟单元。</td></tr><tr><td></td><td>1 延迟线使用 MU_BYPASS_VAL 指示的延迟单元。</td></tr><tr><td>9-0 MU_BYP_VAL</td><td>测量旁路的延迟单元数量。该字段用于调试模式，保存 MU_BYP_EN 置位时延迟线将使用的延迟单元数量。</td></tr></table>

# 35.12.74 MMDC 写 CA 延迟线控制器 (MMDC_MPWRCADL)

该寄存器用于对 CA（LPDDR2 总线的命令/地址）相对于 DDR 时钟进行微调调整。

地址: 21B_0000h 基址 + 8BCh 偏移 = 21B_08BCh

<table><tr><td>位</td><td>31</td><td>30</td><td>29</td><td>28</td><td>27</td><td>26</td><td>25</td><td>24</td><td>23</td><td>22</td><td>21</td><td>20</td><td>19</td><td>18</td><td>17</td><td>16</td></tr><tr><td>R</td><td colspan="12">0</td><td rowspan="2" colspan="2">WR_CA9_DEL</td><td rowspan="2" colspan="2">WR_CA8_DEL</td></tr><tr><td>W</td><td colspan="12"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr><tr><td>位</td><td>15</td><td>14</td><td>13</td><td>12</td><td>11</td><td>10</td><td>9</td><td>8</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr><tr><td>R</td><td colspan="2">WR_CA7_DEL</td><td colspan="2">WR_CA6_DEL</td><td colspan="2">WR_CA5_DEL</td><td colspan="2">WR_CA4_DEL</td><td colspan="2">WR_CA3_DEL</td><td colspan="2">WR_CA2_DEL</td><td colspan="2">WR_CA1_DEL</td><td colspan="2">WR_CA0_DEL</td></tr><tr><td>W</td><td colspan="16"></td></tr><tr><td>复位</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></table>

# MMDC_MPWRCADL 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31-20 保留</td><td>此只读字段保留，始终读为 0。</td></tr><tr><td>19-18 WR_CA9_DEL</td><td>CA（LPDDR2 总线的命令/地址）位9延迟微调。该字段保存添加到 CA（命令/地址总线）位9（相对于时钟）的延迟单元数量。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPWRCADL 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>00 CA9 延迟不变</td></tr><tr><td></td><td>01 添加 CA9 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA9 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA9 延迟 3 个延迟单元</td></tr><tr><td>17-16 WR_CA8_DEL</td><td>CA（LPDDR2 总线的命令/地址）位8延迟微调。该字段保存添加到 CA（命令/地址总线）位8（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA8 延迟不变</td></tr><tr><td></td><td>01 添加 CA8 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA8 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA8 延迟 3 个延迟单元</td></tr><tr><td>15-14 WR_CA7_DEL</td><td>CA（LPDDR2 总线的命令/地址）位7延迟微调。该字段保存添加到 CA（命令/地址总线）位7（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA7 延迟不变</td></tr><tr><td></td><td>01 添加 CA7 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA7 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA7 延迟 3 个延迟单元</td></tr><tr><td>13-12 WR_CA6_DEL</td><td>CA（LPDDR2 总线的命令/地址）位6延迟微调。该字段保存添加到 CA（命令/地址总线）位6（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA6 延迟不变</td></tr><tr><td></td><td>01 添加 CA6 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA6 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA6 延迟 3 个延迟单元</td></tr><tr><td>11-10 WR_CA5_DEL</td><td>CA（LPDDR2 总线的命令/地址）位5延迟微调。该字段保存添加到 CA（命令/地址总线）位5（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA5 延迟不变</td></tr><tr><td></td><td>01 添加 CA5 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA5 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA5 延迟 3 个延迟单元</td></tr><tr><td>9-8 WR_CA4_DEL</td><td>CA（LPDDR2 总线的命令/地址）位4延迟微调。该字段保存添加到 CA（命令/地址总线）位4（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA4 延迟不变</td></tr><tr><td></td><td>01 添加 CA4 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA4 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA4 延迟 3 个延迟单元</td></tr><tr><td>7-6 WR_CA3_DEL</td><td>CA（LPDDR2 总线的命令/地址）位3延迟微调。该字段保存添加到 CA（命令/地址总线）位3（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA3 延迟不变</td></tr><tr><td></td><td>01 添加 CA3 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA3 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA3 延迟 3 个延迟单元</td></tr><tr><td>5-4 WR_CA2_DEL</td><td>CA（LPDDR2 总线的命令/地址）位2延迟微调。该字段保存添加到 CA（命令/地址总线）位2（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA2 延迟不变</td></tr><tr><td></td><td>01 添加 CA2 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA2 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA2 延迟 3 个延迟单元</td></tr><tr><td>3-2 WR_CA1_DEL</td><td>CA（LPDDR2 总线的命令/地址）位1延迟微调。该字段保存添加到 CA（命令/地址总线）位1（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA1 延迟不变</td></tr><tr><td></td><td>01 添加 CA1 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA1 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA1 延迟 3 个延迟单元</td></tr><tr><td>1-0 WR_CA0_DEL</td><td>CA（LPDDR2 总线的命令/地址）位0延迟微调。该字段保存添加到 CA（命令/地址总线）位0（相对于时钟）的延迟单元数量。</td></tr><tr><td></td><td>00 CA0 延迟不变</td></tr><tr><td></td><td>01 添加 CA0 延迟 1 个延迟单元</td></tr><tr><td></td><td>10 添加 CA0 延迟 2 个延迟单元</td></tr><tr><td></td><td>11 添加 CA0 延迟 3 个延迟单元</td></tr></table>

# 35.12.75 MMDC 占空比控制寄存器 (MMDC_MPDCCR)

该寄存器用于控制 DQS 和主时钟（CK0）的占空比。通过 LPMD/DVFS 机制使 DDR 器件进入自刷新模式后，才允许对此寄存器进行编程。

MMDC1_MPDCCR 仅影响 SDCLK0。

MMDC2_MPDCCR 仅影响 SDCLK1。

# 注意

如果在 DDR 初始化后修改占空比，DDR 必须被置于自刷新模式。

# 注意

在初始 DDR 初始化期间可以更改占空比，无需进入自刷新模式。

地址: 21B_0000h 基址 + 8C0h 偏移 = 21B_08C0h

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/0b3f4560-d6b7-4cd9-8e7b-37d48434fad6/e0aad64e1c99ef1512f62ce252bc0ff6f9e3e5b26332581069320f8dc8a7cb48.jpg)

# MMDC_MPDCCR 字段描述

<table><tr><td>字段</td><td>描述</td></tr><tr><td>31 -</td><td>此字段保留。保留</td></tr><tr><td>30-28 -</td><td>此字段保留。保留</td></tr><tr><td>27-25 -</td><td>此字段保留。保留</td></tr><tr><td>24-22 RD_DQS1_FT_DCC</td><td>字节1读 DQS 占空比微调控制。该字段控制字节1读 DQS 的占空比。注意：不允许其他选项。001 51.5% 低 48.5% 高；010 50% 占空比（默认）；100 48.5% 低 51.5% 高</td></tr><tr><td>21-19 RD_DQS0_FT_DCC</td><td>字节0读 DQS 占空比微调控制。该字段控制字节0读 DQS 的占空比。注意：不允许其他选项。001 51.5% 低 48.5% 高；010 50% 占空比（默认）；100 48.5% 低 51.5% 高</td></tr><tr><td>18-16 CK_FT1_DCC</td><td>DDR 时钟的次级占空比微调控制。该字段控制 DDR 时钟的占空比，并与 CK_FT0_DCC 级联。注意：不允许其他选项。</td></tr></table>

表格续下页...

i.MX 6ULL 应用处理器参考手册, Rev. 1, 11/2017

MMDC_MPDCCR 字段描述（续）

<table><tr><td>字段</td><td>描述</td></tr><tr><td></td><td>001 48.5% 低 51.5% 高</td></tr><tr><td></td><td>010 50% 占空比（默认）</td></tr><tr><td></td><td>100 51.5% 低 48.5% 高</td></tr><tr><td>15 -</td><td>此字段保留。保留</td></tr><tr><td>14-12 CK_FT0_DCC</td><td>DDR 时钟的主占空比微调控制。该字段控制 DDR 时钟的占空比。</td></tr><tr><td></td><td>注意：不允许其他选项。</td></tr><tr><td></td><td>001 48.5% 低 51.5% 高</td></tr><tr><td></td><td>010 50% 占空比（默认）</td></tr><tr><td></td><td>100 51.5% 低 48.5% 高</td></tr><tr><td>11-9 -</td><td>此字段保留。保留</td></tr><tr><td>8-6 -</td><td>此字段保留。保留</td></tr><tr><td>5-3 WR_DQS1_FT_DCC</td><td>字节1写 DQS 占空比微调控制。该字段控制字节1写 DQS 的占空比。</td></tr><tr><td></td><td>注意：不允许其他选项。</td></tr><tr><td></td><td>001 51.5% 低 48.5% 高</td></tr><tr><td></td><td>010 50% 占空比（默认）</td></tr><tr><td></td><td>100 48.5% 低 51.5% 高</td></tr><tr><td>2-0 WR_DQS0_FT_DCC</td><td>字节0写 DQS 占空比微调控制。该字段控制字节0写 DQS 的占空比。</td></tr><tr><td></td><td>注意：不允许其他选项。</td></tr><tr><td></td><td>001 51.5% 低 48.5% 高</td></tr><tr><td></td><td>010 50% 占空比（默认）</td></tr><tr><td></td><td>100 48.5% 低 51.5% 高</td></tr></table>
