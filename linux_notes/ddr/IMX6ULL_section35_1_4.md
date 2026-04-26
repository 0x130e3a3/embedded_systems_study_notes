# Chapter 35 Multi Mode DDR Controller (MMDC)

# 35.1 Overview

MMDC is a multi-mode DDR controller that supports DDR3/DDR3L x16 and LPDDR2x16 memory types. MMDC is configurable, high performance, and optimized. The following figure shows the MMDC block diagram. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/38b044e75ed1b59d806a215d31c9ae0ade0dbf737840b05492e7c8cf9170bdb3.jpg)



Figure 35-1. MMDC block diagram


MMDC consists of a core (MMDC_CORE) and PHY (MMDC_PHY). 

i.MX 6ULL Applications Processor Reference Manual, Rev. 1, 11/2017 

# Overview

• The core is responsible for communication with the system through an AXI interface, DDR command generation, DDR command optimizations, and a read/write data path. 

• The PHY is responsible for the timing adjustment; it uses special calibration mechanisms to ensure data capture margin at a clock rate of up to 400 MHz. 

The internal memory map (configuration registers) of the MMDC can be configured through an IP channel (IP0). 

# 35.1.1 MMDC feature summary

The table found here summarizes the MMDC features. 


Table 35-1. MMDC feature summary


<table><tr><td>Feature</td><td>Details</td></tr><tr><td>DDR standards</td><td>• DDR3L, DDR3 x16
• LPDDR2 x16
• Does not support LPDDR1MDDR or DDR2</td></tr><tr><td>DDR interface</td><td>• x16 data bus width
• Density per DDR device of 256 Mbits-8 Gbits with the following column and row combinations:
• Column size of 8-12 bits
• Row size of 11-16 bits
• Two chip selects (one chip select for DDR3/DDR3L, LPDDR2)
• Up to 4 Gbytes of address space with configurable partitioning between CS0 and CS1 (for LPDDR2 2ch x32 up to 2 Gbytes per channel)
• Supports burst length of 8 (aligned) for DDR3
• Supports burst length of 4 for LPDDR2</td></tr><tr><td>DDR performance</td><td>• MMDC running at up to 400 MHz (800MT/s), see CCM block for actual clock frequencies supported.
• Supports Real-Time priority by means of QoS sideband priority signals from the chip to enable various priority levels in the re-ordering mechanism: real-time, latency sensitive, normal priority.
• Page hit/page miss optimizations
• Consecutive read/write access optimizations
• Supports deep read and write request queues to enable bank prediction.
• Drives back the critical word in a read transaction as soon as it is received by the DDR device (does not wait until the whole data phase has been completed).
• Keeps tracking of open memory pages
• Supports bank interleaving
• Special optimization in case of non-aligned wrap accesses in DDR3 mode (burst length 8)
NOTE: Due to reordering and optimization mechanisms (per different AXI Identifier (ID)), the transactions towards the DDR device may be driven in a different ID order than was received by the AXI master. In a similar fashion, the write response, read response or read data may be driven to the AXI master in a different ID order.</td></tr><tr><td>AXI interface</td><td>• AXI bus compliant
• Supports bus transfers of 8, 16, 64 bits (single accesses and bursts) running at 400 MHz.</td></tr><tr><td></td><td>Supports AXI bursts length of up to 16Supports burst types of WRAP, INCR and FIXEDSupports 16 bits AXI IDWrite data interleave depth is 1 (no support for Write Data Interleave)Supports write data before addressSupports buffered/non-buffered accesses (AWCACHED[0] = 0b means a non-bufferable access and AWCACHED[0] = 1b means a bufferable access). The rest of the Cache options are not supportedTo keep data access coherency between write and read access of the same master, the response signal is sent as follows:Bufferable write access—BRESP will be sent when last data of the access has entered the MMDC.Non-bufferable write access—BRESP will be sent when the data was physically written into the external memory device.Supports four exclusive monitors per configurable ID for only a single access with a size of up to 64 bitsSupports AXI responses as follows:Okay in case the access has been successful or exclusive access failureSlave error in case of security violationExclusive okay in case the read or the write portion of an exclusive access has been successful</td></tr><tr><td>DDR calibration and delay-lines.</td><td>Supports various calibration processes which can be performed either automatically (hardware) or manually (software) towards either CS0 or CS1. (At the end of the process the delay-lines will work with one set of results.) The following calibration processes are supported:ZQ calibration for external DDR device (in DDR3 through ZQ calibration command and in LPDDR2 through MRW command)Can be handled automatically for ZQ Short (periodically) and ZQ Long (at exit from self-refresh)Can be handled manually at ZQ INITZQ calibration for DDR I/O pads for calibrating the DDR driving strengthThe sequence can be handled automatically by hardwareThe sequence can be handled step by step manually by softwareRead data calibration. Adjustment of read DQS with read data byte.Read DQS gating calibration for DDR3 only. Adjustment of DQS gate with read preamble window.Write data calibration. Adjustment of write DQS with write data byte.Write leveling calibration. Adjustment of write DQS with CK (DDR differential clock).Read fine tuning. Adjustment of up to 7 delay-line units for each read data bit.Write fine tuning. Adjustment of up to 3 delay-line units for each read data bit.Periodic delay-line measurement for keeping its accuracy during refresh interval.Additional fine tuning delay lines to adjust DDR clock delay, DDR clock duty cycle, DQS duty cycle.</td></tr><tr><td>Power saving</td><td>Support of dynamic voltage, frequency change and self-refresh mode entry through hardware and software negotiation with the system (request/acknowledge handshake)Upon hardware or software self-refresh request assertion, further AXI requests are blocked (even before the assertion of the acknowledge).During self-refresh mode the system may deassert the operating clock of the MMDC for power saving.During self-refresh mode the clock (CK) that is driven to the DDR device will be gated for power saving.Supports automatic self-refresh and power down entry and exitIn automatic self-refresh, the internal operating clock will be gated for power saving.</td></tr><tr><td></td><td>Supports fast and slow precharge power down in DDR3Automatic active and precharge power down timer per chip select (one chip select can enter power down while the other is still working)While CS (chip-select) is inactive (high) the command and address buses are not toggling for power saving.</td></tr><tr><td>DDR general</td><td>Configurable timing parametersConfigurable refresh schemePage boundary crossing supportAutomatically generates precharge command and activates the next rowSupports various ODT control schemesAssertion or deassertion of ODT control per read or write accesses and for active or passive CS (chip-select)Supports MRW and MRR commands for LPDDR2Software control in LPDDR2 mode for switching to derated timing parameters and/or update the refresh rate according to temperature sensorDebug and profiling capabilities</td></tr></table>

# 35.2 External Signals

The table found here describes the external signals of MMDC. 


Table 35-2. MMDC External Signals


<table><tr><td>Signal</td><td>Description</td><td>Pad</td><td>Mode</td><td>Direction</td></tr><tr><td>DRAM_ADDR[15:0]</td><td>Address Bus Signals</td><td>DRAM_A[15:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_CAS</td><td>Column Address Strobe Signal</td><td>DRAM_CAS</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_CS[1:0]</td><td>Chip Selects</td><td>DRAM_CS[1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_DATA[31:0]</td><td>Data Bus Signals</td><td>DRAM_D[31:0]</td><td>No Muxing</td><td>I/O</td></tr><tr><td>DRAM_DQM[1:0]</td><td>Data Mask Signals</td><td>DRAM_DQM[1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_ODT[1:0]</td><td>On-Die Termination Signals</td><td>DRAM_SDODT[1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_RAS</td><td>Row Address Strobe Signal</td><td>DRAM_RAS</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_RESET</td><td>Reset Signal</td><td>DRAM_RESET</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDBA[2:0]</td><td>Bank Select Signals</td><td>DRAM_SDBA[2:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDCKE[1:0]</td><td>Clock Enable Signals</td><td>DRAM_SDCKE[1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDCLK0_N</td><td>Negative Clock Signals</td><td>DRAM_SDCLK_1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDCLK0_P</td><td>Positive Clock Signals</td><td>DRAM_SDCLK_1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDQS[1:0]_N</td><td>Negative DQS Signals</td><td>DRAM_SDQS[1:0]_N</td><td>No Muxing</td><td>I/O</td></tr><tr><td>DRAM_SDQS[1:0]_P</td><td>Positive DQS Signals</td><td>DRAM_SDQS[1:0]_P</td><td>No Muxing</td><td>I/O</td></tr><tr><td>DRAM_SDWE</td><td>WE signal</td><td>DRAM_SDWE</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_ZQPAD</td><td>ZQ signal</td><td>DRAM_ZQPAD</td><td>No Muxing</td><td>O</td></tr></table>

# 35.3 Clocks

The table found here describes the clock sources for MMDC. 

See Clock Controller Module (CCM) for clock setting, configuration and gating information. 

# NOTE

The terms clocks and cycles are used interchangeably and refer to the clock period of the main ddr clock (mmdc_axi_clk_root), commonly referred to as the DDR frequency. 


Table 35-3. MMDC Clocks


<table><tr><td>Clock name</td><td>Clock Root</td><td>Description</td></tr><tr><td>aclk_fast_core_p0</td><td>mmdc_axi_clk_root</td><td>Fast clock (channel 1)</td></tr><tr><td>ipg_clk_p0</td><td>ipg_clk_root</td><td>Peripheral clock (channel 1)</td></tr><tr><td>aclk_fast_phy_p0</td><td>mmdc_axi_clk_root</td><td>Fast clock (channel 1 - PHY)</td></tr></table>

# 35.4 Functional Description

This section provides a complete functional description of the block. 

# 35.4.1 Write/Read data flow

# 35.4.1.1 Write data flow

1. Write requests are received into an 8 entry request FIFO. Access is received only when there are at least two available entries. Each entry holds all of the AXI attributes. 

• If the burst length is greater than 8, the access splits into two accesses: one with burst length 8 and the other with the remainder. 

• The access can be performed as soon as the entire data phase of the associated write request is completed (all data beats were received). 

2. A simple round-robin arbitration between the pending read and write accesses is performed, and the pointer to this stage's winner access is sent to the re-ordering buffer. 

# Functional Description

3. The reordering mechanism is activated to find the winner access, which is the access that best utilizes the DDR bus, based on its dynamic score. For further information see Dynamic scoring mode (Arbitration Winning Conditions). 

4. The winner write access at the previous stage is received and is held for dispatch to the DDR logic. 

5. When the DDR command control unit is ready to accept the write request, it issues (if needed) a precharge/active command to the DDR device according to the status of the bank model and the parameters of the timers. 

6. The DDR logic drives the associated data to the DDR device through the DDR PHY. 

# 35.4.1.2 Read data flow

1. Read requests are received into a 16 entry request FIFO in MMDC if there are at least two available entries. Each entry holds all of the AXI attributes. 

# NOTE

If the burst length is greater than 8, the access splits into 2 accesses (one with burst length 8 and the other with the remainder). 

2. A simple round-robin arbitration between the pending read and write accesses is performed and the pointer to this phase's winner access is sent to the re-ordering buffer. 

3. The reordering mechanism is activated to find the winner access, which is the access that best utilizes the DDR bus, based on its dynamic score. For further information see Dynamic scoring mode (Arbitration Winning Conditions). 

4. The winner read access at the previous stage is sampled and is held for dispatch to the DDR logic. This read access will be dispatched when there is at least one free slot in the read data buffer to store the data. 

5. When the DDR command control unit is ready to accept the read request, it issues (if needed) a precharge/active command to the DDR device according to the status of the bank model and the parameters of the timers. 

6. The MMDC PHY samples the read data, and the DDR logic transfers the data to the associated slot in the read data buffer. 

7. MMDC transfers the data back to the master. 

# 35.4.2 MMDC initialization

Because the MMDC is disabled when the chip exits reset, no clock is driven to the DDR device and the whole interface towards the DDR device is inactive. The following steps are required to activate the MMDC properly. 

# NOTE

To guarantee that the DRAM_RESET and DRAM_SDCKE signals are kept low during the power-up and reset sequences of the chip (as defined by JEDEC), you must connect those signals to pull-down resistors. 

1. Set MDSCR[CON_REQ], which sets the configuration request; note that because the MMDC is disabled, there is no need to poll the configuration acknowledge bit at MDSCR[CON_ACK]. 

2. Configure the desired timing parameters at the MDCFG0, MDCFG1, MDOTC, and MDCFG2 registers. 

3. Configure the DDR type and other miscellaneous parameters at the MDMISC register. 

4. Configure the required delay while leaving reset, at the MDOR register. 

5. Configure the DDR physical parameters (density and burst length) at the MDCTL register. 

6. Perform a ZQ calibration of the MMDC module to correctly initialize drive strengths. 

7. Enable MMDC with the desired chip select at MDCTL[SDE_0] (for chip select 0) and MDCTL[SDE_1] (for chip select 1). At this point, MMDC starts the reset and initialization sequence related to DRAM_RESET/DRAM_SDCKE as defined by JEDEC. 

8. Complete the initialization sequence as defined by JEDEC by issuing MRS/MRW commands for (ZQ, ODT, PRE, and so on). To issue those commands, configure the appropriate command and address at the MDSCR register. 

9. Program the DDR mode registers by configuring the appropriate command and address at the MDSCR register. 

10. Configure the power down and self-refresh entry and exit parameters at the MDPDC and MAPSR registers. 

11. Configure the ZQ scheme at the MPZQHWCTRL and MPZQLP2CTL registers. 

12. Configure and activate the periodic refresh scheme at the MDREF register. 

13. Deassert the configuration request by clearing MDSCR[CON_REQ]. 

# NOTE

Steps 1 through 6 are non-blocking and can be done in any order. 

Upon completion of these steps, MMDC is ready for work and to process AXI accesses. 

# NOTE

To achieve better timing and better precision, it is recommended that users configure the MMDC PHY delay parameters by operating either the automatic or manual 

i.MX 6ULL Applications Processor Reference Manual, Rev. 1, 11/2017 

# Functional Description

calibration process. Before starting any calibration process, you must disable the periodic refresh scheme (MDREF[REF_SEL] $= 1 1$ ) and then issue a manual refresh command by configuring MDSCR[CMD] to 2h. For further information, see Calibration Process. 

# 35.4.3 Configuring the MMDC registers

To safely modify MMDC's internal configuration registers, MMDC must be placed into configuration mode. 

Use the following steps to enter configuration mode. 

1. Issue a configuration request by setting MDSCR[CON_REQ]. 

2. Poll on configuration acknowledge until it is set at MDSCR[CON_ACK]. 

At this point, MMDC enters configuration mode and accessing the MMDC registers is permitted. 

# NOTE

During configuration mode, MMDC prevents further AXI accesses from being acknowledged. 

Upon deassertion of MDSCR[CON_REQ], MMDC leaves configuration mode and AXI accesses are processed. 

# 35.4.4 MMDC Address Space

# 35.4.4.1 Address decoding

MMDC supports up to two consecutive chip selects, each with the same density. 

It is optional to configure the partition between the chip selects through MDASP[CS0_END]. 

The incoming AXI address bus is 32 bits. MMDC decodes each access as follows: 

1. chip select 

2. bank number 

3. row number 

4. column number 

The following registers in the MMDC define the DDR address space: 

• MDMISC[DDR_4_BANK]—Defines either 4 or 8 banks in the DDR device 

• MDCTL[DSIZ]—Defines the DDR data bus width of x16 

• MDMISC[BI]—Defines whether bank interleaving is on or off 

• MDCTL[COL]—Defines the column size of the DDR device 

• MDCTL[ROW]—Defines the row size of the DDR device 

The following tables show address decoding examples for x16 bit DDR devices when bank interleaving is both on and off. It is assumed that the configuration is as follows: 8 banks (3 bits), 15 bit assignment for the row, and 10 bit assignment for the column. The total density is 256 MWords (512 Mbytes for x16 ). 

# NOTE

Chip selection is done by comparing the 7 most significant address bits (ARADDR[31:25]/AWADDR[31:25]) with MDASP[CS0_END]. 


Table 35-4. Address decoding—bank interleaving off


<table><tr><td>AXI ADDRESS</td><td>x16 DDR</td><td>x32 DDR</td></tr><tr><td>A29</td><td>—</td><td>BANK[2]</td></tr><tr><td>A28</td><td>BANK[2]</td><td>BANK[1]</td></tr><tr><td>A27</td><td>BANK[1]</td><td>BANK[0]</td></tr><tr><td>A26</td><td>BANK[0]</td><td>ROW[14]</td></tr><tr><td>A25</td><td>ROW[14]</td><td>ROW[13]</td></tr><tr><td>A24</td><td>ROW[13]</td><td>ROW[12]</td></tr><tr><td>A23</td><td>ROW[12]</td><td>ROW[11]</td></tr><tr><td>A22</td><td>ROW[11]</td><td>ROW[10]</td></tr><tr><td>A21</td><td>ROW[10]</td><td>ROW[9]</td></tr><tr><td>A20</td><td>ROW[9]</td><td>ROW[8]</td></tr><tr><td>A19</td><td>ROW[8]</td><td>ROW[7]</td></tr><tr><td>A18</td><td>ROW[7]</td><td>ROW[6]</td></tr><tr><td>A17</td><td>ROW[6]</td><td>ROW[5]</td></tr><tr><td>A16</td><td>ROW[5]</td><td>ROW[4]</td></tr><tr><td>A15</td><td>ROW[4]</td><td>ROW[3]</td></tr><tr><td>A14</td><td>ROW[3]</td><td>ROW[2]</td></tr><tr><td>A13</td><td>ROW[2]</td><td>ROW[1]</td></tr><tr><td>A12</td><td>ROW[1]</td><td>ROW[0]</td></tr><tr><td>A11</td><td>ROW[0]</td><td>COL[9]</td></tr><tr><td>A10</td><td>COL[9]</td><td>COL[8]</td></tr><tr><td>A9</td><td>COL[8]</td><td>COL[7]</td></tr><tr><td>A8</td><td>COL[7]</td><td>COL[6]</td></tr><tr><td>A7</td><td>COL[6]</td><td>COL[5]</td></tr><tr><td>A6</td><td>COL[5]</td><td>COL[4]</td></tr><tr><td>A5</td><td>COL[4]</td><td>COL[3]</td></tr><tr><td>A4</td><td>COL[3]</td><td>COL[2]</td></tr><tr><td>A3</td><td>COL[2]</td><td>COL[1]</td></tr><tr><td>A2</td><td>COL[1]</td><td>COL[0]</td></tr><tr><td>A1</td><td>COL[0]</td><td>—</td></tr><tr><td>A0</td><td>—</td><td>—</td></tr></table>


Table 35-5. Address decoding—bank interleaving on


<table><tr><td>AXI ADDRESS</td><td>x16 DDR</td><td>x32 DDR</td></tr><tr><td>A29</td><td>—</td><td>ROW[14]</td></tr><tr><td>A28</td><td>ROW[14]</td><td>ROW[13]</td></tr><tr><td>A27</td><td>ROW[13]</td><td>ROW[12]</td></tr><tr><td>A26</td><td>ROW[12]</td><td>ROW[11]</td></tr><tr><td>A25</td><td>ROW[11]</td><td>ROW[10]</td></tr><tr><td>A24</td><td>ROW[10]</td><td>ROW[9]</td></tr><tr><td>A23</td><td>ROW[9]</td><td>ROW[8]</td></tr><tr><td>A22</td><td>ROW[8]</td><td>ROW[7]</td></tr><tr><td>A21</td><td>ROW[7]</td><td>ROW[6]</td></tr><tr><td>A20</td><td>ROW[6]</td><td>ROW[5]</td></tr><tr><td>A19</td><td>ROW[5]</td><td>ROW[4]</td></tr><tr><td>A18</td><td>ROW[4]</td><td>ROW[3]</td></tr><tr><td>A17</td><td>ROW[3]</td><td>ROW[2]</td></tr><tr><td>A16</td><td>ROW[2]</td><td>ROW[1]</td></tr><tr><td>A15</td><td>ROW[1]</td><td>ROW[0]</td></tr><tr><td>A14</td><td>ROW[0]</td><td>BANK[2]</td></tr><tr><td>A13</td><td>BANK[2]</td><td>BANK[1]</td></tr><tr><td>A12</td><td>BANK[1]</td><td>BANK[0]</td></tr><tr><td>A11</td><td>BANK[0]</td><td>COL[9]</td></tr><tr><td>A10</td><td>COL[9]</td><td>COL[8]</td></tr><tr><td>A9</td><td>COL[8]</td><td>COL[7]</td></tr><tr><td>A8</td><td>COL[7]</td><td>COL[6]</td></tr><tr><td>A7</td><td>COL[6]</td><td>COL[5]</td></tr><tr><td>A6</td><td>COL[5]</td><td>COL[4]</td></tr><tr><td>A5</td><td>COL[4]</td><td>COL[3]</td></tr><tr><td>A4</td><td>COL[3]</td><td>COL[2]</td></tr><tr><td>A3</td><td>COL[2]</td><td>COL[1]</td></tr><tr><td>A2</td><td>COL[1]</td><td>COL[0]</td></tr><tr><td>A1</td><td>COL[0]</td><td>—</td></tr><tr><td>A0</td><td>—</td><td>—</td></tr></table>

# NOTE

In cases where this is an access to a non-initialized or disconnected chip select, behavior may be unexpected. 

# 35.4.4.2 Chip select settings

MMDC drives the incoming access to either CS0 or CS1 by comparing the 7 most significant address bits (ARADDR[31:25]/AWADDR[31:25]) with MDASP[CS0_END]. 

Generally, the total density per chip-select must be a power of two and the total density must be the same for each chip-select. 

Creating 4 Gbyte address space with 2 Gbyte CS density and Creating 2 Gbyte address spaces with 1 Gbyte CS density show how to create a continous address space and configure the MMDC accordingly. 

# 35.4.4.2.1 Creating 4 Gbyte address space with 2 Gbyte CS density

If the DDR memory space allocation is 4 Gbytes, only one configuration of chip select partition is allowed. The register MDASP[CS0_END] should be set to 2 Gbytes partition (16Gb). 

The figure below shows the associated memory space. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/63ce86576320fd9875718188a22c1645e2ac0a67a8fcd25c160aad1b76e98ec3.jpg)



Figure 35-2. Chip select partion—2 Gbytes per chip select


# 35.4.4.2.2 Creating 2 Gbyte address spaces with 1 Gbyte CS density

If the DDR memory space allocation is 2 Gbytes, there are three options for configuring the chip select partition:MDASP[CS0_END] to 001_1111 (1 Gbyte), MDASP[CS0_END] to 011_1111 (2 Gbytes), and MDASP[CS0_END] to 101_1111 (3 Gbytes). 

# Functional Description

If DDR memory space allocation is 2 Gbytes, there are three options for configuring the chip select partition: 

• MDASP[CS0_END] to 001_1111 (1 Gbyte) 

• MDASP[CS0_END] to 011_1111 (2 Gbytes) 

• MDASP[CS0_END] to 101_1111 (3 Gbytes) 

The figure below shows the associated memory space: 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/e355b01792121d2ba52900d3754bb248ea1e7ca344aebe6f412b70f1fd524074.jpg)



Figure 35-3. Chip select partion—1 Gbyte per chip select


# 35.4.4.3 Translation of AXI accesses to DDR accessess

# 35.4.4.3.1 Example 1

Assume the AXI read access has the following attributes: 

• Wrap (arburst $[ 1 { : } 0 ] = 1 0 \mathrm { b }$ ) 

• AXI size of 128 bits (arsize $[ 2 ; 0 ] = 1 0 0 0 )$ 

• AXI length of 8 (arlen[3:0] = 0111b) 

• AXI address with suffix B0h (non-aligned to AXI wrap boundary which is $1 6 \mathbf { B } \mathbf { x } 8 = 1 2 8 \mathbf { B } = 0 \mathbf { x } 8 0 )$ 

Toward DDR3(MDMISC[DDR_TYPE] = 00b) with the following attributes: 

• x32 (MDCTL[DSIZ] = 01b) 

• burst length of 8 (MDCTL[BL] = 1b) 

In this case, the AXI wrap boundary is every 16Bx8=128B (0x80) and the DDR wrap boundary is every $4 \mathbf { B } \mathbf { x } 8 { = } 3 2 \mathbf { B } ( 0 \mathbf { x } 2 0 )$ . 

The master expects to fetch the data that is associated with the following addresses: 0xB0, 0xC0, 0xD0, 0xE0, 0xF0, 0x80, 0x90, 0xA0. 

The first aligned AXI address that is associated with suffix 0xB0 is with suffix $0 \mathrm { { x } 8 0 }$ , and the last wrap AXI address is with suffux 0xFF. Because the AXI master expects to get the first data from AXI address with suffix 0xB0, the MMDC issues the following accesses toward the DDR: 

• Read access toward logic address with suffix 0xA0 (DDR boundary is $0 \times 2 0$ and 0xA0 is the closest to 0xB0) 

# NOTE

Logic address is the address of the column normalized to 1 byte. 

• Read access toward logic address with suffix 0xC0 

• Read access toward logic address with suffix 0xE0 

• Read access toward logic address with suffix 0x80 

The MMDC breaks the AXI access into four DDR accesses and returns the read data associated with address 0xB0 to the master first. The read data fetched from address 0xA0 is stored in the internal buffers and is driven back to the master at the end. 

# 35.4.4.3.2 Example 2

Assume the AXI write access has the following attributes: 

• Increment (awburst[1:0]=2'b01) 

• AXI size of 64bits (awsize[2:0]=3'b011) 

• AXI length of 8 (awlen[3:0]=4'b0111) 

• AXI address with suffix 0xB0 (aligned as the size of the increment is 8B) 

Toward DDR3(MDMISC[DDR_TYPE]=2'b00) with the following attributes: 

• x64 (MDCTL[DSIZ]=2'b10) 

• burst length of 8 (MDCTL[BL]=1'b1) 

In this case, the AXI alignment is every 8B and the DDR boundary is every $8 \mathrm { B x } 8 { = } 6 4 \mathrm { B } ( 0 \mathrm { x } 4 0 )$ . 

The master expects to write the data to the following addresses: 0xB0, 0xB8, 0xC0, 0xC8, 0xD0, 0xD8, 0xE0, 0xE8. 

The MMDC will issue the following accesses toward the DDR: 

# Functional Description

• Write access toward logic address with suffix 0x80 (DDR boundary is 0x40 and $0 \mathrm { { x } 8 0 }$ is the closest to 0xB0) while address $0 \times 8 0$ to 0xAF are masked by DM (data masking signal). 

# NOTE

Logic address is the address of the column normalized to 1 byte. 

• Write access toward logic address with suffix 0xC0 while addresses 0xF0 through 0xFF are masked by DM (data masking signal) 

The MMDC will break the AXI access into two DDR accesses. 

# 35.4.4.3.3 Example 3

Assume the AXI write access has the following attributes: 

• Wrap (awburst[1:0]=2'b10) 

• AXI size of 128bits (awsize[2:0] $=$ 3'b100) 

• AXI length of 4 (awlen[3:0]=4'b0011) 

• AXI address with suffix 0x80 (aligned) 

Toward DDR3(MDMISC[DDR_TYPE]=2'b00) with the following attributes: 

• x64 (MDCTL[DSIZ]=2'b10) 

• burst length of 8 (MDCTL[BL]=1'b1) 

In this case, the AXI wrap boundary is every 16Bx4=64B (0x40) and the DDR wrap boundary is every $8 \mathrm { x } 8 { = } 6 4 \mathrm { B } ( 0 \mathrm { x } 4 0 )$ . 

The master expects to write the data to the following addresses: 0x80, 0x90, 0xA0, 0xB0. 

Because the AXI wrap boundary and DDR wrap boundary are similar and the starting AXI address is aligned, the MMDC will issue only one access toward the DDR as follows: 

• Write access towards logic address with suffix 0x80 

# NOTE

Logic address is the address of the column normalized to 1 byte. 

# 35.4.4.3.4 Example 4

Assume the AXI write access has the following attributes: 

• Increment (awburst[1:0]=2'b01) 

• AXI size of 64bits (awsize[2:0]=3'b011) 

• AXI length of 2 (awlen[3:0]=4'b0001) 

• AXI address with suffix 0x5 (non aligned) 

Toward DDR3(MDMISC[DDR_TYPE]=2'b00) with the following attributes: 

• x32 (MDCTL[DSIZ]=2'b10) 

• burst length of 8 (MDCTL[BL]=1'b1) 

In this case the AXI alignment is every 8B (0x8) and the DDR boundary is every $4 \mathbf { B } \mathbf { x } 8 { = } 3 2 \mathbf { B } ( 0 \mathbf { x } 2 0 )$ . 

The master expects to write the data to the following addresses: 0x5 (with WSTRB=0xE0), 0x8 (till 0xF). 

The MMDC will issue one access toward the DDR as follows: 

Write access toward logic address with suffix 0x0 (DDR boundary is $0 \times 2 0$ and $0 \mathrm { x 0 }$ is the closest to 0x0) while address 0x0 till 0x4 are masked by DM (data masking signal) and address 0x10 till 0x1F are also masked by DM. 

# 35.4.4.3.5 Example 5

Assume AXI write access has the following attributes: 

• Increment (awburst[1:0]=2'b01) 

• AXI size of 64bits (awsize[2:0]=3'b011) 

• AXI length of 7 (awlen[3:0]=4'b0001) 

• AXI address with suffix 0x10 (aligned) 

Toward DDR3 (MDMISC[DDR_TYPE]=2'b00) with the following attributes: 

• x64 (MDCTL[DSIZ]=2'b10) 

• burst length of 8 (MDCTL[BL]=1'b1) 

In this case the AXI alignment is every 8B (0x8) and the DDR boundary is every $8 \mathrm { B x } 8 { = } 6 4 \mathrm { B } ( 0 \mathrm { x } 4 0 )$ . 

The master expects to write the data to the following addresses: 0x10, 0x18, 0x20, 0x28, 0x30, 0x38, 0x40, 0x48. 

Because the AXI access is not aligned to DDR boundary, which is every 0x40, the MMDC will issue two accesses toward the DDR as follows: 

• Write access toward logic address with suffix 0x0 while address 0x0 till 0xF are masked by DM (data masking signal). 

# NOTE

Logic address is the address of the column normalized to 1 byte. 

• Write access towards logic address with suffix 0x40 while addresses 0x50 till 0x7F are masked by DM (data masking signal). 

# 35.4.4.4 Address mirroring

When enabling this feature, address bits DRAM_A3, DRAM_A4, DRAM_A5, DRAM_A6, DRAM_A7, DRAM_A8, DRAM_SDBA0, and DRAM_SDBA1 behave differently according to the associated chip select. 

This feature facilitates PCB board routing for devices on chip select 1, which are typically populated on the opposite side of the PCB from the devices on chip select 0. 

# NOTE

This feature will not be supported for DDR3 since only a single chip select is supported for DDR3 

The following table specifies the address mirroring options: 


Table 35-6. Address mirroring options


<table><tr><td>MMDC pin</td><td>Chip select 0 pin</td><td>Chip select 1 pin</td></tr><tr><td>DRAM_A3</td><td>DRAM_A3</td><td>DRAM_A4</td></tr><tr><td>DRAM_A4</td><td>DRAM_A4</td><td>DRAM_A3</td></tr><tr><td>DRAM_A5</td><td>DRAM_A5</td><td>DRAM_A6</td></tr><tr><td>DRAM_A6</td><td>DRAM_A6</td><td>DRAM_A5</td></tr><tr><td>DRAM_A7</td><td>DRAM_A7</td><td>DRAM_A8</td></tr><tr><td>DRAM_A8</td><td>DRAM_A8</td><td>DRAM_A7</td></tr><tr><td>DRAM_SDBA0</td><td>DRAM_SDBA0</td><td>DRAM_SDBA1</td></tr><tr><td>DRAM_SDBA1</td><td>DRAM_SDBA1</td><td>DRAM_SDBA0</td></tr></table>

# 35.4.5 LPDDR2 and DDR3 pin mux mapping

The following table shows the pin mux mapping between LPDDR2 and DDR3. The i.MX DDR I/O pads corresponds with the DDR3 standard. 

• In DDR3, all DRAM_DATA, DRAM_SDQS, and DRAM_DQM data lines work with channel 0. 

• In LPDDR2, DRAM_DDQS[3:0], DRAM_DATA[31:0] and DRAM_DQM[3:0] work with channel 0. DRAM_SDQS[7:4], DRAM_DATA[63:32], and DRAM_DQM[7:4] work with channel 1. 


Table 35-7. LPDDR2 and DRAM pin mux mapping


<table><tr><td>DRAM I/O pad</td><td>LPDDR2 I/O pad</td></tr><tr><td>DRAM_ADDR00</td><td>LPDDR2_CA0</td></tr><tr><td>DRAM_ADDR01</td><td>LPDDR2_CA1</td></tr><tr><td>DRAM_ADDR02</td><td>LPDDR2_CA2</td></tr><tr><td>DRAM_ADDR03</td><td>LPDDR2_CA3</td></tr><tr><td>DRAM_ADDR04</td><td>LPDDR2_CA4</td></tr><tr><td>DRAM_ADDR05</td><td>LPDDR2_CA5</td></tr><tr><td>DRAM_ADDR06</td><td>LPDDR2_CA6</td></tr><tr><td>DRAM_ADDR07</td><td>LPDDR2_CA7</td></tr><tr><td>DRAM_ADDR08</td><td>LPDDR2_CA8</td></tr><tr><td>DRAM_ADDR09</td><td>LPDDR2_CA9</td></tr><tr><td>DRAM_ADDR10</td><td>—</td></tr><tr><td>DRAM_ADDR11</td><td>—</td></tr><tr><td>DRAM_ADDR12</td><td>—</td></tr><tr><td>DRAM_ADDR13</td><td>—</td></tr><tr><td>DRAM_ADDR14</td><td>—</td></tr><tr><td>DRAM_ADDR15</td><td>—</td></tr><tr><td>DRAM_CAS_B</td><td>—</td></tr><tr><td>DRAM_RAS_B</td><td>—</td></tr><tr><td>DRAM_WE_B</td><td>—</td></tr><tr><td>DRAM_SDCKE0</td><td>LPDDR2_CKE0</td></tr><tr><td>DRAM_SDCKE1</td><td>LPDDR2_CKE1</td></tr><tr><td>DRAM_CS_B0</td><td>LPDDR2_CS_B0</td></tr><tr><td>DRAM_CS_B1</td><td>LPDDR2_CS_B1</td></tr><tr><td>DRAM_ODT0</td><td>LPDDR2_ODT0</td></tr><tr><td>DRAM_ODT1</td><td>LPDDR2_ODT1</td></tr><tr><td>DRAM_SDCLK0_P</td><td>LPDDR2_CK0</td></tr><tr><td>DRAM_SDCLK1</td><td>LPDDR2_CK1</td></tr><tr><td>DRAM_BA0</td><td>—</td></tr><tr><td>DRAM_BA1</td><td>—</td></tr><tr><td>DRAM_BA2</td><td>—</td></tr></table>

# 35.4.6 Power Saving and Clock Frequency Change modes

# 35.4.6.1 Power saving general

MMDC supports multiple DDR power saving modes. 

# NOTE

At default, the power saving modes are disabled. These modes may dramatically decrease the power consumption of DDR memories. 

1. Self-refresh entry to the entire DDR device (for both chip select 0 and 1) can be activated through two mechanisms: 

• LPMD (Low Power Mode) 

• Hardware handshaking (LPMD/LPACK) with the clock module in the system 

• Software handshaking by setting the field MAPSR[LPMD] and polling MAPSR[LPACK] 

• Automatic entry by configuring the amount of idle cycle for triggering selfrefresh entry through MAPSR[PST] and by clearing MAPSR[PSD] 

• DVFS (Dynamic Voltage and Frequency Change) 

• Hardware handshaking (DVFS/DVACK) with the clock module in the system 

• Software handshaking by setting the field MAPSR[DVFS] and polling MAPSR[DVACK] 

# NOTE

If hardware or software requests for self-refresh entry were detected by the MMDC (even before the assertion of the LPACK), no write or read accesses will be acknowledged until the deassertion of those requests. 

2. Automatic active/precharge power down entry to a specific chip select can be activated by configuring the ESDPDC register: 

• PWDT_0/PWDT_1 - define the number of idle cycles before entering power down, can be different value per chip select. 

• SLOW_PD - In case of DDR3 memory is configured to use slow precharge power down then this bit should be set as well. 

• BOTH_CS_PS - The MMDC can either set each chip select independently to power down, according to its idle state, or set both chip selects to power down only if both in idle state for the configured period. 

• Few parameters must be configured in addition: 

• Timing parameters at MDCFG0[tXP and tXPDLL]. 

• ODT timing at MDOTC[tAOFPD, tAONPD, tANPD and tAXPD] 

# NOTE

It is possible to enter certain chip selects to low power consumption while the second chip select is activated. 

3. Automatic precharge of all DDR banks to a specific chip select. Can be activated by configuring ESDPDC fields: PRCT_0 and PRCT_1. Each field determines a value loaded to a different chip select. 

# 35.4.6.2 Self refresh and Frequency change entry/exit

As described in Power saving general, the MMDC supports two mechanisms that will cause the DDR device to enter self-refresh mode: 

• LPMD (Low Power Mode) - For power saving purposes 

• DVFS (Dynamic Voltage and Frequency Change) - For clock frequency changes 

While the DDR device is in self-refresh mode, there is no need to provide periodic refresh commands. 

The MMDC treats hardware/software handshaking of LPMD/DVFS in the same manner: 

• Upon the assertion of LPMD/DVFS request, the following is done: 

• The MMDC blocks any further AXI accesses even before the acknowledge is asserted 

• Completes all opened AXI accesses 

• Closes (precharge) all banks in the appropriate timing 

• Drives self-refresh command by deasserting clock enable signal (DRAM_SDCKE is driven to $" 0 "$ ) together with a refresh command. This occurs after satisfying tRP/tRPA from the precharge all command. 

• Deasserts the clock (CK) that is driven to the DDR device 

• Asserts LPMD/DVFS acknowledge (LPACK/DVACK) 

• Allows deassertion of the operating clock of the MMDC (AXI clock) 

• Upon the deassertion of LPMD/DVFS request, the following is done: 

• Operating clock of the MMDC must be turned on before LPMD/DVFS is deasserted 

• Starts driving the clock (CK) to the DDR device 

• After satisfying tCKSRX from clock renewal the clock enable signal (DRAM_SDCKE) is asserted 

• LPMD/DVFS acknowledge (LPACK/DVACK) is deasserted 

# Functional Description

• After satisfying tXS from the assertion of DRAM_SDCKE, a refresh command is driven to the DDR device. 

• If ZQ calibration is enabled then tRFC is satisfied from the refresh command and a long ZQ command is driven. 

• tZQoper idle cycles are counted after the ZQ command. 

• After satisfying tDLLK from the assertion DRAM_SDCKE, the MMDC returns to normal operation. 

The figure below shows the timing diagram of the hardware/software handshaking of LPMD/DVFS: 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/992dc6e3050a7b3e7c1a13bf942bc250f90ebd776f8578611b5b028a747cbd66.jpg)



Figure 35-4. LPMD/DVFS Hardware/Software Handshaking


Note for self-refresh: 

• As soon as LPMD or DVFS requests are detected by either hardware or software handshaking, the MMDC will deassert the AXI ARREADY/AWREADY signals immediately to block further requests from the system. 

• In case of automatic self-refresh, the internal operating clock will be negated to save power. 

# 35.4.7 Reset

# 35.4.7.1 Hard reset

When hard reset is asserted (aresetn is driven to $" 0 "$ ) while warm reset is deasserted (warm_reset is driven to $" 0 "$ ), the entire MMDC will be initialized, including configuration/status registers and state machines. 

In order to access the DDR device, the MMDC will then have to be reconfigured. 

# 35.4.7.2 Warm reset

The MMDC supports warm reset signal. The warm reset signal must envelop the hard reset signal and then the MMDC will reset all the internal registers. The only registers that are not reset are those that are essential for returning it to normal operation without repeating the initialization sequence and without losing data stored in the memory (configuration/status registers won't be initialized). 

For the successful operation of warm reset, the following steps must be performed: 

• The MMDC must enter self-refresh mode. This can be achieved by either LPMD or DFVS requests 

• Wait for LPMD or DVFS acknowledge 

• Assert warm reset signal (i.e. drive warm_reset to "1") 

• Assert hard reset signal (i.e. drive aresetn to "0") 

• Deassert hard reset signal 

• Deassert warm reset 

• Get out of the LPMD/DVFS mode 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-22/6dad159b-7fa4-4cd5-9a0a-2f4207cb43bf/540c8d7db3a3fca3e890853e9fea499f18e4d39ee54b1ef773ed9e7fc6478236.jpg)



Figure 35-5. Warm Reset Diagram


# 35.4.7.3 Software reset

The MMDC supports software reset. When software reset is configured then the MMDC will reset all the internal registers except those that are essential for returning to normal operation without repeating the initialization sequence or without losing data stored in the memory (configuration/status registers won't be initialized). 

The following steps should be performed for successful operation of software reset: 

• The MMDC should enter self-refresh mode. This can be achieved by either LPMD or DFVS request. 

• Wait for LPMD or DVFS acknowledge 

# Functional Description

• Assert software reset, by setting MDMISC[RST] 

• Get out of the LPMD/DVFS mode 

Normal operation can be resumed. 

# 35.4.8 Refresh Scheme

The MMDC supports various automatic refresh options which can be configured via the MDREF register. 

The periodic auto refresh can be triggered by the following clocks: 

• 32 kHz clock 

• 64 kHz clock 

• MMDC operating clock 

The refresh scheme of the MMDC is flexible and allows the system to configure the desired AXI accesses delay/latency in each refresh cycle. 

The table below shows an example of four configurations of the refresh cycles that will be handled by the MMDC. Each configuration meets a refresh rate of 3.9μs (tREFI, refresh command every $3 . 9 \mu \mathrm { s } \dot { }$ ). 


Table 35-8. MMDC Refresh Scheme


<table><tr><td>Option number</td><td>Description</td><td>REFR</td><td>REF_SEL</td><td>REF_CNT</td><td>DDR hang time</td></tr><tr><td>1</td><td>Issue 8 refresh commands every 31,250 ns</td><td>0x7 (8 refreshes)</td><td>0x0 (64 kHz)</td><td>not needed</td><td>tRFC x 8</td></tr><tr><td>2</td><td>Issue 4 refresh commands every 15,625ns</td><td>0x3 (4 refreshes)</td><td>0x1(32 kHz)</td><td>not needed</td><td>tRFC x 4</td></tr><tr><td>3</td><td>Issue 2 refresh commands every 7800ns</td><td>0x1(2 refreshes)</td><td>0x2 (REF_CNT)</td><td>7800/2.5 = 3120 (0xC30)</td><td>tRFC x 2</td></tr><tr><td>4</td><td>Issue 1 refresh command every 3900 ns</td><td>0x0 (1 refresh)</td><td>0x2 (REF_CNT)</td><td>3900/2.5 = 1560(0x618)</td><td>tRFC</td></tr></table>

# 35.4.9 Burst Length options towards DDR

The MMDC supports burst lengths which can be configured through MD+CTL[BL] as follows: 

• In DDR3 mode, only burst length 8 can be used. 

• In LPDDR2 mode, only burst length 4 can be used. 

In DDR3 mode read/write accesses to the DDR are always 8 words (x16) and aligned in according to JEDEC standards. 

In case of AXI INCREMENT, accesses that are not aligned the irrelevant data is masked in write accesses and ignored in read accesses. In case of AXI WRAP accesses, even if the access is not aligned, then the MMDC provides an internal optimization mechanism for better efficiency of the DDR data bus. 

# 35.4.10 Exclusive accesses handling

The MMDC contains four exclusive monitors, each for dedicated ID as configured in MAEXIDR0 and MAEXIDR1. 

• If legal read exclusive is received by the MMDC, the associated monitor is turned on. 

• While the monitor is turned on upon legal write exclusive, the monitor will be turned off and the write will be completed successfully with EXOKAY. 

• The following rules must be met for successful exclusive access: 

• Aligned access (the AXI address is aligned to the AXI size) 

• AXI single access (AXI burst length isn't greater than 1) 

• AXI size of up to 64 bits 

• AXI non-cachable access (i.e. ARCACHE[1]/AWCACHE[1] is equal "0" or ARCACHE[1]/AWCACHE[1] is equal "1" while ARCACHE[3:2]/ AWCACHE[3:2] are equal "00") 

• AXI ID that matches one of the four exclusive IDs 

Exclusive read behavior (first bullet also correct for non-exclusive accesses): 

• In case of security violation, the read is blocked and is not sent to DDR. There are two options for response: 

• If ARCR_SEC_ERR_EN (MAARCR[30] ) is high, SLV error is issued towards the Master, otherwise OKAY response is sent to the Master. 

• If AXI exclusive rules violation occurs (as described above), the read access is not blocked and is sent to DDR. The data will be fetched and be driven to the master, but the type of response may be unpredicted. 

• If none of the above occurs, the read is sent to the DDR. The exclusive monitor will be turned on and the response is EXOKAY 

• If additional legal AXI read exclusive is received with the same ID before the AXI exclusive write, the monitor will be updated with the latest attributes. 

Exclusive write behavior (first bullet also correct for non-exclusive accesses): 

# Performance

• In case of security violation, the write is blocked and is not sent to DDR, but the monitor will be kept on. There are two options for response: 

• If ARCR_SEC_ERR_EN (MAARCR[30]) is high then SLV error is issued towards the Master, otherwise OKAY response is sent to the Master. 

• In case of AXI exclusive rules violation (as described above), the write is blocked and is not sent to DDR. In that case the type of response may be unpredicted. 

• In case the exclusive write access has different AXI attributes, but the same ID as the read exclusive access, the write is blocked and is not sent to DDR and the monitor will be turned off. There are two options for response: 

• If ARCR_EXC_ERR_EN (MAARCR[28]) is high then SLV error is issued towards the Master, otherwise OKAY response is sent to the Master. 

• In case of regular (non exclusive) write access is received to the same address or overlapping addresses then the write will be sent to the DDR and the monitor will be turned off. 

• In case of legal write exclusive access is received with the same attributes as the read exclusive access while the monitor is on ( no write accesses occured to the same address between the read exclusive and write exclusive), then the write is sent to DDR and the response is EXOKAY. But, if the legal write exclusive is received while the monitor is off, the write is blocked and there are two options for response. 

• If ARCR_EXC_ERR_EN (MAARCR[28]) is high then SLV error is issued towards the Master, otherwise OKAY response is sent to the Master. 

# 35.4.11 AXI Error Handling

The MMDC supports the AXI responses listed here. 

• In case of AXI exclusive violation there are two options for response: 

• If MAARCR[28] is high then SLV Error is issued towards the Master, Otherwise OKAY response is sent to the Master 

# NOTE

In case of read error MMDC drives zeros on the read data bus 
