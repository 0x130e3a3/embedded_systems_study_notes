# JEDEC STANDARD

# DDR3 SDRAM Standard

# JESD79-3D

(Revision of JESD79-3C, November 2008) 

September 2009 

JEDEC SOLID STATE TECHNOLOGY ASSOCIATION 

# NOTICE

JEDEC standards and publications contain material that has been prepared, reviewed, and approved through the JEDEC Board of Directors level and subsequently reviewed and approved by the JEDEC legal counsel. 

JEDEC standards and publications are designed to serve the public interest through eliminating misunderstandings between manufacturers and purchasers, facilitating interchangeability and improvement of products, and assisting the purchaser in selecting and obtaining with minimum delay the proper product for use by those other than JEDEC members, whether the standard is to be used either domestically or internationally. 

JEDEC standards and publications are adopted without regard to whether or not their adoption may involve patents or articles, materials, or processes. By such action JEDEC does not assume any liability to any patent owner, nor does it assume any obligation whatever to parties adopting the JEDEC standards or publications. 

The information included in JEDEC standards and publications represents a sound approach to product specification and application, principally from the solid state device manufacturer viewpoint. Within the JEDEC organization there are procedures whereby a JEDEC standard or publication may be further processed and ultimately become an ANSI standard. 

No claims to be in conformance with this standard may be made unless all requirements stated in the standard are met. 

Inquiries, comments, and suggestions relative to the content of this JEDEC standard or publication should be addressed to JEDEC at the address below, or call (703) 907-7559 or www.jedec.org 

# Published by

©JEDEC Solid State Technology Association 2009 

3103 North 10th Street, Suite 240 South 

Arlington, VA 22201 

This document may be downloaded free of charge; however JEDEC retains the copyright on this material. By downloading this file the individual agrees not to charge for or resell the resulting material. 

# PRICE: Please refer to the current

Catalog of JEDEC Engineering Standards and Publications online at 

http://www.jedec.org/Catalog/catalog.cfm 

Printed in the U.S.A. 

All rights reserved 

# PLEASE!

# DON'T VIOLATE THE LAW!

This document is copyrighted by JEDEC and may not be reproduced without permission. 

Organizations may obtain permission to reproduce a limited number of copies through entering into a license agreement. For information, contact: 

JEDEC Solid State Technology Association 

3103 North 10th Street, Suite 240 South 

Arlington, Virginia 22201 

or call (703) 907-7559 

# Contents

1 Scope... 

2 DDR3 SDRAM Package Pinout and Addressing . 3 

2.1 DDR3 SDRAM x4 Ballout using MO-207. 3 

2.2 DDR3 SDRAM x8 Ballout using MO-207.. .4 

2.3 DDR3 SDRAM x16 Ballout using MO-207.. .5 

2.4 Stacked / dual-die DDR3 SDRAM x4 Ballout using MO-207. .6 

2.5 Stacked / dual-die DDR3 SDRAM x8 Ballout using MO-207. 7 

2.6 Stacked / dual-die DDR3 SDRAM x16 Ballout using MO-207. .8 

2.7 Quad-stacked / Quad-die DDR3 SDRAM x4 Ballout using MO-207. .9 

2.8 Quad-stacked / Quad-die DDR3 SDRAM x8 Ballout using MO-207. . 10 

2.9 Quad-stacked / Quad-die DDR3 SDRAM x16 Ballout using MO-207.. 11 

2.10 Pinout Description. .13 

2.11 DDR3 SDRAM Addressing. .15 

2.11.1 512Mb . 15 

2.11.2 1Gb.. .15 

2.11.3 2Gb . . 15 

2.11.4 4Gb . . 15 

2.11.5 8Gb . 16 

3 Functional Description. . 17 

3.1 Simplified State Diagram. .17 

3.2 Basic Functionality .18 

3.3 RESET and Initialization Procedure .. .19 

3.3.1 Power-up Initialization Sequence . . 19 

3.3.2 Reset Initialization with Stable Power.. .21 

3.4 Register Definition . . 22 

3.4.1 Programming the Mode Registers .. . 22 

3.4.2 Mode Register MR0. . 23 

3.4.3 Mode Register MR1. .27 

3.4.4 Mode Register MR2. . 30 

3.4.5 Mode Register MR3. . 32 

4 DDR3 SDRAM Command Description and Operation.. . 33 

4.1 Command Truth Table . .33 

4.2 CKE Truth Table.. . 35 

4.3 No OPeration (NOP) Command . . 36 

4.4 Deselect Command . . 36 

4.5 DLL-off Mode.. . 37 

4.6 DLL on/off switching procedure.. . 38 

4.6.1 DLL “on” to DLL “off” Procedure. . 38 

4.6.2 DLL “off” to DLL “on” Procedure. . 39 

4.7 Input clock frequency change . . 40 

4.8 Write Leveling . . 42 

4.8.1 DRAM setting for write leveling & DRAM termination function in that mode ...... 43 

4.8.2 Procedure Description. .43 

4.8.3 Write Leveling Mode Exit . .45 

# Contents

4.9 Extended Temperature Usage . .. 46 

4.9.1 Self-Refresh Temperature Range - SRT . .. 46 

4.10 Multi Purpose Register.. . 48 

4.10.1 MPR Functional Description . 49 

4.10.2 MPR Register Address Definition . 50 

4.10.3 Relevant Timing Parameters. . 50 

4.10.4 Protocol Example. . 50 

4.11 ACTIVE Command . 55 

4.12 PRECHARGE Command . .55 

4.13 READ Operation.. . 56 

4.13.1 READ Burst Operation. . 56 

4.13.2 READ Timing Definitions 57 

4.13.3 Burst Read Operation followed by a Precharge. .. 66 

4.14 WRITE Operation . . 68 

4.14.1 DDR3 Burst Operation . . 68 

4.14.2 WRITE Timing Violations . 68 

4.14.3 Write Data Mask . .69 

4.14.4 tWPRE Calculation.. . 70 

4.14.5 tWPST Calculation . . 70 

4.15 Refresh Command.. . 77 

4.16 Self-Refresh Operation . 79 

4.17 Power-Down Modes .81 

4.17.1 Power-Down Entry and Exit. . 81 

4.17.2 Power-Down clarifications - Case 1 . .86 

4.17.3 Power-Down clarifications - Case 2 .. . 87 

4.17.4 Power-Down clarifications - Case 3 .. . 88 

4.18 ZQ Calibration Commands .. . 89 

4.18.1 ZQ Calibration Description.. . 89 

4.18.2 ZQ Calibration Timing . . 90 

4.18.3 ZQ External Resistor Value, Tolerance, and Capacitive loading . . 90 

5 On-Die Termination (ODT).. .91 

5.1 ODT Mode Register and ODT Truth Table. . 91 

5.2 Synchronous ODT Mode . . 92 

5.2.1 ODT Latency and Posted ODT.. . 92 

5.2.2 Timing Parameters . . 92 

5.2.3 ODT during Reads . . 94 

5.3 Dynamic ODT. .96 

5.3.1 Functional Description:. . 96 

5.3.2 ODT Timing Diagrams. . 97 

5.4 Asynchronous ODT Mode . .. 102 

5.4.1 Synchronous to Asynchronous ODT Mode Transitions. .. 103 

5.4.2 Synchronous to Asynchronous ODT Mode Transition during Power-Down Entry103 

5.4.3 Asynchronous to Synchronous ODT Mode Transition during Power-Down Exit.106 

# Contents

5.4.4 Asynchronous to Synchronous ODT Mode during short CKE high and short CKE low periods.. .107 

6 Absolute Maximum Ratings . .. 109 

6.1 Absolute Maximum DC Ratings. .109 

6.2 DRAM Component Operating Temperature Range . .. 109 

7 AC & DC Operating Conditions. 111 

7.1 Recommended DC Operating Conditions.. .111 

8 AC and DC Input Measurement Levels. .113 

8.1 AC and DC Logic Input Levels for Single-Ended Signals . .113 

8.1.1 AC and DC Input Levels for Single-Ended Command and Address Signals.........113 

8.1.2 AC and DC Input Levels for Single-Ended Data Signals. .113 

8.2 Vref Tolerances. .114 

8.3 AC and DC Logic Input Levels for Differential Signals .. .115 

8.3.1 Differential signal definition. .115 

8.3.2 Differential swing requirements for clock (CK - CK#) and strobe (DQS - DQS#)115 

8.3.3 Single-ended requirements for differential signals . .116 

8.4 Differential Input Cross Point Voltage . .117 

8.5 Slew Rate Definitions for Single-Ended Input Signals.. .119 

8.6 Slew Rate Definitions for Differential Input Signals. .119 

9 AC and DC Output Measurement Levels . .121 

9.1 Single Ended AC and DC Output Levels. .121 

9.2 Differential AC and DC Output Levels . .121 

9.3 Single Ended Output Slew Rate.. .. 122 

9.4 Differential Output Slew Rate.. .123 

9.5 Reference Load for AC Timing and Output Slew Rate . .. 124 

9.6 Overshoot and Undershoot Specifications. .. 125 

9.6.1 Address and Control Overshoot and Undershoot Specifications. .125 

9.6.2 Clock, Data, Strobe and Mask Overshoot and Undershoot Specifications. .. 126 

9.7 34 ohm Output Driver DC Electrical Characteristics . .. 127 

9.7.1 Output Driver Temperature and Voltage sensitivity. .128 

9.8 On-Die Termination (ODT) Levels and I-V Characteristics . .130 

9.8.1 On-Die Termination (ODT) Levels and I-V Characteristics . .. 130 

9.8.2 ODT DC Electrical Characteristics. .131 

9.8.3 ODT Temperature and Voltage sensitivity .. .. 134 

9.9 ODT Timing Definitions.. .134 

9.9.1 Test Load for ODT Timings . .134 

9.9.2 ODT Timing Definitions. .135 

10 IDD and IDDQ Specification Parameters and Test Conditions.. .139 

10.1 IDD and IDDQ Measurement Conditions . .139 

10.2 IDD Specifications. .150 

11 Input/Output Capacitance . .153 

11.1 Input/Output Capacitance . .153 

# Contents

12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133.. .. 155 

12.1 Clock Specification . .155 

12.1.1 Definition for tCK(avg) . .155 

12.1.2 Definition for tCK(abs).. .155 

12.1.3 Definition for tCH(avg) and tCL(avg).. .155 

12.1.4 Definition for tJIT(per) and tJIT(per,lck) . .155 

12.1.5 Definition for tJIT(cc) and tJIT(cc,lck) . .156 

12.1.6 Definition for tERR(nper).. .156 

12.2 Refresh parameters by device density. .156 

12.3 Standard Speed Bins . .157 

12.3.1 Speed Bin Table Notes 165 

13 Electrical Characteristics and AC Timing . .. 167 

13.1 Timing Parameters for DDR3-800, DDR3-1067, DDR3-1333, and DDR3-1600.......167 

13.2 Timing Paramters for DDR3-1866 and DDR3-2133 Speed Bins. .174 

13.3 Jitter Notes . .179 

13.4 Timing Parameter Notes . .180 

13.5 Address / Command Setup, Hold and Derating. .182 

13.6 Data Setup, Hold and Slew Rate Derating. .189 

# List of Figures

Figure 1 —Qual-stacked / Quad-die DDR3 SDRAM x4 rank association 12 

Figure 2 —Qual-stacked / Quad-die DDR3 SDRAM x8 rank association 12 

Figure 3 —Qual-stacked / Quad-die DDR3 SDRAM x16 rank association 12 

Figure 4 —Simplified State Diagram 17 

Figure 5 —Reset and Initialization Sequence at Power-on Ramping . 20 

Figure 6 —Reset Procedure at Power Stable Condition 21 

Figure 7 —tMRD Timing 22 

Figure 8 —tMOD Timing 22 

Figure 9 —MR0 Definition 24 

Figure 10 —MR1 Definition 27 

Figure 11 —MR2 Definition 30 

Figure 12 —MR3 Definition 32 

Figure 13 —DLL-off mode READ Timing Operation 37 

Figure 14 — DLL Switch Sequence from DLL-on to DLL-off 38 

Figure 15 —DLL Switch Sequence from DLL Off to DLL On 39 

Figure 16 —Change Frequency during Precharge Power-down . . . 41 

Figure 17 —Write Leveling Concept 42 

Figure 18 —Timing details of Write leveling sequence [DQS - DQS# is capturing CK - CK# low at T1 and CK - CK# high at T2 44 

Figure 19 —Timing details of Write leveling exit . 45 

Figure 20 —MPR Block Diagram . 48 

Figure 21 —MPR Readout of predefined pattern, BL8 fixed burst order, single readout . . . . . 51 

Figure 22 —MPR Readout of predefined pattern, BL8 fixed burst order, back-to-back readout 52 

Figure 23 —MPR Readout predefined pattern, BC4, lower nibble then upper nibble . . . 53 

Figure 24 —MPR Readout of predefined pattern, BC4, upper nibble then lower nibble . . . . . . 54 

Figure 25 —READ Burst Operation $\mathrm { R L } = 5$ $\mathrm { A L } = 0$ , $\mathrm { C L } = 5$ , BL8) 56 

Figure 26 —READ Burst Operation $\mathrm { R L } = 9$ $\mathrm { A L } = 4$ , $\mathrm { C L } = 5$ , BL8) . 56 

Figure 27 —READ Timing Definition 57 

Figure 28 —Clock to Data Strobe Relationship 58 

Figure 29 —Data Strobe to Data Relationship 59 

Figure 30 —tLZ and tHZ method for calculating transitions and endpoints . 60 

Figure 31 —Method for calculating tRPRE transitions and endpoints 61 

Figure 32 —Method for calculating tRPST transitions and endpoints 61 

Figure 33 —READ (BL8) to READ (BL8) . 62 

Figure 34 —READ (BC4) to READ (BC4) 62 

Figure 35 —READ (BL8) to WRITE (BL8) . 63 

Figure 36 —READ (BC4) to WRITE (BC4) OTF 63 

Figure 37 —READ (BL8) to READ (BC4) OTF 64 

Figure 38 —READ (BC4) to READ (BL8) OTF 64 

Figure 39 —READ (BC4) to WRITE (BL8) OTF 65 

Figure 40 —READ (BL8) to WRITE (BC4) OTF 65 

Figure 41 —READ to PRECHARGE, $\mathrm { R L } = 5$ , $\mathrm { A L } = 0$ , $\mathrm { C L } = 5$ , tRTP $= 4$ , $\mathrm { t R P } = 5$ . 66 

Figure 42 —READ to PRECHARGE, $\mathrm { R L } = 8$ , $\mathbf { A L } = \mathbf { C L } { - 2 }$ , $\mathrm { C L } = 5$ , tRTP $= 6$ , $\mathrm { t R P } = 5$ . . . . . . 67 

Figure 43 —Write Timing Definition and Parameters 69 

Figure 44 —Method for calculating tWPRE transitions and endpoints 70 

Figure 45 —Method for calculating tWPST transitions and endpoints . . 70 

Figure 46 —WRITE Burst Operation ${ \mathrm { W L } } = 5$ $\mathrm { A L } = 0$ , ${ \mathrm { C W L } } = 5$ , BL8) . 71 

# List of Figures

Figure 47 —WRITE Burst Operation $\mathrm { W L } = 9$ $\mathbf { \hat { A } L } = \mathbf { C L - 1 }$ , CWL = 5, BL8) 71 

Figure 48 —WRITE (BC4) to READ (BC4) Operation . 72 

Figure 49 —WRITE (BC4) to PRECHARGE Operation 72 

Figure 50 —WRITE (BC4) OTF to PRECHARGE Operation . 72 

Figure 51 —WRITE (BL8) to WRITE (BL8) . 73 

Figure 52 —WRITE (BC4) to WRITE (BC4) OTF 73 

Figure 53 —WRITE (BL8) to READ (BC4/BL8) OTF 74 

Figure 54 —WRITE (BC4) to READ (BC4/BL8) OTF 74 

Figure 55 —WRITE (BC4) to READ (BC4) 75 

Figure 56 —WRITE (BL8) to WRITE (BC4) OTF 75 

Figure 57 —WRITE (BC4) to WRITE (BL8) OTF 76 

Figure 58 —Refresh Command Timing 77 

Figure 59 —Postponing Refresh Commands (Example) 77 

Figure 60 —Pulling-in Refresh Commands (Example) 78 

Figure 61 —Self-Refresh Entry/Exit Timing 80 

Figure 62 —Active Power-Down Entry and Exit Timing Diagram 82 

Figure 63 —Power-Down Entry after Read and Read with Auto Precharge 82 

Figure 64 —Power-Down Entry after Write with Auto Precharge . 83 

Figure 65 —Power-Down Entry after Write 83 

Figure 66 —Precharge Power-Down (Fast Exit Mode) Entry and Exit 84 

Figure 67 — Precharge Power-Down (Slow Exit Mode) Entry and Exit 84 

Figure 68 — Refresh Command to Power-Down Entry 85 

Figure 69 — Active Command to Power-Down Entry 85 

Figure 70 — Precharge / Precharge all Command to Power-Down Entry 86 

Figure 71 — MRS Command to Power-Down Entry 86 

Figure 72 —Power-Down Entry/Exit Clarifications - Case 1 87 

Figure 73 —Power-Down Entry/Exit Clarifications - Case 2 . . 87 

Figure 74 —Power-Down Entry/Exit Clarifications - Case 3 . 88 

Figure 75 —ZQ Calibration Timing 90 

Figure 76 —Functional Representation of ODT 91 

Figure 77 —Synchronous ODT Timing Example for $\mathrm { A L } = 3$ ; ${ \mathrm { C W L } } = 5$ $= 5$ ; ODTLon $\mathbf { \tau } = \mathbf { A } \mathbf { L } + \mathbf { C } \mathbf { W } \mathbf { L }$ $=$ - $2 = 6 . 0$ ; ODTLoff $= \mathrm { A L } + \mathrm { C W L } - 2 = 6$ . 93 

Figure 78 —Synchronous ODT example with ${ \mathrm { B L } } = 4 _ { \mathrm { { i } } }$ , $\mathrm { W L } = 7$ . 94 

Figure 79 —ODT must be disabled externally during Reads by driving ODT low. (example: $\mathrm { C L } = 6$ ; ${ \mathrm { A L } } = { \mathrm { C L } } - 1 = 5$ ; $\mathrm { R L } = \mathrm { A L } + \mathrm { C L } = 1 1 ; \mathrm { C W L } = 5$ ; ODTLon $=$ CWL + AL - $2 = 8$ ; ODTLoff $= \mathrm { C W L } + \mathrm { A L } - 2 = 8 )$ . . . 95 

Figure 80 —Dynamic ODT: Behavior with ODT being asserted before and after the write . . . 98 

Figure 81 —Dynamic ODT: Behavior without write command, $\mathrm { { A L } } = 0$ , ${ \mathrm { C W L } } = 5$ . 98 

Figure 82 —Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 6 clock cycles 99 

Figure 83 —Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 6 clock cycles, example for BC4 (via MRS or OTF), $\mathrm { A L } = 0$ , ${ \mathrm { C W L } } = 5$ . . . 100 

Figure 84 —Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 4 clock cycles 101 

Figure 85 —Asynchronous ODT Timings on DDR3 SDRAM with fast ODT transition: AL is ignored 102 

# List of Figures

Figure 86 —Synchronous to asynchronous transition during Precharge Power Down (with DLL frozen) entry $( \mathrm { A L } = 0$ ; ${ \mathrm { C W L } } = 5$ ; $\mathrm { t A N P D } = \mathrm { W L } - 1 = 4 )$ 104 

Figure 87 —Synchronous to asynchronous transition after Refresh command $[ \mathrm { A L } = 0$ ; ${ \mathrm { C W L } } = 5$ ; $\mathrm { t A N P D } = \mathrm { W L } - 1 = 4 )$ ) . 105 

Figure 88 —Asynchronous to synchronous transition during Precharge Power Down (with DLL frozen) exit ( $\mathrm { C L } = 6$ ; $\mathbf { A L } = \mathbf { C L } - 1$ ; ${ \mathrm { C W L } } = 5$ ; $\mathrm { t A N P D } = \mathrm { W L } - 1 = 9 )$ . . . . . . . 106 

Figure 89 —Transition period for short CKE cycles, entry and exit period overlapping $[ \mathrm { A L } = 0$ , ${ \mathrm { W L } } = 5$ , $\mathrm { t A N P D } = \mathrm { W L } - 1 = 4 )$ . 107 

Figure 90 —Illustration of VRef(DC) tolerance and VRef ac-noise limits . 114 

Figure 91 —Definition of differential ac-swing and “time above ac-level” tDVAC . 115 

Figure 92 —Single-ended requirement for differential signals. 117 

Figure 93 —Vix Definition 118 

Figure 94 —Differential Input Slew Rate Definition for DQS, DQS# and CK, CK# . . . . . . . . 119 

Figure 95 —Single Ended Output Slew Rate Definition . 122 

Figure 96 —Differential Output Slew Rate Definition 123 

Figure 97 —Reference Load for AC Timing and Output Slew Rate 124 

Figure 98 —Address and Control Overshoot and Undershoot Definition 125 

Figure 99 —Clock, Data, Strobe and Mask Overshoot and Undershoot Definition . . . 126 

Figure 100 —Output Driver: Definition of Voltages and Currents . 127 

Figure 101 —On-Die Termination: Definition of Voltages and Currents . 130 

Figure 102:ODT Timing Reference Load 134 

Figure 103 —Definition of tAON . 136 

Figure 104 —Definition of tAONPD . 136 

Figure 105 —Definition of tAOF 137 

Figure 106 —Definition of tAOFPD . 137 

Figure 107 —Definition of tADC 138 

Figure 108 — Measurement Setup and Test Load for IDD and IDDQ (optional) Measurements 140 

Figure 109 —Correlation from simulated Channel IO Power to actual Channel IO Power supported by IDDQ Measurement. . 140 

Figure 110 —Illustration of nominal slew rate and tVAC for setup time tIS (for ADD/CMD with respect to clock). 185 

Figure 111 —Illustration of nominal slew rate for hold time tIH (for ADD/CMD with respect to clock). 186 

Figure 112 —Illustration of tangent line for setup time tIS (for ADD/CMD with respect to clock) 187 

Figure 113 —Illustration of tangent line for for hold time tIH (for ADD/CMD with respect to clock) 188 

Figure 114 —Illustration of nominal slew rate and tVAC for setup time tDS (for DQ with respect to strobe) 192 

Figure 115 —Illustration of nominal slew rate for hold time tDH (for DQ with respect to strobe) 193 

Figure 116 —Illustration of tangent line for setup time tDS (for DQ with respect to strobe) . . 194 

Figure 117 —Illustration of tangent line for for hold time tDH (for DQ with respect to strobe) 195 

# List of Tables

Table 1 —Input/output functional description . 13 

Table 2 —State Diagram Command Definitions . 17 

Table 3 —Burst Type and Burst Order. 25 

Table 4 —Additive Latency (AL) Settings. . 28 

Table 5 —TDQS, TDQS# Function Matrix . 29 

Table 6 —Command Truth Table. . 33 

Table 7 —CKE Truth Table . 35 

Table 8 —MR setting involved in the leveling procedure . 43 

Table 9 —DRAM termination function in the leveling mode . 43 

Table 10 —Mode Register Description 46 

Table 11 —Self-Refresh mode summary . 47 

Table 12 —MPR MR3 Register Definition . 48 

Table 13 —MPR MR3 Register Definition . 50 

Table 14 —Power-Down Entry Definitions . . 81 

Table 15 —Termination Truth Table . 91 

Table 16 —Latencies and timing parameters relevant for Dynamic ODT. 96 

Table 17 —Timing Diagrams for “Dynamic ODT” . 97 

Table 18 —Asynchronous ODT Timing Parameters for all Speed Bins 102 

Table 19 —ODT timing parameters for Power Down (with DLL frozen) entry and exit transition period . 103 

Table 20 —Absolute Maximum DC Ratings . . 109 

Table 21 —Temperature Range . . 109 

Table 22 —Recommended DC Operating Conditions . 111 

Table 23 —Single-Ended AC and DC Input Levels for Command and Address . . . 113 

Table 24 —Single-Ended AC and DC Input Levels for DQ and DM . 113 

Table 25 —Differential AC and DC Input Levels . 115 

Table 26 —Allowed time before ringback (tDVAC) for CK - CK# and DQS - DQS# . . . . . . . 116 

Table 27 —Single-ended levels for CK, DQS, DQSL, DQSU, CK#, DQS#, DQSL# or DQSU# . 117 

Table 28 —Cross point voltage for differential input signals (CK, DQS) . . . 118 

Table 29 —Differential Input Slew Rate Definition 119 

Table 30 —Single-ended AC and DC Output Levels. . 121 

Table 31 —Differential AC and DC Output Levels . 121 

Table 32 —Single-ended Output Slew Rate Definition 122 

Table 33 —Output Slew Rate (single-ended) 122 

Table 34 —Differential Output Slew Rate Definition 123 

Table 35 —Differential Output Slew Rate . 123 

Table 36 —AC Overshoot/Undershoot Specification for Address and Control Pins. . . . . . 125 

Table 37 —AC Overshoot/Undershoot Specification for Clock, Data, Strobe and Mask . . . . . 126 

Table 38 —Output Driver DC Electrical Characteristics, assuming $\mathsf { R } ^ { Z \mathsf { Q } } = 2 4 0 \mathsf { W }$ ; entire operating temperature range; after proper ZQ calibration 128 

Table 39 —Output Driver Sensitivity Definition . . 129 

Table 40 —Output Driver Voltage and Temperature Sensitivity. . 129 

# List of Tables

Table 41 —ODT DC Electrical Characteristics, assuming $\mathrm { R } ^ { Z \mathrm { Q } } = 2 4 0 \ \mathrm { W } + / - \ 1 \%$ entire operating temperature range; after proper ZQ calibration 131 

Table 42 —ODT Sensitivity Definition . 134 

Table 43 —ODT Voltage and Temperature Sensitivity . . 134 

Table 44 —ODT Timing Definitions . 135 

Table 45 —Reference Settings for ODT Timing Measurements . 135 

Table 46 —Timings used for IDD and IDDQ Measurement-Loop Patterns . . 141 

Table 47 —Basic IDD and IDDQ Measurement Conditions . 141 

Table 48 —IDD0 Measurement-Loop Pattern . 144 

Table 49 —IDD1 Measurement-Loop Pattern . 145 

Table 50 —IDD2N and IDD3N Measurement-Loop Pattern. 146 

Table 51 —IDD2NT and IDDQ2NT Measurement-Loop Pattern. . 146 

Table 52 —IDD4R and IDDQ4R Measurement-Loop Pattern 147 

Table 53 —IDD4W Measurement-Loop Pattern . 147 

Table 54 —IDD5B Measurement-Loop Pattern. 148 

Table 55 —IDD7 Measurement-Loop Pattern . 149 

Table 56 —IDD Specification Example 512M DDR3. 150 

Table 57 —IDD6 Specification. . 151 

Table 58 —Input / Output Capacitance 153 

Table 59 —Refresh parameters by device density . . 156 

Table 60 —DDR3-800 Speed Bins and Operating Conditions 157 

Table 61 —DDR3-1066 Speed Bins and Operating Conditions 158 

Table 62 —DDR3-1333 Speed Bins and Operating Conditions 159 

Table 63 —DDR3-1600 Speed Bins and Operating Conditions 160 

Table 64 —DDR3-1866 Speed Bins and Operating Conditions 162 

Table 65 —DDR3-2133 Speed Bins and Operating Conditions 163 

Table 66 —Timing Parameters by Speed Bin 167 

Table 67 —Timing Parameters by Speed Bin 174 

Table 68 —ADD/CMD Setup and Hold Base-Values for 1V/ns 182 

Table 69 —Derating values DDR3-800/1066/1333/1600 tIS/tIH - ac/dc based AC175 Threshold 183 

Table 70 —Derating values DDR3-800/1066/1333/1600 tIS/tIH - ac/dc based - Alternate AC150 Threshold 183 

Table 71 —Required time tVAC above VIH(ac) {below VIL(ac)} for valid transition . . . . . . 184 

Table 72 —Data Setup and Hold Base-Values 189 

Table 73 —Derating values DDR3-800/1066 tDS/tDH - (AC175) . . 190 

Table 74 —Derating values for DDR3-800/1066/1333/1600 tDS/tDH - (AC150) . . . . . 190 

Table 75 —Required time tVAC above VIH(ac) {below VIL(ac)} for valid transition . . . . . . 191 

This page left blank. 

# DDR3 SDRAM STANDARD

(From JEDEC Board Ballot, JCB-09-29, formulated under the cognizance of the JC-42.3 Subcommittee on Volatile RAM.) 

# 1 Scope

This document defines the DDR3 SDRAM specification, including features, functionalities, AC and DC characteristics, packages, and ball/signal assignments. The purpose of this document is to define the minimum set of requirements for JEDEC compliant 512 Mb through 8 Gb for x4, x8, and x16 DDR3 SDRAM devices. This standard was created based on the DDR2 standard (JESD79-2) and some aspects of the DDR standard (JESD79). Each aspect of the changes for DDR3 SDRAM operation were considered and approved by committee ballot(s). The accumulations of these ballots were then incorporated to prepare this document, JESD79-3D, replacing whole sections and incorporating the changes into Functional Description and Operation. 

This page left blank. 

# 2 DDR3 SDRAM Package Pinout and Addressing

# 2.1 DDR3 SDRAM x4 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/71f8d10320079ff6799bf96f830e83849490762742525cccfc8e1b995d17ca13.jpg)



NOTE: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application.


MO-207 Variation DT-z (x4) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/93e3b3a782803f6591a09df9c2d038dc0412c130b0800799a1a2e4ebd521117b.jpg)


Populated ball 

Ball not populated 


MO-207 Variation DW-z (x4) with support balls


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/c7a604d6da51efb5546adb1bc267aa690d00fd8e3e8f57534711c259dd86eeb3.jpg)


# 2 DDR3 SDRAM Package Pinout and Addressing (Cont’d)

# 2.2 DDR3 SDRAM x8 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/2f94ce43e3c04cad918deb9eb56e570b232bdf946cf01a45c998b9ee0a24eb67.jpg)



NOTE: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application.


MO-207 Variation DT-z (x8) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/f284f65b15d990c6073c5c558f834c2324034cb7202fd49cae27a5db53366ad2.jpg)



Populated ball Ball not populated


MO-207 Variation DW-z (x8) with support balls 1 2 3 4 8 95 6 7 10 11 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/6a75c90ad6498f4b5a543621fbd6412ea8cfc36b13785d43cb6cfe517874ceb1.jpg)


# 2 DDR3 SDRAM Package Pinout and Addressing (Cont’d)

# 2.3 DDR3 SDRAM x16 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/07a545e1a19238512b8ad8f2da803c0f7c2c7e57caa93af67024006262c37dcc.jpg)



NOTE: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application.


MO - 207 Variation DU-z (x16) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a2a102e05916e3ad5dd5142f9624f89e89a4a588fcb522b9e9221ec3a66ced27.jpg)



Populated ball Ball not populated


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/87247d7daa6f215305dac85c015bd451e2cc8d6ad46d29ab399b39108468a344.jpg)


# 2.4 Stacked / dual-die DDR3 SDRAM x4 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/5c968d5a061ca37f98a6256a7c4ba8ee54281480731b180551b5e05b6c8404fd.jpg)



NOTE 1: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application.



NOTE 2: This stacked ballout is intended for use only with stacked/dual-die packages, and does not apply to non-stacked/single-die packages. This document (JESD79-3) focuses on nonstacked, single-die devices unless otherwise explicitly stated.


MO-207 Variation DT-z (x4) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/27cde33aa699c34810e355b965cb4be0950583a10eebe28c4ee71ac2b664b392.jpg)



Populated ball



Ball not populated



MO-207 Variation DW-z (x4) with support balls


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/98cdf6de3aacda0c65d18ddfcaae3a2152ce0c8e9a79276b10b2f89f47596f8c.jpg)


# 2 DDR3 SDRAM Package Pinout and Addressing (Cont’d)

# 2.5 Stacked / dual-die DDR3 SDRAM x8 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/c6e7e335d2ca93b51d1339c6c1fdcb9ccaf26d76050e74098b5afa7acaff527e.jpg)


NOTE 1: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application. 

NOTE 2: This stacked ballout is intended for use only with stacked/dual-die packages, and does not apply to non-stacked/single-die packages. This document (JESD79-3) focuses on nonstacked, single-die devices unless otherwise explicitly stated. 

MO-207 Variation DT-z (x8) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/2f2509290c0c4443e8538284bc9a77045270087dd0e27e7e933850bebb02f1b6.jpg)


Populated ball Ball not populated 

MO - 207 Variation DW-z (x8) with support balls 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/ade1d45a77126207eafc4e5bf21007e851a5b18c8af014237b1fd5216d45498b.jpg)


# 2.6 Stacked / dual-die DDR3 SDRAM x16 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/d52b573c7bfd7766221a2c1523629133d3a082a167413b765b06be8ab62d005e.jpg)



NOTE 1: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application.



NOTE 2: This stacked ballout is intended for use only with stacked/dual-die packages, and does not apply to non-stacked/single-die packages. This document (JESD79-3) focuses on nonstacked, single-die devices unless otherwise explicitly stated.


MO - 207 Variation DU-z (x16) 1 2 3 4 8 95 6 7 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/cc372b932147107f60fdb709c9f643c4cbd3c3d2b44987a67db11f6b2be17418.jpg)



Populated ball Ball not populated


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/1c735b4ecfc26ee5c957fa9586c3a7e91949ed9ef6903b5ab1dae2feb4acaa38.jpg)


# 2 DDR3 SDRAM Package Pinout and Addressing (Cont’d)

# 2.7 Quad-stacked / Quad-die DDR3 SDRAM x4 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/42ec59eeb88b0b7d45941f216a8457090484a7f8d7ec5af3d63c5a7abbb188b1.jpg)



NOTE 1: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application.



NOTE 2: This stacked ballout is intended for use only with quad-stacked/quad-die packages, and does not apply to non-stacked/single-die packages. This document (JESD79-3) focuses on non-stacked, single-die devices unless otherwise explicitly stated.


MO-207 Variation DT-z (x4) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/065f7310bfab4b63b6f8d93c3d0322ba70a2cc67a6e6a9f83ca6a185bf5a254e.jpg)



Populated ball



Ball not populated



MO-207 Variation DW-z (x4) with support balls


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/2d595b670b21463d9a6542ffc14fa08ed05b66c7ac5b41895d293bfdc494a228.jpg)


# 2.8 Quad-stacked / Quad-die DDR3 SDRAM x8 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/391981bbcb6a62d21bb36454ed4d75dccc75914e9d098a8bc3d2866a6c3a1dee.jpg)



NOTE 1: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application.



NOTE 2: This stacked ballout is intended for use only with quad-stacked/quad-die packages, and does not apply to non-stacked/single-die packages. This document (JESD79-3) focuses on non-stacked, single-die devices unless otherwise explicitly stated.


MO-207 Variation DT-z (x8) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/0fa73e32c576204bdc560ce79906a9bfee6593a7526c8d5c7139a15d0b055b22.jpg)



Populated ball Ball not populated


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/cfd1509a5b93d7dab8c1f643b98a6b61370ca2534f37a498a3db931cc89ba982.jpg)


# 2.9 Quad-stacked / Quad-die DDR3 SDRAM x16 Ballout using MO-207

(Top view: see balls through package) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/cfcd5d1bc35baa4c02aa57ec1bc18cec955173cd659582cbd807b8e592f55c9e.jpg)



NOTE 1: Green NC balls indicate mechanical support balls with no internal connection. Any of the support ball locations may or may not be populated with a ball depending upon the DRAM Vendor’s actual package size. Therefore, it's recommended to consider landing pad location for all possible support balls based upon maximum DRAM package size allowed in the application.



NOTE 2: This stacked ballout is intended for use only with quad-stacked/quad-die packages, and does not apply to non-stacked/single-die packages. This document (JESD79-3) focuses on non-stacked, single-die devices unless otherwise explicitly stated.



MO - 207 Variation DU-z (x16) 1 2 3 4 8 9 5 6 7


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/21b733a566931938855f35707651a929128e19ce1105c56a97e0cc4c317d44c7.jpg)



Populated ball Ball not populated



MO - 207 Variation DY-z (x16) with support balls


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/33eb8281dab64fd6ced5f2c0f22c1301d300dcdab380cc930588ac4afb6ae5b8.jpg)


# 2 DDR3 SDRAM Package Pinout and Addressing (Cont’d)

# 2.9 Quad-stacked / Quad-die DDR3 SDRAM x16 Ballout using MO-207 (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/96203d44d421dc6e77880de16858d0f74bba3eaa4513d023e9ca20fc4011a0ff.jpg)



Figure 1 — Qual-stacked / Quad-die DDR3 SDRAM x4 rank association


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/d3de5893edcdca527c5df012dfeb96f48a220819a8b8eef0d568245fa95630c1.jpg)



Figure 2 — Qual-stacked / Quad-die DDR3 SDRAM x8 rank association


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/f08c0506d78731fb2f6d47be83941adb92df1e90b7932802cb99e1d8c8494658.jpg)



Figure 3 — Qual-stacked / Quad-die DDR3 SDRAM x16 rank association


# 2.10 Pinout Description


Table 1 — Input/output functional description


<table><tr><td>Symbol</td><td>Type</td><td>Function</td></tr><tr><td>CK, CK#</td><td>Input</td><td>Clock: CK and CK# are differential clock inputs. All address and control input signals are sampled on the crossing of the positive edge of CK and negative edge of CK#.</td></tr><tr><td>CKE, (CKE0), (CKE1)</td><td>Input</td><td>Clock Enable: CKE HIGH activates, and CKE Low deactivates, internal clock signals and device input buffers and output drivers. Taking CKE Low provides Precharge Power-Down and Self-Refresh operation (all banks idle), or Active Power-Down (row Active in any bank). CKE is asynchronous for Self-Refresh exit. After VREFCA and VREFDQ have become stable during the power on and initialization sequence, they must be maintained during all operations (including Self-Refresh). CKE must be maintained high throughout read and write accesses. Input buffers, excluding CK, CK#, ODT and CKE, are disabled during power-down. Input buffers, excluding CKE, are disabled during Self-Refresh.</td></tr><tr><td>CS#, (CS0#), (CS1#), (CS2#), (CS3#)</td><td>Input</td><td>Chip Select: All commands are masked when CS# is registered HIGH. CS# provides for external Rank selection on systems with multiple Ranks. CS# is considered part of the command code.</td></tr><tr><td>ODT, (ODT0), (ODT1)</td><td>Input</td><td>On Die Termination: ODT (registered HIGH) enables termination resistance internal to the DDR3 SDRAM. When enabled, ODT is only applied to each DQ, DQS, DQS# and DM/TDQS, NU/TDQS# (When TDQS is enabled via Mode Register A11=1 in MR1) signal for x4/x8 configurations. For x16 configuration, ODT is applied to each DQ, DQSU, DQSU#, DQSL, DQSL#, DMU, and DML signal. The ODT pin will be ignored if MR1 and MR2 are programmed to disable RTT.</td></tr><tr><td>RAS#, CAS#, WE#</td><td>Input</td><td>Command Inputs: RAS#, CAS# and WE# (along with CS#) define the command being entered.</td></tr><tr><td>DM, (DMU), (DML)</td><td>Input</td><td>Input Data Mask: DM is an input mask signal for write data. Input data is masked when DM is sampled HIGH coincident with that input data during a Write access. DM is sampled on both edges of DQS. For x8 device, the function of DM or TDQS/TDQS# is enabled by Mode Register A11 setting in MR1.</td></tr><tr><td>BA0 - BA2</td><td>Input</td><td>Bank Address Inputs: BA0 - BA2 define to which bank an Active, Read, Write, or Precharge command is being applied. Bank address also determines which mode register is to be accessed during a MRS cycle.</td></tr><tr><td>A0 - A15</td><td>Input</td><td>Address Inputs: Provide the row address for Active commands and the column address for Read/Write commands to select one location out of the memory array in the respective bank. (A10/AP and A12/BC# have additional functions; see below). The address inputs also provide the op-code during Mode Register Set commands.</td></tr><tr><td>A10 / AP</td><td>Input</td><td>Auto-precharge: A10 is sampled during Read/Write commands to determine whether Autoprecharge should be performed to the accessed bank after the Read/Write operation. (HIGH: Autoprecharge; LOW: no Autoprecharge). A10 is sampled during a Precharge command to determine whether the Precharge applies to one bank (A10 LOW) or all banks (A10 HIGH). If only one bank is to be precharged, the bank is selected by bank addresses.</td></tr><tr><td>A12 / BC#</td><td>Input</td><td>Burst Chop: A12 / BC# is sampled during Read and Write commands to determine if burst chop (on-the-fly) will be performed. (HIGH, no burst chop; LOW: burst chopped). See command truth table for details.</td></tr><tr><td>RESET#</td><td>Input</td><td>Active Low Asynchronous Reset: Reset is active when RESET# is LOW, and inactive when RESET# is HIGH. RESET# must be HIGH during normal operation. RESET# is a CMOS rail-to-rail signal with DC high and low at 80% and 20% of VDD, i.e., 1.20V for DC high and 0.30V for DC low.</td></tr><tr><td>DQ</td><td>Input / Output</td><td>Data Input/ Output: Bi-directional data bus.</td></tr><tr><td>DQU, DQL, DQS, DQS#, DQSU, DQSU#, DQSL, DQSL#</td><td>Input / Output</td><td>Data Strobe: output with read data, input with write data. Edge-aligned with read data, centered in write data. For the x16, DQSL corresponds to the data on DQL0-DQL7; DQSU corresponds to the data on DQU0-DQU7. The data strobes DQS, DQSL, and DQSU are paired with differential signals DQS#, DQSL#, and DQSU#, respectively, to provide differential pair signaling to the system during reads and writes. DDR3 SDRAM supports differential data strobe only and does not support single-ended.</td></tr></table>

# 2 DDR3 SDRAM Package Pinout and Addressing (Cont’d)

# 2.10 Pinout Description (Cont’d)


Table 1 — Input/output functional description (Cont’d)


<table><tr><td>Symbol</td><td>Type</td><td>Function</td></tr><tr><td>TDQS, TDQS#</td><td>Output</td><td>Termination Data Strobe: TDQS/TDQS# is applicable for x8 DRAMs only. When enabled via Mode Register A11 = 1 in MR1, the DRAM will enable the same termination resistance function on TDQS/TDQS# that is applied to DQS/DQS#. When disabled via mode register A11 = 0 in MR1, DM/TDQS will provide the data mask function and TDQS# is not used. x4/x16 DRAMs must disable the TDQS function via mode register A11 = 0 in MR1.</td></tr><tr><td>NC</td><td></td><td>No Connect: No internal electrical connection is present.</td></tr><tr><td>VDDQ</td><td>Supply</td><td>DQ Power Supply: 1.5 V +/- 0.075 V</td></tr><tr><td>VSSQ</td><td>Supply</td><td>DQ Ground</td></tr><tr><td>VDD</td><td>Supply</td><td>Power Supply: 1.5 V +/- 0.075 V</td></tr><tr><td>VSS</td><td>Supply</td><td>Ground</td></tr><tr><td>VREFDQ</td><td>Supply</td><td>Reference voltage for DQ</td></tr><tr><td>VREFCA</td><td>Supply</td><td>Reference voltage for CA</td></tr><tr><td>ZQ, (ZQ0), (ZQ1), (ZQ2), (ZQ3)</td><td>Supply</td><td>Reference Pin for ZQ calibration</td></tr><tr><td colspan="3">NOTE: Input only pins (BA0-BA2, A0-A15, RAS#, CAS#, WE#, CS#, CKE, ODT, and RESET#) do not sup-ply termination.</td></tr></table>

# 2 DDR3 SDRAM Package Pinout and Addressing (Cont’d)

# 2.11 DDR3 SDRAM Addressing

# 2.11.1 512Mb

<table><tr><td>Configuration</td><td>128Mb x 4</td><td>64Mb x 8</td><td>32Mb x 16</td></tr><tr><td># of Banks</td><td>8</td><td>8</td><td>8</td></tr><tr><td>Bank Address</td><td>BA0 - BA2</td><td>BA0 - BA2</td><td>BA0 - BA2</td></tr><tr><td>Auto precharge</td><td>A10/AP</td><td>A10/AP</td><td>A10/AP</td></tr><tr><td>BC switch on the fly</td><td>A12/BC#</td><td>A12/BC#</td><td>A12/BC#</td></tr><tr><td>Row Address</td><td>A0 - A12</td><td>A0 - A12</td><td>A0 - A11</td></tr><tr><td>Column Address</td><td>A0 - A9,A11</td><td>A0 - A9</td><td>A0 - A9</td></tr><tr><td>Page size1</td><td>1 KB</td><td>1 KB</td><td>2 KB</td></tr></table>

# 2.11.2 1Gb

<table><tr><td>Configuration</td><td>256Mb x 4</td><td>128Mb x 8</td><td>64Mb x 16</td></tr><tr><td># of Banks</td><td>8</td><td>8</td><td>8</td></tr><tr><td>Bank Address</td><td>BA0 - BA2</td><td>BA0 - BA2</td><td>BA0 - BA2</td></tr><tr><td>Auto precharge</td><td>A10/AP</td><td>A10/AP</td><td>A10/AP</td></tr><tr><td>BC switch on the fly</td><td>A12/BC#</td><td>A12/BC#</td><td>A12/BC#</td></tr><tr><td>Row Address</td><td>A0 - A13</td><td>A0 - A13</td><td>A0 - A12</td></tr><tr><td>Column Address</td><td>A0 - A9,A11</td><td>A0 - A9</td><td>A0 - A9</td></tr><tr><td>Page size1</td><td>1 KB</td><td>1 KB</td><td>2 KB</td></tr></table>

# 2.11.3 2Gb

<table><tr><td>Configuration</td><td>512Mb x 4</td><td>256Mb x 8</td><td>128Mb x 16</td></tr><tr><td># of Banks</td><td>8</td><td>8</td><td>8</td></tr><tr><td>Bank Address</td><td>BA0 - BA2</td><td>BA0 - BA2</td><td>BA0 - BA2</td></tr><tr><td>Auto precharge</td><td>A10/AP</td><td>A10/AP</td><td>A10/AP</td></tr><tr><td>BC switch on the fly</td><td>A12/BC#</td><td>A12/BC#</td><td>A12/BC#</td></tr><tr><td>Row Address</td><td>A0 - A14</td><td>A0 - A14</td><td>A0 - A13</td></tr><tr><td>Column Address</td><td>A0 - A9,A11</td><td>A0 - A9</td><td>A0 - A9</td></tr><tr><td>Page size1</td><td>1 KB</td><td>1 KB</td><td>2 KB</td></tr></table>

# 2.11.4 4Gb

<table><tr><td>Configuration</td><td>1Gb x 4</td><td>512Mb x 8</td><td>256Mb x 16</td></tr><tr><td># of Banks</td><td>8</td><td>8</td><td>8</td></tr><tr><td>Bank Address</td><td>BA0 - BA2</td><td>BA0 - BA2</td><td>BA0 - BA2</td></tr><tr><td>Auto precharge</td><td>A10/AP</td><td>A10/AP</td><td>A10/AP</td></tr><tr><td>BC switch on the fly</td><td>A12/BC#</td><td>A12/BC#</td><td>A12/BC#</td></tr><tr><td>Row Address</td><td>A0 - A15</td><td>A0 - A15</td><td>A0 - A14</td></tr><tr><td>Column Address</td><td>A0 - A9,A11</td><td>A0 - A9</td><td>A0 - A9</td></tr><tr><td>Page size1</td><td>1 KB</td><td>1 KB</td><td>2 KB</td></tr></table>

# 2 DDR3 SDRAM Package Pinout and Addressing (Cont’d)

# 2.11 DDR3 SDRAM Addressing (Cont’d)


2.11.5 8Gb


<table><tr><td>Configuration</td><td>2Gb x 4</td><td>1Gb x 8</td><td>512Mb x 16</td></tr><tr><td># of Banks</td><td>8</td><td>8</td><td>8</td></tr><tr><td>Bank Address</td><td>BA0 - BA2</td><td>BA0 - BA2</td><td>BA0 - BA2</td></tr><tr><td>Auto precharge</td><td>A10/AP</td><td>A10/AP</td><td>A10/AP</td></tr><tr><td>BC switch on the fly</td><td>A12/BC#</td><td>A12/BC#</td><td>A12/BC#</td></tr><tr><td>Row Address</td><td>A0 - A15</td><td>A0 - A15</td><td>A0 - A15</td></tr><tr><td>Column Address</td><td>A0 - A9, A11, A13</td><td>A0 - A9, A11</td><td>A0 - A9</td></tr><tr><td>Page size1</td><td>2 KB</td><td>2 KB</td><td>2 KB</td></tr></table>


NOTE 1. Page size is the number of bytes of data delivered from the array to the internal sense amplifiers when an ACTIVE command is registered. Page size is per bank, calculated as follows: 


pag $\mathrm { e \ s i z e } = 2 ^ { \mathrm { C O L B I T S } } * \mathrm { O R G } \div 8$ 

where 

COLBITS $=$ the number of column address bits 

$\mathrm { O R G } =$ $=$ the number of I/O (DQ) bits 

# 3 Functional Description

# 3.1 Simplified State Diagram

This simplified State Diagram is intended to provide an overview of the possible state transitions and the commands to control them. In particular, situations involving more than one bank, the enabling or disabling of on-die termination, and some other events are not captured in full detail. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/ce8dde90e2def3d58e23bb5c7dea989fba7075813626c964ea064778ef07b96f.jpg)



Figure 4 — Simplified State Diagram



Table 2 — State Diagram Command Definitions


<table><tr><td>Abbreviation</td><td>Function</td><td>Abbreviation</td><td>Function</td><td>Abbreviation</td><td>Function</td></tr><tr><td>ACT</td><td>Active</td><td>Read</td><td>RD, RDS4, RDS8</td><td>PDE</td><td>Enter Power-down</td></tr><tr><td>PRE</td><td>Precharge</td><td>Read A</td><td>RDA, RDAS4, RDAS8</td><td>PDX</td><td>Exit Power-down</td></tr><tr><td>PREA</td><td>Precharge All</td><td>Write</td><td>WR, WRS4, WRS8</td><td>SRE</td><td>Self-Refresh entry</td></tr><tr><td>MRS</td><td>Mode Register Set</td><td>Write A</td><td>WRA, WRAS4, WRAS8</td><td>SRX</td><td>Self-Refresh exit</td></tr><tr><td>REF</td><td>Refresh</td><td>RESET</td><td>Start RESET Procedure</td><td>MPR</td><td>Multi-Purpose Register</td></tr><tr><td>ZQCL</td><td>ZQ Calibration Long</td><td>ZQCS</td><td>ZQ Calibration Short</td><td>-</td><td>-</td></tr><tr><td colspan="6">NOTE: See “Command Truth Table” on page 33 for more details.</td></tr></table>

# 3 Functional Description (Cont’d)

# 3.2 Basic Functionality

The DDR3 SDRAM is a high-speed dynamic random-access memory internally configured as an eight-bank DRAM. The DDR3 SDRAM uses a 8n prefetch architecture to achieve high-speed operation. The 8n prefetch architecture is combined with an interface designed to transfer two data words per clock cycle at the I/O pins. A single read or write operation for the DDR3 SDRAM consists of a single 8n-bit wide, four clock data transfer at the internal DRAM core and two corresponding n-bit wide, one-half clock cycle data transfers at the I/O pins. 

Read and write operation to the DDR3 SDRAM are burst oriented, start at a selected location, and continue for a burst length of eight or a ‘chopped’ burst of four in a programmed sequence. Operation begins with the registration of an Active command, which is then followed by a Read or Write command. The address bits registered coincident with the Active command are used to select the bank and row to be activated (BA0-BA2 select the bank; A0-A15 select the row; refer to “DDR3 SDRAM Addressing” on page 15 for specific requirements). The address bits registered coincident with the Read or Write command are used to select the starting column location for the burst operation, determine if the auto precharge command is to be issued (via A10), and select BC4 or BL8 mode ‘on the fly’ (via A12) if enabled in the mode register. 

Prior to normal operation, the DDR3 SDRAM must be powered up and initialized in a predefined manner. The following sections provide detailed information covering device reset and initialization, register definition, command descriptions, and device operation. 

# 3 Functional Description (Cont’d)

# 3.3 RESET and Initialization Procedure

# 3.3.1 Power-up Initialization Sequence

The following sequence is required for POWER UP and Initialization. 

1. Apply power (RESET# is recommended to be maintained below 0.2 x VDD; all other inputs may be undefined). RESET# needs to be maintained for minimum 200 us with stable power. CKE is pulled “Low” anytime before RESET# being de-asserted (min. time 10 ns). The power voltage ramp time between 300 mv to VDDmin must be no greater than $2 0 0 \mathrm { m s }$ ; and during the ramp, VDD $>$ VDDQ and $( \mathrm { V D D - V D D Q } ) < 0 . 3$ volts. 

• VDD and VDDQ are driven from a single power converter output, AND 

• The voltage levels on all pins other than VDD, VDDQ, VSS, VSSQ must be less than or equal to VDDQ and VDD on one side and must be larger than or equal to VSSQ and VSS on the other side. In addition, VTT is limited to 0.95 V max once power ramp is finished, AND 

• Vref tracks VDDQ/2. 

# OR

• Apply VDD without any slope reversal before or at the same time as VDDQ. 

• Apply VDDQ without any slope reversal before or at the same time as VTT & Vref. 

• The voltage levels on all pins other than VDD, VDDQ, VSS, VSSQ must be less than or equal to VDDQ and VDD on one side and must be larger than or equal to VSSQ and VSS on the other side. 

2. After RESET# is de-asserted, wait for another 500 us until CKE becomes active. During this time, the DRAM will start internal state initialization; this will be done independently of external clocks. 

3. Clocks (CK, CK#) need to be started and stabilized for at least 10 ns or 5 tCK (which is larger) before CKE goes active. Since CKE is a synchronous signal, the corresponding set up time to clock (tIS) must be met. Also, a NOP or Deselect command must be registered (with tIS set up time to clock) before CKE goes active. Once the CKE is registered “High” after Reset, CKE needs to be continuously registered “High” until the initialization sequence is finished, including expiration of tDLLK and tZQinit. 

4. The DDR3 SDRAM keeps its on-die termination in high-impedance state as long as RESET# is asserted. Further, the SDRAM keeps its on-die termination in high impedance state after RESET# deassertion until CKE is registered HIGH. The ODT input signal may be in undefined state until tIS before CKE is registered HIGH. When CKE is registered HIGH, the ODT input signal may be statically held at either LOW or HIGH. If RTT_NOM is to be enabled in MR1, the ODT input signal must be statically held LOW. In all cases, the ODT input signal remains static until the power up initialization sequence is finished, including the expiration of tDLLK and tZQinit. 

5. After CKE is being registered high, wait minimum of Reset CKE Exit time, tXPR, before issuing the first MRS command to load mode register. $( t X P R { = } m a x ~ ( t X S ~ ; ~ 5 ~ x ~ t C K )$ 

6. Issue MRS Command to load MR2 with all application settings. (To issue MRS command for MR2, provide “Low” to BA0 and BA2, “High” to BA1.) 

7. Issue MRS Command to load MR3 with all application settings. (To issue MRS command for MR3, provide “Low” to BA2, “High” to BA0 and BA1.) 

8. Issue MRS Command to load MR1 with all application settings and DLL enabled. (To issue "DLL Enable" command, provide "Low" to A0, "High" to BA0 and "Low" to BA1 – BA2). 

9. Issue MRS Command to load MR0 with all application settings and “DLL reset”. (To issue DLL reset command, provide "High" to A8 and "Low" to BA0-2). 

10. Issue ZQCL command to starting ZQ calibration. 

11. Wait for both tDLLK and tZQinit completed. 

12. The DDR3 SDRAM is now ready for normal operation. 

# 3.3 RESET and Initialization Procedure (Cont’d)

# 3.3.1 Power-up Initialization Sequence (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/c106c4ce867a0303dcc37dd46ed7c48958a55551259f0367b16163402d959514.jpg)



NOTE 1. From time point “Td” until “Tk” NOP or DES commands must be applied between MRS and ZQCL commands.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/2a2dd70df32338a163ba0c9a6ab5d6633e002511b1e7dcf516b201ec2a6dce57.jpg)



Figure 5 — Reset and Initialization Sequence at Power-on Ramping


# 3 Functional Description (Cont’d)

# 3.3 RESET and Initialization Procedure (Cont’d)

# 3.3.2 Reset Initialization with Stable Power

The following sequence is required for RESET at no power interruption initialization. 

1. Asserted RESET below ${ 0 . 2 } \ast \mathrm { V D D }$ anytime when reset is needed (all other inputs may be undefined). RESET needs to be maintained for minimum 100 ns. CKE is pulled “LOW” before RESET being deasserted (min. time 10 ns). 

2. Follow Power-up Initialization Sequence steps 2 to 11. 

3. The Reset sequence is now completed; DDR3 SDRAM is ready for normal operation. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/19fc059fb88728abdb04000c77a4fc14a0320335f309270315ec66cf5a798ab9.jpg)



NOTE 1. From time point “Td” until “Tk” NOP or DES commands must be applied between MRS and ZQCL commands.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/5f30332287188c5d750a6beb0067237785e22e391677c90ce8acfcfb86c00ad8.jpg)



Figure 6 — Reset Procedure at Power Stable Condition


# 3.4 Register Definition

# 3.4.1 Programming the Mode Registers

For application flexibility, various functions, features, and modes are programmable in four Mode Registers, provided by the DDR3 SDRAM, as user defined variables and they must be programmed via a Mode Register Set (MRS) command. As the default values of the Mode Registers (MR#) are not defined, contents of Mode Registers must be fully initialized and/or re-initialized, i.e., written, after power up and/or reset for proper operation. Also the contents of the Mode Registers can be altered by re-executing the MRS command during normal operation. When programming the mode registers, even if the user chooses to modify only a sub-set of the MRS fields, all address fields within the accessed mode register must be redefined when the MRS command is issued. MRS command and DLL Reset do not affect array contents, which means these commands can be executed any time after power-up without affecting the array contents. 

The mode register set command cycle time, tMRD is required to complete the write operation to the mode register and is the minimum time required between two MRS commands shown in Figure 7 . 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/9f545ba406e5fa4cc276f5cf77fe8f4d9d5583cee78875867ea4505af5debb8b.jpg)



Figure 7 — tMRD Timing


The MRS command to Non-MRS command delay, tMOD, is required for the DRAM to update the features, except DLL reset, and is the minimum time required from an MRS command to a non-MRS command excluding NOP and DES shown in Figure 8. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/0549ab60f503bb2216f4f6e1a6fd04fe3174920f34a8e827b82e586f5f5c46d1.jpg)



Figure 8 — tMOD Timing


# 3.4 Register Definition (Cont’d)

# 3.4.1 Programming the Mode Registers (Cont’d)

The mode register contents can be changed using the same command and timing requirements during normal operation as long as the DRAM is in idle state, i.e., all banks are in the precharged state with tRP satisfied, all data bursts are completed and CKE is high prior to writing into the mode register. If the RTT_NOM Feature is enabled in the Mode Register prior and/or after an MRS Command, the ODT Signal must continuously be registered LOW ensuring RTT is in an off State prior to the MRS command. The ODT Signal may be registered high after tMOD has expired. If the RTT_NOM Feature is disabled in the Mode Register prior and after an MRS command, the ODT Signal can be registered either LOW or HIGH before, during and after the MRS command. The mode registers are divided into various fields depending on the functionality and/or modes. 

# 3.4.2 Mode Register MR0

The mode register MR0 stores the data for controlling various operating modes of DDR3 SDRAM. It controls burst length, read burst type, CAS latency, test mode, DLL reset, WR and DLL control for precharge Power-Down, which include various vendor specific options to make DDR3 SDRAM useful for various applications. The mode register is written by asserting low on CS#, RAS#, CAS#, WE#, BA0, BA1, and BA2, 

# 3.4 Register Definition (Cont’d)

# 3.4.2 Mode Register MR0 (Cont’d)

while controlling the states of address pins according to Figure 9. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/33f835eec3cb244a2bb585d2105f36d3aa1e1663fe954a1f3af71692abc3b4be.jpg)


*1: BA2 and A13~A15 are RFU and must be programmed to 0 during MRS. 

$^ { * 2 }$ : WR (write recovery for autoprecharge)min in clock cycles is calculated by dividing tWR(in ns) by tCK(in ns) and rounding up to the next integer: WRmin[cycles] $=$ Roundup(tWR[ns] / tCK[ns]). The WR value in the mode register must be programmed to be equal or larger than WRmin. The programmed WR value is used with tRP to determine tDAL. 

$^ { * 3 }$ : The table only shows the encodings for a given Cas Latency. For actual supported Cas Latency, please refer to speedbin tables for each frequency 

$^ { * 4 }$ : The table only shows the encodings for Write Recovery. For actual Write recovery timing, please refer to AC timingtable. 


Figure 9 — MR0 Definition


# 3.4 Register Definition (Cont’d)

# 3.4.2 Mode Register MR0 (Cont’d)

# 3.4.2.1 Burst Length, Type and Order

Accesses within a given burst may be programmed to sequential or interleaved order. The burst type is selected via bit A3 as shown in Figure 9. The ordering of accesses within a burst is determined by the burst length, burst type, and the starting column address as shown in Table 3. The burst length is defined by bits A0-A1. Burst length options include fixed BC4, fixed BL8, and ‘on the fly’ which allows BC4 or BL8 to be selected coincident with the registration of a Read or Write command via A12/BC#. 


Table 3 — Burst Type and Burst Order


<table><tr><td>Burst Length</td><td>READ/WRITE</td><td>Starting Column ADDRESS(A2,A1,A0)</td><td>burst type = Sequential (decimal) A3 = 0</td><td>burst type = Interleaved (decimal) A3 = 1</td><td>Notes</td></tr><tr><td rowspan="10">4 Chop</td><td rowspan="8">READ</td><td>000</td><td>0,1,2,3,T,T,T,T</td><td>0,1,2,3,T,T,T,T</td><td>1,2,3</td></tr><tr><td>001</td><td>1,2,3,0,T,T,T,T</td><td>1,0,3,2,T,T,T</td><td>1,2,3</td></tr><tr><td>010</td><td>2,3,0,1,T,T,T,T</td><td>2,3,0,1,T,T,T,T</td><td>1,2,3</td></tr><tr><td>011</td><td>3,0,1,2,T,T,T,T</td><td>3,2,1,0,T,T,T,T</td><td>1,2,3</td></tr><tr><td>100</td><td>4,5,6,7,T,T,T,T</td><td>4,5,6,7,T,T,T,T</td><td>1,2,3</td></tr><tr><td>101</td><td>5,6,7,4,T,T,T,T</td><td>5,4,7,6,T,T,T,T</td><td>1,2,3</td></tr><tr><td>110</td><td>6,7,4,5,T,T,T,T</td><td>6,7,4,5,T,T,T,T</td><td>1,2,3</td></tr><tr><td>111</td><td>7,4,5,6,T,T,T,T</td><td>7,6,5,4,T,T,T,T</td><td>1,2,3</td></tr><tr><td rowspan="2">WRITE</td><td>0,V,V</td><td>0,1,2,3,X,X,X,X</td><td>0,1,2,3,X,X,X,X</td><td>1,2,4,5</td></tr><tr><td>1,V,V</td><td>4,5,6,7,X,X,X,X</td><td>4,5,6,7,X,X,X,X</td><td>1,2,4,5</td></tr><tr><td rowspan="9">8</td><td rowspan="8">READ</td><td>000</td><td>0,1,2,3,4,5,6,7</td><td>0,1,2,3,4,5,6,7</td><td>2</td></tr><tr><td>001</td><td>1,2,3,0,5,6,7,4</td><td>1,0,3,2,5,4,7,6</td><td>2</td></tr><tr><td>010</td><td>2,3,0,1,6,7,4,5</td><td>2,3,0,1,6,7,4,5</td><td>2</td></tr><tr><td>011</td><td>3,0,1,2,7,4,5,6</td><td>3,2,1,0,7,6,5,4</td><td>2</td></tr><tr><td>100</td><td>4,5,6,7,0,1,2,3</td><td>4,5,6,7,0,1,2,3</td><td>2</td></tr><tr><td>101</td><td>5,6,7,4,1,2,3,0</td><td>5,4,7,6,1,0,3,2</td><td>2</td></tr><tr><td>110</td><td>6,7,4,5,2,3,0,1</td><td>6,7,4,5,2,3,0,1</td><td>2</td></tr><tr><td>111</td><td>7,4,5,6,3,0,1,2</td><td>7,6,5,4,3,2,1,0</td><td>2</td></tr><tr><td>WRITE</td><td>V,V,V</td><td>0,1,2,3,4,5,6,7</td><td>0,1,2,3,4,5,6,7</td><td>2,4</td></tr><tr><td colspan="6">NOTE 1 In case of burst length being fixed to 4 by MR0 setting, the internal write operation starts two clock cycles earlier than for the BL8 mode. This means that the starting point for tWR and tWTR will be pulled in by two clocks. In case of burst length being selected on-the-fly via A12/BC#, the internal write operation starts at the same point in time like a burst of 8 write operation. This means that during on-the-fly control, the starting point for tWR and tWTR will not be pulled in by two clocks. NOTE 2 0...7 bit number is value of CA[2:0] that causes this bit to be the first read during a burst. NOTE 3 T: Output driver for data and strobes are in high impedance. NOTE 4 V: a valid logic level (0 or 1), but respective buffer input ignores level on input pins. NOTE 5 X: Don&#x27;t Care.</td></tr></table>

# 3.4.2.2 CAS Latency

The CAS Latency is defined by MR0 (bits A9-A11) as shown in Figure 9. CAS Latency is the delay, in clock cycles, between the internal Read command and the availability of the first bit of output data. DDR3 SDRAM does not support any half-clock latencies. The overall Read Latency (RL) is defined as Additive Latency (AL) + CAS Latency (CL); $\mathrm { R L } = \mathrm { A L } + \mathrm { C L }$ . For more information on the supported CL and AL settings based on the operating clock frequency, refer to “Standard Speed Bins” on page 157. For detailed Read operation, refer to “READ Operation” on page 56. 

# 3.4 Register Definition (Cont’d)

# 3.4.2 Mode Register MR0 (Cont’d)

# 3.4.2.3 Test Mode

The normal operating mode is selected by MR0 (bit $\mathrm { A } 7 = 0$ ) and all other bits set to the desired values shown in Figure 9. Programming bit A7 to a ‘1’ places the DDR3 SDRAM into a test mode that is only used by the DRAM Manufacturer and should NOT be used. No operations or functionality is specified if $\mathrm { A } 7 = 1$ . 

# 3.4.2.4 DLL Reset

The DLL Reset bit is self-clearing, meaning that it returns back to the value of $^ { \circ }$ after the DLL reset function has been issued. Once the DLL is enabled, a subsequent DLL Reset should be applied. Any time that the DLL reset function is used, tDLLK must be met before any functions that require the DLL can be used (i.e., Read commands or ODT synchronous operations). 

# 3.4.2.5 Write Recovery

The programmed WR value MR0 (bits A9, A10, and A11) is used for the auto precharge feature along with tRP to determine tDAL. WR (write recovery for auto-precharge) min in clock cycles is calculated by dividing tWR (in ns) by tCK (in ns) and rounding up to the next integer: WRmin[cycles] $=$ Roundup(tWR[ns]/ tCK[ns]). The WR must be programmed to be equal to or larger than tWR(min). 

# 3.4.2.6 Precharge PD DLL

MR0 (bit A12) is used to select the DLL usage during precharge power-down mode. When MR0 $( \mathbf { A } 1 2 = 0$ ), or ‘slow-exit’, the DLL is frozen after entering precharge power-down (for potential power savings) and upon exit requires tXPDLL to be met prior to the next valid command. When MR0 $\mathbf { A } 1 2 = 1$ ), or ‘fast-exit’, the DLL is maintained after entering precharge power-down and upon exiting power-down requires tXP to be met prior to the next valid command. 

# 3 Functional Description (Cont’d)

# 3.4 Register Definition (Cont’d)

# 3.4.3 Mode Register MR1

The Mode Register MR1 stores the data for enabling or disabling the DLL, output driver strength, Rtt_Nom impedance, additive latency, Write leveling enable, TDQS enable and Qoff. The Mode Register 1 is written by asserting low on CS#, RAS#, CAS#, WE#, high on BA0 and low on BA1 and BA2, while controlling the states of address pins according to Figure 10. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e8b916362b5d669f4be451eceac23f551bfeadeda79769cc16178171ad73fbb6.jpg)



*2: Outputs disabled - DQs, DQSs, DQS#s.


<table><tr><td>BA1</td><td>BA0</td><td>MR Select</td></tr><tr><td>0</td><td>0</td><td>MR0</td></tr><tr><td>0</td><td>1</td><td>MR1</td></tr><tr><td>1</td><td>0</td><td>MR2</td></tr><tr><td>1</td><td>1</td><td>MR3</td></tr></table>

<table><tr><td>A5</td><td>A1</td><td>Output Driver Impedance Control</td></tr><tr><td>0</td><td>0</td><td>RZQ/6</td></tr><tr><td>0</td><td>1</td><td>RZQ/7</td></tr><tr><td>1</td><td>0</td><td>RZQ/TBD</td></tr><tr><td>1</td><td>1</td><td>RZQ/TBD</td></tr></table>


Note: $\mathrm { R Z Q } = 2 4 0 \Omega$ 


* 1 : BA2 and A8, A10, and A13 ~ A15 are RFU and must be programmed to 0 during MRS. 

# Figure 10 — MR1 Definition

# 3.4.3.1 DLL Enable/Disable

The DLL must be enabled for normal operation. DLL enable is required during power up initialization, and upon returning to normal operation after having the DLL disabled. During normal operation (DLL-on) with 

# 3.4 Register Definition (Cont’d)

# 3.4.3 Mode Register MR1 (Cont’d)

MR1 $( \mathrm { A } 0 = 0 ) _ { , }$ ), the DLL is automatically disabled when entering Self-Refresh operation and is automatically re-enabled upon exit of Self-Refresh operation. Any time the DLL is enabled and subsequently reset, tDLLK clock cycles must occur before a Read or synchronous ODT command can be issued to allow time for the internal clock to be synchronized with the external clock. Failing to wait for synchronization to occur may result in a violation of the tDQSCK, tAON or tAOF parameters. During tDLLK, CKE must continuously be registered high. DDR3 SDRAM does not require DLL for any Write operation, except when RTT_WR is enabled and the DLL is required for proper ODT operation. For more detailed information on DLL Disable operation refer to “DLL-off Mode” on page 37. 

The direct ODT feature is not supported during DLL-off mode. The on-die termination resistors must be disabled by continuously registering the ODT pin low and/or by programming the RTT_Nom bits MR1{A9,A6,A2} to {0,0,0} via a mode register set command during DLL-off mode. 

The dynamic ODT feature is not supported at DLL-off mode. User must use MRS command to set Rtt_WR, MR2 $\{ \mathrm { A } 1 0 , \mathrm { A } 9 \} = \{ 0 , 0 \}$ , to disable Dynamic ODT externally. 

# 3.4.3.2 Output Driver Impedance Control

The output driver impedance of the DDR3 SDRAM device is selected by MR1 (bits A1 and A5) as shown in Figure 10. 

# 3.4.3.3 ODT Rtt Values

DDR3 SDRAM is capable of providing two different termination values (Rtt_Nom and Rtt_WR). The nominal termination value Rtt_Nom is programmed in MR1. A separate value (Rtt_WR) may be programmed in MR2 to enable a unique RTT value when ODT is enabled during writes. The Rtt_WR value can be applied during writes even when Rtt_Nom is disabled. 

# 3.4.3.4 Additive Latency (AL)

Additive Latency (AL) operation is supported to make command and data bus efficient for sustainable bandwidths in DDR3 SDRAM. In this operation, the DDR3 SDRAM allows a read or write command (either with or without auto-precharge) to be issued immediately after the active command. The command is held for the time of the Additive Latency (AL) before it is issued inside the device. The Read Latency (RL) is controlled by the sum of the AL and CAS Latency (CL) register settings. Write Latency (WL) is controlled by the sum of the AL and CAS Write Latency (CWL) register settings. A summary of the AL register options are shown in Table 4. 


Table 4 — Additive Latency (AL) Settings


<table><tr><td>A4</td><td>A3</td><td>AL</td></tr><tr><td>0</td><td>0</td><td>0 (AL Disabled)</td></tr><tr><td>0</td><td>1</td><td>CL - 1</td></tr><tr><td>1</td><td>0</td><td>CL - 2</td></tr><tr><td>1</td><td>1</td><td>Reserved</td></tr></table>

NOTE: AL has a value of CL - 1 or CL - 2 as per the CL values programmed in the MR0 register. 

# 3.4.3.5 Write leveling

For better signal integrity, DDR3 memory module adopted fly-by topology for the commands, addresses, control signals, and clocks. The fly-by topology has the benefit of reducing the number of stubs and their length, but it also causes flight time skew between clock and strobe at every DRAM on the DIMM. This makes it difficult for the Controller to maintain tDQSS, tDSS, and tDSH specification. Therefore, the DDR3 SDRAM supports a ‘write leveling’ feature to allow the controller to compensate for skew. See 4.8 “Write Leveling” on page 42 for more details. 

# 3.4 Register Definition (Cont’d)

# 3.4.3 Mode Register MR1 (Cont’d

# 3.4.3.6 Output Disable

The DDR3 SDRAM outputs may be enabled/disabled by MR1 (bit A12) as shown in Figure 10. When this feature is enabled $( \mathbf { A } 1 2 = 1$ ), all output pins (DQs, DQS, DQS#, etc.) are disconnected from the device, thus removing any loading of the output drivers. This feature may be useful when measuring module power, for example. For normal operation, A12 should be set to $^ { \circ }$ . 

# 3.4.3.7 TDQS, TDQS#

TDQS (Termination Data Strobe) is a feature of X8 DDR3 SDRAM that provides additional termination resistance outputs that may be useful in some system configurations. 

TDQS is not supported in X4 or X16 configurations. When enabled via the mode register, the same termination resistance function is applied to the TDQS/TDQS# pins that is applied to the DQS/DQS# pins. 

In contrast to the RDQS function of DDR2 SDRAM, TDQS provides the termination resistance function only. The data strobe function of RDQS is not provided by TDQS. 

The TDQS and DM functions share the same pin. When the TDQS function is enabled via the mode register, the DM function is not supported. When the TDQS function is disabled, the DM function is provided and the TDQS# pin is not used. See Table 5 for details. 

The TDQS function is available in X8 DDR3 SDRAM only and must be disabled via the mode register $\mathrm { A l l } { = } 0$ in MR1 for X4 and X16 configurations. 


Table 5 — TDQS, TDQS# Function Matrix


<table><tr><td>MR1 (A11)</td><td>DM / TDQS</td><td>NU / TDQS</td></tr><tr><td>0 (TDQS Disabled)</td><td>DM</td><td>Hi-Z</td></tr><tr><td>1 (TDQS Enabled)</td><td>TDQS</td><td>TDQS#</td></tr></table>


NOTE 1 If TDQS is enabled, the DM function is disabled. 



NOTE 2 When not used, TDQS function can be disabled to save termination power. 



NOTE 3 TDQS function is only available for X8 DRAM and must be disabled for X4 and X16. 


# 3 Functional Description (Cont’d)

# 3.4 Register Definition (Cont’d)

# 3.4.4 Mode Register MR2

The Mode Register MR2 stores the data for controlling refresh related features, Rtt_WR impedance, and CAS write latency. The Mode Register 2 is written by asserting low on CS#, RAS#, CAS#, WE#, high on BA1 and low on BA0 and BA2, while controlling the states of address pins according to the table below. 

MR2 Programming 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/54b7e679e592841f163ba76eff802ead3a52b323724a2e55e9e4b8cd56e448c3.jpg)



* 1 : BA2, A5, A8, A11 ~ A15 are RFU and must be programmed to 0 during MRS.



* 2 : The Rtt_WR value can be applied during writes even when Rtt_Nom is disabled. During write leveling, Dynamic ODT is not available.



Figure 11 — MR2 Definition


# 3.4 Register Definition (Cont’d)

# 3.4.4 Mode Register MR2 (Cont’d)

# 3.4.4.1 Partial Array Self-Refresh (PASR)

Optional in DDR3 SDRAM: Users should refer to the DRAM supplier data sheet and/or the DIMM SPD to determine if DDR3 SDRAM devices support the following options or requirements referred to in this material. If PASR (Partial Array Self-Refresh) is enabled, data located in areas of the array beyond the specified address range shown in Figure 11 will be lost if Self-Refresh is entered. Data integrity will be maintained if tREFI conditions are met and no Self-Refresh command is issued. 

# 3.4.4.2 CAS Write Latency (CWL)

The CAS Write Latency is defined by MR2 (bits A3-A5), as shown in Figure 11. CAS Write Latency is the delay, in clock cycles, between the internal Write command and the availability of the first bit of input data. DDR3 SDRAM does not support any half-clock latencies. The overall Write Latency (WL) is defined as Additive Latency $( \mathrm { A L } ) + \mathrm { C A S }$ Write Latency (CWL); $\mathrm { W L } = \mathbf { A } \mathbf { L } + \mathbf { C } \mathbf { W } \mathbf { L }$ . For more information on the supported CWL and AL settings based on the operating clock frequency, refer to “Standard Speed Bins” on page 157. For detailed Write operation refer to “WRITE Operation” on page 68. 

# 3.4.4.3 Auto Self-Refresh (ASR) and Self-Refresh Temperature (SRT)

Optional in DDR3 SDRAM: Users should refer to the DRAM supplier data sheet and/or the DIMM SPD to determine if DDR3 SDRAM devices support the following options or requirements referred to in this material. For more details refer to “Extended Temperature Usage” on page 46. DDR3 SDRAMs must support Self-Refresh operation at all supported temperatures. Applications requiring Self-Refresh operation in the Extended Temperature Range must use the optional ASR function or program the SRT bit appropriately. 

# 3.4.4.4 Dynamic ODT (Rtt_WR)

DDR3 SDRAM introduces a new feature “Dynamic ODT”. In certain application cases and to further enhance signal integrity on the data bus, it is desirable that the termination strength of the DDR3 SDRAM can be changed without issuing an MRS command. MR2 Register locations A9 and A10 configure the Dynamic ODT setings. In Write leveling mode, only RTT_Nom is available. For details on Dynamic ODT operation, refer to “Dynamic ODT” on page 96. 

# 3 Functional Description (Cont’d)

# 3.4 Register Definition (Cont’d)

# 3.4.5 Mode Register MR3

The Mode Register MR3 controls Multi purpose registers. The Mode Register 3 is written by asserting low on CS#, RAS#, CAS#, WE#, high on BA1 and BA0, and low on BA2 while controlling the states of address pins according to the table below. 

# MR3 Programming

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/4d146881cbeb43ef3be22a3b787cdc855ae142ac618ec730c93a171502353c1f.jpg)


<table><tr><td>BA1</td><td>BA0</td><td>MR Select</td></tr><tr><td>0</td><td>0</td><td>MR0</td></tr><tr><td>0</td><td>1</td><td>MR1</td></tr><tr><td>1</td><td>0</td><td>MR2</td></tr><tr><td>1</td><td>1</td><td>MR3</td></tr></table>


* 1 : BA2, A3 - A15 are RFU and must be programmed to 0 during MRS. 



* 2 : The predefined pattern will be used for read synchronization. 



* 3 : When MPR control is set for normal operation (MR3 A[2] = 0) then MR3 A[1:0] will be ignored. 



Figure 12 — MR3 Definition


# 3.4.5.1 Multi-Purpose Register (MPR)

The Multi Purpose Register (MPR) function is used to Read out a predefined system timing calibration bit sequence. To enable the MPR, a MODE Register Set (MRS) command must be issued to MR3 Register with bit $\mathbf { A } 2 = 1$ . Prior to issuing the MRS command, all banks must be in the idle state (all banks precharged and tRP met). Once the MPR is enabled, any subsequent RD or RDA commands will be redirected to the Multi Purpose Register. When the MPR is enabled, only RD or RDA commands are allowed until a subsequent MRS command is issued with the MPR disabled (MR3 bit ${ \bf A } 2 = 0$ ). Power-Down mode, Self-Refresh, and any other non-RD/RDA command is not allowed during MPR enable mode. The RESET function is supported during MPR enable mode. For detailed MPR operation refer to “Multi Purpose Register” on page 48. 

# 4 DDR3 SDRAM Command Description and Operation

# 4.1 Command Truth Table

Notes 1, 2, 3, and 4 apply to the entire Command Truth Table 

Note 5 applies to all Read/Write commands 

[BA $\ c =$ Bank Address, RA=Row Address, CA=Column Address, BC#=Burst Chop, X=Don’t Care, V=Valid] 


Table 6 — Command Truth Table


<table><tr><td rowspan="2">Function</td><td rowspan="2">Abbreviation</td><td colspan="2">CKE</td><td rowspan="2">CS#</td><td rowspan="2">RAS#</td><td rowspan="2">CAS#</td><td rowspan="2">WE#</td><td rowspan="2">BA0-BA2</td><td rowspan="2">A13-A15</td><td rowspan="2">A12-BC#</td><td rowspan="2">A10-AP</td><td rowspan="2">A0-A9,A11</td><td rowspan="2">Notes</td></tr><tr><td>Previous Cycle</td><td>Current Cycle</td></tr><tr><td>Mode Register Set</td><td>MRS</td><td>H</td><td>H</td><td>L</td><td>L</td><td>L</td><td>L</td><td>BA</td><td colspan="4">OP Code</td><td></td></tr><tr><td>Refresh</td><td>REF</td><td>H</td><td>H</td><td>L</td><td>L</td><td>L</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td><td></td></tr><tr><td>Self Refresh Entry</td><td>SRE</td><td>H</td><td>L</td><td>L</td><td>L</td><td>L</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td><td>7,9,12</td></tr><tr><td rowspan="2">Self Refresh Exit</td><td rowspan="2">SRX</td><td rowspan="2">L</td><td rowspan="2">H</td><td>H</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td rowspan="2">7,8,9,12</td></tr><tr><td>L</td><td>H</td><td>H</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td></tr><tr><td>Single Bank Precharge</td><td>PRE</td><td>H</td><td>H</td><td>L</td><td>L</td><td>H</td><td>L</td><td>BA</td><td>V</td><td>V</td><td>L</td><td>V</td><td></td></tr><tr><td>Precharge all Banks</td><td>PREA</td><td>H</td><td>H</td><td>L</td><td>L</td><td>H</td><td>L</td><td>V</td><td>V</td><td>V</td><td>H</td><td>V</td><td></td></tr><tr><td>Bank Activate</td><td>ACT</td><td>H</td><td>H</td><td>L</td><td>L</td><td>H</td><td>H</td><td>BA</td><td colspan="4">Row Address (RA)</td><td></td></tr><tr><td>Write (Fixed BL8 or BC4)</td><td>WR</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>V</td><td>L</td><td>CA</td><td></td></tr><tr><td>Write (BC4, on the Fly)</td><td>WRS4</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>L</td><td>L</td><td>CA</td><td></td></tr><tr><td>Write (BL8, on the Fly)</td><td>WRS8</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>H</td><td>L</td><td>CA</td><td></td></tr><tr><td>Write with Auto Precharge (Fixed BL8 or BC4)</td><td>WRA</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>V</td><td>H</td><td>CA</td><td></td></tr><tr><td>Write with Auto Precharge (BC4, on the Fly)</td><td>WRAS4</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>L</td><td>H</td><td>CA</td><td></td></tr><tr><td>Write with Auto Precharge (BL8, on the Fly)</td><td>WRAS8</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>H</td><td>H</td><td>CA</td><td></td></tr><tr><td>Read (Fixed BL8 or BC4)</td><td>RD</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>V</td><td>L</td><td>CA</td><td></td></tr><tr><td>Read (BC4, on the Fly)</td><td>RDS4</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>L</td><td>L</td><td>CA</td><td></td></tr><tr><td>Read (BL8, on the Fly)</td><td>RDS8</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>H</td><td>L</td><td>CA</td><td></td></tr><tr><td>Read with Auto Precharge (Fixed BL8 or BC4)</td><td>RDA</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>V</td><td>H</td><td>CA</td><td></td></tr><tr><td>Read with Auto Precharge (BC4, on the Fly)</td><td>RDAS4</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>L</td><td>H</td><td>CA</td><td></td></tr><tr><td>Read with Auto Precharge (BL8, on the Fly)</td><td>RDAS8</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>H</td><td>H</td><td>CA</td><td></td></tr><tr><td>No Operation</td><td>NOP</td><td>H</td><td>H</td><td>L</td><td>H</td><td>H</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td><td>10</td></tr><tr><td>Device Deselect</td><td>DES</td><td>H</td><td>H</td><td>H</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>11</td></tr><tr><td rowspan="2">Power Down Entry</td><td rowspan="2">PDE</td><td rowspan="2">H</td><td rowspan="2">L</td><td>L</td><td>H</td><td>H</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td><td rowspan="2">6,12</td></tr><tr><td>H</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td rowspan="2">Power Down Exit</td><td rowspan="2">PDX</td><td rowspan="2">L</td><td rowspan="2">H</td><td>L</td><td>H</td><td>H</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td><td rowspan="2">6,12</td></tr><tr><td>H</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>ZQ Calibration Long</td><td>ZQCL</td><td>H</td><td>H</td><td>L</td><td>H</td><td>H</td><td>L</td><td>X</td><td>X</td><td>X</td><td>H</td><td>X</td><td></td></tr><tr><td>ZQ Calibration Short</td><td>ZQCS</td><td>H</td><td>H</td><td>L</td><td>H</td><td>H</td><td>L</td><td>X</td><td>X</td><td>X</td><td>L</td><td>X</td><td></td></tr></table>

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.1 Command Truth Table (Cont’d)


Table 6 — Command Truth Table (Cont’d)


<table><tr><td rowspan="2">Function</td><td rowspan="2">Abbreviation</td><td colspan="2">CKE</td><td rowspan="2">CS#</td><td rowspan="2">RAS#</td><td rowspan="2">CAS#</td><td rowspan="2">WE#</td><td rowspan="2">BA0-BA2</td><td rowspan="2">A13-A15</td><td rowspan="2">A12-BC#</td><td rowspan="2">A10-AP</td><td rowspan="2">A0-A9,A11</td><td rowspan="2">Notes</td></tr><tr><td>Previous Cycle</td><td>Current Cycle</td></tr><tr><td>NOTE 1</td><td colspan="13">All DDR3 SDRAM commands are defined by states of CS#, RAS#, CAS#, WE# and CKE at the rising edge of the clock. The MSB of BA, RA and CA are device density and configuration dependant.</td></tr><tr><td>NOTE 2</td><td colspan="13">RESET# is Low enable command which will be used only for asynchronous reset so must be maintained HIGH during any function.</td></tr><tr><td>NOTE 3</td><td colspan="13">Bank addresses (BA) determine which bank is to be operated upon. For (E)MRS BA selects an (Extended) Mode Register.</td></tr><tr><td>NOTE 4</td><td colspan="13">“V” means “H or L (but a defined logic level)” and “X” means either “defined or undefined (like floating) logic level”.</td></tr><tr><td>NOTE 5</td><td colspan="13">Burst reads or writes cannot be terminated or interrupted and Fixed/on-the-Fly BL will be defined by MRS.</td></tr><tr><td>NOTE 6</td><td colspan="13">The Power Down Mode does not perform any refresh operation.</td></tr><tr><td>NOTE 7</td><td colspan="13">The state of ODT does not affect the states described in this table. The ODT function is not available during Self Refresh.</td></tr><tr><td>NOTE 8</td><td colspan="13">Self Refresh Exit is asynchronous.</td></tr><tr><td>NOTE 9</td><td colspan="13">VREF(Both VrefDQ and VrefCA) must be maintained during Self Refresh operation. VrefDQ supply may be turned OFF and VREFDQ may take any value between VSS and VDD during Self Refresh operation, provided that VrefDQ is valid and stable prior to CKE going back High and that first Write operation or first Write Level-ing Activity may not occur earlier than 512 nCK after exit from Self Refresh.</td></tr><tr><td>NOTE 10</td><td colspan="13">The No Operation command should be used in cases when the DDR3 SDRAM is in an idle or wait state. The purpose of the No Operation command (NOP) is to prevent the DDR3 SDRAM from registering any unwanted commands between operations. A No Operation command will not terminate a pervious operation that is still executing, such as a burst read or write cycle.</td></tr><tr><td>NOTE 11</td><td colspan="13">The Deselect command performs the same function as No Operation command.</td></tr><tr><td>NOTE 12</td><td colspan="13">Refer to the CKE Truth Table for more detail with CKE transition.</td></tr></table>

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.2 CKE Truth Table

Notes 1-7 apply to the entire CKE Truth Table. 

For Power-down entry and exit parameters See 4.17 “Power-Down Modes” on page 81. 

CKE low is allowed only if tMRD and tMOD are satisfied. 


Table 7 — CKE Truth Table


<table><tr><td rowspan="2">Current State2</td><td colspan="2">CKE</td><td rowspan="2">Command (N)3RAS#, CAS#, WE#, CS#</td><td rowspan="2">Action (N)3</td><td rowspan="2">Notes</td></tr><tr><td>Previous Cycle1(N-1)</td><td>Current Cycle1(N)</td></tr><tr><td rowspan="2">Power-Down</td><td>L</td><td>L</td><td>X</td><td>Maintain Power-Down</td><td>14, 15</td></tr><tr><td>L</td><td>H</td><td>DESELECT or NOP</td><td>Power-Down Exit</td><td>11, 14</td></tr><tr><td rowspan="2">Self-Refresh</td><td>L</td><td>L</td><td>X</td><td>Maintain Self-Refresh</td><td>15, 16</td></tr><tr><td>L</td><td>H</td><td>DESELECT or NOP</td><td>Self-Refresh Exit</td><td>8, 12, 16</td></tr><tr><td>Bank(s) Active</td><td>H</td><td>L</td><td>DESELECT or NOP</td><td>Active Power-Down Entry</td><td>11, 13, 14</td></tr><tr><td>Reading</td><td>H</td><td>L</td><td>DESELECT or NOP</td><td>Power-Down Entry</td><td>11, 13, 14, 17</td></tr><tr><td>Writing</td><td>H</td><td>L</td><td>DESELECT or NOP</td><td>Power-Down Entry</td><td>11, 13, 14, 17</td></tr><tr><td>Precharging</td><td>H</td><td>L</td><td>DESELECT or NOP</td><td>Power-Down Entry</td><td>11, 13, 14, 17</td></tr><tr><td>Refreshing</td><td>H</td><td>L</td><td>DESELECT or NOP</td><td>Precharge Power-Down Entry</td><td>11</td></tr><tr><td rowspan="2">All Banks Idle</td><td>H</td><td>L</td><td>DESELECT or NOP</td><td>Precharge Power-Down Entry</td><td>11, 13, 14, 18</td></tr><tr><td>H</td><td>L</td><td>REFRESH</td><td>Self-Refresh</td><td>9, 13, 18</td></tr><tr><td colspan="5">For more details with all signals See 4.1 &quot;Command Truth Table&quot; on page 33.</td><td>10</td></tr><tr><td colspan="6">NOTE 1 CKE (N) is the logic state of CKE at clock edge N; CKE (N-1) was the state of CKE at the previous clock edge. 
NOTE 2 Current state is defined as the state of the DDR3 SDRAM immediately prior to clock edge N. 
NOTE 3 COMMAND (N) is the command registered at clock edge N, and ACTION (N) is a result of COMMAND (N), ODT is not included here. 
NOTE 4 All states and sequences not shown are illegal or reserved unless explicitly described elsewhere in this document. 
NOTE 5 The state of ODT does not affect the states described in this table. The ODT function is not available during Self-Refresh. 
NOTE 6 CKE must be registered with the same value on tCKEmin consecutive positive clock edges. CKE must remain at the valid input level the entire time it takes to achieve the tCKEmin clocks of registration. Thus, after any CKE transition, CKE may not transition from its valid level during the time period of tIS + tCKEmin + tIH. 
NOTE 7 DESELECT and NOP are defined in the Command Truth Table. 
NOTE 8 On Self-Refresh Exit DESELECT or NOP commands must be issued on every clock edge occurring during the tXS period. Read or ODT commands may be issued only after tXSDLL is satisfied. 
NOTE 9 Self-Refresh mode can only be entered from the All Banks Idle state. 
NOTE 10 Must be a legal command as defined in the Command Truth Table. 
NOTE 11 Valid commands for Power-Down Entry and Exit are NOP and DESELECT only. 
NOTE 12 Valid commands for Self-Refresh Exit are NOP and DESELECT only. 
NOTE 13 Self-Refresh can not be entered during Read or Write operations. For a detailed list of restrictions See 4.16 &quot;Self-Refresh Operation&quot; on page 79 and See 4.17 &quot;Power-Down Modes&quot; on page 81.</td></tr></table>

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.2 CKE Truth Table (Cont’d)


Table 7 — CKE Truth Table (Cont’d)


<table><tr><td rowspan="2">Current State2</td><td colspan="2">CKE</td><td rowspan="2">Command (N)3RAS#, CAS#, WE#, CS#</td><td rowspan="2">Action (N)3</td><td rowspan="2">Notes</td></tr><tr><td>Previous Cycle1(N-1)</td><td>Current Cycle1(N)</td></tr><tr><td colspan="6">NOTE 14 The Power-Down does not perform any refresh operations.</td></tr><tr><td colspan="6">NOTE 15 “X” means “don’t care” (including floating around VREF) in Self-Refresh and Power-Down. It also applies to Address pins.</td></tr><tr><td colspan="6">NOTE 16 VREF (Both Vref_DQ and Vref_CA) must be maintained during Self-Refresh operation. VrefDQ supply may be turned OFF and VREFDQ may take any value between VSS and VDD during Self Refresh operation, provided that VrefDQ is valid and stable prior to CKE going back High and that first Write operation or first Write Level-ing Activity may not occur earlier than 512 nCK after exit from Self Refresh.</td></tr><tr><td colspan="6">NOTE 17 If all banks are closed at the conclusion of the read, write or precharge command, then Precharge Power-Down is entered, otherwise Active Power-Down is entered.</td></tr><tr><td colspan="6">NOTE 18 ‘Idle state’ is defined as all banks are closed (tRP, tDAL, etc. satisfied), no data bursts are in progress, CKE is high, and all timings from previous operations are satisfied (tMRD, tMOD, tRFC, tZQinit, tZQoper, tZQCS, etc.) as well as all Self-Refresh exit and Power-Down Exit parameters are satisfied (tXS, tXP, tXPDLL, etc).</td></tr></table>

# 4.3 No OPeration (NOP) Command

The No OPeration (NOP) command is used to instruct the selected DDR3 SDRAM to perform a NOP (CS# LOW and RAS#, CAS#, and WE# HIGH). This prevents unwanted commands from being registered during idle or wait states. Operations already in progress are not affected. 

# 4.4 Deselect Command

The DESELECT function (CS# HIGH) prevents new commands from being executed by the DDR3 SDRAM. The DDR3 SDRAM is effectively deselected. Operations already in progress are not affected. 

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.5 DLL-off Mode

DDR3 DLL-off mode is entered by setting MR1 bit A0 to “1”; this will disable the DLL for subsequent operations until A0 bit is set back to $^ { \circ } 0 ^ { \circ }$ . The MR1 A0 bit for DLL control can be switched either during initialization or later. Refer to “Input clock frequency change” on page 40 

The DLL-off Mode operations listed below are an optional feature for DDR3. The maximum clock frequency for DLL-off Mode is specified by the parameter tCKDLL_OFF. There is no minimum frequency limit besides the need to satisfy the refresh interval, tREFI. 

Due to latency counter and timing restrictions, only one value of CAS Latency (CL) in MR0 and CAS Write Latency (CWL) in MR2 are supported. The DLL-off mode is only required to support setting of both $\mathrm { C L } { = } 6$ and CWL=6. 

DLL-off mode will affect the Read data Clock to Data Strobe relationship (tDQSCK), but not the Data Strobe to Data relationship (tDQSQ, tQH). Special attention is needed to line up Read data to controller time domain. 

Comparing with DLL-on mode, where tDQSCK starts from the rising clock edge $\mathrm { A L ^ { + C L } }$ ) cycles after the Read command, the DLL-off mode tDQSCK starts $\scriptstyle ( { \mathrm { A L } } + { \mathrm { C L } } - 1$ ) cycles after the read command. Another difference is that tDQSCK may not be small compared to tCK (it might even be larger than tCK) and the difference between tDQSCKmin and tDQSCKmax is significantly larger than in DLL-on mode. tDQSCK(DLL_off) values are vendor specific. 

The timing relations on DLL-off mode READ operation are shown in the following Timing Diagram (CL=6, BL=8): 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b5abff5a551f388e593b1ed38a390a07faa1322e8e22125ccb52ec33ad9267a0.jpg)



Figure 13 — DLL-off mode READ Timing Operation


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.6 DLL on/off switching procedure

DDR3 DLL-off mode is entered by setting MR1 bit A0 to “1”; this will disable the DLL for subsequent operations until A0 bit is set back to $^ { \circ } 0 ^ { \circ }$ . 

# 4.6.1 DLL “on” to DLL “off” Procedure

To switch from DLL “on” to DLL “off” requires the frequency to be changed during Self-Refresh, as outlined in the following procedure: 

1. Starting from Idle state (All banks pre-charged, all timings fulfilled, and DRAMs On-die Termination resistors, RTT, must be in high impedance state before MRS to MR1 to disable the DLL.) 

2. Set MR1 bit A0 to “1” to disable the DLL. 

3. Wait tMOD. 

4. Enter Self Refresh Mode; wait until (tCKSRE) is satisfied. 

5. Change frequency, in guidance with “Input clock frequency change” on page 40. 

6. Wait until a stable clock is available for at least (tCKSRX) at DRAM inputs. 

7. Starting with the Self Refresh Exit command, CKE must continuously be registered HIGH until all tMOD timings from any MRS command are satisfied. In addition, if any ODT features were enabled in the mode registers when Self Refresh mode was entered, the ODT signal must continuously be registered LOW until all tMOD timings from any MRS command are satisfied. If both ODT features were disabled in the mode registers when Self Refresh mode was entered, ODT signal can be registered LOW or HIGH. 

8. Wait tXS, then set Mode Registers with appropriate values (especially an update of CL, CWL and WR may be necessary. A ZQCL command may also be issued after tXS). 

9. Wait for tMOD, then DRAM is ready for next command. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/22c4639ae3dca512b128f6bee8aec93d17749ea884881b495ef42c8ff772856a.jpg)


1. Starting with Idle State, RTT in Hi-Z stateNOTES: 

2. Disable DLL by setting MR1 Bit A0 to 1 

3. Enter SR 

4. Change Frequency 

5. Clock must be stable tCKSRX 

6. Exit SR 

7. Update Mode registers with DLL off parameters setting 

8. Any valid command 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/89bd70de55f624668e370bbb38a98110344024bb44393ec4779621b2740543b9.jpg)



Figure 14 — DLL Switch Sequence from DLL-on to DLL-off


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.6 DLL on/off switching procedure (Cont’d)

# 4.6.2 DLL “off” to DLL “on” Procedure

To switch from DLL “off” to DLL “on” (with required frequency change) during Self-Refresh: 

1. Starting from Idle state (All banks pre-charged, all timings fulfilled and DRAMs On-die Termination resistors (RTT) must be in high impedance state before Self-Refresh mode is entered.) 

2. Enter Self Refresh Mode, wait until tCKSRE satisfied. 

3. Change frequency, in guidance with "Input clock frequency change" on page 40. 

4. Wait until a stable clock is available for at least (tCKSRX) at DRAM inputs. 

5. Starting with the Self Refresh Exit command, CKE must continuously be registered HIGH until tDLLK timing from subsequent DLL Reset command is satisfied. In addition, if any ODT features were enabled in the mode registers when Self Refresh mode was entered, the ODT signal must continuously be registered LOW until tDLLK timings from subsequent DLL Reset command is satisfied. If both ODT features are disabled in the mode registers when Self Refresh mode was entered, ODT signal can be registered LOW or HIGH. 

6. Wait tXS, then set MR1 bit A0 to $^ { \circ } 0 ^ { \circ }$ to enable the DLL. 

7. Wait tMRD, then set MR0 bit A8 to “1” to start DLL Reset. 

8. Wait tMRD, then set Mode Registers with appropriate values (especially an update of CL, CWL and WR may be necessary. After tMOD satisfied from any proceeding MRS command, a ZQCL command may also be issued during or after tDLLK.) 

9. Wait for tMOD, then DRAM is ready for next command (Remember to wait tDLLK after DLL Reset before applying command requiring a locked DLL!). In addition, wait also for tZQoper in case a ZQCL command was issued. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/6369afe0e20eae63c5fbe225fcb7ea2c0d64b2d23da408cec87c570ed6aab6af.jpg)



ODT: Static LOW in case RTT_Nom and RTT_WR is enabled, otherwise static Low or High


1. Starting with Idle StateNOTES: 

2. Enter SR 

3. Change Frequency 

4. Clock must be stable tCKSRX 

5. Exit SR 

6. Set DLL on by MR1 $\mathsf { A O } { = } 0$ 

7. Update Mode registers 

8. Any valid command 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/cb78d46b61972adec2dcb412441007ad5c4e89654660530242928249dd9ae455.jpg)



Figure 15 — DLL Switch Sequence from DLL Off to DLL On


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.7 Input clock frequency change

Once the DDR3 SDRAM is initialized, the DDR3 SDRAM requires the clock to be “stable” during almost all states of normal operation. This means that, once the clock frequency has been set and is to be in the “stable state”, the clock period is not allowed to deviate except for what is allowed for by the clock jitter and SSC (spread spectrum clocking) specifications. 

The input clock frequency can be changed from one stable clock rate to another stable clock rate under two conditions: (1) Self-Refresh mode and (2) Precharge Power-down mode. Outside of these two modes, it is illegal to change the clock frequency. 

For the first condition, once the DDR3 SDRAM has been successfully placed in to Self-Refresh mode and t CKSRE has been satisfied, the state of the clock becomes a don’t care. Once a don’t care, changing the clock frequency is permissible, provided the new clock frequency is stable prior to t CKSRX. When entering and exiting Self-Refresh mode for the sole purpose of changing the clock frequency, the Self-Refresh entry and exit specifications must still be met as outlined in See 4.16 “Self-Refresh Operation” on page 79. The DDR3 SDRAM input clock frequency is allowed to change only within the minimum and maximum operating frequency specified for the particular speed grade. Any frequency change below the minimum operating frequency would require the use of DLL_on- mode $\mathrm { . > }$ DLL_off -mode transition sequence, refer to “DLL on/off switching procedure” on page 38. 

The second condition is when the DDR3 SDRAM is in Precharge Power-down mode (either fast exit mode or slow exit mode). If the RTT_NOM feature was enabled in the mode register prior to entering Precharge power down mode, the ODT signal must continuously be registered LOW ensuring RTT is in an off state. If the RTT_NOM feature was disabled in the mode register prior to entering Precharge power down mode, RTT will remain in the off state. The ODT signal can be registered either LOW or HIGH in this case. A minimum of t CKSRE must occur after CKE goes LOW before the clock frequency may change. The DDR3 SDRAM input clock frequency is allowed to change only within the minimum and maximum operating frequency specified for the particular speed grade. During the input clock frequency change, ODT and CKE must be held at stable LOW levels. Once the input clock frequency is changed, stable new clocks must be provided to the DRAM t CKSRX before Precharge Power-down may be exited; after Precharge Power-down is exited and tXP has expired, the DLL must be RESET via MRS. Depending on the new clock frequency, additional MRS commands may need to be issued to appropriately set the WR, CL, and CWL with CKE continuously registered high. During DLL re-lock period, ODT must remain LOW and CKE must remain HIGH. After the DLL lock time, the DRAM is ready to operate with new clock frequency. This process is depicted in Figure 16 on page 41. 

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.7 Input clock frequency change (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/8486594779360fe725d6d013d61dd6d6908b40821db40e5f4a7594c66f602294.jpg)



NOTES: 1. Applicable for both SLOW recharge Power-down



2. tAOFPD and tAOF must be statisfied and outputs High-Z prior to T1; refer to ODT timing section for exact requirements



3. If the RTT_NOM feature was enabled in the mode register prior to entering Precharge power down mode, the ODT signal must continuously be registered LOW ensuring RTT is in an off state, as shown in Figure 13. If the RTT_NOM feature was disabled in the mode register prior to entering Precharge power down mode, RTT will remain in the off state. The ODT signal can be registered either LOW or HIGH in this case.



Figure 16 — Change Frequency during Precharge Power-down


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.8 Write Leveling

For better signal integrity, the DDR3 memory module adopted fly-by topology for the commands, addresses, control signals, and clocks. The fly-by topology has benefits from reducing number of stubs and their length, but it also causes flight time skew between clock and strobe at every DRAM on the DIMM. This makes it difficult for the Controller to maintain tDQSS, tDSS, and tDSH specification. Therefore, the DDR3 SDRAM supports a ‘write leveling’ feature to allow the controller to compensate for skew. 

The memory controller can use the ‘write leveling’ feature and feedback from the DDR3 SDRAM to adjust the DQS - DQS# to CK - CK# relationship. The memory controller involved in the leveling must have adjustable delay setting on DQS - DQS# to align the rising edge of DQS - DQS# with that of the clock at the DRAM pin. The DRAM asynchronously feeds back CK - CK#, sampled with the rising edge of DQS - DQS#, through the DQ bus. The controller repeatedly delays DQS - DQS# until a transition from 0 to 1 is detected. The DQS - DQS# delay established though this exercise would ensure tDQSS specification. Besides tDQSS, tDSS and tDSH specification also needs to be fulfilled. One way to achieve this is to combine the actual tDQSS in the application with an appropriate duty cycle and jitter on the DQS - DQS# signals. Depending on the actual tDQSS in the application, the actual values for tDQSL and tDQSH may have to be better than the absolute limits provided in the chapter "AC Timing Parameters" in order to satisfy tDSS and tDSH specification. A conceptual timing of this scheme is shown in Figure 17. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/4770307884bcb4de0d194e486fd3356a56d931e36defd5415e301a27d8b60604.jpg)



Figure 17 — Write Leveling Concept


DQS - DQS# driven by the controller during leveling mode must be terminated by the DRAM based on ranks populated. Similarly, the DQ bus driven by the DRAM must also be terminated at the controller. 

One or more data bits should carry the leveling feedback to the controller across the DRAM configurations X4, X8, and X16. On a X16 device, both byte lanes should be leveled independently. Therefore, a separate feedback mechanism should be available for each byte lane. The upper data bits should provide the feedback of the upper diff_DQS(diff_UDQS) to clock relationship whereas the lower data bits would indicate the lower diff_DQS(diff_LDQS) to clock relationship. 

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.8 Write Leveling (Cont’d)

# 4.8.1 DRAM setting for write leveling & DRAM termination function in that mode

DRAM enters into Write leveling mode if A7 in MR1 set ’High’ and after finishing leveling, DRAM exits from write leveling mode if A7 in MR1 set ’Low’ (Table 8). Note that in write leveling mode, only DQS/ DQS# terminations are activated and deactivated via ODT pin, unlike normal operation (Table 9). 


Table 8 — MR setting involved in the leveling procedure


<table><tr><td>Function</td><td>MR1</td><td>Enable</td><td>Disable</td></tr><tr><td>Write leveling enable</td><td>A7</td><td>1</td><td>0</td></tr><tr><td>Output buffer mode (Qoff)</td><td>A12</td><td>0</td><td>1</td></tr></table>


Table 9 — DRAM termination function in the leveling mode


<table><tr><td>ODT pin @DRAM</td><td>DQS/DQS# termination</td><td>DQs termination</td></tr><tr><td>De-asserted</td><td>Off</td><td>Off</td></tr><tr><td>Asserted</td><td>On</td><td>Off</td></tr></table>


NOTE: In Write Leveling Mode with its output buffer disabled $( \mathbf { M R } 1 [ \mathbf { b i t } 7 ] = 1$ with MR1[bit12] $= 1$ ) all RTT_Nom settings are allowed; in Write Leveling Mode with its output buffer enabled (MR1[bit7] $= 1$ with MR1[bit12] $= 0$ ) only RTT_Nom settings of RZQ/2, RZQ/4 and RZQ/6 are allowed. 


# 4.8.2 Procedure Description

The Memory controller initiates Leveling mode of all DRAMs by setting bit 7 of MR1 to 1. When entering write leveling mode, the DQ pins are in undefined driving mode. During write leveling mode, only NOP or DESELECT commands are allowed, as well as an MRS command to exit write leveling mode. Since the controller levels one rank at a time, the output of other ranks must be disabled by setting MR1 bit A12 to 1. The Controller may assert ODT after tMOD, at which time the DRAM is ready to accept the ODT signal. 

The Controller may drive DQS low and DQS# high after a delay of tWLDQSEN, at which time the DRAM has applied on-die termination on these signals. After tDQSL and tWLMRD, the controller provides a single DQS, DQS# edge which is used by the DRAM to sample CK - CK# driven from controller. tWLMRD(max) timing is controller dependent. 

DRAM samples CK - CK# status with rising edge of DQS - DQS# and provides feedback on all the DQ bits asynchronously after tWLO timing. Either one or all data bits ("prime DQ bit(s)") provide the leveling feedback. The DRAM's remaining DQ bits are driven Low statically after the first sampling procedure. There is a DQ output uncertainty of tWLOE defined to allow mismatch on DQ bits. The tWLOE period is defined from the transition of the earliest DQ bit to the corresponding transition of the latest DQ bit. There are no read strobes (DQS/DQS#) needed for these DQs. Controller samples incoming DQ and decides to increment or decrement DQS - DQS# delay setting and launches the next DQS/DQS# pulse after some time, which is controller dependent. Once a 0 to 1 transition is detected, the controller locks DQS - DQS# delay setting and write leveling is achieved for the device. Figure 18 describes the timing diagram and parameters for the overall Write Leveling procedure. 

# 4.8 Write Leveling (Cont’d)

# 4.8.2 Procedure Description (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a4335c8707e0ca8831690ad2be84e9fda565c6c8f3beaff84286d284b19f458d.jpg)



NOTES: 1. DRAM has the option to drive leveling feedback on a prime DQ or all DQs. If feedback is driven only on one DQ, the remaining DQs must be driven low, as shown in above Figure, and maintained at this state through out the leveling procedure.



2. MRS: Load MR1 to enter write leveling mode.



3. NOP: NOP or Deselect.



4. diff_DQS is the differential data strobe (DQS, DQS#). Timing reference points are the zero crossings. DQS is shown with solid line, DQS# is shown with dotted line.



5. CK, CK# : CK is shown with solid dark line, where as CK# is drawn with dotted line.



6. DQS, DQS# needs to fulfill minimum pulse width requirements tDQSH(min) and tDQSL(min) as defined for regular Writes; the max pulse width is system dependent.



Figure 18 — Timing details of Write leveling sequence [DQS - DQS# is capturing CK - CK# low at T1 and CK - CK# high at T2


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.8 Write Leveling (Cont’d)

# 4.8.3 Write Leveling Mode Exit

The following sequence describes how the Write Leveling Mode should be exited: 

1. After the last rising strobe edge (see ~T0), stop driving the strobe signals (see ~Tc0). Note: From now on, DQ pins are in undefined driving mode, and will remain undefined, until tMOD after the respective MR command (Te1). 

2. Drive ODT pin low (tIS must be satisfied) and continue registering low. (see Tb0). 

3. After the RTT is switched off, disable Write Level Mode via MRS command (see Tc2). 

4. 4. After tMOD is satisfied (Te1), any valid command may be registered. (MR commands may be issued after tMRD (Td1). 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e0f76ef002d5925f5494853b966653707e43bb94134a60c968d771a1fcedee45.jpg)



NOTES: 1. The DQ result $= 1$ between Ta0 and Tc0 is a result of the DQS, DQS# signals capturing CK high just after the T0 state.



2. Refer to Figure 15 for specific tWLO timing.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/7495e3c07b0e8286549238dfaeab3b62f646f8fa438e1c389b092551e7475f22.jpg)



UNDEFINED DRIVING MODE


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/f6dce79cb551cd7b90e10c51b7d2c8b1fe48d48c8422f1e18a2ea2ece9ae6f50.jpg)



TRANSITIONING


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e640a72ec852738e7e7d4c7e4eaa590e29711b0932aac0903c680af1abfc57bf.jpg)



TIME BREAK


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a3234c75aa120bdbefd9638248c526c4343868a5fa88e50b21fec7c53c9cb768.jpg)



DON’T CARE



Figure 19 — Timing details of Write leveling exit


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.9 Extended Temperature Usage

Users should refer to the DRAM supplier data sheet and/or the DIMM SPD to determine if DDR3 SDRAM devices support the following options or requirements referred to in this material: 

a. Auto Self-refresh supported 

b. Extended Temperature Range supported 

c. Double refresh required for operation in the Extended Temperature Range (applies only for devices supporting the Extended Temperature Range) 


Table 10 — Mode Register Description


<table><tr><td>Field</td><td>Bits</td><td>Description</td></tr><tr><td>ASR</td><td>MR2 (A6)</td><td>Auto Self-Refresh (ASR) (Optional) when enabled, DDR3 SDRAM automatically provides Self-Refresh power management functions for all supported operating temperature values. If not enabled, the SRT bit must be programmed to indicate TOPER during subsequent Self-Refresh operation0 = Manual SR Reference (SRT)1 = ASR enable (optional)</td></tr><tr><td>SRT</td><td>MR2 (A7)</td><td>Self-Refresh Temperature (SRT) RangeIf ASR = 0, the SRT bit must be programmed to indicate TOPER during subsequent Self-Refresh operationIf ASR = 1, SRT bit must be set to 0b0 = Normal operating temperature range1 = Extended (optional) operating temperature range</td></tr></table>

# 4.9.0.1 Auto Self-Refresh mode - ASR Mode (optional)

DDR3 SDRAM provides an Auto Self-Refresh mode (ASR) for application ease. ASR mode is enabled by setting MR2 bit ${ \mathsf { A } } 6 = { \mathsf { l } } _ { \mathsf { b } }$ and MR2 bit $\mathrm { A } 7 = 0 _ { \mathrm { b } }$ . The DRAM will manage Self-Refresh entry in either the Normal or Extended (optional) Temperature Ranges. In this mode, the DRAM will also manage Self-Refresh power consumption when the DRAM operating temperature changes, lower at low temperatures and higher at high temperatures. 

If the ASR option is not supported by the DRAM, MR2 bit A6 must be set to $0 _ { \mathrm { b } }$ . 

If the ASR mode is not enabled (MR2 bit. ${ \mathrm { A } } 6 = 0 _ { \mathrm { b } }$ ), the SRT bit (MR2 A7) must be manually programmed with the operating temperature range required during Self-Refresh operation. 

Support of the ASR option does not automatically imply support of the Extended Temperature Range. 

Please refer to the supplier data sheet and/or the DIMM SPD for Extended Temperature Range and Auto Self-Refresh option availability. 

# 4.9.1 Self-Refresh Temperature Range - SRT

SRT applies to devices supporting Extended Temperature Range only. If $\mathrm { A S R } = 0 _ { \mathrm { b } }$ , the Self-Refresh Temperature (SRT) Range bit must be programmed to guarantee proper self-refresh operation. If $\mathrm { S R T } = 0 _ { \mathrm { b } }$ , then the DRAM will set an appropriate refresh rate for Self-Refresh operation in the Normal Temperature Range. If $\mathrm { S R T } = 1 _ { \mathrm { b } }$ then the DRAM will set an appropriate, potentially different, refresh rate to allow Self-Refresh operation in either the Normal or Extended Temperature Ranges. The value of the SRT bit can effect self-refresh power consumption, please refer to the IDD table for details. 

For parts that do not support the Extended Temperature Range, MR2 bit A7 must be set to $0 _ { \mathrm { b } }$ and the DRAM should not be operated outside the Normal Temperature Range. 

# 4.9 Extended Temperature Usage (Cont’d)

# 4.9.1 Self-Refresh Temperature Range - SRT (Cont’d)

Please refer to the supplier data sheet and/or the DIMM SPD for Extended Temperature Range availability. 


Table 11 — Self-Refresh mode summary


<table><tr><td>MR2 A[6]</td><td>MR2 A[7]</td><td>Self-Refresh operation</td><td>Allowed Operating Temperature Range for Self-Refresh Mode</td></tr><tr><td>0</td><td>0</td><td>Self-refresh rate appropriate for the Normal Temperature Range</td><td>Normal (0 - 85 °C)</td></tr><tr><td>0</td><td>1</td><td>Self-refresh rate appropriate for either the Normal or Extended Temperature Ranges. The DRAM must support Extended Temperature Range. The value of the SRT bit can effect self-refresh power consumption, please refer to the IDD table for details.</td><td>Normal and Extended (0 - 95 °C)</td></tr><tr><td>1</td><td>0</td><td>ASR enabled (for devices supporting ASR and Normal Temperature Range). Self-Refresh power consumption is temperature dependent</td><td>Normal (0 - 85 °C)</td></tr><tr><td>1</td><td>0</td><td>ASR enabled (for devices supporting ASR and Extended Temperature Range). Self-Refresh power consumption is temperature dependent</td><td>Normal and Extended (0 - 95 °C)</td></tr><tr><td>1</td><td>1</td><td>Illegal</td><td></td></tr></table>

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.10 Multi Purpose Register

The Multi Purpose Register (MPR) function is used to Read out a predefined system timing calibration bit sequence. The basic concept of the MPR is shown in Figure 20. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/4bef917eaddaf998a9df16715d50398db105ad6dba3172a973723ba957d6b887.jpg)



Figure 20 — MPR Block Diagram


To enable the MPR, a MODE Register Set (MRS) command must be issued to MR3 Register with bit ${ \bf A } 2 =$ 1, as shown in Table 12. Prior to issuing the MRS command, all banks must be in the idle state (all banks precharged and tRP met). Once the MPR is enabled, any subsequent RD or RDA commands will be redirected to the Multi Purpose Register. The resulting operation, when a RD or RDA command is issued, is defined by MR3 bits A[1:0] when the MPR is enabled as shown in Table 13. When the MPR is enabled, only RD or RDA commands are allowed until a subsequent MRS command is issued with the MPR disabled (MR3 bit ${ \bf A } 2 = 0$ ). Note that in MPR mode RDA has the same functionality as a READ command which means the auto precharge part of RDA is ignored. Power-Down mode, Self-Refresh, and any other non-RD/RDA command is not allowed during MPR enable mode. The RESET function is supported during MPR enable mode. 


Table 12 — MPR MR3 Register Definition


<table><tr><td>MR3 A[2]</td><td>MR3 A[1:0]</td><td>Function</td></tr><tr><td>MPR</td><td>MPR-Loc</td><td></td></tr><tr><td>0b</td><td>don’t care
(0b or 1b)</td><td>Normal operation, no MPR transaction.
All subsequent Reads will come from DRAM array.
All subsequent Write will go to DRAM array.</td></tr><tr><td>1b</td><td>See Table 13</td><td>Enable MPR mode, subsequent RD/RDA commands defined by MR3 A[1:0].</td></tr></table>

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.10 Multi Purpose Register (Cont’d)

# 4.10.1 MPR Functional Description

• One bit wide logical interface via all DQ pins during READ operation. 

• Register Read on x4: 

• DQ[0] drives information from MPR. 

• DQ[3:1] either drive the same information as DQ[0], or they drive 0b. 

• Register Read on x8: 

• DQ[0] drives information from MPR. 

• DQ[7:1] either drive the same information as DQ[0], or they drive 0b. 

• Register Read on x16: 

• DQL[0] and DQU[0] drive information from MPR. 

• DQL[7:1] and DQU[7:1] either drive the same information as DQL[0], or they drive 0b. 

• Addressing during for Multi Purpose Register reads for all MPR agents: 

• BA[2:0]: don’t care 

• A[1:0]: A[1:0] must be equal to ${ } ^ { \circ } 0 0 ^ { \circ } \mathrm { b }$ . Data read burst order in nibble is fixed 

• A[2]: For BL=8, A[2] must be equal to 0b, burst order is fixed to [0,1,2,3,4,5,6,7], *) For Burst Chop 4 cases, the burst order is switched on nibble base $\mathrm { A } [ 2 ] { = } 0 \mathrm { b }$ , Burst order: 0,1,2,3 *) $\mathrm { A } [ 2 ] { = } 1 6$ , Burst order: 4,5,6,7 *) 

• A[9:3]: don’t care 

• A10/AP: don’t care 

• A12/BC: Selects burst chop mode on-the-fly, if enabled within MR0. 

• A11, A13,... (if available): don’t care 

• Regular interface functionality during register reads: 

• Support two Burst Ordering which are switched with A2 and A[1:0]=00b. 

• Support of read burst chop (MRS and on-the-fly via A12/BC) 

• All other address bits (remaining column address bits including A10, all bank address bits) will be ignored by the DDR3 SDRAM. 

• Regular read latencies and AC timings apply. 

• DLL must be locked prior to MPR Reads. 

NOTE: *) Burst order bit 0 is assigned to LSB and burst order bit 7 is assigned to MSB of the selected MPR agent. 

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.10 Multi Purpose Register (Cont’d)

# 4.10.2 MPR Register Address Definition

Table 13 provides an overview of the available data locations, how they are addressed by MR3 A[1:0] during a MRS to MR3, and how their individual bits are mapped into the burst order bits during a Multi Purpose Register Read. 


Table 13 — MPR MR3 Register Definition


<table><tr><td>MR3 A[2]</td><td>MR3 A[1:0]</td><td>Function</td><td>Burst Length</td><td>Read Address A[2:0]</td><td>Burst Order and Data Pattern</td></tr><tr><td rowspan="3">1b</td><td rowspan="3">00b</td><td rowspan="3">Read Predefined Pattern for System Calibration</td><td>BL8</td><td>000b</td><td>Burst order 0,1,2,3,4,5,6,7
Pre-defined Data Pattern [0,1,0,1,0,1,0,1]</td></tr><tr><td>BC4</td><td>000b</td><td>Burst order 0,1,2,3
Pre-defined Data Pattern [0,1,0,1]</td></tr><tr><td>BC4</td><td>100b</td><td>Burst order 4,5,6,7
Pre-defined Data Pattern [0,1,0,1]</td></tr><tr><td rowspan="3">1b</td><td rowspan="3">01b</td><td rowspan="3">RFU</td><td>BL8</td><td>000b</td><td>Burst order 0,1,2,3,4,5,6,7</td></tr><tr><td>BC4</td><td>000b</td><td>Burst order 0,1,2,3</td></tr><tr><td>BC4</td><td>100b</td><td>Burst order 4,5,6,7</td></tr><tr><td rowspan="3">1b</td><td rowspan="3">10b</td><td rowspan="3">RFU</td><td>BL8</td><td>000b</td><td>Burst order 0,1,2,3,4,5,6,7</td></tr><tr><td>BC4</td><td>000b</td><td>Burst order 0,1,2,3</td></tr><tr><td>BC4</td><td>100b</td><td>Burst order 4,5,6,7</td></tr><tr><td rowspan="3">1b</td><td rowspan="3">11b</td><td rowspan="3">RFU</td><td>BL8</td><td>000b</td><td>Burst order 0,1,2,3,4,5,6,7</td></tr><tr><td>BC4</td><td>000b</td><td>Burst order 0,1,2,3</td></tr><tr><td>BC4</td><td>100b</td><td>Burst order 4,5,6,7</td></tr><tr><td colspan="6">NOTE: Burst order bit 0 is assigned to LSB and the burst order bit 7 is assigned to MSB of the selected MPR agent.</td></tr></table>

# 4.10.3 Relevant Timing Parameters

The following AC timing parameters are important for operating the Multi Purpose Register: tRP, tMRD, tMOD, and tMPRR. For more details refer to “Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133” on page 155. 

# 4.10.4 Protocol Example

Protocol Example (This is one example): 

Read out predetermined read-calibration pattern. 

Description: Multiple reads from Multi Purpose Register, in order to do system level read timing calibration based on predetermined and standardized pattern. 

Protocol Steps: 

• Precharge All. 

• Wait until tRP is satisfied. 

• MRS MR3, Opcode $^ { \circ } \mathrm { A } 2 = 1 \mathrm { b } ^ { \circ }$ and $^ { * } \mathrm { A } [ 1 ; 0 ] = 0 0 \mathrm { b } ^ { \th }$ 

• Redirect all subsequent reads into the Multi Purpose Register, and load Pre-defined pattern into MPR. 

• Wait until tMRD and tMOD are satisfied (Multi Purpose Register is then ready to be read). During the period MR3 $\mathbf { A } 2 = 1$ , no data write operation is allowed. 

• Read: 

• $\mathrm { A } [ 1 { : } 0 ] = \mathrm { \Omega ^ { \circ } } 0 0 ^ { \circ } \mathrm { b }$ (Data burst order is fixed starting at nibble, always 00b here) 

• $\mathrm { A } [ 2 ] = { } ^ { \circ } 0 ^ { \circ } \mathrm { b }$ (For $\mathrm { B L } { = } 8$ , burst order is fixed as 0,1,2,3,4,5,6,7) 

• $_ { \mathrm { A } 1 2 / \mathrm { B C } } = 1$ (use regular burst length of 8) 

• All other address pins (including BA[2:0] and A10/AP): don’t care 

• After $\mathrm { R L } = \mathrm { A L } + \mathrm { C L }$ , DRAM bursts out the predefined Read Calibration Pattern. 

• Memory controller repeats these calibration reads until read data capture at memory controller is optimized. 

• After end of last MPR read burst wait until tMPRR is satisfied. 

• MRS MR3 Opcode $^ { * } \mathrm { A } 2 _ { } = 0 \mathrm { b } ^ { \ast }$ and ${ } ^ { * } \mathrm { A } [ 1 { : } 0 ] =$ valid data but value are don ’t care“ 

• All sub sequent read and write acces ses will be regular reads and writes from/to the DRAM array. 

• Wait until tMRD and tMOD are satisfied. 

• Continue with “regular” DRAM commands, like activate a memory bank for regular read or write access, . . . 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a849f19c9e62552238470916f5c0100ee5851aca2ad3a3e70e47e26fb65e9b69.jpg)



4.10 Multi Purpose Register (Cont’d) 4.10.4 Protocol Example Cont’d)



Figure 2 1 — MPR Readout of predefined pattern, BL8 fixed burst order, single readout


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/6b6bc026325c59a2407d4d39f2686c94d064a048cd88605cfa4a937192ca04fc.jpg)



Multi Purpose Register (C 4 Protocol Example Co



EC Standard No. 7 Page 5



Figure 22 — MPR Readout of predefined pattern, BL8 fixed burst order, back-to-back readout


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/2a95991cc1a37a3038591dfa851c51608913f8cc0b216bdd5dcfd36c7316703e.jpg)



Multi Purpose Register (C 4 Protocol Example Co



Figure 23 — MPR Readout predefined pattern, BC4, lower nibble then upper nibble


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/3e14297026af01e34e9dac43cf241fa25f3034c45ac3b8677c5f538c09ad35e1.jpg)



Multi Purpose Register (C 4 Protocol Example Co



EC Standard No. 7 Page 5



Figure 24 — MPR Readout of predefined pattern, BC4, upper nibble then lower nibble


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.11 ACTIVE Command

The ACTIVE command is used to open (or activate) a row in a particular bank for a subsequent access. The value on the BA0-BA2 inputs selects the bank, and the address provided on inputs A0-A15 selects the row. This row remains active (or open) for accesses until a precharge command is issued to that bank. A PRECHARGE command must be issued before opening a different row in the same bank. 

# 4.12 PRECHARGE Command

The PRECHARGE command is used to deactivate the open row in a particular bank or the open row in all banks. The bank(s) will be available for a subsequent row activation a specified time (tRP) after the PRE-CHARGE command is issued, except in the case of concurrent auto precharge, where a READ or WRITE command to a different bank is allowed as long as it does not interrupt the data transfer in the current bank and does not violate any other timing parameters. Once a bank has been precharged, it is in the idle state and must be activated prior to any READ or WRITE commands being issued to that bank. A PRE-CHARGE command is allowed if there is no open row in that bank (idle state) or if the previously open row is already in the process of precharging. However, the precharge period will be determined by the last PRECHARGE command issued to the bank. 

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.13 READ Operation

# 4.13.1 READ Burst Operation

During a READ or WRITE command, DDR3 will support BC4 and BL8 on the fly using address A12 during the READ or WRITE (AUTO PRECHARGE can be enabled or disabled). 

$$
A 1 2 = 0, B C 4 (B C 4 = b u r s t c h o p, t C C D = 4)
$$

$$
\mathrm {A} 1 2 = 1, \mathrm {B L} 8
$$

A12 is used only for burst length control, not as a column address. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/4fcc9c9810488b4f64afee5d61f83c8bbd2c013084e26620c29608f5f2908199.jpg)



NOTES: 1. BL8, $\mathsf { R L } = 5$ , ${ \mathsf { A L } } = 0 _ { i }$ $\mathtt { C L } = 5$ .



2. DOUT $n =$ data-out from column n.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BL8 setting activated by either MR0[A1: $0 = 0 0 ]$ or MR0[A1 $\left[ 0 = 0 1 \right]$ ] and $\mathsf { A } 1 2 = 1$ during READ command at T0.


TRANSITIONING DATA DON’T CARE 

Figure 25 — READ Burst Operation RL = 5 $\mathbf { A L } = \mathbf { 0 }$ , CL = 5, BL8) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/0213953ad2227f6f3567e5aef8071646f8ed362b074e5e258618ddf112932ef0.jpg)



NOTES: 1. BL8, $\mathbb { R L } = 9$ , $\mathsf { A L } = ( \mathsf { C L } - 1 )$ , $\mathtt { C L } = 5$ .



2. DOUT $n =$ data-out from column n.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BL8 setting activated by either MR0[A1: $0 = 0 0 ]$ or MR0[A1: $0 = 0 1 ]$ and $A 1 2 = 1$ during READ command at T0.


TRANSITIONING DATA DON’T CARE 


Figure 26 — READ Burst Operation $\mathbf { R L } = \mathbf { 9 }$ $\mathbf { A L } = 4$ , $\mathbf { C L } = 5 .$ , BL8)


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.13 READ Operation (Cont’d)

# 4.13.2 READ Timing Definitions

Read timing is shown in Figure 27 and is applied when the DLL is enabled and locked. 

Rising data strobe edge parameters: 

• tDQSCK min/max describes the allowed range for a rising data strobe edge relative to CK, CK#. 

• tDQSCK is the actual position of a rising strobe edge relative to CK, CK#. 

• tQSH describes the DQS, DQS# differential output high time. 

• tDQSQ describes the latest valid transition of the associated DQ pins. 

• tQH describes the earliest invalid transition of the associated DQ pins. 

Falling data strobe edge parameters: 

• tQSL describes the DQS, DQS# differential output low time. 

• tDQSQ describes the latest valid transition of the associated DQ pins. 

• tQH describes the earliest invalid transition of the associated DQ pins. 

tDQSQ; both rising/falling edges of DQS, no tAC defined. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/68e769234f573acadcc009a7b74e26a988f81e69c257b824a600c1bb9b556f67.jpg)



Figure 27 — READ Timing Definition


# 4.13 READ Operation (Cont’d)

# 4.13.2 READ Timing Definitions (Cont’d)

# 4.13.2.1 READ Timing; Clock to Data Strobe relationship

Clock to Data Strobe relationship is shown in Figure 28 and is applied when the DLL is enabled and locked. 

Rising data strobe edge parameters: 

• tDQSCK min/max describes the allowed range for a rising data strobe edge relative to CK, CK#. 

• tDQSCK is the actual position of a rising strobe edge relative to CK, CK#. 

• tQSH describes the data strobe high pulse width. 

Falling data strobe edge parameters: 

• tQSL describes the data strobe low pulse width. 

tLZ(DQS), tHZ(DQS) for preamble/postam ble (see 4.13.2.3 and Figure 30) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/0520d4b1767b2ecd0f9f07e2a4cca2430ee198905380b5621265a178ab1c25ea.jpg)



NOTES: 1. Within a burst, rising strobe edge is not necessarily fixed to be always at tDQSCK(min) or tDQSCK(max). Instead, rising strobe edge can vary between tDQSCK(min) and tDQSCK(max).



2. Notwithstanding note 1, a rising strobe edge with tDQSCK(max) at T(n) can not be immediately followed by a rising strobe edge with tDQSCK(min) at T(n+1). This is because other timing relationships (tQSH, tQSL) exist:



if tDQSCK(n+1) < 0:



tDQSCK(n) < 1.0 tCK - (tQSHmin $^ +$ tQSLmin) - | tDQSCK(n+1) |



3. The DQS, DQS# differential output high time is defined by tQSH and the DQS, DQS# differential output low time is defined by tQSL.



4. Likewise, tLZ(DQS)min and tHZ(DQS)min are not tied to tDQSCKmin (early strobe case) and tLZ(DQS)max and tHZ(DQS)max are not tied to tDQSCKmax (late strobe case).



5. The minimum pulse width of read preamble is defined by tRPRE(min).



6. The maximum read postamble is bound by tDQSCK(min) plus tQSH(min) on the left side and tHZDSQ(max) on the right side.



7. The minimum pulse width of read postamble is defined by tRPST(min).



8. The maximum read preamble is bound by tLZDQS(min) on the left side and tDQSCK(max) on the right side.



Figure 28 — Clock to Data Strobe Relationship


# 4.13 READ Operation (Cont’d)

# 4.13.2 READ Timing Definitions (Cont’d)

# 4.13.2.2 READ Timing; Data Strobe to Data relationship

The Data Strobe to Data relationship is shown in Figure 29 and is applied when the DLL is enabled and locked. 

Rising data strobe edge parameters: 

• tDQSQ describes the latest valid transition of the associated DQ pins. 

• tQH describes the earliest invalid transition of the associated DQ pins. 

Falling data strobe edge parameters: 

• tDQSQ describes the latest valid transition of the associated DQ pins. 

• tQH describes the earliest invalid transition of the associated DQ pins. 

tDQSQ; both rising/falling edges of DQS, no tAC defined 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/1c2cb03cfc0fac16e378c372ce21ed74050aab444f44a29d1759be47d2575a7f.jpg)



NOTES: 1. $B L = 8 ,$ $\mathsf { R L } = 5$ $( { \mathsf { A L } } = 0$ , $\mathbb { C } \mathbb { L } = 5 )$



2. DOUT $n =$ data-out from column n.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BL8 setting activated by either MR0[A1:0 = 00] or MR0[A $1 : 0 = 0 1 1$ ] and $\mathsf { A } 1 2 = 1$ during READ command at T0.



5. Output timings are referenced to VDDQ/2, and DLL on for locking.



6. tDQSQ defines the skew between DQS,DQS# to Data and does not define DQS,DQS# to Clock.



7. Early Data transitions may not always happen at the same DQ. Data transitions of a DQ can vary (either early or late) within a burst.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/d6dc115d670d0683738f16fd7748a91ed6651b4fc973ee1aeb45ca3914a31284.jpg)


TRANSITIONING DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/369960d4ca80840b4a567bbdce94a42401e85c129e00fd6b9608a53c07194b54.jpg)


DON’T CARE 


Figure 29 — Data Strobe to Data Relationship


# 4.13.2.3 tLZ(DQS), tLZ(DQ), tHZ(DQS), tHZ(DQ) Calculation

tHZ and tLZ transitions occur in the same time window as valid data transitions. These parameters are referenced to a specific voltage level that specifies when the device output is no longer driving tHZ(DQS) and tHZ(DQ), or begins driving tLZ(DQS), tLZ(DQ). Figure 30 shows a method to calculate the point when the device is no longer driving tHZ(DQS) and tHZ(DQ), or begins driving tLZ(DQS), tLZ(DQ), by measuring the signal at two different voltages. The actual voltage measurement points are not critical as long as the calculation is consistent. The parameters tLZ(DQS), tLZ(DQ), tHZ(DQS), and tHZ(DQ) are defined as singled ended. 

# 4.13 READ Operation (Cont’d)

# 4.13.2 READ Timing Definitions (Cont’d)


tLZ(DQS): CK - CK# rising crossing at RL - 1 tLZ(DQ): CK - CK# rising crossing at RL


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/7d85fa875933e721ccd8a03968ef07533d08456d4d231fa580e25220fd80654f.jpg)



tHZ(DQS), tHZ(DQ) with BL8: CK - CK# rising crossing at RL + 4 nCK tHZ(DQS), tHZ(DQ) with BC4: CK - CK# rising crossing at RL $^ { + 2 }$ nCK


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/d56fb0b5790b02100d96373e0a37d3c368e8d26273640864fb12e6f8d4b0797d.jpg)



Figure 30 — tLZ and tHZ method for calculating transitions and endpoints


# 4.13 READ Operation (Cont’d)

# 4.13.2 READ Timing Definitions (Cont’d)

# 4.13.2.4 tRPRE Calculation

The method for calculating differential pulse widths for tRPRE is shown in Figure 31. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/45962e79a87f7a35a76ef306133828779d8a19e5c29be4d92ac121b37984735e.jpg)



Figure 31 — Method for calculating tRPRE transitions and endpoints


# 4.13.2.5 tRPST Calculation

The method for calculating differential pulse widths for tRPST is shown in Figure 32. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/7e33ebd76083faf86c964556bcc746d85a6623aebccdd6adc42672853a772b5a.jpg)



Figure 32 — Method for calculating tRPST transitions and endpoints


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a82d988951dd55190e5ee2624f0a7ddc264a36ab5fdd5ef50084fb9c78c54035.jpg)



N OTE : 1 B L8 $\mathsf { R L } = 5$ (C L = 5 $\mathbb { A } \mathbb { L } = 0 )$



2 . D O UT n (or b) = d ata -o ut fro m co l u m n n (or column b) .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B L8 sett i n g a ct ivated by e it h e r M R0 [A 1 : $0 = 0 0 ]$ o r M R0 [A 1 : 0 = 0 1 ] a n d $A 1 2 = 1$ d u ri n g R EAD co m m a n d s at T0 a n d T4.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e669cc4bcca52c020004811f4499d6ee775a3ecf8f3bdce9fe5d2ade63a427d0.jpg)


TRANSITI O N I N G DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a441e40baef1a40fd122c61b3679a22a36f78eb2b0b28212d2ab52844d0eb740.jpg)


DO N ’T CARE 


Figure 33 — READ (BL8) to READ (BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e05fcfac34db3716fd208bcbe6cefeb4d80df5fd3750ca596c74d00960ecdfe9.jpg)



N OTE : 1 B C4, $\mathsf { R L } = 5$ $\mathtt { ( C L = 5 }$ , $\mathbb { A } \mathbb { L } = 0 )$



2 . D O UT n (or b) $=$ d ata -o ut fro m co l u m n n (or column b) .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B C4 sett i n g a ct ivated by e it h e r M R0 [A 1 $\left[ 0 = 1 0 \right]$ o r M R0 [A 1 $0 = 0 1 ]$ ] a n d $\mathsf { A } 1 2 = 0$ d u ri n g R EAD co m m a n d s at T0 a n d T4.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/82e962e4b1bffda67d9671cc29c42d229ca5b7c9e7e24790a24aeb758fe02dac.jpg)


TRANSITI O N I N G DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/983920117e21c19278a5b20c006a581daf2456c553a74632d7f9488aa302fde5.jpg)


DO N ’T CARE 


Figure 34 — READ (BC4) to READ (BC4)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/76cc31e1cb26d5c20ba11d4103e4204485467f7f39bee8dbd2ee3db187992bf6.jpg)



N OT E : 1 . B L8, $\mathsf { R L } = 5$ $\mathrm { C L } = 5 ,$ $\mathsf { A L } = 0 )$ , ${ \mathsf { W L } } = 5$ ${ \mathrm { C W L } } = 5 $ ${ \mathsf { A L } } = 0 )$



2 . D O UT $n =$ d ata -o ut fro m co l u m n, D I N $b \ =$ d ata - i n f ro m co l u m n b .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 B L8 sett i n g a ct ivated by e it h e r M R0 [A 1 : 0 = 00] o r M R0 [A 1 $\mathbf { \delta } \cdot \mathbf { 0 } = 0 1 ]$ a n d $A 1 2 = 1$ d u ri n g R EAD co m m a n d at T0 a n d WR ITE co m m a n d at T6 .



4.13 READ Operation (Cont’d) 4.13.2 READ Timing Definitions (Cont’d)



Figure 35 — READ (BL8) to WRITE (BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/5000ef480ce2dbe566a43619ed2bd7f152779e17dc81b90fb9aa892cd90b66a2.jpg)



N OTE : 1 . B C4, $\mathsf { R L } = 5$ $\mathtt { C L } = 5 ,$ $\mathbb { A } \mathbb { L } = 0 )$ ) , W L = 5 ${ \mathsf { C W L } } = 5 ,$ $\mathbb { A } \mathbb { L } = 0 _ { i }$



2 . D O UT $n =$ d ata -o ut fro m co l u m n, D I N b = d ata - i n fro m co l u m n b .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4. B C4 sett i n g a ct ivated by M R0 [A 1 $\left[ 0 = 0 1 \right]$ a n d $\mathsf { A } 1 2 = 0$ d u r i n g R EAD co m m a n d at T0 a n d WR ITE co m m a n d at T4.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/30cba95616032f385c53887eb3e25db9943784459b5398e7943b4aeaff036116.jpg)



TRANSITI O N I N G DATA


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/23dc37a949a0a14fa5a16099a01b4886b2ce068ab66c9a3a2817c4b8f76055ce.jpg)



O N ’T CARE



Figure 36 — READ (BC4) to WRITE (BC4) OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/d82773850f18e9a516ee6ac1c8f51cb5288cd13a3eaa200932399f9aa32e77fe.jpg)



N OT E : 1 . R L = 5 $\displaystyle \left( \mathbb { C } \ L \right) = 5 ,$ $\mathbb { A } \mathbb { L } = 0 )$



2 . D O UT n (or b) = d ata -o ut fro m co l u m n n (or column b) .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B L8 sett i n g a ct ivated by M R0 [A 1 $\left[ 0 = 0 1 \right]$ a n d $\mathsf { A } 1 2 = 1$ d u ri n g R EAD co m m a n d at T0 .



B C4 sett i n g a ct ivated by M R0 [A 1 : 0 = 0 1 ] a n d $\mathsf { A } 1 2 = 0$ d u r i n g R EAD co m m a n d at T4.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a7b6114500f75a6db67f7ec4953fa310a56740edb76dec522ed3edb259aab5f7.jpg)


TRANSITI O N I N G DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/090be7f907877ab94e47951a2d9a943acc8597bdb8296aeca9ee0323ce12b2fa.jpg)


DO N ’T CARE 


Figure 37 — READ (BL8) to READ (BC4) OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/f6153c2f7f48d1cef829263b50fefddb91f2ddef461caa48ee1057fe014df8f0.jpg)



N OTE : 1 $\mathsf { R L } = 5$ $\mathtt { ( C L = 5 , }$ $\mathbb { A } \mathbb { L } = 0 )$



2 . D O UT n (or b) = d ata -o ut fro m co l u m n n (or column b) .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B C4 sett i n g a ct ivated by $\mathsf { M R O } [ \mathsf { A } 1 ; 0 = 0 1 ]$ a n d $\mathsf { A } 1 2 = 0$ d u r i n g R EAD co m m a n d at T0 .



B L8 sett i n g a ct ivated by $\mathsf { M R O } [ \mathsf { A } 1 ; 0 = 0 1 ]$ a n d $\mathsf { A } 1 2 = 1$ d u ri n g R EAD co m m a n d at T4.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/894b7872d8d601fbe7e187be2545df469404183edd6923d1e9ba4d9ec995c3d5.jpg)


TRANSITI O N I N G DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/ab72968b7fe7e27b71064350d8558c6fafa71652f5688f96086ba977a871ea1b.jpg)


DO N ’T CARE 


Figure 38 — READ (BC4) to READ (BL8) OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/3c047e819891fd7343a710cfdf22a3e262e478893f335d3d56f95099ff7aba72.jpg)



N OTE : 1 . $\mathsf { R L } = 5$ ${ \mathsf { C L } } = 5 ,$ ${ \mathsf { A L } } = 0 )$ ) ${ \mathsf { W L } } = 5$ (CW L - 1 ${ \mathsf { A L } } = 0 _ { \cdot }$ )



2 . D O UT $n =$ d ata -o ut fro m co l u m n, D I N b = d ata - i n fro m co l u m n b .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4. B C4 sett i n g a ct ivated by M R0 [A 1 $0 = 0 1 ]$ a n d $\mathsf { A } 1 2 = 0$ d u r i n g R EAD co m m a n d at T0 .



B L8 sett i n g a ct ivated by $\mathsf { M R O } [ \mathsf { A } 1 ; 0 = 0 1 ]$ a n d $\mathsf { A } 1 2 = 1$ d u r i n g WR ITE co m m a n d at T4.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/ad92475ab9c38405d5d83819e7a7700c22ff2c8d8cc3b5b603e65107bafd4014.jpg)


TRANSITI O N I N G DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/9eeedefd8f3ee54df8c1f855364ad2a4ff2b07040bfeb75769cd498134e48199.jpg)


DO N ’T CARE 


Figure 39 — READ (BC4) to WRITE (BL8) OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/0aa888b6f4239842b629ee0d2fdb53fedc5b56b887860d5ad2456469dd451939.jpg)



N OT E : 1 . $\mathsf { R L } = 5$ $\mathrm { C L } = 5 ,$ $\mathbb { A } \mathbb { L } = 0 )$ , ${ \mathsf { W L } } = 5$ ${ \mathrm { C W L } } = 5 ,$ A L = 0)



2 . D O UT $n =$ d ata -o ut f ro m co l u m n, D I N b = d ata - i n f ro m co l u m n b .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 B L8 sett i n g a ct ivated by M R0 [A 1 $\left[ 0 = 0 1 \right]$ a n d $A 1 2 = 1$ d u ri n g R EAD co m m a n d at T0 .



B C4 sett i n g a ct ivated by M R0 [A 1 : 0 = 0 1 ] a n d $\mathsf { A } 1 2 = 0$ d u r i n g WR ITE co m m a n d at T6 .


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/7efb645b3874b5e4540163e78377a84ef6e2b2f967e96a464462572d80c525a6.jpg)


TRANSITI O N I N G DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/1f1a81447aa9b58d406050d1f79cc35938ba3a62e3d111c805456ffaff2f0570.jpg)


DO N ’T CARE 


Figure 40 — READ (BL8) to WRITE (BC4) OTF


# 4. 1 3.3 B u rst Read Operation fol lowed by a Precharge

The minimum external Read command to Precharge command spacing to the same bank is equal to AL + tRTP with tRTP being the Internal Read Command to Precharge Command Delay. Note that the minimum ACT to PRE timing, tRAS , must be satisfied as well. The minimum value for the Internal Read Command to Precharge Command Delay is given by tRTP.MIN $=$ max(4 × nCK, 7 . 5 ns) . A new bank active command may be issued to the same bank if the following two conditions are satisfied simultaneously: 

1 . The minimum RAS precharge time (tRP.MIN) has been satisfied from the clock at which the precharge begins . 

2 . The minimum RAS cycle time (tRC .MIN) from the previous bank activation has been satisfied. 

Examples of Read commands followed by Precharge are show in Figure 4 1 and Figure 42 . 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/c24d0b93827c7fb97df1ecf7d3d09064a5f927744041fd6d95987610ff259f38.jpg)



N OTE : 1 R L = 5 (C L = 5 AL = 0)



2 . DOUT n = d ata -o ut fro m co l u m n n .



3 N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m a be va l i d at t h ese t i m es



4 . Th e exa m p l e a ss u m es t RAS . M I N i s sat i sf i ed at P rec h a rg e co m m a n d t i m e (T5) a n d t h at t RC . M I N i s sat i sf i ed at t h e n ext Act i ve co m m a n d t i m e (T 1 0) .


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/bf2d0283ac2af0a4f89ce6bf40fdb454d4cdc3c375f62cf2e825813b0678d29a.jpg)


Tra n s it i o n i n g Data 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/8f624a119e25e9349243ec60931846bf4344b274d5ff4fa37e7be4ea037bb1ef.jpg)


Do n ’t Ca re 


Figure 41 — READ to PRECHARGE, $\mathbf { R L } = 5 .$ , $\mathbf { A } \mathbf { L } = \mathbf { 0 }$ , $\mathbf { C L } = 5$ , tRTP = 4, tRP = 5


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/05aa037088ddb13b07db7dfbd012f41b63d22768db39401555de38d1765daa75.jpg)



N OTE : 1 R L = 8 (C L = 5 AL = C L - 2)



2 . D O UT n = d ata -o ut f ro m co l u m n n .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . Th e exa m p l e a ss u m es t RAS . M I N i s sat i sf i ed at P rec h a rg e co m m a n d t i m e (T 1 0) a n d t h at t RC . M I N i s sat i sf i ed at t h e n ext Act i ve co m m a n d t i m e (T 1 5) .


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e6befa468e7a7c31bacddaf81745a9bf750507fd71cc21c7c64c744e640e6aca.jpg)


Tra n s it i o n i n g Data 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/6fb9ff1010faf285374f66d4bb4b22c74bc392924deb23f7b4b85f3dbcfe2445.jpg)


Do n ’t Ca re 


Figure 42 — READ to PRECHARGE, $\mathbf { R L } = \mathbf { 8 } .$ , $\mathbf { A L } = \mathbf { C L - 2 } , \mathbf { C L } = 5 , \mathbf { t R T P } = 6 , \mathbf { t R P } = 5$ ${ \bf A } { \bf L } = { \bf C } { \bf L } { - } 2$


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.14 WRITE Operation

# 4.14.1 DDR3 Burst Operation

During a READ or WRITE command, DDR3 will support BC4 and BL8 on the fly using address A12 during the READ or WRITE (AUTO PRECHARGE can be enabled or disabled). 

$$
\begin{array}{l} A 1 2 = 0, B C 4 (B C 4 = b u r s t c h o p, t C C D = 4) \\ \mathrm {A} 1 2 = 1, \mathrm {B L} 8 \\ \end{array}
$$

A12 is used only for burst length control, not as a column address. 

# 4.14.2 WRITE Timing Violations

# 4.14.2.1 Motivation

Generally, if timing parameters are violated, a complete reset/initialization procedure has to be initiated to make sure that the DRAM works properly. However, it is desirable, for certain minor violations, that the DRAM is guaranteed not to “hang up,” and that errors are limited to that particular operation. 

For the following, it will be assumed that there are no timing violations with regards to the Write command itself (including ODT, etc.) and that it does satisfy all timing requirements not mentioned below. 

# 4.14.2.2 Data Setup and Hold Violations

Should the data to strobe timing requirements (tDS, tDH) be violated, for any of the strobe edges associated with a write burst, then wrong data might be written to the memory location addressed with this WRITE command. 

In the example (Figure 43 on page 69), the relevant strobe edges for write burst A are associated with the clock edges: T5, T5.5, T6, T6.5, T7, T7.5, T8, T8.5. 

Subsequent reads from that location might result in unpredictable read data, however the DRAM will work properly otherwise. 

# 4.14.2.3 Strobe to Strobe and Strobe to Clock Violations

Should the strobe timing requirements (tDQSH, tDQSL, tWPRE, tWPST) or the strobe to clock timing requirements (tDSS, tDSH, tDQSS) be violated, for any of the strobe edges associated with a Write burst, then wrong data might be written to the memory location addressed with the offending WRITE command. Subsequent reads from that location might result in unpredictable read data, however the DRAM will work properly otherwise. 

In the example (Figure 51 on page 73) the relevant strobe edges for Write burst n are associated with the clock edges: T4, T4.5, T5, T5.5, T6, T6.5, T7, T7.5, T8, T8.5 and T9. Any timing requirements starting or ending on one of these strobe edges need to be fulfilled for a valid burst. For Write burst $^ b$ the relevant edges are T8, T8.5, T9, T9.5, T10, T10.5, T11, T11.5, T12, T12.5 and T13. Some edges are associated with both bursts. 

# 4.14.2.4 Write Timing Parameters

This drawing is for example only to enumerate the strobe edges that “belong” to a Write burst. No actual timing violations are shown here. For a valid burst all timing parameters for each edge of a burst need to be satisfied (not only for one edge - as shown). 

# 4.14 WRITE Operation (Cont’d)

# 4.14.2 WRITE Timing Violations (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/2874f21c16a28067585dee8ce66fdb23407d175e8c355a1b0ca71250c47d0ec4.jpg)



NOTE: 1. BL8, ${ \sf W L } = 5$ ${ \mathbb { A } } \bot = 0$ , CWL $= 5$ )



2. DIN n $=$ data-in from column n.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BL8 setting activated by either MR0[A1: $0 = 0 0 ]$ or MR0[A1:0 = 01] and $A 1 2 = 1$ during WRITE command at T0.



5. tDQSS must be met at each rising clock edge.


TRANSITIONING DATA DON’T CARE 


Figure 43 — Write Timing Definition and Parameters


# 4.14.3 Write Data Mask

One write data mask (DM) pin for each 8 data bits (DQ) will be supported on DDR3 SDRAMs, consistent with the implementation on DDR2 SDRAMs. It has identical timings on write operations as the data bits as shown in Figure 43, and though used in a unidirectional manner, is internally loaded identically to data bits to ensure matched system timing. DM is not used during read cycles for any bit organizations including x4, x8, and x16, however, DM of x8 bit organization can be used as TDQS during write cycles if enabled by the MR1[A11] setting. See 3.4.3.7 “TDQS, TDQS#” on page 29 for more details on TDQS vs. DM operations. 

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.14 WRITE Operation (Cont’d)

# 4.14.4 tWPRE Calculation

The method for calculating differential pulse widths for tWPRE is shown in Figure 44. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/081600edf2388e0816882e75fddc93978ea2338768cd52b331e2f61146ba30a3.jpg)



Figure 44 — Method for calculating tWPRE transitions and endpoints


# 4.14.5 tWPST Calculation

The method for calculating differential pulse widths for tWPST is shown in Figure 45. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/dd7eb02112b06f1b4941177e3ad95b48218db8853a19cf640275e1526547430d.jpg)



Figure 45 — Method for calculating tWPST transitions and endpoints


# 4.14 WRITE Operation (Cont’d)

# 4.14.5 tWPST Calculation (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b60a9f19ba78e96953a68a67dc00d7ca721453a2cf0e4f733d30e5f540b756ad.jpg)



NOTE: 1. BL8, WL $. = 5 ;$ ${ \mathsf { A L } } = 0 ,$ , CWL = 5.



2. DIN $n =$ data-in from column n.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BL8 setting activated by either MR0[A1 $\left[ 0 = 0 0 \right]$ or MR0[A1 $\left[ 0 = 0 1 \right]$ and $A 1 2 = 1$ during WRITE command at T0.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/db24432d7f91e0ee0f26854ce31ec4c4494b86136e92132e54a818168170969a.jpg)



TRANSITIONING DATA


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/879d2c878fe3e565c2f7b0b187125e6767212056ea19ed330a3835745c087529.jpg)



DON’T CARE



Figure 46 — WRITE Burst Operation WL = 5 ( $\mathbf { A } \mathbf { L } = \mathbf { 0 }$ , CWL = 5, BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/5f008ece7a95d5add9871d9e38485e06388b18a68122fd8dee79b5b634ba6c50.jpg)



NOTE: 1. BL8, ${ \mathsf { W L } } = 9$ ; $\mathsf { A L } = ( \mathsf { C L } - 1 )$ , ${ \mathsf { C L } } = 5 ,$ CWL = 5.



2. DIN $n =$ data-in from column n.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BL8 setting activated by either MR0[A1: $\left[ 0 = 0 0 \right]$ or MR0[A1 $\left[ 0 = 0 1 \right]$ and $\mathsf { A } 1 2 = 1$ during WRITE command at T0.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/74af252d3f984634ae1fc5aa6ec223a48aa31ab311d0947b3382835880d85b24.jpg)



TRANSITIONING DATA


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/d625bbbef689a4de75c4e826e5875bf6b995c6fb988a01d122fd445a8da299db.jpg)



DON’T CARE



Figure 47 — WRITE Burst Operation $\mathbf { W } \mathbf { L } = \mathbf { 9 }$ (AL = CL-1, CWL = 5, BL8)


# 4.14 WRITE Operation (Cont’d)

# 4.14.5 tWPST Calculation (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/f4451f4d30e3539e0b2e9d650471ce901fa607cb8885050cde2688d72af19ba4.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/878f2b55e23e9dfaf58d87eb352f92cb37646241a07670f7e21a24017e189880.jpg)



TRANSITIONING DATA


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/bb8592c63b9b42185cd6083d74970d0cdf0cffde86449b46fe8127c708555b5f.jpg)



DON’T CARE



NOTE: 1. BC4, WL $= 5$ , $\mathsf { R L } = 5$



2. DIN $n =$ data-in from column n; DOUT $b =$ data-out from column b.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BC4 setting activated by MR0[A1:0 = 10] during WRITE command at T0 and READ command at Tn.



5. tWTR controls the write to read delay to the same device and starts with the first rising clock edge after the last write data shown at T7.



Figure 48 — WRITE (BC4) to READ (BC4) Operation


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/18511aef3f8b24943e3d106bd3c70c11fd99f9056dc9b46c34e0189d08401669.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/060f4fe288f4cee8d8f1c9e26ec02590d89211715f3403fd9665879e205969c6.jpg)



TRANSITIONING DATA


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/c88a3beab55519431ca5ad8374875f9968e5ab0dd39cf918f211df57b8a8b015.jpg)



DON’T CARE



NOTE: 1. BC4, WL $= 5$ , $\mathsf { R L } = 5$



2. DIN $n =$ data-in from column n; DOUT $b =$ data-out from column b.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BC4 setting activated by MR0[A1:0 = 10] during WRITE command at T0.



5. The write recovery time (tWR) referenced from the first rising clock edge after the last write data shown at T7. tWR specifies the last burst write cycle until the precharge command can be issued to the same bank .



Figure 49 — WRITE (BC4) to PRECHARGE Operation


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/fb999586a3a099174840847b4ef9fea10837c900a06ed765eb9b9cd420b16460.jpg)



NOTE: 1. BC4 OTF, WL = 5 (CWL = 5, AL = 0)



2. DIN n (or b) = data-in from column n.



3. NOP commands are shown for ease of illustration; other commands may be valid at these times.



4. BC4 OTF setting activated by MR0[A1:0 = 01] and $A 1 2 = 0$ during WRITE command at T0.



5. The write recovery time (tWR) starts at the rising clock edge T9 (4 clocks from T5).


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/1884b362a295cab7fdcab2aff9d4a99e1d6a6855b62fd51f6ad49714a4fe9178.jpg)



Time Break


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/9f39d2dcea8cc917cb0b080caaaa4b011fffd4e4b29791c4f62180ba56f3bf34.jpg)



Don’t Care



Figure 50 — WRITE (BC4) OTF to PRECHARGE Operation


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/27b30010c44c74fd45ccff5ee9a25ed17bd274da52b504b436b998cf61b51a6f.jpg)



N OT E : 1 . B L8 ${ \sf N L } = 5$ ${ \mathsf { C W L } } = 5 ,$ ${ \mathsf { A L } } = 0 )$ )



2 . D I N n (or b) $=$ d ata - i n fro m co l u m n n (or column b) .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B L8 sett i n g a ct ivated by e it h e r $\mathsf { M R } 0 [ \mathsf { A } 1 : 0 = 0 0 ]$ o r M R0 [A 1 : 0 = 0 1 ] a n d $\mathsf { A } 1 2 = 1$ d u r i n g WR ITE co m m a n d at T0 a n d T4.



5 T h e w r i te recove ry t i m e (tWR) a n d w r i te t i m i n g p a ra m ete r (tWT R) a re refe re n ce d f ro m t h e f i rst r i s i n g c l oc k e d g e a fte r t h e l a st w r i te d ata s h ow n at T 1 3 .



Figure 5 1 — WRITE (BL8) to WRITE (BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/3e6561c50eb8294d48ca339eebccf929ebcc39da1578ba78de75423ade37b8d0.jpg)



N OT E : 1 . B C4, W $\mathsf { L } = 5$ ${ \mathsf { C W L } } = 5$ , ${ \mathsf { A L } } = 0 )$



2 . D I N n (or b) $=$ d ata - i n fro m co l u m n n (or column b) .



3 . N O P co m m a n d s a re s h own fo r ease of i l l u strat i o n; oth e r co m m a n d s m ay be va l i d at th ese t i m es .



4 . B C4 sett i n g act ivated by M R0 [A 1 $: 0 = 0 1 ]$ a n d $\mathsf { A } 1 2 = 0$ d u ri n g WR ITE co m m a n d at T0 a n d T4.



5 . T h e w r i te recove ry t i m e (tWR) a n d w r i te t i m i n g p a ra m ete r (tWT R) a re refe re n ce d f ro m t h e f i rst r i s i n g c l oc k e d g e at T 1 3 (4 c l oc ks f ro m T9) .


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/f385febf62c4547841d28a960171ee4125537f43528a99b2124c62a2418017e4.jpg)



TRANSITI O N I N G DATA


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/5477ea3c7f392703006bd73d63704d91fa3d084b7777a896eb99f60d5bbc037b.jpg)



DO N ’T CARE



Figure 52 — WRITE (BC4) to WRITE (BC4) OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/90bde1230df8aceafa3cf2f52a817f4c876bed59724dd1dc398036ae2660796c.jpg)



1 $\mathsf { R L } = 5$ $\left( \mathsf { C L } \right) = 5$ , $\mathbb { A } \mathbb { L } = 0 )$ , ${ \sf W L } = 5$ (CWL = 5, ${ \mathsf { A L } } = 0 )$



2 . D I N $n =$ d ata - i n fro m co l u m n n; D O UT $b \ =$ d ata -o ut fro m co l u m n b .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B L8 sett i n g a ct ivated by e it h e r M R0 [A 1 $: 0 = 0 0 1$ o r $\mathsf { M R O } [ \mathsf { A } 1 ; 0 = 0 1 ]$ a n d $A 1 2 = 1$ d u r i n g WR ITE co m m a n d at T0 .



R EAD co m m a n d at T 1 3 ca n be e it h e r B C4 o r B L8 d e pe n d i n g o n M R0 [A 1 : 0] a n d A 1 2 stat u s at T 1 3 .


Figure 53 — WRITE (BL8) to READ (BC4/BL8) OTF 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/06bccac4333033750236809ef9f12fd9aefe2491d4385f442b96f6d48c4f91b4.jpg)



N OT E : 1 . $\mathsf { \Pi } \mathsf { K } \mathsf { L } = \mathsf { \mathsf { 3 } } \mathsf { \Pi } ( \mathsf { L } \mathsf { L } = \mathsf { 3 } ,$ ${ \mathsf { A L } } = \mathsf { U } ) .$ , W L $= >$ (CW $= 5 .$ , ${ \mathsf { A L } } = { \mathsf { U } } )$



$n =$ d ata - i n f ro m co l u m n n; D O UT $b =$ d ata -o ut f ro m co l u m n b .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B C4 sett i n g a ct ivated by M R0 [A 1 $\left[ 0 = 0 1 \right]$ a n d $\mathsf { A } 1 2 = 0$ d u r i n g WR ITE co m m a n d at T0 .



R EAD co m m a n d at T 1 3 ca n be e it h e r B C4 o r B L8 d e pe n d i n g o n A 1 2 stat u s at T 1 3 .



Figure 54 — WRITE (BC4) to READ (BC4/BL8) OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/8491e1b9c160667ab0729bca2fe697bc180ebb7a66bca1ff894fce01f8c32855.jpg)



2 . D I N $n =$ d ata - i n fro m co l u m n n; D O UT $b =$ d ata -o ut fro m co l u m n b .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B C4 sett i n g a ct i vate d by M R0 [A 1 : 0 = 1 0] .



Figure 55 — WRITE (BC4) to READ (BC4)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/981b74a0e8cf6067a10e0c9529249350f3decd63b6a7f77cb8bf40b67a7e4913.jpg)



N OT E : 1 . WL $= 5$ ${ \mathsf { C W L } } = 5$ , ${ \mathsf { A L } } = 0 .$



2 . D I N n (or b) $=$ d ata - i n fro m co l u m n n (or column b) .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B L8 sett i n g a ct ivated by M R0 [A 1 : 0 = 0 1 ] a n d $\mathsf { A } 1 2 = 1$ d u r i n g WR ITE co m m a n d at T0 .



B C4 sett i n g a ct ivated by M R0 [A $1 : 0 = 0 : 1 1$ a n d $\mathsf { A } 1 2 = 0$ d u r i n g WR ITE co m m a n d at T4.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/57df200dc1a61d15b2f5d539d7d0a94972ea8e0449a6131dc0390eca2bcae9ea.jpg)


TRANSITI O N I N G DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b1cfc187ab3339efa84b9fb26243aeb5492ab76479c0b1f11bda8565e08a8f3f.jpg)


DO N ’T CARE 


Figure 56 — WRITE (BL8) to WRITE (BC4) OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/40737e4f32af8993178a3193db285f3b100e5fbdb064082bc4405e073a2e9923.jpg)



N OT E : 1 . WL = 5 $\mathrm { C W L } = 5$ , ${ \mathsf { A L } } = 0 .$



2 . D I N n (or b) $=$ d ata - i n fro m co l u m n n (or column b) .



3 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es .



4 . B C4 sett i n g a ct ivated by $\mathsf { M R O } [ \mathsf { A } 1 ; 0 = 0 1 ]$ a n d $\mathsf { A } 1 2 = 0$ d u ri n g WR ITE co m m a n d at T0 .



B L8 sett i n g a ct ivated by $\mathsf { M R O } [ \mathsf { A } 1 ; 0 = 0 1 ]$ a n d $\mathsf { A } 1 2 = 1$ d u r i n g WR ITE co m m a n d at T4.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/4ddde2facfbe58ec63eb1c2982d72baa28b45462695d6909feb794e8f7dcbe32.jpg)


TRANSITI O N I N G DATA 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/1355b0fb064a12dca6b51d187331332919fa91fa292f7752a0a7ba6630b60d23.jpg)


O N ’T CARE 


Figure 57 — WRITE (BC4) to WRITE (BL8) OTF


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.15 Refresh Command

The Refresh command (REF) is used during normal operation of the DDR3 SDRAMs. This command is non persistent, so it must be issued each time a refresh is required. The DDR3 SDRAM requires Refresh cycles at an average periodic interval of tREFI. When CS#, RAS# and CAS# are held Low and WE# High at the rising edge of the clock, the chip enters a Refresh cycle. All banks of the SDRAM must be precharged and idle for a minimum of the precharge time tRP(min) before the Refresh Command can be applied. The refresh addressing is generated by the internal refresh controller. This makes the address bits “Don’t Care” during a Refresh command. An internal address counter supplies the addresses during the refresh cycle. No control of the external address bus is required once this cycle has started. When the refresh cycle has completed, all banks of the SDRAM will be in the precharged (idle) state. A delay between the Refresh Command and the next valid command, except NOP or DES, must be greater than or equal to the minimum Refresh cycle time tRFC(min) as shown in Figure 58. Note that the tRFC timing parameter depends on memory density. 

In general, a Refresh command needs to be issued to the DDR3 SDRAM regularly every tREFI interval. To allow for improved efficiency in scheduling and switching between tasks, some flexibility in the absolute refresh interval is provided. A maximum of 8 Refresh commands can be postponed during operation of the DDR3 SDRAM, meaning that at no point in time more than a total of 8 Refresh commands are allowed to be postponed. In case that 8 Refresh commands are postponed in a row, the resulting maximum interval between the surrounding Refresh commands is limited to $9 \times$ tREFI (see Figure 59). A maximum of 8 additional Refresh commands can be issued in advance (“pulled in”), with each one reducing the number of regular Refresh commands required later by one. Note that pulling in more than 8 Refresh commands in advance does not further reduce the number of regular Refresh commands required later, so that the resulting maximum interval between two surrounding Refresh commands is limited to $9 \times$ tREFI (see Figure 60). At any given time, a maximum of 16 REF commands can be issued within $2 \mathrm { ~ x ~ }$ tREFI. Self-Refresh Mode may be entered with a maximum of eight Refresh commands being postponed. After exiting Self-Refresh Mode with one or more Refresh commands postponed, additional Refresh commands may be postponed to the extent that the total number of postponed Refresh commands (before and after the Self-Refresh) will never exceed eight. During Self-Refresh Mode, the number of postponed or pulled-in REF commands does not change. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/abc9a1d19018e76d2744566882da78938c2b7a7f5e047f6384a26d2cbb4f7188.jpg)



NOTES:



1. Only NOP/DES commands allowed after Refresh command registered until tRFC(min) expires.



2. Time interval between two Refresh commands may be extended to a maximum of 9 x tREFI


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/9a42abe56f0ea4a495312a20cf573d81bfb0a70105d719c9038fe86397abdccc.jpg)



TIME BREAK


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/c87af1c9440f8d56951316577836692ed8a304b028626d5130db83cceff628e8.jpg)



DON’T CARE



Figure 58 — Refresh Command Timing


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/66ed5c3a7608ddcd81f00a609935cae5163a894d34f4a7dad8e69eae298f37ff.jpg)



Figure 59 — Postponing Refresh Commands (Example)


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.15 Self-Refresh Operation (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b84a8a023ed4aebc516a01da36e5c75d5c4338120ac3737e8d4618346fa86029.jpg)



Figure 60 — Pulling-in Refresh Commands (Example)


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.16 Self-Refresh Operation

The Self-Refresh command can be used to retain data in the DDR3 SDRAM, even if the rest of the system is powered down. When in the Self-Refresh mode, the DDR3 SDRAM retains data without external clocking. The DDR3 SDRAM device has a built-in timer to accommodate Self-Refresh operation. The Self-Refresh-Entry (SRE) Command is defined by having CS#, RAS#, CAS#, and CKE held low with WE# high at the rising edge of the clock. 

Before issuing the Self-Refresh-Entry command, the DDR3 SDRAM must be idle with all bank precharge state with tRP satisfied. ‘Idle state’ is defined as all banks are closed (tRP, tDAL, etc. satisfied), no data bursts are in progress, CKE is high, and all timings from previous operations are satisfied (tMRD, tMOD, tRFC, tZQinit, tZQoper, tZQCS, etc.) Also, on-die termination must be turned off before issuing Self-Refresh-Entry command, by either registering ODT pin low $\mathrm { ^ { * } O D T L } + 0 . 5 \mathrm { t C K } ^ { \dag 3 }$ prior to the Self-Refresh Entry command or using MRS to MR1 command. Once the Self-Refresh Entry command is registered, CKE must be held low to keep the device in Self-Refresh mode. During normal operation (DLL on), MR1 $( \mathbf { A } 0 = 0 )$ ), the DLL is automatically disabled upon entering Self-Refresh and is automatically enabled (including a DLL-Reset) upon exiting Self-Refresh. 

When the DDR3 SDRAM has entered Self-Refresh mode, all of the external control signals, except CKE and RESET#, are “don’t care.” For proper Self-Refresh operation, all power supply and reference pins (VDD, VDDQ, VSS, VSSQ, VRefCA and VRefDQ) must be at valid levels. VrefDQ supply may be turned OFF and VREFDQ may take any value between VSS and VDD during Self Refresh operation, provided that VrefDQ is valid and stable prior to CKE going back High and that first Write operation or first Write Leveling Activity may not occur earlier than $5 1 2 { \mathrm { n C K } }$ after exit from Self Refresh. The DRAM initiates a minimum of one Refresh command internally within tCKE period once it enters Self-Refresh mode. 

The clock is internally disabled during Self-Refresh Operation to save power. The minimum time that the DDR3 SDRAM must remain in Self-Refresh mode is tCKE. The user may change the external clock frequency or halt the external clock tCKSRE after Self-Refresh entry is registered, however, the clock must be restarted and stable tCKSRX before the device can exit Self-Refresh operation. 

The procedure for exiting Self-Refresh requires a sequence of events. First, the clock must be stable prior to CKE going back HIGH. Once a Self-Refresh Exit command (SRX, combination of CKE going high and either NOP or Deselect on command bus) is registered, a delay of at least tXS must be satisfied before a valid command not requiring a locked DLL can be issued to the device to allow for any internal refresh in progress. Before a command that requires a locked DLL can be applied, a delay of at least tXSDLL and applicable ZQCAL function requirements (TBD) must be satisfied. 

Before a command that requires a locked DLL can be applied, a delay of at least tXSDLL must be satisfied. Depending on the system environment and the amount of time spent in Self-Refresh, ZQ calibration commands may be required to compensate for the voltage and temperature drift as described in “ZQ Calibration Commands” on page 89. To issue ZQ calibration commands, applicable timing requirements must be satisfied (See Figure 75 — “ZQ Calibration Timing” on page 90). 

CKE must remain HIGH for the entire Self-Refresh exit period tXSDLL for proper operation except for Self-Refresh re-entry. Upon exit from Self-Refresh, the DDR3 SDRAM can be put back into Self-Refresh mode after waiting at least tXS period and issuing one refresh command (refresh period of tRFC). NOP or deselect commands must be registered on each positive clock edge during the Self-Refresh exit interval tXS. ODT must be turned off during tXSDLL. 

# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.16 Self-Refresh Operation (Cont’d)

The use of Self-Refresh mode introduces the possibility that an internally timed refresh event can be missed when CKE is raised for exit from Self-Refresh mode. Upon exit from Self-Refresh, the DDR3 SDRAM requires a minimum of one extra refresh command before it is put back into Self-Refresh Mode. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e8d4e052eaad650e2f76f9f1c7659f847dad719c220c4a0fc49911f4c2abc67e.jpg)



NOTES: 1. Only NOP or DES command.



2. Valid commands not requiring a locked DLL.



3. Valid commands requiring a locked DLL.



Figure 61 — Self-Refresh Entry/Exit Timing


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.17 Power-Down Modes

# 4.17.1 Power-Down Entry and Exit

Power-down is synchronously entered when CKE is registered low (along with NOP or Deselect command). CKE is not allowed to go low while mode register set command, MPR operations, ZQCAL operations, DLL locking or read / write operation are in progress. CKE is allowed to go low while any of other operations such as row activation, precharge or auto-precharge and refresh are in progress, but powerdown IDD spec will not be applied until finishing those operations. Timing diagrams are shown in Figures 62 through Figures 74 with details for entry and exit of Power-Down. 

The DLL should be in a locked state when power-down is entered for fastest power-down exit timing. If the DLL is not locked during power-down entry, the DLL must be reset after exiting power-down mode for proper read operation and synchronous ODT operation. DRAM design provides all AC and DC timing and voltage specification as well as proper DLL operation with any CKE intensive operations as long as DRAM controller complies with DRAM specifications. 

During Power-Down, if all banks are closed after any in-progress commands are completed, the device will be in precharge Power-Down mode; if any bank is open after in-progress commands are completed, the device will be in active Power-Down mode. 

Entering power-down deactivates the input and output buffers, excluding CK, CK#, ODT, CKE and RESET#. To protect DRAM internal delay on CKE line to block the input signals, multiple NOP or Deselect commands are needed during the CKE switch off and cycle(s) after, this timing period are defined as tCPDED. CKE_low will result in deactivation of command and address receivers after tCPDED has expired. 


Table 14 — Power-Down Entry Definitions


<table><tr><td>Status of DRAM</td><td>MRS bit A12</td><td>DLL</td><td>PD Exit</td><td>Relevant Parameters</td></tr><tr><td>Active (A bank or more Open)</td><td>Don’t Care</td><td>On</td><td>Fast</td><td>tXP to any valid command</td></tr><tr><td>Precharged (All banks Precharged)</td><td>0</td><td>Off</td><td>Slow</td><td>tXP to any valid command. Since it is in precharge state, commands here will be ACT, REF, MRS, PRE or PREA.
tXPDLL to commands that need the DLL to operate, such as RD, RDA or ODT control line.</td></tr><tr><td>Precharged (All banks Precharged)</td><td>1</td><td>On</td><td>Fast</td><td>tXP to any valid command.</td></tr></table>

Also, the DLL is disabled upon entering precharge power-down (Slow Exit Mode), but the DLL is kept enabled during precharge power-down (Fast Exit Mode) or active power-down. In power-down mode, CKE low, RESET# high, and a stable clock signal must be maintained at the inputs of the DDR3 SDRAM, and ODT should be in a valid state, but all other input signals are “Don’t Care.” (If RESET# goes low during Power-Down, the DRAM will be out of PD mode and into reset state.) CKE low must be maintained until tCKE has been satisfied. Power-down duration is limited by 9 times tREFI of the device. 

The power-down state is synchronously exited when CKE is registered high (along with a NOP or Deselect command). CKE high must be maintained until tCKE has been satisfied. A valid, executable command can be applied with power-down exit latency, tXP and/or tXPDLL after CKE goes high. Power-down exit latency is defined in the AC specifications table in Section 8. 

Active Power Down Entry and Exit timing diagram example is shown in Figure 62. Timing Diagrams for CKE with PD Entry, PD Exit with Read and Read with Auto Precharge, Write, Write with Auto Precharge, 

# 4.17 Power-Down Modes (Cont’d)

# 4.17.1 Power-Down Entry and Exit (Cont’d)

Activate, Precharge, Refresh, and MRS are shown in Figure 63 through Figure 71. Additional clarifications are shown in Figure 72 through Figure 74. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/2b8f8daa5ab055c7bab901c16bbb1bd31b77226ec81cd4b8ee91270493908be1.jpg)



Note: VALID command at T0 is ACT, NOP, DES or PRE with still one bank remaining open after completion of the precharge command.



Figure 62 — Active Power-Down Entry and Exit Timing Diagram


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b1937b7b596adc27a83f9a9e127d775cbc8979dff8253d233f20ce144184352a.jpg)



Figure 63 — Power-Down Entry after Read and Read with Auto Precharge


# 4.17 Power-Down Modes (Cont’d)

# 4.17.1 Power-Down Entry and Exit (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/3843512d8fdceafec2753d3c56f362729446c34b3b56a22c2f3464a47618aa46.jpg)



Figure 64 — Power-Down Entry after Write with Auto Precharge


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/78f93a8ec5405afae3629e7e654ace739109425ef54dfc537dd67fe8b436a453.jpg)



Figure 65 — Power-Down Entry after Write


# 4.17 Power-Down Modes (Cont’d)

# 4.17.1 Power-Down Entry and Exit (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/8a45b8c7d9ea97b78bf6c4dd6e37acdfe4506d64fe659682aa38899f642609ef.jpg)



Figure 66 — Precharge Power-Down (Fast Exit Mode) Entry and Exit


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/df886d6ce9cf54de55cec795689f1604793769ea23559ddb8776f2ca35ac2d1a.jpg)



Figure 67 — Precharge Power-Down (Slow Exit Mode) Entry and Exit


# 4.17 Power-Down Modes (Cont’d)

# 4.17.1 Power-Down Entry and Exit (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b44ba3ce47c91bac0024f5e2bcd922650bd0bbf89d3f1499608dba702e427115.jpg)



Figure 68 — Refresh Command to Power-Down Entry


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/8af8553977883d2aabbd79abaf9e01c26e587988849f81fbeff89a907fea494c.jpg)



Figure 69 — Active Command to Power-Down Entry


# 4.17 Power-Down Modes (Cont’d)

# 4.17.1 Power-Down Entry and Exit (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/7cfbe48448abc64aa40017856c4be88c1315ccf1e18945c3b3c47a48f0829992.jpg)



Figure 70 — Precharge / Precharge all Command to Power-Down Entry


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b8c55d59c608f08989b51097754c5264deeb830bc94aab9fafec940d5d341d37.jpg)



Figure 71 — MRS Command to Power-Down Entry


# 4.17.2 Power-Down clarifications - Case 1

When CKE is registered low for power-down entry, tPD(min) must be satisfied before CKE can be registered high for power-down exit. The minimum value of parameter tPD(min) is equal to the minimum value 

# 4.17 Power-Down Modes (Cont’d)

# 4.17.2 Power-Down clarifications - Case 1 (Cont’d)

of parameter tCKE(min) as shown in Table 66, Timing Parameters by Speed Bin. A detailed example of Case 1 is shown in Figure 72.) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/52baad2abb613d523a49aa81a3f43e8029e08f510b907f4612d3c852284a7958.jpg)



Figure 72 — Power-Down Entry/Exit Clarifications - Case 1


# 4.17.3 Power-Down clarifications - Case 2

For certain CKE intensive operations, for example, repeated ‘PD Exit - Refresh - PD Entry’ sequences, the number of clock cycles between PD Exit and PD Entry may be insufficient to keep the DLL updated. Therefore, the following conditions must be met in addition to tCKE in order to maintain proper DRAM operation when the Refresh command is issued between PD Exit and PD Entry. Power-down mode can be used in conjunction with the Refresh command if the following conditions are met: 1) tXP must be satisfied before issuing the command. 2) tXPDLL must be satisfied (referenced to the registration of PD Exit) before the next power-down can be entered. A detailed example of Case 2 is shown in Figure 73. 


)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/014d7e98f039795fd691619dd17b3b959b4030ab3ec93e3e9987e9e0718190bc.jpg)



Figure 73 — Power-Down Entry/Exit Clarifications - Case 2


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.17 Power-Down Modes (Cont’d)

# 4.17.4 Power-Down clarifications - Case 3

If an early PD Entry is issued after a Refresh command, once PD Exit is issued, NOP or DES with CKE High must be issued until tRFC(min) from the Refresh command is satisfied. This means CKE can not be registered low twice within a tRFC(min) window. A detailed example of Case 3 is shown in Figure 74. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/14efa4f821bbd17363657f321457500c2a0ff1856b47c324f87166c5415e5599.jpg)



Figure 74 — Power-Down Entry/Exit Clarifications - Case 3


# 4 DDR3 SDRAM Command Description and Operation (Cont’d)

# 4.18 ZQ Calibration Commands

# 4.18.1 ZQ Calibration Description

ZQ Calibration command is used to calibrate DRAM Ron & ODT values. DDR3 SDRAM needs longer time to calibrate output driver and on-die termination circuits at initialization and relatively smaller time to perform periodic calibrations. 

ZQCL command is used to perform the initial calibration during power-up initialization sequence. This command may be issued at any time by the controller depending on the system environment. ZQCL command triggers the calibration engine inside the DRAM and, once calibration is achieved, the calibrated values are transferred from the calibration engine to DRAM IO, which gets reflected as updated output driver and on-die termination values. 

The first ZQCL command issued after reset is allowed a timing period of tZQinit to perform the full calibration and the transfer of values. All other ZQCL commands except the first ZQCL command issued after RESET are allowed a timing period of tZQoper. 

ZQCS command is used to perform periodic calibrations to account for voltage and temperature variations. A shorter timing window is provided to perform the calibration and transfer of values as defined by timing parameter tZQCS. One ZQCS command can effectively correct a minimum of $0 . 5 \%$ (ZQ Correction) of RON and RTT impedance error within 64 nCK for all speed bins assuming the maximum sensitivities specified in the ‘Output Driver Voltage and Temperature Sensitivity’ and ‘ODT Voltage and Temperature Sensitivity’ tables. The appropriate interval between ZQCS commands can be determined from these tables and other application-specific parameters. One method for calculating the interval between ZQCS commands, given the temperature (Tdriftrate) and voltage (Vdriftrate) drift rates that the SDRAM is subject to in the application, is illustrated. The interval could be defined by the following formula: 

$$
\frac {Z Q C o r r e c t i o n}{(T S e n s \times T d r i f t r a t e) + (V S e n s \times V d r i f t r a t e)}
$$

where TSens $=$ max(dRTTdT, dRONdTM) and VSens $=$ max(dRTTdV, dRONdVM) define the SDRAM temperature and voltage sensitivities. 

For example, if TSens $= 1 . 5 \% / ^ { 0 } \mathrm { C }$ , VSens $= 0 . 1 5 \%$ / mV, Tdriftrate $= 1 ~ ^ { \mathrm { { o } } } \mathrm { { C } }$ / sec and Vdriftrate $= 1 5 \mathrm { m V } /$ sec, then the interval between ZQCS commands is calculated as: 

$$
\frac {0 . 5}{(1 . 5 \times 1) + (0 . 1 5 \times 1 5)} = 0. 1 3 3 \approx 1 2 8 m s
$$

No other activities should be performed on the DRAM channel by the controller for the duration of tZQinit, tZQoper, or tZQCS. The quiet time on the DRAM channel allows accurate calibration of output driver and on-die termination values. Once DRAM calibration is achieved, the DRAM should disable ZQ current consumption path to reduce power. 

All banks must be precharged and tRP met before ZQCL or ZQCS commands are issued by the controller. See “[BA $\circleddash$ Bank Address, RA=Row Address, CA=Column Address, BC#=Burst Chop, $\mathrm { X = }$ Don’t Care, V=Valid]” on page 33 for a description of the ZQCL and ZQCS commands. 

ZQ calibration commands can also be issued in parallel to DLL lock time when coming out of self refresh. Upon Self-Refresh exit, DDR3 SDRAM will not perform an IO calibration without an explicit ZQ calibration command. The earliest possible time for ZQ Calibration command (short or long) after self refresh exit is tXS. 

# 4.18 DDR3 SDRAM Command Description and Operation) (Cont’d)

# 4.18.1 ZQ Calibration Description (Cont’d)

In systems that share the ZQ resistor between devices, the controller must not allow any overlap of tZQoper, tZQinit, or tZQCS between the devices. 

# 4.18.2 ZQ Calibration Timing

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/150f0b8535f4c154efda1bf3c4626b539fbaa96e58bb830c94c7d22fb92afe7b.jpg)



NOTES: 1. CKE must be continuously registered high during the calibration procedure.



2. On-die termination must be disabled via the ODT signal or MRS during the calibration procedure.



3. All devices connected to the DQ bus should be high impedance during the calibration procedure.


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/aa110777fa20fb344de8158f9770d7d550ae57340b851f10926cc6617d3bddf6.jpg)



TIME BREAK


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/475f775f419c70996c758ff5295994cd9b34c6f5db589812853e05557f841035.jpg)



DON’T CARE



Figure 75 — ZQ Calibration Timing


# 4.18.3 ZQ External Resistor Value, Tolerance, and Capacitive loading

In order to use the ZQ Calibration function, a $2 4 0 \ \mathrm { o h m } + / - \ 1 \%$ tolerance external resistor must be connected between the ZQ pin and ground. The single resistor can be used for each SDRAM or one resistor can be shared between two SDRAMs if the ZQ calibration timings for each SDRAM do not overlap. The total capacitive loading on the ZQ pin must be limited (See Table 58 — “Input / Output Capacitance” on page 153). 

# 5 On-Die Termination (ODT)

ODT (On-Die Termination) is a feature of the DDR3 SDRAM that allows the DRAM to turn on/off termination resistance for each DQ, DQS, DQS# and DM for x4 and x8 configuration (and TDQS, TDQS# for X8 configuration, when enabled via $\mathbf { A } 1 1 { = } 1$ in MR1) via the ODT control pin. For x16 configuration, ODT is applied to each DQU, DQL, DQSU, DQSU#, DQSL, DQSL#, DMU and DML signal via the ODT control pin. The ODT feature is designed to improve signal integrity of the memory channel by allowing the DRAM controller to independently turn on/off termination resistance for any or all DRAM devices. More details about ODT control modes and ODT timing modes can be found further down in this document: 

• The ODT control modes are described in 5.1. 

• The ODT synchronous mode is described in 5.2 

• The dynamic ODT feature is described in 5.3 

• The ODT asynchronous mode is described in 5.4 

• The transitions between ODT synchronous and asynchronous are described in 5.4.1 through 5.4.4 

The ODT feature is turned off and not supported in Self-Refresh mode. 

A simple functional representation of the DRAM ODT feature is shown in Figure 76. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/cdbfb7fca101dcbe807e2d7d7b4df89ccc40e72d740d86c66dc9daa057a9ce17.jpg)



Figure 76 — Functional Representation of ODT


The switch is enabled by the internal ODT control logic, which uses the external ODT pin and other control information, see below. The value of RTT is determined by the settings of Mode Register bits (see Figure 10 on page 27 and Figure 11 on page 30). The ODT pin will be ignored if the Mode Registers MR1 and MR2 are programmed to disable ODT, and in self-refresh mode. 

# 5.1 ODT Mode Register and ODT Truth Table

The ODT Mode is enabled if any of MR1 {A9, A6, A2} or MR2 {A10, A9} are non zero. In this case, the value of RTT is determined by the settings of those bits (see Figure on page 27). 

Application: Controller sends WR command together with ODT asserted. 

• One possible application: The rank that is being written to provides termination. 

• DRAM turns ON termination if it sees ODT asserted (unless ODT is disabled by MR). 

• DRAM does not use any write or read command decode information. 

• The Termination Truth Table is shown in Table 15. 


Table 15 — Termination Truth Table


<table><tr><td>ODT pin</td><td>DRAM Termination State</td></tr><tr><td>0</td><td>OFF</td></tr><tr><td>1</td><td>ON, (OFF, if disabled by MR1 {A9, A6, A2} and MR2 {A10, A9} in general)</td></tr></table>

# 5 On-Die Termination (ODT) (Cont’d)

# 5.2 Synchronous ODT Mode

Synchronous ODT mode is selected whenever the DLL is turned on and locked. Based on the power-down definition, these modes are: 

• Any bank active with CKE high 

• Refresh with CKE high 

• Idle mode with CKE high 

• Active power down mode (regardless of MR0 bit A12) 

• Precharge power down mode if DLL is enabled during precharge power down by MR0 bit A12. 

The direct ODT feature is not supported during DLL-off mode. The on-die termination resistors must be disabled by continuously registering the ODT pin low and/or by programming the RTT_Nom bits MR1{A9,A6,A2} to {0,0,0} via a mode register set command during DLL-off mode. 

In synchronous ODT mode, RTT will be turned on ODTLon clock cycles after ODT is sampled high by a rising clock edge and turned off ODTLoff clock cycles after ODT is registered low by a rising clock edge. 

The ODT latency is tied to the write latency (WL) by: ODTLon $= \mathrm { W L } - 2$ $=$ ; ODTLoff $= \mathrm { W L } - 2$ ${ } = { }$ 

# 5.2.1 ODT Latency and Posted ODT

In Synchronous ODT Mode, the Additive Latency (AL) programmed into the Mode Register (MR1) also applies to the ODT signal. The DRAM internal ODT signal is delayed for a number of clock cycles defined by the Additive Latency (AL) relative to the external ODT signal. ODTLon $= \mathrm { C W L } + \mathrm { A L } - 2$ $=$ ; 

ODTLoff $= \mathrm { C W L } + \mathrm { A L } - 2 .$ . For details, refer to the ODT Timing Parameters listed in Table 66 on page 167 and Table 67 on page 174. 

# 5.2.2 Timing Parameters

In synchronous ODT mode, the following timing parameters apply (see also Figures 77): 

ODTLon, ODTLoff, tAON,min,max, tAOF,min,max. 

Minimum RTT turn-on time $\left( t _ { \mathrm { A O N } } \mathrm { m i n } \right)$ is the point in time when the device leaves high impedance and ODT resistance begins to turn on. Maximum RTT turn on time $( t _ { \mathrm { A O N } } \mathrm { m a x } )$ is the point in time when the ODT resistance is fully on. Both are measured from ODTLon. 

Minimum RTT turn-off time $( t _ { \mathrm { A O F } } \mathrm { m i n } )$ is the point in time when the device starts to turn off the ODT resistance. Maximum RTT turn off time $\left( t _ { \mathrm { A O F } } \mathrm { m a x } \right)$ is the point in time when the on-die termination has reached high impedance. Both are measured from ODTLoff. 

When ODT is asserted, it must remain high until ODTH4 is satisfied. If a Write command is registered by the SDRAM with ODT high, then ODT must remain high until ODTH4 $[ \mathrm { B L } = 4 _ { , }$ ) or ODTH8 $\mathrm { \Delta B L = 8 ) }$ ) after the Write command (see Figure 78). ODTH4 and ODTH8 are measured from ODT registered high to ODT registered low or from the registration of a Write command until ODT is registered low. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/90a617b0c843c499c5d12295f81b82adb71097a45c1f97da1ffbea582d0086be.jpg)



5.2 Synchronous ODT Mode (Cont’d) 5.2.2 Timing Parameters (Cont’d)



Figure 77 — Synchronous ODT Timing Example for $\mathbf { A } \mathbf { L } = 3$ ; $\mathbf { C W L } = 5$ ; ODTLon = AL + CWL - 2 = 6.0 ; ODTLoff $\mathbf { \delta } = \mathbf { A } \mathbf { L } + \mathbf { C } \mathbf { W } \mathbf { L } - \mathbf { \delta } 2 = \mathbf { 6 }$ $=$


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/570d6ba2812e5f3cb98d3027daca954db30d56562239a30b835f760d0c9bd3be.jpg)



5.2 Synchronous ODT Mode (Cont’d) 5.2.2 Timing Parameters (Cont’d)



Figure 78 — Synchronous ODT example with $\mathbf { B L } = 4$ , $\mathbf { W } \mathbf { L } = 7$


ODT must be held high for at least ODTH4 after assertion (T 1 ) ; ODT must be kept high ODTH4 ${ \mathrm { ( B L } } = 4$ ) or ODTH8 $[ \mathrm { B L } = 8 $ ) after Write command (T7 ) . ODTH is measured from ODT first registered high to ODT first registered low, or from registration of Write command with ODT high to ODT registered low. Note that although ODTH4 is satisfied from ODT registered high at T6 , ODT must not go low before T 1 1 as ODTH4 must also be satisfied from the registration of the Write command at T7 . 

# 5.2 .3 ODT d u ri ng Reads

As the DDR3 SDRAM can not terminate and drive at the same time, RTT must be disabled at least half a clock cycle before the read preamble by driving the ODT pin low appropriately. RTT may not be enabled until the end of the post-amble as shown in the example below. As shown in Figure 79 below, at cycle T 1 5 , DRAM turns on the termination when it stop s driving, which is determined by tHZ . If DRAM stops driving early (i . e . , tHZ is early) , then tAONmin timing may apply. If DRAM stops driving late (i . e . , tHZ is late) , then DRAM complies with tAONmax timing. Note that ODT may be disabled earlier before the Read and enabled later after the Read than shown in this example in Figure 79 . 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/1045e67a0373bcb42016fb79e4fba6ac269efa3e0020cee3e7084df9c56e790c.jpg)



5.2 Synchronous ODT Mode (Cont’d) 5.2.3 ODT during Reads (Cont’d)



Figure 79 — ODT must be disabled externally during Reads by driving ODT low. (example : $\mathbf { C L } = \mathbf { 6 }$ ; $\mathbf { A L } = \mathbf { C L } - \mathbf { 1 } = \mathbf { 5 } ;$ ; $\mathbf { R L } = \mathbf { A L } + \mathbf { C L } = \mathbf { 1 1 }$ ; CWL $= 5$ ; ODTLon $=$ $\mathbf { \Delta } = \mathbf { C W L } + \mathbf { A L } - 2 = 8$ ; ODTLoff $=$ $\mathbf { \sigma } = \mathbf { C W L } + \mathbf { A L } - 2 = 8 )$


# 5.3 Dynamic ODT

In certain application cases and to further enhance signal integrity on the data bus, it is desirable that the termination strength of the DDR3 SDRAM can be changed without issuing an MRS command. This requirement is supported by the “Dynamic ODT” feature as described as follows: 

# 5.3.1 Functional Description:

The Dynamic ODT Mode is enabled if bit (A9) or (A10) of MR2 is set to ’1’. The function is described as follows: 

• Two RTT values are available: RTT_Nom and RTT_WR. 

• The value for RTT_Nom is preselected via bits A[9,6,2] in MR1. 

• The value for RTT_WR is preselected via bits A[10,9] in MR2. 

• During operation without write commands, the termination is controlled as follows: 

• Nominal termination strength RTT_Nom is selected. 

• Termination on/off timing is controlled via ODT pin and latencies ODTLon and ODTLoff. 

• When a write command (WR, WRA, WRS4, WRS8, WRAS4, WRAS8) is registered, and if Dynamic ODT is enabled, the termination is controlled as follows: 

• A latency ODTLcnw after the write command, termination strength RTT_WR is selected. 

• A latency ODTLcwn8 (for BL8, fixed by MRS or selected OTF) or ODTLcwn4 (for BC4, fixed by MRS or selected OTF) after the write command, termination strength RTT_Nom is selected. 

• Termination on/off timing is controlled via ODT pin and ODTLon, ODTLoff. 

Table 16 shows latencies and timing parameters which are relevant for the on-die termination control in Dynamic ODT mode. 

The dynamic ODT feature is not supported at DLL-off mode. User must use MRS command to set $\mathrm { R t t \_ W R } , \mathrm { M R } 2 \{ \mathrm { A } 1 0 , \mathrm { A } 9 \} { = } \{ 0 , 0 \}$ , to disable Dynamic ODT externally. 

When ODT is asserted, it must remain high until ODTH4 is satisfied. If a Write command is registered by the SDRAM with ODT high, then ODT must remain high until ODTH4 ${ \mathrm { ( B L } } = 4 { \mathrm { ) } }$ ) or ODTH8 $\mathrm { \Delta B L = 8 }$ ) after the Write command (see Figure 78). ODTH4 and ODTH8 are measured from ODT registered high to ODT registered low or from the registration of a Write command until ODT is registered low. 


Table 16 — Latencies and timing parameters relevant for Dynamic ODT


<table><tr><td>Name and Description</td><td>Abbr.</td><td>Defined from</td><td>Defined to</td><td>Definition for all DDR3 speed bins</td><td>Unit</td></tr><tr><td>ODT turn-on Latency</td><td>ODTLon</td><td>registering external ODT signal high</td><td>turning termination on</td><td>ODTLon = WL - 2</td><td>tCK</td></tr><tr><td>ODT turn-off Latency</td><td>ODTLoff</td><td>registering external ODT signal low</td><td>turning termination off</td><td>ODTLoff = WL - 2</td><td>tCK</td></tr><tr><td>ODT Latency for changing from RTT_Nom to RTT_WR</td><td>ODTLcnw</td><td>registering external write command</td><td>change RTT strength from RTT_Nom to RTT_WR</td><td>ODTLcnw = WL - 2</td><td>tCK</td></tr><tr><td>ODT Latency for change from RTT_WR to RTT_Nom (BL = 4)</td><td>ODTLcwn4</td><td>registering external write command</td><td>change RTT strength from RTT_WR to RTT_Nom</td><td>ODTLcwn4 = 4 + ODTLoff</td><td>tCK</td></tr><tr><td>ODT Latency for change from RTT_WR to RTT_Nom (BL = 8)</td><td>ODTLcwn8</td><td>registering external write command</td><td>change RTT strength from RTT_WR to RTT_Nom</td><td>ODTLcwn8 = 6 + ODTLoff</td><td>tCK(avg)</td></tr></table>

# 5.3 Dynamic ODT (Cont’d)

# 5.3.1 Functional Description (Cont’d)


Table 16 — Latencies and timing parameters relevant for Dynamic ODT (Cont’d)


<table><tr><td>Name and Description</td><td>Abbr.</td><td>Defined from</td><td>Defined to</td><td>Definition for all DDR3 speed bins</td><td>Unit</td></tr><tr><td>minimum ODT high time after ODT assertion</td><td>ODTH4</td><td>registering ODT high</td><td>ODT registered low</td><td>ODTH4 = 4</td><td>tCK(avg)</td></tr><tr><td>minimum ODT high time after Write (BL = 4)</td><td>ODTH4</td><td>registering Write with ODT high</td><td>ODT registered low</td><td>ODTH4 = 4</td><td>tCK(avg)</td></tr><tr><td>minimum ODT high time after Write (BL = 8)</td><td>ODTH8</td><td>registering Write with ODT high</td><td>ODT registered low</td><td>ODTH8 = 6</td><td>tCK(avg)</td></tr><tr><td>RTT change skew</td><td>tADC</td><td>ODTLcnw ODTLcwn</td><td>RTT valid</td><td>tADC(min) = 0.3 * tCK(avg)
tADC(max) = 0.7 * tCK(avg)</td><td>tCK(avg)</td></tr></table>


NOTE: tAOF,nom and tADC,nom are 0.5 tCK (effectively adding half a clock cycle to ODTLoff, ODTcnw and ODTLcwn) 


# 5.3.2 ODT Timing Diagrams

The following pages provide exemplary timing diagrams as described in Table 17: 


Table 17 — Timing Diagrams for “Dynamic ODT”


<table><tr><td>Figure and Page</td><td>Description</td></tr><tr><td>Figure 80 on page 98</td><td>Figure 80, Dynamic ODT: Behavior with ODT being asserted before and after the write.</td></tr><tr><td>Figure 81 on page 98</td><td>Figure 81, Dynamic ODT: Behavior without write command, AL = 0, CWL = 5.</td></tr><tr><td>Figure 82 on page 99</td><td>Figure 82, Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 6 clock cycles.</td></tr><tr><td>Figure 83 on page 100</td><td>Figure 83, Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 6 clock cycles, example for BC4 (via MRS or OTF), AL = 0, CWL = 5.</td></tr><tr><td>Figure 84 on page 101</td><td>Figure 84, Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 4 clock cycles.</td></tr></table>

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/63b758d9d0c29e95e5f761f9becc09d75ad9575fa5dc2bbc873fda553cfa7814.jpg)



5.3 Dynamic ODT (Cont’d) 5.3.2 ODT Timing Diagrams (Cont’d)



N OTE : Exam ple for BC4 (via M RS or OTF), $\mathbb { A } \mathbb { L } = 0$ , CWL $= 5$ . O DTH4 a p pl ies to fi rst reg iste ri ng O DT h ig h a nd to th e reg istration of th e Write com ma nd . I n th is exa m pl e , O DTH4 wou ld be satisfied if O DT we nt low at T8 (4 clocks afte r th e Write com ma nd ) .



Figure 80 — Dynamic ODT: Behavior with ODT being asserted before and after the write


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/cf52db6c7b380ad2ab2df86491d5d12ee2d3923e41285e0146946206987b9709.jpg)



Figure 81 — Dynamic ODT: Behavior without write command, AL = 0, CWL = 5


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/985124d08e28c632fea84143c8c1060cd068fcc5061ad457774695c707681f86.jpg)



Figure 82 — Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 6 clock cycles



Dynamic ODT (Co ODT Timing Diagrams (C)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/d45c3694c1c1a561f4701ad4e00db8d7fe4cbe88e63488a8adda898dfcca1c4b.jpg)



Figure 83 — Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 6 clock cycles, example for BC4 (via MRS or OTF), $\mathbf { A } \mathbf { L } = \mathbf { 0 }$ , $\mathbf { C W L } = 5 .$ .



5.3 Dynamic ODT (Cont’d) 5.3.2 ODT Timing Diagrams (Cont’d)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/0ef164d337c3db707ae8425e19239b8dc2a5ab8638b2334f3b7ee7484d605360.jpg)



Figure 84 — Dynamic ODT: Behavior with ODT pin being asserted together with write command for a duration of 4 clock cycles



Dynamic ODT (Co ODT Timing Diagrams (C)


# 5.4 Asynch ronous ODT Mode

Asynchronous ODT mode is selected when DRAM runs in DLLon mode, but DLL is temporarily disabled (i . e . frozen) in precharge power-down (by MR0 bit A 1 2) . B ased on the power down mode definitions, this is currently (comment: update editorially after everything is set and done . . .) : Precharge power down mode if DLL is disabled during precharge power down by MR0 bit A 1 2 . 

In asynchronous ODT timing mode, internal ODT command is NOT delayed by Additive Latency (AL) relative to the external ODT command. 

In asynchronous ODT mode, the following timing parameters apply (see Figure 8 5) : tAONPD,min,max, tAOFPD,min,max. 

Minimum RTT turn-on time $( t _ { \mathrm { A O N P D } } \mathrm { m i n } )$ is the point in time when the device termination circuit leaves high impedance state and ODT resistance begins to turn on. Maximum RTT turn on time $( t _ { \mathrm { A O N P D } } \mathrm { m a x } )$ is the point in time when the ODT re sistance is fully on. 

tAONPDmin and tAONPDmax are measured from ODT being sampled high. 

Minimum RTT turn-off time (tAOFPDmin) is the point in time when the devices termination circuit starts to turn off the ODT resistance . Maximum ODT turn off time (tAOFPDmax) is the point in time when the on-die termination has reached high impedance . tAOFPDmin and tAOFPDmax are measured from ODT being sampled low. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e99831053ff715c4b15ad839cc793005454ceb9fd85a62123e3a3440272c12a9.jpg)



Figure 85 — Asynchronous ODT Timings on DDR3 SDRAM with fast ODT transition : AL is ignored


In Precharge Power Down, ODT receiver remains active, however no Read or Write command can be issued, as the respective ADD/CMD receivers may be disabled. 


Table 1 8 — Asynchronous ODT Timing Parameters for all Speed Bins


<table><tr><td>Symbol</td><td>Description</td><td>min</td><td>max</td><td>Unit</td></tr><tr><td>tAONPD</td><td>Asynchronous RTT turn-on delay (Power-Down with DLL frozen)</td><td>2</td><td>8.5</td><td>ns</td></tr><tr><td>tAOFPD</td><td>Asynchronous RTT turn-off delay (Power-Down with DLL frozen)</td><td>2</td><td>8.5</td><td>ns</td></tr></table>

# 5 On-Die Termination (ODT) (Cont’d)

# 5.4 Asynchronous ODT Mode (Cont’d)

# 5.4.1 Synchronous to Asynchronous ODT Mode Transitions


Table 19 — ODT timing parameters for Power Down (with DLL frozen) entry and exit transition period


<table><tr><td>Description</td><td>min</td><td>max</td></tr><tr><td rowspan="2">ODT to RTT 
turn-on delay</td><td>min{ ODTLon * tCK + tAONmin; tAONPDmin}</td><td>max{ ODTLon * tCK + tAONmax; tAONPDmax}</td></tr><tr><td>min{ (WL - 2) * tCK + tAONmin; tAONPDmin}</td><td>max{ (WL - 2) * tCK + tAONmax; tAONPDmax}</td></tr><tr><td rowspan="2">ODT to RTT 
turn-off delay</td><td>min{ ODTOff * tCK +tAOFmin; tAOFPDmin}</td><td>max{ ODTOff * tCK + tAOFmax; tAOFPDmax}</td></tr><tr><td>min{ (WL - 2) * tCK +tAOFmin; tAOFPDmin}</td><td>max{ (WL - 2) * tCK + tAOFmax; tAOFPDmax}</td></tr><tr><td>tANPD</td><td colspan="2">WL -1</td></tr></table>

# 5.4.2 Synchronous to Asynchronous ODT Mode Transition during Power-Down Entry

If DLL is selected to be frozen in Precharge Power Down Mode by the setting of bit A12 in MR0 to $^ { \circ } 0 ^ { \circ }$ , there is a transition period around power down entry, where the DDR3 SDRAM may show either synchronous or asynchronous ODT behavior. 

The transition period is defined by the parameters tANPD and tCPDED(min). tANPD is equal to (WL -1) and is counted backwards in time from the clock cycle where CKE is first registered low. tCPDED(min) starts with the clock cycle where CKE is first registered low. The transition period begins with the starting point of tANPD and terminates at the end point of tCPDED(min), as shown in Figure 86. If there is a Refresh command in progress while CKE goes low, then the transition period ends at the later one of tRFC(min) after the Refresh command and the end point of tCPDED(min), as shown in Figure 87. Please note that the actual starting point at tANPD is excluded from the transition period, and the actual end points at tCPDED(min) and tRFC(min), respectively, are included in the transition period. 

ODT assertion during the transition period may result in an RTT change as early as the smaller of tAONPDmin and (ODTLon $^ * \mathrm { t } _ { \mathrm { C K } } + \mathrm { t } _ { \mathrm { A O N } } \mathrm { m i n } )$ and as late as the larger of tAONPDmax and 

$( \mathrm { O D T L o n ^ { * } t _ { C K } + t _ { A O N } m a x } )$ . ODT de-assertion during the transition period may result in an RTT change as early as the smaller of tAOFPDmin and (ODTLoff* $\mathrm { \dot { \Omega } t _ { C K } } + \mathrm { \Delta t _ { A O F } m i n } )$ and as late as the larger of tAOFPDmax and (ODTLoff $^ * \mathrm { t } _ { \mathrm { C K } } + \mathrm { t } _ { \mathrm { A O F } } \mathrm { m a x } )$ . See Figure 19 and Figure 86. Note that, if AL has a large value, the range where RTT is uncertain becomes quite large. Figure 86 shows the three different cases: ODT_A, synchronous behavior before tANPD; ODT_B has a state change during the transition period; ODT_C shows a state change after the transition period. 

# 5.4 Asynchronous ODT Mode (Cont’d)

# 5.4.2 Synchronous to Asynchronous ODT Mode Transition during Power-Down Entry (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/c9156dd97326efd86c847a15441cef8cee5839659f83580d101551d3b9cb725b.jpg)



Figure 86 — Synchronous to asynchronous transition during Precharge Power Down (with DLL frozen) entry $( \mathbf { A } \mathbf { L } = \mathbf { 0 }$ ; $\mathbf { C W L } = 5$ ; t $\mathbf { \hat { A } N P D } = \mathbf { W L } - \mathbf { 1 } = 4 )$ $=$


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/ae76a3b8e20da035f67daa877dfcc9c490d9a93f012308c88fbedb62d5464844.jpg)



Figure 87 — Synchronous to asynchronous transition after Refresh command $\mathbf { A L } = \mathbf { 0 }$ ; CWL = 5 ; tANPD = WL - 1 = 4)


# 5.4.3 Asynch ronous to Synch ronous ODT Mode Trans ition d u ri ng Power-Down Exit

If DLL is selected to be frozen in Precharge Power Down Mode by the setting of bit A 1 2 in MR0 to $^ { \circ } 0 ^ { \circ }$ , there is also a transition period around power down exit, where either synchronous or asynchronous response to a change in ODT must be expected from the DDR3 SDRAM. 

This transition period starts tANPD before CKE is first registered high, and ends tXPDLL after CKE is first registered high. tANPD is equal to (WL - 1 ) and is counted (backwards) from the clock cycle where CKE is first registered high. 

ODT assertion during the transition period may result in an RTT change as early as the smaller of tAONPDmin and $( \mathrm { O D T L o n ^ { * } t _ { C K } + t _ { A O N } m i n } )$ and as late as the larger of tAONPDmax and (ODTLon $^ * \mathrm { t } _ { \mathrm { C K } } + \mathrm { t } _ { \mathrm { A O N } } \mathrm { m a x } )$ . ODT de-assertion during the transition period may result in an RTT change as early as the smaller of tAOFPDmin and $( \mathrm { O D T L o f f ^ { * } t _ { C K } + t _ { A O F } m i n } )$ and as late as the larger of tAOFPDmax and $( \mathrm { O D T L o f f ^ { * } t _ { C K } + t _ { A O F } m a x } )$ . S ee Table 1 9 . 

Note that, if AL has a large value, the range where RTT is uncertain becomes quite large . Figure 8 8 shows the three different cases : ODT_C, asynchronous response before $\mathfrak { t } _ { \mathrm { A N P D } }$ ; ODT_B has a state change of ODT during the transition period; ODT_A shows a state change of ODT after the transition period with synchronous response . 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a5c14e224cfc2abb3fccce1118e6f996c0a6d88a36c870458f2d4b39bed8ccb4.jpg)



Figure 88 — Asynchronous to synchronous transition during Precharge Power Down (with DLL frozen) exit $\mathbf { \hat { C } L } = \mathbf { 6 }$ ; $\mathbf { A L } = \mathbf { C L } - \mathbf { 1 }$ ; $\mathbf { C W L } = 5$ $= 5$ ; tANPD $=$ WL - 1 = 9)


# 5.4.4 Asynch ronous to Synch ronous ODT Mode d u ri ng s hort C KE h ig h and s hort C KE low periods

If the total time in Precharge Power Down state or Idle state is very short, the transition periods for PD entry and PD exit may overlap (see Figure 8 9) . In this case, the response of the DDR3 SDRAMs RTT to a change in ODT state at the input may be synchronous OR asynchronous from the start of the PD entry transition period to the end of the PD exit transition period (even if the entry period ends later than the exit period) . 

If the total time in Idle state is very short, the transition periods for PD exit and PD entry may overlap . In this case the re sponse of the DDR3 SDRAMs RTT to a change in ODT state at the input may be synchronous OR asynchronous from the start of the PD exit transition period to the end of the PD entry transition period. Note that in the bottom part of Figure 8 9 it is as sumed that there was no Refresh command in progres s when Idle state was entered. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/37f6347ff771fc7227397c64a56c04aa003f6404a627db514b97fc80b8082d97.jpg)



Figure 89 — Transition period for short CKE cycles, entry and exit period overlapping $\mathbf { A L } = \mathbf { 0 }$ , $\mathbf { W L } = 5 ,$ , $\mathrm { \Delta t A N P D = W L - 1 } = 4 )$ $=$


This page left blank. 

# 6 Absolute Maximum Ratings

# 6.1 Absolute Maximum DC Ratings


Table 20 — Absolute Maximum DC Ratings


<table><tr><td>Symbol</td><td>Parameter</td><td>Rating</td><td>Units</td><td>Notes</td></tr><tr><td>VDD</td><td>Voltage on VDD pin relative to Vss</td><td>-0.4 V ~ 1.975 V</td><td>V</td><td>1,3</td></tr><tr><td>VDDQ</td><td>Voltage on VDDQ pin relative to Vss</td><td>-0.4 V ~ 1.975 V</td><td>V</td><td>1,3</td></tr><tr><td>VIN, VOUT</td><td>Voltage on any pin relative to Vss</td><td>-0.4 V ~ 1.975 V</td><td>V</td><td>1</td></tr><tr><td>TSTG</td><td>Storage Temperature</td><td>-55 to +100</td><td>°C</td><td>1,2</td></tr><tr><td colspan="5">NOTE 1. Stresses greater than those listed under “Absolute Maximum Ratings” may cause permanent damage to the device. This is a stress rating only and functional operation of the device at these or any other conditions above those indicated in the operational sections of this specification is not implied. Exposure to absolute maximum rating conditions for extended periods may affect reliability
NOTE 2. Storage Temperature is the case surface temperature on the center/top side of the DRAM. For the measurement conditions, please refer to JESD51-2 standard.
NOTE 3. VDD and VDDQ must be within 300 mV of each other at all times;and VREF must be not greater than 0.6 x VDDQ, When VDD and VDDQ are less than 500 mV; VREF may be equal to or less than 300 mV</td></tr></table>

# 6.2 DRAM Component Operating Temperature Range


Table 21 — Temperature Range


<table><tr><td>Symbol</td><td>Parameter</td><td>Rating</td><td>Units</td><td>Notes</td></tr><tr><td rowspan="2">TOPER</td><td>Normal Operating Temperature Range</td><td>0 to 85</td><td>°C</td><td>1,2</td></tr><tr><td>Extended Temperature Range (Optional)</td><td>85 to 95</td><td>°C</td><td>1,3</td></tr><tr><td colspan="5">NOTE 1. Operating Temperature TOPER is the case surface temperature on the center / top side of the DRAM. For measurement conditions, please refer to the JEDEC document JESD51-2.</td></tr><tr><td colspan="5">NOTE 2. The Normal Temperature Range specifies the temperatures where all DRAM specifications will be supported. During operation, the DRAM case temperature must be maintained between 0 to 85 °C under all operating conditions</td></tr><tr><td colspan="5">NOTE 3. Some applications require operation of the DRAM in the Extended Temperature Range between 85 °C and 95 °C case temperature. Full specifications are supported in this range, but the following additional conditions apply: 
a Refresh commands must be doubled in frequency, therefore reducing the Refresh interval tREFI to 3.9 μs. It is also possible to specify a component with 1X refresh (tREFI to 7.8μs) in the Extended Temperature Range. Please refer to supplier data sheet and/or the DIMM SPD for option availability. 
b If Self-Refresh operation is required in the Extended Temperature Range, then it is mandatory to either use the Manual Self-Refresh mode with Extended Temperature Range capability (MR2 A6 = 0b and MR2 A7 = 1b) or enable the optional Auto Self-Refresh mode (MR2 A6 = 1b and MR2 A7 = 0b). Please refer to the supplier data sheet and/or the DIMM SPD for Auto Self-Refresh option availability, Extended Temperature Range support and tREFI requirements in the Extended Temperature Range.</td></tr></table>

Ths page left blank. 

# 7 AC & DC Operating Conditions

# 7.1 Recommended DC Operating Conditions


Table 22 — Recommended DC Operating Conditions


<table><tr><td rowspan="2">Symbol</td><td rowspan="2">Parameter</td><td colspan="3">Rating</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Typ</td><td>Max</td></tr><tr><td>VDD</td><td>Supply Voltage</td><td>1.425</td><td>1.5</td><td>1.575</td><td>V</td><td>1,2</td></tr><tr><td>VDDQ</td><td>Supply Voltage for Output</td><td>1.425</td><td>1.5</td><td>1.575</td><td>V</td><td>1,2</td></tr><tr><td colspan="7">NOTE 1. Under all conditions VDDQ must be less than or equal to VDD. 
NOTE 2. VDDQ tracks with VDD. AC parameters are measured with VDD and VDDQ tied together.</td></tr></table>

Ths page left blank. 

# 8 AC and DC Input Measurement Levels

# 8.1 AC and DC Logic Input Levels for Single-Ended Signals

# 8.1.1 AC and DC Input Levels for Single-Ended Command and Address Signals Table 23 — Single-Ended AC and DC Input Levels for Command and Address

<table><tr><td rowspan="2">Symbol</td><td rowspan="2">Parameter</td><td colspan="2">DDR3-800/1066/1333/1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td></tr><tr><td>VIH.CA(DC100)</td><td>DC input logic high</td><td>Vref + 0.100</td><td>VDD</td><td>V</td><td>1</td></tr><tr><td>VIL.CA(DC100)</td><td>DC input logic low</td><td>VSS</td><td>Vref - 0.100</td><td>V</td><td>1</td></tr><tr><td>VIH.CA(AC175)</td><td>AC input logic high</td><td>Vref + 0.175</td><td>Note 2</td><td>V</td><td>1, 2</td></tr><tr><td>VIL.CA(AC175)</td><td>AC input logic low</td><td>Note 2</td><td>Vref - 0.175</td><td>V</td><td>1, 2</td></tr><tr><td>VIH.CA(AC150)</td><td>AC input logic high</td><td>Vref + 0.150</td><td>Note 2</td><td>V</td><td>1, 2</td></tr><tr><td>VIL.CA(AC150)</td><td>AC input logic low</td><td>Note 2</td><td>Vref - 0.150</td><td>V</td><td>1, 2</td></tr><tr><td>\( V_{RefCA} \)(DC)</td><td>Reference Voltage for ADD, CMD inputs</td><td>0.49 * VDD</td><td>0.51 * VDD</td><td>V</td><td>3, 4</td></tr><tr><td colspan="6">NOTE 1. For input only pins except RESET#. Vref = VrefCA(DC).NOTE 2. See 9.6 “Overshoot and Undershoot Specifications” on page 125.NOTE 3. The ac peak noise on \( V_{Ref} \) may not allow \( V_{Ref} \) to deviate from \( V_{RefCA} \)(DC) by more than +/-1% VDD (for reference: approx. +/- 15 mV).NOTE 4. For reference: approx. VDD/2 +/- 15 mV.</td></tr></table>

# 8.1.2 AC and DC Input Levels for Single-Ended Data Signals

DDR3 SDRAM will support two Vih/Vil AC levels for DDR3-800 and DDR3-1066 as specified in Table 24. DDR3 SDRAM will also support corresponding tDS values (Table 66 on page 167 and Table 72 on page 189) as well as derating tables Table 69 on page 183 depending on Vih/Vil AC levels. 


Table 24 — Single-Ended AC and DC Input Levels for DQ and DM


<table><tr><td rowspan="2">Symbol</td><td rowspan="2">Parameter</td><td colspan="2">DDR3-800, DDR3-1066</td><td colspan="2">DDR3-1333, DDR3-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td>VIH.DQ(DC100)</td><td>DC input logic high</td><td>Vref + 0.100</td><td>VDD</td><td>Vref + 0.100</td><td>VDD</td><td>V</td><td>1</td></tr><tr><td>VIL.DQ(DC100)</td><td>DC input logic low</td><td>VSS</td><td>Vref - 0.100</td><td>VSS</td><td>Vref - 0.100</td><td>V</td><td>1</td></tr><tr><td>VIH.DQ(AC175)</td><td>AC input logic high</td><td>Vref + 0.175</td><td>Note 2</td><td>-</td><td>-</td><td>V</td><td>1,2</td></tr><tr><td>VIL.DQ(AC175)</td><td>AC input logic low</td><td>Note 2</td><td>Vref - 0.175</td><td>-</td><td>-</td><td>V</td><td>1,2</td></tr><tr><td>VIH.DQ(AC150)</td><td>AC input logic high</td><td>Vref + 0.150</td><td>Note 2</td><td>Vref + 0.150</td><td>Note 2</td><td>V</td><td>1,2</td></tr><tr><td>VIL.DQ(AC150)</td><td>AC input logic low</td><td>Note 2</td><td>Vref - 0.150</td><td>Note 2</td><td>Vref - 0.150</td><td>V</td><td>1,2</td></tr><tr><td>\( V_{RefDQ} \)(DC)</td><td>Reference Voltage for DQ,DM inputs</td><td>0.49 * VDD</td><td>0.51 * VDD</td><td>0.49 * VDD</td><td>0.51 * VDD</td><td>V</td><td>3,4</td></tr><tr><td colspan="8">NOTE 1. Vref = VrefDQ(DC).NOTE 2. See 9.6 “Overshoot and Undershoot Specifications” on page 125.NOTE 3. The ac peak noise on \( V_{Ref} \) may not allow \( V_{Ref} \) to deviate from \( V_{RefDQ} \)(DC) by more than +/-1% VDD (for reference: approx. +/- 15 mV).NOTE 4. For reference: approx. VDD/2 +/- 15 mV.</td></tr></table>

# 8.2 Vref Tolerances

The dc-tolerance limits and ac-noise limits for the reference voltages $\mathrm { V _ { R e f C A } }$ and $\mathrm { \Delta V _ { R e f D Q } }$ are illustrated in Figure 90. It shows a valid reference voltage $\mathrm { { V _ { R e f } ( t ) } }$ as a function of time. $\mathrm { \Delta V _ { R e f } }$ stands for $\mathrm { V _ { R e f C A } }$ and $\mathrm { \Delta V _ { R e f D Q } }$ likewise). 

$\mathrm { V _ { R e f } ( D C ) }$ is the linear average of $\mathrm { { V } _ { R e f } ( t ) }$ over a very long period of time (e.g., 1 sec). This average has to meet the min/max requirements in Table 23. Furthermore $\mathrm { { V } _ { R e f } ( t ) }$ may temporarily deviate from $\mathrm { V _ { R e f ( D C ) } }$ by no more than $+ / - 1 \%$ VDD. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/06aaabaec43a3691b00b8147a86788fcd409dd438fc0ab0333f47b1604baf0b5.jpg)



Figure 90 — Illustration of $\mathbf { V _ { R e f ( D C ) } }$ tolerance and $\mathbf { V _ { R e f } }$ ac-noise limits


The voltage levels for setup and hold time measurements $\mathrm { V _ { I H ( A C ) } , V _ { I H ( D C ) } , V _ { I L ( A C ) } , }$ and $\mathrm { \Delta V _ { I L ( D C ) } }$ are dependent on $\mathrm { \Delta V _ { R e f } } .$ 

$^ { \mathrm { e } \mathrm { e } } \mathrm { \overline { { { \mathrm { \Lambda } } } } \times \ e f { \mathrm { \Lambda } } } ^ { \mathrm { 3 } \mathrm { 3 } }$ shall be understood as $\mathrm { { V _ { R e f ( D C ) } } } .$ , as defined in Figure 90. 

This clarifies that dc-variations of $\mathrm { \Delta V _ { R e f } }$ affect the absolute voltage a signal has to reach to achieve a valid high or low level and therefore the time to which setup and hold is measured. System timing and voltage budgets need to account for $\mathrm { V _ { R e f ( D C ) } }$ deviations from the optimum position within the data-eye of the input signals. 

This also clarifies that the DRAM setup/hold specification and derating values need to include time and voltage associated with $\mathrm { \Delta V _ { R e f } }$ ac-noise. Timing and voltage effects due to ac-noise on $\mathrm { \Delta V _ { R e f } }$ up to the specified limit $( + / - 1 \%$ of VDD) are included in DRAM timings and their associated deratings. 

# 8.3 AC and DC Logic Input Levels for Differential Signals

# 8.3.1 Differential signal definition

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/4c21e5c0a56d2a4869661a017051a2b8ed08b1b7e9154136e4898cf1feaa7500.jpg)



Figure 91 — Definition of differential ac-swing and “time above ac-level” tDVAC


# 8.3.2 Differential swing requirements for clock (CK - CK#) and strobe (DQS - DQS#)


Table 25 — Differential AC and DC Input Levels


<table><tr><td rowspan="2">Symbol</td><td rowspan="2">Parameter</td><td colspan="2">DDR3-800, 1066, 1333, &amp; 1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td></tr><tr><td>VIHdiff</td><td>Differential input high</td><td>+ 0.200</td><td>note 3</td><td>V</td><td>1</td></tr><tr><td>VILdiff</td><td>Differential input logic low</td><td>Note 3</td><td>- 0.200</td><td>V</td><td>1</td></tr><tr><td>VIHdiff(ac)</td><td>Differential input high ac</td><td>2 x (VIH(ac) - Vref)</td><td>Note 3</td><td>V</td><td>2</td></tr><tr><td>VILdiff(ac)</td><td>Differential input low ac</td><td>note 3</td><td>2 x (VIL(ac) - Vref)</td><td>V</td><td>2</td></tr><tr><td colspan="6">NOTE 1. Used to define a differential signal slew-rate.NOTE 2. For CK - CK# use VIH/VIL(ac) of ADD/CMD and VREFCA; for DQS - DQS#, DQSL, DQSL#, DQSU ,DQSU# use VIH/VIL(ac) of DQs and VREFDQ; if a reduced ac-high or ac-low level is used for a signal group,then the reduced level applies also here.NOTE 3. These values are not defined; however, the single-ended signals CK, CK#, DQS, DQS#, DQSL, DQSL#, DQSU,DQSU# need to be within the respective limits (VIH(dc) max, VIL(dc)min) for single-ended signals as well asthe limitations for overshoot and undershoot. Refer to “Overshoot and Undershoot Specifications” on page 125</td></tr></table>

# 8.3 AC and DC Logic Input Levels for Differential Signals (Cont’d)

# 8.3.2 Differential swing requirements for clock (CK - CK#) and strobe (DQS - DQS#) (Cont’d)


Table 26 — Allowed time before ringback (tDVAC) for CK - CK# and DQS - DQS#


<table><tr><td>Slew Rate [V/ns]</td><td colspan="2">tDVAC [ps] @ |VIH/Ldiff(ac)| = 350mV</td><td colspan="2">tDVAC [ ps ] @ |VIH/Ldiff(ac)| = 300mV</td></tr><tr><td></td><td>min</td><td>max</td><td>min</td><td>max</td></tr><tr><td>&gt;4.0</td><td>75</td><td>-</td><td>175</td><td>-</td></tr><tr><td>4.0</td><td>57</td><td>-</td><td>170</td><td>-</td></tr><tr><td>3.0</td><td>50</td><td>-</td><td>167</td><td>-</td></tr><tr><td>2.0</td><td>38</td><td>-</td><td>163</td><td>-</td></tr><tr><td>1.8</td><td>34</td><td>-</td><td>162</td><td>-</td></tr><tr><td>1.6</td><td>29</td><td>-</td><td>161</td><td>-</td></tr><tr><td>1.4</td><td>22</td><td>-</td><td>159</td><td>-</td></tr><tr><td>1.2</td><td>13</td><td>-</td><td>155</td><td>-</td></tr><tr><td>1.0</td><td>0</td><td>-</td><td>150</td><td>-</td></tr><tr><td>&lt;1.0</td><td>0</td><td>-</td><td>150</td><td>-</td></tr></table>

# 8.3.3 Single-ended requirements for differential signals

Each individual component of a differential signal (CK, DQS, DQSL, DQSU, CK#, DQS#, DQSL#, or DQSU#) has also to comply with certain requirements for single-ended signals. 

CK and CK# have to approximately reach VSEHmin / VSELmax (approximately equal to the ac-levels (VIH(ac) / VIL(ac) ) for ADD/CMD signals) in every half-cycle. 

DQS, DQSL, DQSU, DQS#, DQSL# have to reach VSEHmin / VSELmax (approximately the ac-levels (VIH(ac) / VIL(ac) ) for DQ signals) in every half-cycle preceding and following a valid transition. 

Note that the applicable ac-levels for ADD/CMD and DQ’s might be different per speed-bin etc. E.g., if VIH.CA(AC150)/VIL.CA(AC150) is used for ADD/CMD signals, then these ac-levels apply also for the single-ended signals CK and CK# 

# 8.3 AC and DC Logic Input Levels for Differential Signals (Cont’d)

# 8.3.3 Single-ended requirements for differential signals (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/c114d92f6d7dc0edcf0747195577e08f9b03b0383756bfc775c33a3ed2e69395.jpg)



Figure 92 — Single-ended requirement for differential signals.


Note that, while ADD/CMD and DQ signal requirements are with respect to Vref, the single-ended components of differential signals have a requirement with respect to VDD / 2; this is nominally the same. The transition of single-ended signals through the ac-levels is used to measure setup time. For single-ended components of differential signals the requirement to reach VSELmax, VSEHmin has no bearing on timing, but adds a restriction on the common mode characteristics of these signals. 


Table 27 — Single-ended levels for CK, DQS, DQSL, DQSU, CK#, DQS#, DQSL# or DQSU#


<table><tr><td rowspan="2">Symbol</td><td rowspan="2">Parameter</td><td colspan="2">DDR3-800, 1066, 1333, &amp; 1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td></tr><tr><td rowspan="2">VSEH</td><td>Single-ended high level for strobes</td><td>(VDD / 2) + 0.175</td><td>note 3</td><td>V</td><td>1, 2</td></tr><tr><td>Single-ended high level for CK, CK#</td><td>(VDD / 2) + 0.175</td><td>note 3</td><td>V</td><td>1, 2</td></tr><tr><td rowspan="2">VSEL</td><td>Single-ended low level for strobes</td><td>note 3</td><td>(VDD / 2) - 0.175</td><td>V</td><td>1, 2</td></tr><tr><td>Single-ended low level for CK, CK#</td><td>note 3</td><td>(VDD / 2) - 0.175</td><td>V</td><td>1, 2</td></tr><tr><td colspan="6">NOTE 1. For CK, CK# use VIH/VIL(ac) of ADD/CMD; for strobes (DQS, DQS#, DQSL, DQSL#, DQSU, DQSU#) use VIH/VIL(ac) of DQs. 
NOTE 2. VIH(ac)/VIL(ac) for DQs is based on VREFDQ; VIH(ac)/VIL(ac) for ADD/CMD is based on VREFCA; if a reduced ac-high or ac-low level is used for a signal group, then the reduced level applies also here 
NOTE 3. These values are not defined, however the single-ended signals CK, CK#, DQS, DQS#, DQSL, DQSL#, DQSU, DQSU# need to be within the respective limits (VIH(dc) max, VIL(dc)min) for single-ended signals as well as the limitations for overshoot and undershoot. Refer to “Overshoot and Undershoot Specifications” on page 125</td></tr></table>

# 8.4 Differential Input Cross Point Voltage

To guarantee tight setup and hold times as well as output skew parameters with respect to clock and strobe, each cross point voltage of differential input signals (CK, CK# and DQS, DQS#) must meet the require-

# 8 AC and DC Input Measurement Levels (Cont’d)

# 8.4 Differential Input Cross Point Voltage (Cont’d)

ments in Table 28. The differential input cross point voltage $\mathrm { V _ { I X } }$ is measured from the actual cross point of true and complement signals to the midlevel between of VDD and VSS. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b71a7a2c4e6c440aac66f5b78447d1518f4ecce27e04a66b270c5a79575d0172.jpg)



Figure 93 — Vix Definition



Table 28 — Cross point voltage for differential input signals (CK, DQS)


<table><tr><td rowspan="2">Symbol</td><td rowspan="2">Parameter</td><td colspan="2">DDR3-800, DDR3-1066, DDR3-1333, DDR3-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td></tr><tr><td rowspan="2">VIX</td><td rowspan="2">Differential Input Cross Point Voltage relative to VDD/2 for CK, CK#</td><td>- 150</td><td>150</td><td>mV</td><td></td></tr><tr><td>- 175</td><td>175</td><td>mV</td><td>1</td></tr><tr><td>VIX</td><td>Differential Input Cross Point Voltage relative to VDD/2 for DQS, DQS#</td><td>- 150</td><td>150</td><td>mV</td><td></td></tr><tr><td colspan="6">NOTE 1. Extended range for Vix is only allowed for clock and if single-ended clock input signals CK and CK# are monotonic with a single-ended swing VSEL / VSEH of at least VDD/2 +/-250 mV, and when the differential slew rate of CK - CK# is larger than 3 V/ns.Refer to Table 27 on page 117 for VSEL and VSEH standard values.</td></tr></table>

# 8.5 Slew Rate Definitions for Single-Ended Input Signals

See 13.5 “Address / Command Setup, Hold and Derating” on page 182 for single-ended slew rate definitions for address and command signals. 

See 13.6 “Data Setup, Hold and Slew Rate Derating” on page 189 for single-ended slew rate definitions for data signals. 

# 8.6 Slew Rate Definitions for Differential Input Signals

Input slew rate for differential signals (CK, CK# and DQS, DQS#) are defined and measured as shown in Table 29 and Figure 94. 


Table 29 — Differential Input Slew Rate Definition


<table><tr><td rowspan="2">Description</td><td colspan="2">Measured</td><td rowspan="2">Defined by</td></tr><tr><td>from</td><td>to</td></tr><tr><td>Differential input slew rate for rising edge (CK - CK# and DQS - DQS#).</td><td>VILdiffmax</td><td>VIHdiffmin</td><td>[VIHdiffmin - VILdiffmax] / DeltaTRdiff</td></tr><tr><td>Differential input slew rate for falling edge (CK - CK# and DQS - DQS#).</td><td>VIHdiffmin</td><td>VILdiffmax</td><td>[VIHdiffmin - VILdiffmax] / DeltaTFdiff</td></tr><tr><td colspan="4">NOTE: The differential signal (i.e., CK - CK# and DQS - DQS#) must be linear between these thresholds.</td></tr></table>

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/096c84d4b310544344b273a587df378cc5760506bd6a24d9bdd98c421e6259fd.jpg)



Figure 94 — Differential Input Slew Rate Definition for DQS, DQS# and CK, CK#


Ths page left blank. 

# 9 AC and DC Output Measurement Levels

# 9.1 Single Ended AC and DC Output Levels

Table 30 shows the output levels used for measurements of single ended signals. 


Table 30 — Single-ended AC and DC Output Levels


<table><tr><td>Symbol</td><td>Parameter</td><td>DDR3-800, 1066, 1333, and 1600</td><td>Unit</td><td>Notes</td></tr><tr><td>VOH(DC)</td><td>DC output high measurement level (for IV curve linearity)</td><td>0.8 x VDDQ</td><td>V</td><td></td></tr><tr><td>VOM(DC)</td><td>DC output mid measurement level (for IV curve linearity)</td><td>0.5 x VDDQ</td><td>V</td><td></td></tr><tr><td>VOL(DC)</td><td>DC output low measurement level (for IV curve linearity)</td><td>0.2 x VDDQ</td><td>V</td><td></td></tr><tr><td>VOH(AC)</td><td>AC output high measurement level (for output SR)</td><td>VTT + 0.1 x VDDQ</td><td>V</td><td>1</td></tr><tr><td>VOL(AC)</td><td>AC output low measurement level (for output SR)</td><td>VTT - 0.1 x VDDQ</td><td>V</td><td>1</td></tr><tr><td colspan="5">NOTE 1. The swing of ± 0.1 × VDDQ is based on approximately 50% of the static single-ended output high or low swing with a driver impedance of 40 Ω and an effective test load of 25 Ω to VTT = VDDQ/2.</td></tr></table>

# 9.2 Differential AC and DC Output Levels

Table 31 shows the output levels used for measurements of differential signals. 


Table 31 — Differential AC and DC Output Levels


<table><tr><td>Symbol</td><td>Parameter</td><td>DDR3-800, 1066, 1333, and 1600</td><td>Unit</td><td>Notes</td></tr><tr><td>VOHdiff(AC)</td><td>AC differential output high measurement level (for output SR)</td><td>+0.2 x VDDQ</td><td>V</td><td>1</td></tr><tr><td>VOLdiff(AC)</td><td>AC differential output low measurement level (for output SR)</td><td>-0.2 x VDDQ</td><td>V</td><td>1</td></tr><tr><td colspan="5">NOTE 1. The swing of ±0.2 × VDDQ is based on approximately 50% of the static single-ended output high or low swing with a driver impedance of 40 Ω and an effective test load of 25 Ω to VTT = VDDQ/2 at each of the differential outputs.</td></tr></table>

# 9.3 Single Ended Output Slew Rate

With the reference load for timing measurements, output slew rate for falling and rising edges is defined and measured between $\mathsf { V } _ { \mathrm { O L } ( \mathrm { A C } ) }$ and $\mathrm { V _ { O H ( A C ) } }$ for single ended signals as shown in Table 32 and Figure 95. 


Table 32 — Single-ended Output Slew Rate Definition


<table><tr><td rowspan="2">Description</td><td colspan="2">Measured</td><td rowspan="2">Defined by</td></tr><tr><td>from</td><td>to</td></tr><tr><td>Single-ended output slew rate for rising edge</td><td>VOL(AC)</td><td>VOH(AC)</td><td>[VOH(AC) - VOL(AC)] / DeltaTRse</td></tr><tr><td>Single-ended output slew rate for falling edge</td><td>VOH(AC)</td><td>VOL(AC)</td><td>[VOH(AC) - VOL(AC)] / DeltaTFse</td></tr><tr><td colspan="4">NOTE: Output slew rate is verified by design and characterization, and may not be subject to production test.</td></tr></table>

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e05576b0a95cdab2d318b304cca5e96c32f59477d07383940bb759c7691cebf7.jpg)



Figure 95 — Single Ended Output Slew Rate Definition



Table 33 — Output Slew Rate (single-ended)


<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td rowspan="2">Units</td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td>Single-ended Output Slew Rate</td><td>SRQse</td><td>2.5</td><td>5</td><td>2.5</td><td>5</td><td>2.5</td><td>5</td><td>TBD</td><td>5</td><td>V/ns</td></tr><tr><td colspan="11">Description: SR: Slew Rate
Q: Query Output (like in DQ, which stands for Data-in, Query-Output)
se: Single-ended Signals
For Ron = RZQ/7 setting</td></tr></table>

# 9 AC and DC Output Measurement Levels (Cont’d)

# 9.4 Differential Output Slew Rate

With the reference load for timing measurements, output slew rate for falling and rising edges is defined and measured between VOLdiff(AC) and VOHdiff(AC) for differential signals as shown in Table 34 and Figure 96. 


Table 34 — Differential Output Slew Rate Definition


<table><tr><td rowspan="2">Description</td><td colspan="2">Measured</td><td rowspan="2">Defined by</td></tr><tr><td>from</td><td>to</td></tr><tr><td>Differential output slew rate for rising edge</td><td>VOLdiff(AC)</td><td>VOHdiff(AC)</td><td>[VOHdiff(AC) - VOLdiff(AC)] / DeltaTRdiff</td></tr><tr><td>Differential output slew rate for falling edge</td><td>VOHdiff(AC)</td><td>VOLdiff(AC)</td><td>[VOHdiff(AC) - VOLdiff(AC)] / DeltaTFdiff</td></tr><tr><td colspan="4">NOTE: Output slew rate is verified by design and characterization, and may not be subject to production test.</td></tr></table>

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a88023adb1e397c1eca4f363a23e9e73e382612462511b1a878fb0f36e80966b.jpg)



Figure 96 — Differential Output Slew Rate Definition



Table 35 — Differential Output Slew Rate


<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td rowspan="2">Units</td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td>Differential Output Slew Rate</td><td>SRQdiff</td><td>5</td><td>10</td><td>5</td><td>10</td><td>5</td><td>10</td><td>TBD</td><td>10</td><td>V/ns</td></tr><tr><td colspan="11">Description: 
SR: Slew Rate 
Q: Query Output (like in DQ, which stands for Data-in, Query-Output) 
diff: Differential Signals 
For Ron = RZQ/7 setting</td></tr></table>

# 9.5 Reference Load for AC Timing and Output Slew Rate

Figure 97 represents the effective reference load of 25 ohms used in defining the relevant AC timing parameters of the device as well as output slew rate measurements. 

It is not intended as a precise representation of any particular system environment or a depiction of the actual load presented by a production tester. System designers should use IBIS or other simulation tools to correlate the timing reference load to a system environment. Manufacturers correlate to their production test conditions, generally one or more coaxial transmission lines terminated at the tester electronics. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/b9e4a983f8010709327d647d921d3bc16ce428e05a658bc1c9cc2d297587822b.jpg)



Figure 97 — Reference Load for AC Timing and Output Slew Rate


# 9.6 Overshoot and Undershoot Specifications

# 9.6.1 Address and Control Overshoot and Undershoot Specifications


Table 36 — AC Overshoot/Undershoot Specification for Address and Control Pins


<table><tr><td></td><td>DDR3-800</td><td>DDR3-1066</td><td>DDR3-1333</td><td>DDR3-1600</td><td>Units</td></tr><tr><td>Maximum peak amplitude allowed for overshoot area. (See Figure 98)</td><td>0.4</td><td>0.4</td><td>0.4</td><td>0.4</td><td>V</td></tr><tr><td>Maximum peak amplitude allowed for undershoot area. (See Figure 98)</td><td>0.4</td><td>0.4</td><td>0.4</td><td>0.4</td><td>V</td></tr><tr><td>Maximum overshoot area above VDD (See Figure 98)</td><td>0.67</td><td>0.5</td><td>0.4</td><td>0.33</td><td>V-ns</td></tr><tr><td>Maximum undershoot area below VSS (See Figure 98)</td><td>0.67</td><td>0.5</td><td>0.4</td><td>0.33</td><td>V-ns</td></tr><tr><td colspan="6">(A0-A15, BA0-BA3, CS#, RAS#, CAS#, WE#, CKE, ODT)</td></tr></table>

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/1b9d48536f5cd11188b7c2cef5d88e46959ea6fe49caea6fcdfdf443f71b2ab1.jpg)



Figure 98 — Address and Control Overshoot and Undershoot Definition


# 9.6.2 Clock, Data, Strobe and Mask Overshoot and Undershoot Specifications


Table 37 — AC Overshoot/Undershoot Specification for Clock, Data, Strobe and Mask


<table><tr><td></td><td>DDR3-800</td><td>DDR3-1066</td><td>DDR3-1333</td><td>DDR3-1600</td><td>Units</td></tr><tr><td>Maximum peak amplitude allowed for overshoot area. (See Figure 99)</td><td>0.4</td><td>0.4</td><td>0.4</td><td>0.4</td><td>V</td></tr><tr><td>Maximum peak amplitude allowed for undershoot area. (See Figure 99)</td><td>0.4</td><td>0.4</td><td>0.4</td><td>0.4</td><td>V</td></tr><tr><td>Maximum overshoot area above VDDQ (See Figure 99)</td><td>0.25</td><td>0.19</td><td>0.15</td><td>0.13</td><td>V-ns</td></tr><tr><td>Maximum undershoot area below VSSQ (See Figure 99)</td><td>0.25</td><td>0.19</td><td>0.15</td><td>0.13</td><td>V-ns</td></tr><tr><td colspan="6">(CK, CK#, DQ, DQS, DQS#, DM)</td></tr></table>

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/d84fe18b8ed9dd6d425f305e478d809185a70b31c3ccde979657cda5c32fcff2.jpg)



Figure 99 — Clock, Data, Strobe and Mask Overshoot and Undershoot Definition


# 9 AC and DC Output Measurement Levels (Cont’d)

# 9.7 34 ohm Output Driver DC Electrical Characteristics

A functional representation of the output buffer is shown in Figure 100. Output driver impedance RON is defined by the value of the external reference resistor RZQ as follows: 

$$
R O N _ {3 4} = R _ {Z Q} / 7 \left(\text {nominal} 34.3 \Omega \pm 10 \% \text {with nominal} R _ {Z Q} = 240 \Omega\right)
$$

The individual pull-up and pull-down resistors ( $R O N _ { \mathrm { P u } }$ and $R O N _ { \mathrm { P d } }$ ) are defined as follows: 

$$
R O N _ {P U} = \frac {V _ {D D Q} - V _ {O u t}}{\left| I _ {O u t} \right|} \quad \text {u n d e r t h e c o n d i t i o n t h a t R O N _ {P d} i s t u r n e d o f f} \tag {1}
$$

$$
R O N _ {P d} = \frac {V _ {O u t}}{| I _ {O u t} |} \quad \text {u n d e r t h e c o n d i t i o n t h a t} R O N _ {\mathrm {P u}} \text {i s t u r n e d o f f} \tag {2}
$$

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/dc87e7f6d0511eacf6a84d251d0cb0eb65c94982b520e28060504f0f82524125.jpg)



Figure 100 — Output Driver: Definition of Voltages and Currents


# 9 AC and DC Output Measurement Levels (Cont’d)

# 9.7 34 ohm Output Driver DC Electrical Characteristics (Cont’d)


Table 38 — Output Driver DC Electrical Characteristics, assuming $\pmb { R } _ { \mathrm { Z Q } } = 2 4 \mathbf { 0 } \Omega$ ; entire operating temperature range; after proper ZQ calibration


<table><tr><td>RONNom</td><td>Resistor</td><td>VOut</td><td>min</td><td>nom</td><td>max</td><td>Unit</td><td>Notes</td></tr><tr><td rowspan="6">34 Ω</td><td rowspan="3">RON34Pd</td><td>VOLdc = 0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.1</td><td>RZQ/7</td><td>1,2,3</td></tr><tr><td>VOMdc = 0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.1</td><td>RZQ/7</td><td>1,2,3</td></tr><tr><td>VOHdc = 0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.4</td><td>RZQ/7</td><td>1,2,3</td></tr><tr><td rowspan="3">RON34Pu</td><td>VOLdc = 0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.4</td><td>RZQ/7</td><td>1,2,3</td></tr><tr><td>VOMdc = 0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.1</td><td>RZQ/7</td><td>1,2,3</td></tr><tr><td>VOHdc = 0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.1</td><td>RZQ/7</td><td>1,2,3</td></tr><tr><td rowspan="6">40 Ω</td><td rowspan="3">RON40Pd</td><td>VOLdc = 0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.1</td><td>RZQ/6</td><td>1,2,3</td></tr><tr><td>VOMdc = 0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.1</td><td>RZQ/6</td><td>1,2,3</td></tr><tr><td>VOHdc = 0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.4</td><td>RZQ/6</td><td>1,2,3</td></tr><tr><td rowspan="3">RON40Pu</td><td>VOLdc = 0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.4</td><td>RZQ/6</td><td>1,2,3</td></tr><tr><td>VOMdc = 0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.1</td><td>RZQ/6</td><td>1,2,3</td></tr><tr><td>VOHdc = 0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.1</td><td>RZQ/6</td><td>1,2,3</td></tr><tr><td colspan="2">Mismatch between pull-up and pull-down, MMPuPd</td><td>VOMdc
0.5 × VDDQ</td><td>-10</td><td></td><td>+10</td><td>%</td><td>1,2,4</td></tr></table>


NOTE 1. The tolerance limits are specified after calibration with stable voltage and temperature. For the behavior of the tolerance limits if temperature or voltage changes after calibration, see following section on voltage and temperature sensitivity. 



NOTE 2. The tolerance limits are specified under the condition that $V _ { \mathrm { D D Q } } = V _ { \mathrm { D D } }$ and that $V _ { \mathrm { S S Q } } = V _ { \mathrm { S S } }$ 



NOTE 3. Pull-down and pull-up output driver impedances are recommended to be calibrated at $0 . 5 \times V _ { \mathrm { D D Q } }$ Other calibration schemes may be used to achieve the linearity spec shown above, e.g. calibration at $0 . 2 \times V _ { \mathrm { D D Q } }$ and $0 . 8 \times V _ { \mathrm { D D Q } }$ . 



NOTE 4. Measurement definition for mismatch between pull-up and pull-down, $M M _ { \mathrm { P u P d } }$ Measure $R O N _ { \mathrm { P u } }$ and $R O N _ { \mathrm { { P d } } }$ , both at $0 . 5 ^ { \ast } V _ { \mathrm { D D Q } }$ : 


$$
M M _ {P u P d} = \frac {R O N _ {P u} - R O N _ {P d}}{R O N _ {N o m}} x 1 0 0
$$

# 9.7.1 Output Driver Temperature and Voltage sensitivity

If temperature and/or voltage change after calibration, the tolerance limits widen according to Table 39 and Table 40. 

$$
\Delta \mathrm {T} = \mathrm {T} - \mathrm {T} (@ \text {c a l i b r a t i o n}); \Delta \mathrm {V} = \mathrm {V D D Q} - \mathrm {V D D Q} (@ \text {c a l i b r a t i o n}); \mathrm {V D D} = \mathrm {V D D Q}
$$

NOTE: $\mathrm { d R } _ { \mathrm { O N } } \mathrm { d T }$ and $\mathrm { d R } _ { \mathrm { O N } } \mathrm { d V }$ are not subject to production test but are verified by design and characterization. 

# 9.7 34 ohm Output Driver DC Electrical Characteristics (Cont’d)

# 9.7.1 Output Driver Temperature and Voltage sensitivity (Cont’d)


Table 39 — Output Driver Sensitivity Definition


<table><tr><td></td><td>min</td><td>max</td><td>unit</td></tr><tr><td>RONPU@ VOHdc</td><td>0.6 - dRONdTH*|DT| - dRONdVH*|DV|</td><td>1.1 + dRONdTH*|DT| + dRONdVH*|DV|</td><td>RZQ/7</td></tr><tr><td>RON@ VOMdc</td><td>0.9 - dRONdTM*|DT| - dRONdVM*|DV|</td><td>1.1 + dRONdTM*|DT| + dRONdVM*|DV|</td><td>RZQ/7</td></tr><tr><td>RONPD@ VOLdc</td><td>0.6 - dRONdTL*|DT| - dRONdVL*|DV|</td><td>1.1 + dRONdTL*|DT| + dRONdVL*|DV|</td><td>RZQ/7</td></tr></table>


Table 40 — Output Driver Voltage and Temperature Sensitivity


<table><tr><td>Speed Bin</td><td colspan="2">800/1066/1333</td><td colspan="2">1600</td><td></td></tr><tr><td></td><td>min</td><td>max</td><td>min</td><td>max</td><td>unit</td></tr><tr><td>dRONdTM</td><td>0</td><td>1.5</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVM</td><td>0</td><td>0.15</td><td>0</td><td>0.13</td><td>%/mV</td></tr><tr><td>dRONdTL</td><td>0</td><td>1.5</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVL</td><td>0</td><td>0.15</td><td>0</td><td>0.13</td><td>%/mV</td></tr><tr><td>dRONdTH</td><td>0</td><td>1.5</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVH</td><td>0</td><td>0.15</td><td>0</td><td>0.13</td><td>%/mV</td></tr></table>


These parameters may not be subject to production test. They are verified by design and characterization. 


# 9.8 On-Die Termination (ODT) Levels and I-V Characteristics

# 9.8.1 On-Die Termination (ODT) Levels and I-V Characteristics

On-Die Termination effective resistance RTT is defined by bits A9, A6 and A2 of the MR1 Register. 

ODT is applied to the DQ, DM, DQS/DQS# and TDQS/TDQS# (x8 devices only) pins. 

A functional representation of the on-die termination is shown in Figure 101. The individual pull-up and pull-down resistors $R T T _ { \mathrm { P u } }$ and $R T T _ { \mathrm { P d } }$ are defined as follows: 

$$
R T T _ {P u} = \frac {V _ {D D Q} - V _ {O u t}}{\left| I _ {O u t} \right|} \text {u n d e r t h e c o n d i t i o n t h a t R T T _ {P d} i s t u r n e d o f f} \tag {3}
$$

$$
R T T _ {P d} = \frac {V _ {O u t}}{\left| I _ {O u t} \right|} \text {u n d e r t h e c o n d i t i o n t h a t R T T _ {P u} i s t u r n e d o f f} \tag {4}
$$

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/90e204cbd0024a3d3b63d582d13adca32208d1e8a15d6aff4f015bc8cb8b9501.jpg)



IO_CTT_DEFINITION_01



Figure 101 — On-Die Termination: Definition of Voltages and Currents


# 9 AC and DC Output Measurement Levels (Cont’d)

# 9.8 On-Die Termination (ODT) Levels and I-V Characteristics (Cont’d)

# 9.8.2 ODT DC Electrical Characteristics

Table 41 provides an overview of the ODT DC electrical characteristics. The values for $R T T _ { \mathrm { 6 0 P d 1 } 2 0 }$ , $R T T _ { \mathrm { 6 0 P u l } 2 0 }$ , RTT120Pd240, $R T T _ { 1 2 0 \mathrm { P u } 2 4 0 }$ , $R T T _ { 4 0 \mathrm { P d } 8 0 }$ , RTT40Pu80, RTT30Pd60, RTT30Pu60 , RTT20Pd40, RTT20Pu40 are not specification requirements, but can be used as design guide lines: 


Table 41 — ODT DC Electrical Characteristics, assuming $ { R _ { \mathrm { Z Q } } } = 2 4 0 \Omega + / - 1 \%$ entire operating temperature range; after proper ZQ calibration


<table><tr><td>MR1 A9, A6, A2</td><td>RTT</td><td>Resistor</td><td>\(V_{\text{Out}}\)</td><td>min</td><td>nom</td><td>max</td><td>Unit</td><td>Notes</td></tr><tr><td rowspan="7">0, 1, 0</td><td rowspan="7">120 Ω</td><td rowspan="3">\(RTT_{120Pd240}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>0.5 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)0.8 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}}\)</td><td>1, 2, 3, 4,</td></tr><tr><td rowspan="3">\(RTT_{120Pu240}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>0.5 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)0.8 ×\(V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(RTT_{120}\)</td><td>\(V_{\text{IL(ac)}}\) to \(V_{\text{IH(ac)}}\)</td><td>0.9</td><td>1.00</td><td>1.6</td><td>\(R_{\text{ZQ}/2}\)</td><td>1, 2, 5,</td></tr><tr><td rowspan="7">0, 0, 1</td><td rowspan="7">60 Ω</td><td rowspan="3">\(RTT_{60Pd120}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/2}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>0.5 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/2}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)0.8 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}/2}\)</td><td>1, 2, 3, 4,</td></tr><tr><td rowspan="3">\(RTT_{60Pu120}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}/2}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>0.5 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/2}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\) 0.8 × \(V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/2}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(RTT_{60}\)</td><td>\(V_{\text{IL(ac)}}\) to \(V_{\text{IH(ac)}}\)</td><td>0.9</td><td>1.00</td><td>1.6</td><td>\(R_{\text{ZQ}/4}\)</td><td>1, 2, 5,</td></tr></table>

# 9.8 On-Die Termination (ODT) Levels and I-V Characteristics (Cont’d)

# 9.8.2 ODT DC Electrical Characteristics (Cont’d)


Table 41 — ODT DC Electrical Characteristics, assuming $\pmb { R } _ { \mathrm { Z Q } } = 2 4 \mathbf { 0 } ~ \Omega + / - 1 \%$ entire operating temperature range; after proper ZQ calibration (Cont’d)


<table><tr><td>MR1 A9, A6, A2</td><td>RTT</td><td>Resistor</td><td>\(V_{\text{Out}}\)</td><td>min</td><td>nom</td><td>max</td><td>Unit</td><td>Notes</td></tr><tr><td rowspan="7">0, 1, 1</td><td rowspan="7">40 Ω</td><td rowspan="3">\(RTT_{40Pd80}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/3}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(0.5 \times V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/3}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)0.8 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}/3}\)</td><td>1, 2, 3, 4,</td></tr><tr><td rowspan="3">\(RTT_{40Pu80}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}/3}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(0.5 \times V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/3}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)\(0.8 \times V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/3}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(RTT_{40}\)</td><td>\(V_{\text{IL(ac)}}\) to \(V_{\text{IH(ac)}}\)</td><td>0.9</td><td>1.00</td><td>1.6</td><td>\(R_{\text{ZQ}/6}\)</td><td>1, 2, 5,</td></tr><tr><td rowspan="7">1, 0, 1</td><td rowspan="7">30 Ω</td><td rowspan="3">\(RTT_{30Pd60}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/4}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(0.5 \times V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/4}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)0.8 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}/4}\)</td><td>1, 2, 3, 4,</td></tr><tr><td rowspan="3">\(RTT_{30Pu60}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}/4}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(0.5 \times V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/4}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)\(0.8 \times V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/4}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(RTT_{30}\)</td><td>\(V_{\text{IL(ac)}}\) to \(V_{\text{IH(ac)}}\)</td><td>0.9</td><td>1.00</td><td>1.6</td><td>\(R_{\text{ZQ}/8}\)</td><td>1, 2, 5,</td></tr><tr><td rowspan="7">1, 0, 0</td><td rowspan="7">20 Ω</td><td rowspan="3">\(RTT_{20Pd40}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/6}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(0.5 \times V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/6}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)0.8 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}/6}\)</td><td>1, 2, 3, 4,</td></tr><tr><td rowspan="3">\(RTT_{20Pu40}\)</td><td>\(V_{\text{OLdc}}\)0.2 × \(V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.4</td><td>\(R_{\text{ZQ}/6}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(0.5 \times V_{\text{DDQ}}\)</td><td>0.9</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/6}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(V_{\text{OHdc}}\)\(0.8 \times V_{\text{DDQ}}\)</td><td>0.6</td><td>1.00</td><td>1.1</td><td>\(R_{\text{ZQ}/6}\)</td><td>1, 2, 3, 4,</td></tr><tr><td>\(RTT_{20}\)</td><td>\(V_{\text{IL(ac)}}\) to \(V_{\text{IH(ac)}}\)</td><td>0.9</td><td>1.00</td><td>1.6</td><td>\(R_{\text{ZQ}/12}\)</td><td>1, 2, 5,</td></tr><tr><td colspan="4">Deviation of \(V_{\text{M w.r.t.}} V_{\text{DDQ}/2}, D V_{\text{M}}\)</td><td>-5</td><td></td><td>+5</td><td>%</td><td>1, 2, 5, 6,</td></tr></table>


NOTE 1. The tolerance limits are specified after calibration with stable voltage and temperature. For the behavior of the tolerance limits if temperature or voltage changes after calibration, see following section on voltage and temperature sensitivity. 



NOTE 2. The tolerance limits are specified under the condition that $V _ { \mathrm { D D Q } } = V _ { \mathrm { D D } }$ and that $V _ { \mathrm { S S Q } } = V _ { \mathrm { S S } }$ . 



NOTE 3. Pull-down and pull-up ODT resistors are recommended to be calibrated at $0 . 5 \times V _ { \mathrm { D D Q } }$ . Other calibration schemes may be used to achieve the linearity spec shown above, e.g. calibration at $0 . 2 \times V _ { \mathrm { D D Q } }$ and 0.8 × VDDQ. $0 . 8 \times V _ { \mathrm { D D Q } }$ 



NOTE 4. Not a specification requirement, but a design guide line. 


# 9.8 On-Die Termination (ODT) Levels and I-V Characteristics (Cont’d)

# 9.8.2 ODT DC Electrical Characteristics (Cont’d)

NOTE 5. Measurement definition for RTT: 

Apply $V _ { \mathrm { I H ( a c ) } }$ to pin under test and measure current $I ( V _ { \mathrm { I H ( a c ) } } )$ , then apply $V _ { \mathrm { I L ( a c ) } }$ to pin under test and measure current $I ( V _ { \mathrm { I L ( a c ) } } )$ respectively. 

$$
R T T = \frac {V _ {\mathrm {I H}} (\mathrm {a c}) - V _ {\mathrm {I L}} (\mathrm {a c})}{I (\mathrm {V I H} (\mathrm {a c})) - I (\mathrm {V I L} (\mathrm {a c}))}
$$

NOTE 6. Measurement definition for $V _ { \mathbf { M } }$ and $\mathrm { D } V _ { \mathrm { M } }$ 

Measure voltage $ { { \cal V } } _ { \mathrm { M } } )$ at test pin (midpoint) with no load: 

$$
\Delta V _ {M} = \left(\frac {2 \times V _ {M}}{V _ {D D Q}} - 1\right) \times 1 0 0
$$

# 9 AC and DC Output Measurement Levels (Cont’d)

# 9.8 On-Die Termination (ODT) Levels and I-V Characteristics (Cont’d)

# 9.8.3 ODT Temperature and Voltage sensitivity

If temperature and/or voltage change after calibration, the tolerance limits widen according to Table 42 and Table 43. 

$$
\mathrm {D T} = \mathrm {T} - \mathrm {T} (@ \text {c a l i b r a t i o n}); \mathrm {D V} = \mathrm {V D D Q} - \mathrm {V D D Q} (@ \text {c a l i b r a t i o n}); \mathrm {V D D} = \mathrm {V D D Q}
$$


Table 42 — ODT Sensitivity Definition


<table><tr><td></td><td>min</td><td>max</td><td>unit</td></tr><tr><td>RTT</td><td>0.9 - dRTdT*|ΔT| - dRTdTV*|ΔV|</td><td>1.6 + dRTdT*|ΔT| + dRTdTV*|ΔV|</td><td>RZQ/2,4,6,8,12</td></tr></table>


Table 43 — ODT Voltage and Temperature Sensitivity


<table><tr><td></td><td>min</td><td>max</td><td>unit</td></tr><tr><td>dRTTdT</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRTTdV</td><td>0</td><td>0.15</td><td>%/mV</td></tr></table>

These parameters may not be subject to production test. They are verified by design and characterization 

# 9.9 ODT Timing Definitions

# 9.9.1 Test Load for ODT Timings

Different than for timing measurements, the reference load for ODT timings is defined in Figure 102. 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/0a50525c9b3bf1add3d9d57f9f0d59d9d8084d07730b4835518786d5cd0d8300.jpg)



Figure 102: ODT Timing Reference Load


# 9 AC and DC Output Measurement Levels (Cont’d)

# 9.9 ODT Timing Definitions (Cont’d)

# 9.9.2 ODT Timing Definitions

Definitions for tAON, tAONPD, tAOF, tAOFPD and $t _ { \mathrm { A D C } }$ are provided in Table 44 and subsequent figures. Measurement reference settings are provided in Table 45. 


Table 44 — ODT Timing Definitions


<table><tr><td>Symbol</td><td>Begin Point Definition</td><td>End Point Definition</td><td>Figure</td></tr><tr><td>tAON</td><td>Rising edge of CK - CK# defined by the end point of ODTLon</td><td>Extrapolated point at VSSQ</td><td>Figure 103</td></tr><tr><td>tAONPD</td><td>Rising edge of CK - CK# with ODT being first registered high</td><td>Extrapolated point at VSSQ</td><td>Figure 104</td></tr><tr><td>tAOF</td><td>Rising edge of CK - CK#defined by the end point of ODTLoff</td><td>End point: Extrapolated point at VRTT_Nom</td><td>Figure 105</td></tr><tr><td>tAOFPD</td><td>Rising edge of CK - CK# with ODT being first registered low</td><td>End point: Extrapolated point at VRTT_Nom</td><td>Figure 106</td></tr><tr><td>tADC</td><td>Rising edge of CK - CK# defined by the end point of ODTLcnw, ODTLcwn4 or ODTLcwn8</td><td>End point: Extrapolated point at VRTT_Wr and VRTT_Nom respectively</td><td>Figure 107</td></tr></table>


Table 45 — Reference Settings for ODT Timing Measurements


<table><tr><td>Measured Parameter</td><td>RTT_Nom Setting</td><td>RTT_Wr Setting</td><td>\(V_{\text{SW1}} [V]\)</td><td>\(V_{\text{SW2}} [V]\)</td><td>Note</td></tr><tr><td rowspan="2">\(t_{\text{AON}}\)</td><td>\(R_{\text{ZQ}}/4\)</td><td>NA</td><td>0.05</td><td>0.10</td><td></td></tr><tr><td>\(R_{\text{ZQ}}/12\)</td><td>NA</td><td>0.10</td><td>0.20</td><td></td></tr><tr><td rowspan="2">\(t_{\text{AONPD}}\)</td><td>\(R_{\text{ZQ}}/4\)</td><td>NA</td><td>0.05</td><td>0.10</td><td></td></tr><tr><td>\(R_{\text{ZQ}}/12\)</td><td>NA</td><td>0.10</td><td>0.20</td><td></td></tr><tr><td rowspan="2">\(t_{\text{AOF}}\)</td><td>\(R_{\text{ZQ}}/4\)</td><td>NA</td><td>0.05</td><td>0.10</td><td></td></tr><tr><td>\(R_{\text{ZQ}}/12\)</td><td>NA</td><td>0.10</td><td>0.20</td><td></td></tr><tr><td rowspan="2">\(t_{\text{AOFPD}}\)</td><td>\(R_{\text{ZQ}}/4\)</td><td>NA</td><td>0.05</td><td>0.10</td><td></td></tr><tr><td>\(R_{\text{ZQ}}/12\)</td><td>NA</td><td>0.10</td><td>0.20</td><td></td></tr><tr><td>\(t_{\text{ADC}}\)</td><td>\(R_{\text{ZQ}}/12\)</td><td>\(R_{\text{ZQ}}/2\)</td><td>0.20</td><td>0.30</td><td></td></tr></table>

# 9.9 ODT Timing Definitions (Cont’d)

# 9.9.2 ODT Timing Definitions (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e78f82b5241dfde0049f0eae4f402bb6a1bb4ff7de1ae25d4460075342c770b2.jpg)



Figure 103 — Definition of tAON


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/fa721154e68d05dbe2c29e817c04f56e54b8b7f34a63785da8515752af54ed3a.jpg)



Figure 104 — Definition of tAONPD


# 9.9 ODT Timing Definitions (Cont’d)

# 9.9.2 ODT Timing Definitions (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/f8765a2f5df501a137edff06b75497739035af48a41fdb4b9dd7e9f0328ee192.jpg)



Figure 105 — Definition of tAOF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/349ab803904ba37b555ae2fc5e4b0a7479f3d936c9530f854fb2b13ac332ce34.jpg)



Figure 106 — Definition of tAOFPD


# 9.9 ODT Timing Definitions (Cont’d)

# 9.9.2 ODT Timing Definitions (Cont’d)

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/0aaa797b0cbc32b503a8265819cb98fc94a39508af834dcbc27e876e78337dfb.jpg)



Figure 107 — Definition of tADC


# 10 IDD and IDDQ Specification Parameters and Test Conditions

# 10.1 IDD and IDDQ Measurement Conditions

In this chapter, IDD and IDDQ measurement conditions such as test load and patterns are defined. Figure 108 shows the setup and test load for IDD and IDDQ measurements. 

• IDD currents (such as IDD0, IDD1, IDD2N, IDD2NT, IDD2P0, IDD2P1, IDD2Q, IDD3N, IDD3P, IDD4R, IDD4W, IDD5B, IDD6, IDD6ET, IDD6TC and IDD7) are measured as time-averaged currents with all VDD balls of the DDR3 SDRAM under test tied together. Any IDDQ current is not included in IDD currents. 

IDDQ currents (such as IDDQ2NT and IDDQ4R) are measured as time-averaged currents with all VDDQ balls of the DDR3 SDRAM under test tied together. Any IDD current is not included in IDDQ currents. 

Attention: IDDQ values cannot be directly used to calculate IO power of the DDR3 SDRAM. They can be used to support correlation of simulated IO power to actual IO power as outlined in Figure 109. In DRAM module application, IDDQ cannot be measured separately since VDD and VDDQ are using one merged-power layer in Module PCB. 

# For IDD and IDDQ measurements, the following definitions apply:

• “0” and “LOW” is defined as $\mathrm { V I N } \mathrm { < = V I L A C ( m a x ) . }$ . 

• “1” and “HIGH” is defined as $\mathrm { { V I N } > = \mathrm { { V I H A C } ( m i n ) } }$ 

• “MID-LEVEL” is defined as inputs are $\mathrm { V R E F } = \mathrm { V D D } / 2$ 

• Timings used for IDD and IDDQ Measurement-Loop Patterns are provided in Table 46 on page 141. 

• Basic IDD and IDDQ Measurement Conditions are described in Table 47 on page 141. 

• Detailed IDD and IDDQ Measurement-Loop Patterns are described in Table 48 on page 144 through Table 55 on page 149. 

• IDD Measurements are done after properly initializing the DDR3 SDRAM. This includes but is not limited to setting 

$\mathrm { R O N } = \mathrm { R Z Q } / 7$ (34 Ohm in MR1); 

Qoff $= 0 _ { \mathrm { B } }$ (Output Buffer enabled in MR1); 

RTT_ $\mathrm { N o m } = \mathrm { R Z Q } / 6$ (40 Ohm in MR1); 

RTT_ $\mathrm { W r } = \mathrm { R Z Q } / 2$ (120 Ohm in MR2); 

TDQS Feature disabled in MR1 

• Attention: The IDD and IDDQ Measurement-Loop Patterns need to be executed at least one time before actual IDD or IDDQ measurement is started. 

• Define $\mathrm { ~ D ~ } = \{ { \mathrm { C S } } \# _ { \mathrm { \scriptsize { 2 } } }$ , RAS#, CAS#, WE# $\beta : = \{ \mathrm { H I G H }$ , LOW, LOW, LOW} 

• Define $\mathrm { D } \# = \{ \mathrm { C S } \#$ , RAS#, CAS#, WE# } : $: =$ {HIGH, HIGH, HIGH, HIGH} 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/e7e7fc0b49d85d3aa8c5197bbe619f8410b3053b1c2408a9a159b4c1e56061ad.jpg)



NOTE: DIMM level Output test load condition may be different from above.



Figure 108 — Measurement Setup and Test Load for IDD and IDDQ (optional) Measurements


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/8c170477-75f9-4268-b689-6c10ca114214/a5f026389d706ccc56bddf3d182f506c635a2cb6174e91b58e77f993701fb97a.jpg)



Figure 109 — Correlation from simulated Channel IO Power to actual Channel IO Power supported by IDDQ Measurement.


# 10 IDD and IDDQ Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 46 — Timings used for IDD and IDDQ Measurement-Loop Patterns


<table><tr><td rowspan="2" colspan="2">Symbol</td><td colspan="2">DDR3-800</td><td colspan="3">DDR3-1066</td><td colspan="4">DDR3-1333</td><td colspan="4">DDR3-1600</td><td rowspan="2">Unit</td></tr><tr><td>5-5-5</td><td>6-6-6</td><td>6-6-6</td><td>7-7-7</td><td>8-8-8</td><td>7-7-7</td><td>8-8-8</td><td>9-9-9</td><td>10-10-10</td><td>8-8-8</td><td>9-9-9</td><td>10-10-10</td><td>11-11-11</td></tr><tr><td colspan="2">tCK</td><td colspan="2">2.5</td><td colspan="3">1.875</td><td colspan="4">1.5</td><td colspan="4">1.25</td><td>ns</td></tr><tr><td colspan="2">CL</td><td>5</td><td>6</td><td>6</td><td>7</td><td>8</td><td>7</td><td>8</td><td>9</td><td>10</td><td>8</td><td>9</td><td>10</td><td>11</td><td>nCK</td></tr><tr><td colspan="2">nRCD</td><td>5</td><td>6</td><td>6</td><td>7</td><td>8</td><td>7</td><td>8</td><td>9</td><td>10</td><td>8</td><td>9</td><td>10</td><td>11</td><td>nCK</td></tr><tr><td colspan="2">nRC</td><td>20</td><td>21</td><td>26</td><td>27</td><td>28</td><td>31</td><td>32</td><td>33</td><td>34</td><td>36</td><td>37</td><td>38</td><td>39</td><td>nCK</td></tr><tr><td colspan="2">nRAS</td><td colspan="2">15</td><td colspan="3">20</td><td colspan="4">24</td><td colspan="4">28</td><td>nCK</td></tr><tr><td colspan="2">nRP</td><td>5</td><td>6</td><td>6</td><td>7</td><td>8</td><td>7</td><td>8</td><td>9</td><td>10</td><td>8</td><td>9</td><td>10</td><td>11</td><td>nCK</td></tr><tr><td rowspan="2">nFAW</td><td>1KB page size</td><td colspan="2">16</td><td colspan="3">20</td><td colspan="4">20</td><td colspan="4">24</td><td>nCK</td></tr><tr><td>2KB page size</td><td colspan="2">20</td><td colspan="3">27</td><td colspan="4">30</td><td colspan="4">32</td><td>nCK</td></tr><tr><td rowspan="2">nRRD</td><td>1KB page size</td><td colspan="2">4</td><td colspan="3">4</td><td colspan="4">4</td><td colspan="4">5</td><td>nCK</td></tr><tr><td>2KB page size</td><td colspan="2">4</td><td colspan="3">6</td><td colspan="4">5</td><td colspan="4">6</td><td>nCK</td></tr><tr><td colspan="2">nRFC 512 Mb</td><td colspan="2">36</td><td colspan="3">48</td><td colspan="4">60</td><td colspan="4">72</td><td>nCK</td></tr><tr><td colspan="2">nRFC 1 Gb</td><td colspan="2">44</td><td colspan="3">59</td><td colspan="4">74</td><td colspan="4">88</td><td>nCK</td></tr><tr><td colspan="2">nRFC 2 Gb</td><td colspan="2">64</td><td colspan="3">86</td><td colspan="4">107</td><td colspan="4">128</td><td>nCK</td></tr><tr><td colspan="2">nRFC 4 Gb</td><td colspan="2">120</td><td colspan="3">160</td><td colspan="4">200</td><td colspan="4">240</td><td>nCK</td></tr><tr><td colspan="2">nRFC 8 Gb</td><td colspan="2">140</td><td colspan="3">187</td><td colspan="4">234</td><td colspan="4">280</td><td>nCK</td></tr></table>


Table 47 — Basic IDD and IDDQ Measurement Conditions


<table><tr><td>Symbol</td><td>Description</td></tr><tr><td>IDD0</td><td>Operating One Bank Active-Precharge Current
CKE: High; External clock: On; tCK, nRC, nRAS, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: High between ACT and PRE; Command, Address, Bank Address Inputs: partially toggling according to Table 48 on page 144; Data IO: MID-LEVEL; DM:stable at 0; Bank Activity: Cycling with one bank active at a time: 0,0,1,1,2,2,... (see Table 48 on page 144); Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0; Pattern Details: see Table 48 on page 144</td></tr><tr><td>IDD1</td><td>Operating One Bank Active-Read-Precharge Current
CKE: High; External clock: On; tCK, nRC, nRAS, nRCD, CL: see Table 46 on page 141; BL: 8(1,7); AL: 0; CS#: High between ACT, RD and PRE; Command, Address, Bank Address Inputs, Data IO: partially toggling according to Table 49 on page 145; DM:stable at 0; Bank Activity: Cycling with one bank active at a time: 0,0,1,1,2,2,... (see Table 49 on page 145); Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0; Pattern Details: see Table 49 on page 145</td></tr><tr><td>IDD2N</td><td>Precharge Standby Current
CKE: High; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: stable at 1; Command, Address, Bank Address Inputs: partially toggling according to Table 50 on page 146; Data IO: MID-LEVEL; DM:stable at 0; Bank Activity: all banks closed; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0; Pattern Details: see Table 50 on page 146</td></tr><tr><td>IDD2NT</td><td>Precharge Standby ODT Current
CKE: High; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: stable at 1; Command, Address, Bank Address Inputs: partially toggling according to Table 51 on page 146; Data IO: MID-LEVEL; DM:stable at 0; Bank Activity: all banks closed; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: toggling according to Table 51 on page 146; Pattern Details: see Table 51 on page 146</td></tr><tr><td>IDDQ2NT
(optional)</td><td>Precharge Standby ODT IDDQ Current
Same definition like for IDD2NT, however measuring IDDQ current instead of IDD current</td></tr></table>

# 10 IDD and IDDQ Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 47 — Basic IDD and IDDQ Measurement Conditions


<table><tr><td>Symbol</td><td>Description</td></tr><tr><td>IDD2P0</td><td>Precharge Power-Down Current Slow ExitCKE: Low; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: stable at 1;Command, Address, Bank Address Inputs: stable at 0; Data IO: MID-LEVEL; DM:stable at 0; Bank Activity: all banks closed; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0; Pecharge Power Down Mode: Slow Exit(3)</td></tr><tr><td>IDD2P1</td><td>Precharge Power-Down Current Fast ExitCKE: Low; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: stable at 1;Command, Address, Bank Address Inputs: stable at 0; Data IO: MID-LEVEL; DM:stable at 0; Bank Activity: all banks closed; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stableat 0; Pecharge Power Down Mode: Fast Exit(3)</td></tr><tr><td>IDD2Q</td><td>Precharge Quiet Standby CurrentCKE: High; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: stable at 1;Command, Address, Bank Address Inputs: stable at 0; Data IO: MID-LEVEL; DM:stable at 0; Bank Activity: all banks closed; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0</td></tr><tr><td>IDD3N</td><td>Active Standby CurrentCKE: High; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: stable at 1;Command, Address, Bank Address Inputs: partially toggling according to Table 50 on page 146; Data IO: MID-LEVEL; DM:stable at 0; Bank Activity: all banks open; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0; Pattern Details: see Table 50 on page 146</td></tr><tr><td>IDD3P</td><td>Active Power-Down CurrentCKE: Low; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: stable at 1;Command, Address, Bank Address Inputs: stable at 0; Data IO: MID-LEVEL;DM:stable at 0; Bank Activity: all banks open; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0</td></tr><tr><td>IDD4R</td><td>Operating Burst Read CurrentCKE: High; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1,7); AL: 0; CS#: High between RD; Command, Address, Bank Address Inputs: partially toggling according to Table 52 on page 147;Data IO: seamless read data burst with different data between one burst and the next one according to Table 52 on page 147; DM:stable at 0; Bank Activity: all banks open, RD commands cycling through banks: 0,0,1,1,2,2,... (see Table 52 on page 147); Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0; Pattern Details: see Table 52 on page 147</td></tr><tr><td>IDDQ4R(optional)</td><td>Operating Burst Read IDDQ CurrentSame definition like for IDD4R, however measuring IDDQ current instead of IDD current</td></tr><tr><td>IDD4W</td><td>Operating Burst Write CurrentCKE: High; External clock: On; tCK, CL: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: High between WR; Command, Address, Bank Address Inputs: partially toggling according to Table 53 on page 147;Data IO: seamless write data burst with different data between one burst and the next one according to Table 53 on page 147; DM:stable at 0; Bank Activity: all banks open, WR commands cycling through banks: 0,0,1,1,2,2,... (see Table 53 on page 147); Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at HIGH; Pattern Details: see Table 53 on page 147</td></tr><tr><td>IDD5B</td><td>Burst Refresh CurrentCKE: High; External clock: On; tCK, CL, nRFC: see Table 46 on page 141; BL: 8(1); AL: 0; CS#: High between REF; Command, Address, Bank Address Inputs: partially toggling according to Table 54 on page 148; Data IO: MID-LEVEL;DM:stable at 0; Bank Activity: REF command every nRFC (see Table 54 on page 148); Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0; Pattern Details: see Table 54 on page 148</td></tr><tr><td>IDD6</td><td>Self Refresh Current: Normal Temperature RangeTCASE: 0 - 85°C; Auto Self-Refresh (ASR): Disabled(4); Self-Refresh Temperature Range (SRT):Normal(5); CKE: Low; External clock: Off; CK and CCK#: LOW; CL: see Table 46 on page 141; BL: 8(1);AL: 0; CS#, Command, Address, Bank Address, Data IO: MID-LEVEL;DM:stable at 0; Bank Activity: Self-Refresh operation; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: MID-LEVEL</td></tr></table>

# 10 IDD and IDDQ Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 47 — Basic IDD and IDDQ Measurement Conditions


<table><tr><td>Symbol</td><td>Description</td></tr><tr><td>IDD6ET</td><td>Self-Refresh Current: Extended Temperature Range (optional)(6)TCASE: 0 - 95°C; Auto Self-Refresh (ASR): Disabled(4); Self-Refresh Temperature Range (SRT):Extended(5); CKE: Low; External clock: Off; CK and CK#: LOW; CL: see Table 46 on page 141; BL: 8(1);AL: 0; CS#, Command, Address, Bank Address, Data IO: MID-LEVEL;DM:stable at 0; Bank Activity: Extended Temperature Self-Refresh operation; Output Buffer and RTT: Enabled in Mode Registers(2);ODT Signal: MID-LEVEL</td></tr><tr><td>IDD6TC</td><td>Auto Self-Refresh Current (optional)(6)TCASE: 0 - 95°C; Auto Self-Refresh (ASR): Enabled(4); Self-Refresh Temperature Range (SRT):Normal(5); CKE: Low; External clock: Off; CK and CK#: LOW; CL: see Table 46 on page 141; BL: 8(1);AL: 0; CS#, Command, Address, Bank Address, Data IO: MID-LEVEL; DM:stable at 0; Bank Activity: Auto Self-Refresh operation; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: MID-LEVEL</td></tr><tr><td>IDD7</td><td>Operating Bank Interleave Read CurrentCKE: High; External clock: On; tCK, nRC, nRAS, nRCD, nRRD, nFAW, CL: see Table 46 on page 141; BL: 8(1,7); AL: CL-1; CS#: High between ACT and RDA; Command, Address, Bank Address Inputs: partially toggling according to Table 55 on page 149; Data IO: read data bursts with different data between one burst and the next one according to Table 55 on page 149; DM:stable at 0; Bank Activity: two times interleaved cycling through banks (0, 1, ...7) with different addressing, see Table 55 on page 149; Output Buffer and RTT: Enabled in Mode Registers(2); ODT Signal: stable at 0; Pattern Details: see Table 55 on page 149</td></tr><tr><td>IDD8 (Optional)</td><td>RESET Low CurrentRESET: LOW; External clock: Off; CK and CK#: LOW; CKE: FLOATING; CS#, Command, Address, Bank Address, Data IO: FLOATING; ODT Signal: FLOATINGRESET Low current reading is valid once power is stable and RESET has been LOW for at least 1ms.</td></tr><tr><td colspan="2">NOTE 1. Burst Length: BL8 fixed by MRS: set MR0 A[1,0]=00BNOTE 2. Output Buffer Enable: set MR1 A[12] = 0B; set MR1 A[5,1] = 01B; RTT_Nom enable: setMR1 A[9,6,2] = 011B; RTT_Wr enable: set MR2 A[10,9] = 10BNOTE 3. Pcharge Power Down Mode: set MR0 A12=0B for Slow Exit or MR0 A12=1B for Fast ExitNOTE 4. Auto Self-Refresh (ASR): set MR2 A6 = 0B to disable or 1B to enable featureNOTE 5. Self-Refresh Temperature Range (SRT): set MR2 A7=0B for normal or 1B for extended temperature rangeNOTE 6. Refer to DRAM supplier data sheet and/or DIMM SPD to determine if optional features or requirements are supported by DDR3 SDRAM deviceNOTE 7. Read Burst Type: Nibble Sequential, set MR0 A[3] = 0B</td></tr></table>

# 10 IDD and IDDQ Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 48 — IDD0 Measurement-Loop Pattern1


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="19">toggling</td><td rowspan="19">Static High</td><td rowspan="12">0</td><td>0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1, 2</td><td>D, D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3, 4</td><td>D#, D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat pattern 1...4 until nRAS - 1, truncate if necessary</td></tr><tr><td>nRAS</td><td>PRE</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat pattern 1...4 until nRC - 1, truncate if necessary</td></tr><tr><td>1*nRC + 0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1*nRC + 1, 2</td><td>D, D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1*nRC + 3, 4</td><td>D#, D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat pattern nRC + 1,..., 4 until 1*nRC + nRAS - 1, truncate if necessary</td></tr><tr><td>1*nRC + nRAS</td><td>PRE</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat nRC + 1,..., 4 until 2*nRC - 1, truncate if necessary</td></tr><tr><td>1</td><td>2*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 1 instead</td></tr><tr><td>2</td><td>4*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 2 instead</td></tr><tr><td>3</td><td>6*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 3 instead</td></tr><tr><td>4</td><td>8*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 4 instead</td></tr><tr><td>5</td><td>10*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 5 instead</td></tr><tr><td>6</td><td>12*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 6 instead</td></tr><tr><td>7</td><td>14*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 7 instead</td></tr></table>


NOTE: 



1.DM must be driven LOW all the time. DQS, DQS# are MID-LEVEL. 



2.DQ signals are MID-LEVEL. 


# 10 IDD Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 49 — IDD1 Measurement-Loop Pattern1


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="23">toggling</td><td rowspan="23">Static High</td><td rowspan="16">0</td><td>0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1, 2</td><td>D, D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3,4</td><td>D#, D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat pattern 1...4 until nRCD - 1, truncate if necessary</td></tr><tr><td>nRCD</td><td>RD</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td>...</td><td colspan="13">repeat pattern 1...4 until nRAS - 1, truncate if necessary</td></tr><tr><td>nRAS</td><td>PRE</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat pattern 1...4 until nRC - 1, truncate if necessary</td></tr><tr><td>1*nRC + 0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1*nRC + 1, 2</td><td>D, D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1*nRC + 3, 4</td><td>D#, D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat pattern nRC + 1,..., 4 until nRC + nRCD - 1, truncate if necessary</td></tr><tr><td>1*nRC + nRCD</td><td>RD</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td>...</td><td colspan="13">repeat pattern nRC + 1,..., 4 until nRC +nRAS - 1, truncate if necessary</td></tr><tr><td>1*nRC + nRAS</td><td>PRE</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat pattern nRC + 1,..., 4 until 2 * nRC - 1, truncate if necessary</td></tr><tr><td>1</td><td>2*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 1 instead</td></tr><tr><td>2</td><td>4*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 2 instead</td></tr><tr><td>3</td><td>6*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 3 instead</td></tr><tr><td>4</td><td>8*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 4 instead</td></tr><tr><td>5</td><td>10*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 5 instead</td></tr><tr><td>6</td><td>12*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 6 instead</td></tr><tr><td>7</td><td>14*nRC</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 7 instead</td></tr></table>


NOTE: 



1. DM must be driven LOW all the time. DQS, DQS# are used according to RD Commands, otherwise MID-LEVEL. 



2.Burst Sequence driven on each DQ signal by Read Command. Outside burst operation, DQ signals are MID-LEVEL. 


# 10 IDD Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 50 — IDD2N and IDD3N Measurement-Loop Pattern1


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="11">toggling</td><td rowspan="11">Static High</td><td rowspan="4">0</td><td>0</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1</td><td>4-7</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 1 instead</td></tr><tr><td>2</td><td>8-11</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 2 instead</td></tr><tr><td>3</td><td>12-15</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 3 instead</td></tr><tr><td>4</td><td>16-19</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 4 instead</td></tr><tr><td>5</td><td>20-23</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 5 instead</td></tr><tr><td>6</td><td>24-27</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 6 instead</td></tr><tr><td>7</td><td>28-31</td><td colspan="13">repeat Sub-Loop 0, use BA[2:0] = 7 instead</td></tr></table>


NOTE: 



1.DM must be driven LOW all the time. DQS, DQS# are MID-LEVEL. 



2.DQ signals are MID-LEVEL. 



Table 51 — IDD2NT and IDDQ2NT Measurement-Loop Pattern1


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="11">toggling</td><td rowspan="11">Static High</td><td rowspan="4">0</td><td>0</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1</td><td>4-7</td><td colspan="13">repeat Sub-Loop 0, but ODT = 0 and BA[2:0] = 1</td></tr><tr><td>2</td><td>8-11</td><td colspan="13">repeat Sub-Loop 0, but ODT = 1 and BA[2:0] = 2</td></tr><tr><td>3</td><td>12-15</td><td colspan="13">repeat Sub-Loop 0, but ODT = 1 and BA[2:0] = 3</td></tr><tr><td>4</td><td>16-19</td><td colspan="13">repeat Sub-Loop 0, but ODT = 0 and BA[2:0] = 4</td></tr><tr><td>5</td><td>20-23</td><td colspan="13">repeat Sub-Loop 0, but ODT = 0 and BA[2:0] = 5</td></tr><tr><td>6</td><td>24-27</td><td colspan="13">repeat Sub-Loop 0, but ODT = 1 and BA[2:0] = 6</td></tr><tr><td>7</td><td>28-31</td><td colspan="13">repeat Sub-Loop 0, but ODT = 1 and BA[2:0] = 7</td></tr></table>


NOTE: 



1.DM must be driven LOW all the time. DQS, DQS# are MID-LEVEL. 



2.DQ signals are MID-LEVEL. 


# 10 IDD Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 52 — IDD4R and IDDQ4R Measurement-Loop Pattern1


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="13">toggling</td><td rowspan="13">Static High</td><td rowspan="6">0</td><td>0</td><td>RD</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2, 3</td><td>D#,D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>4</td><td>RD</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td>5</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>6, 7</td><td>D#,D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1</td><td>8-15</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 1</td></tr><tr><td>2</td><td>16-23</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 2</td></tr><tr><td>3</td><td>24-31</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 3</td></tr><tr><td>4</td><td>32-39</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 4</td></tr><tr><td>5</td><td>40-47</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 5</td></tr><tr><td>6</td><td>48-55</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 6</td></tr><tr><td>7</td><td>56-63</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 7</td></tr></table>


NOTE: 



1.DM must be driven LOW all the time. DQS, DQS# are used according to RD Commands, otherwise MID-LEVEL. 



2.Burst Sequence driven on each DQ signal by Read Command. Outside burst operation, DQ signals are MID-LEVEL. 



Table 53 — IDD4W Measurement-Loop Pattern1


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="13">toggling</td><td rowspan="13">Static High</td><td rowspan="6">0</td><td>0</td><td>WR</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2, 3</td><td>D#,D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>4</td><td>WR</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td>5</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>6, 7</td><td>D#,D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1</td><td>8-15</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 1</td></tr><tr><td>2</td><td>16-23</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 2</td></tr><tr><td>3</td><td>24-31</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 3</td></tr><tr><td>4</td><td>32-39</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 4</td></tr><tr><td>5</td><td>40-47</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 5</td></tr><tr><td>6</td><td>48-55</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 6</td></tr><tr><td>7</td><td>56-63</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 7</td></tr></table>


NOTE: 



1.DM must be driven LOW all the time. DQS, DQS# are used according to WR Commands, otherwise MID-LEVEL. 



2.Burst Sequence driven on each DQ signal by Write Command. Outside burst operation, DQ signals are MID-LEVEL. 


# 10 IDD Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 54 — IDD5B Measurement-Loop Pattern1


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="11">toggling</td><td rowspan="11">Static High</td><td>0</td><td>0</td><td>REF</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td rowspan="9">1</td><td>1, 2</td><td>D, D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3, 4</td><td>D#, D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>5...8</td><td colspan="13">repeat cycles 1...4, but BA[2:0] = 1</td></tr><tr><td>9...12</td><td colspan="13">repeat cycles 1...4, but BA[2:0] = 2</td></tr><tr><td>13...16</td><td colspan="13">repeat cycles 1...4, but BA[2:0] = 3</td></tr><tr><td>17...20</td><td colspan="13">repeat cycles 1...4, but BA[2:0] = 4</td></tr><tr><td>21...24</td><td colspan="13">repeat cycles 1...4, but BA[2:0] = 5</td></tr><tr><td>25...28</td><td colspan="13">repeat cycles 1...4, but BA[2:0] = 6</td></tr><tr><td>29...32</td><td colspan="13">repeat cycles 1...4, but BA[2:0] = 7</td></tr><tr><td>2</td><td>33 ... nRFC - 1</td><td colspan="13">repeat Sub-Loop 1, until nRFC - 1. Truncate, if necessary.</td></tr></table>


NOTE: 



1.DM must be driven Low all the time. DQS, DQS# are MID-LEVEL. 



2.DQ signals are MID-LEVEL. 


# 10 IDD Specification Parameters and Test Conditions (Cont’d)

# 10.1 IDD and IDDQ Measurement Conditions (Cont’d)


Table 55 — IDD7 Measurement-Loop Pattern1


ATTENTION: Sub-Loops 10-19 have inverse A[6:3] Pattern and Data Pattern than Sub-Loops 0-9 

<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="36">toggling</td><td rowspan="36">Static High</td><td rowspan="4">0</td><td>0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1</td><td>RDA</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>00</td><td>1</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td>2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat above D Command until nRRD - 1</td></tr><tr><td rowspan="4">1</td><td>nRRD</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRRD + 1</td><td>RDA</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>00</td><td>1</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td>nRRD + 2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>...</td><td colspan="13">repeat above D Command until 2 * nRRD -1</td></tr><tr><td>2</td><td>2 * nRRD</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 2</td></tr><tr><td>3</td><td>3 * nRRD</td><td colspan="13">repeat Sub-Loop 1, but BA[2:0] = 3</td></tr><tr><td rowspan="2">4</td><td rowspan="2">4 * nRRD</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>3</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td colspan="13">Assert and repeat above D Command until nFAW - 1, if necessary</td></tr><tr><td>5</td><td>nFAW</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 4</td></tr><tr><td>6</td><td>nFAW+nRRD</td><td colspan="13">repeat Sub-Loop 1, but BA[2:0] = 5</td></tr><tr><td>7</td><td>nFAW+2*nRRD</td><td colspan="13">repeat Sub-Loop 0, but BA[2:0] = 6</td></tr><tr><td>8</td><td>nFAW+3*nRRD</td><td colspan="13">repeat Sub-Loop 1, but BA[2:0] = 7</td></tr><tr><td rowspan="2">9</td><td rowspan="2">nFAW+4*nRRD</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>7</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td colspan="13">Assert and repeat above D Command until 2 * nFAW - 1, if necessary</td></tr><tr><td rowspan="4">10</td><td>2*nFAW+0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>2*nFAW+1</td><td>RDA</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>00</td><td>1</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td rowspan="2">2*nFAW+2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td colspan="13">Repeat above D Command until 2 * nFAW + nRRD - 1</td></tr><tr><td rowspan="4">11</td><td>2*nFAW+nRRD</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2*nFAW+nRRD+1</td><td>RDA</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>00</td><td>1</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td rowspan="2">2*nFAW+nRRD+2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td colspan="13">repeat above D Command until 2 * nFAW + 2 * nRRD -1</td></tr><tr><td>12</td><td>2*nFAW+2*nRRD</td><td colspan="13">repeat Sub-Loop 10, but BA[2:0] = 2</td></tr><tr><td>13</td><td>2*nFAW+3*nRRD</td><td colspan="13">repeat Sub-Loop 11, but BA[2:0] = 3</td></tr><tr><td rowspan="2">14</td><td rowspan="2">2*nFAW+4 * nRRD</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>3</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td colspan="13">Assert and repeat above D Command until 3 * nFAW - 1, if necessary</td></tr><tr><td>15</td><td>3*nFAW</td><td colspan="13">repeat Sub-Loop 10, but BA[2:0] = 4</td></tr><tr><td>16</td><td>3*nFAW+nRRD</td><td colspan="13">repeat Sub-Loop 11, but BA[2:0] = 5</td></tr><tr><td>17</td><td>3*nFAW+2*nRRD</td><td colspan="13">repeat Sub-Loop 10, but BA[2:0] = 6</td></tr><tr><td>18</td><td>3*nFAW+3*nRRD</td><td colspan="13">repeat Sub-Loop 11, but BA[2:0] = 7</td></tr><tr><td rowspan="2">19</td><td rowspan="2">3*nFAW+4*nRRD</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>7</td><td>00</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td colspan="13">Assert and repeat above D Command until 4 * nFAW - 1, if necessary</td></tr></table>


NOTE: 



1.DM must be driven LOW all the time. DQS, DQS# are used according to RD Commands, otherwise MID-LEVEL 



2.Burst Sequence driven on each DQ signal by Read Command. Outside burst operation, DQ signals are MID-LEVEL. 


# 10 IDD Specification Parameters and Test Conditions (Cont’d)

# 10.2 IDD Specifications

IDD values are for full operating range of voltage and temperature unless otherwise noted. 


Table 56 — $I _ { \mathrm { D D } }$ Specification Example 512M DDR3


<table><tr><td>Speed Grade Bin</td><td>DDR3 - 8005-5-5</td><td>DDR3 - 10667-7-7</td><td>DDR3 - 13338-8-8</td><td>DDR3 - 16009-9-9</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Symbol</td><td>Max.</td><td>Max.</td><td>Max.</td><td>Max.</td></tr><tr><td rowspan="2">\(I_{DD0}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x16</td></tr><tr><td rowspan="2">\(I_{DD1}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x16</td></tr><tr><td>\(I_{DD2P}\)(0) slow exit</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8/x16</td></tr><tr><td>\(I_{DD2P}\)(1) fast exit</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8/x16</td></tr><tr><td>\(I_{DD2N}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8/x16</td></tr><tr><td rowspan="2">\(I_{DD2NT}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x16</td></tr><tr><td rowspan="2">\(I_{DDQ2NT}\)(Optional)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x16</td></tr><tr><td>\(I_{DD2Q}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8/x16</td></tr><tr><td>\(I_{DD3P}\)(fast exit)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8/x16</td></tr><tr><td>\(I_{DD3N}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8/x16</td></tr><tr><td rowspan="3">\(I_{DD4R}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x8</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x16</td></tr><tr><td rowspan="3">\(I_{DDQ4R}\)(Optional)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x8</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x16</td></tr><tr><td rowspan="3">\(I_{DD4W}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x8</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x16</td></tr><tr><td>\(I_{DD5B}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8/x16</td></tr><tr><td>\(I_{DD6}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td rowspan="3">Refer toTable 57 onpage 151</td></tr><tr><td>\(I_{DD6ET}^1\)</td><td></td><td></td><td></td><td></td><td>mA</td></tr><tr><td>\(I_{DD6TC1}\)</td><td></td><td></td><td></td><td></td><td>mA</td></tr><tr><td rowspan="2">\(I_{DD7}\)</td><td></td><td></td><td></td><td></td><td>mA</td><td>x4/x8</td></tr><tr><td></td><td></td><td></td><td></td><td>mA</td><td>x16</td></tr><tr><td colspan="7">NOTE 1. Users should refer to the DRAM supplier data sheet and/or the DIMM SPD to determine if DDR3 SDRAMdevices support the following options or requirements referred to in this material.</td></tr></table>

# 10 IDD Specification Parameters and Test Conditions (Cont’d)

# 10.2 IDD Specifications (Cont’d)


Table 57 — $I _ { \mathrm { D D 6 } }$ Specification


<table><tr><td rowspan="2">Symbol</td><td rowspan="2">Temperature Range</td><td>Value</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td></td></tr><tr><td>IDD6</td><td>0 - 85 °C</td><td></td><td>mA</td><td>3,4</td></tr><tr><td>IDD6ET</td><td>0 - 95 °C</td><td></td><td>mA</td><td>5,6</td></tr><tr><td rowspan="3">IDD6TC</td><td>0 °C ~ Ta</td><td></td><td>mA</td><td>6,7,8</td></tr><tr><td>Tb ~ Ty</td><td></td><td>mA</td><td>6,7,8</td></tr><tr><td>Tz ~ TOPERmax</td><td></td><td>mA</td><td>6,7,8</td></tr><tr><td colspan="5">NOTE 1. Some IDD currents are higher for x16 organization due to larger page-size architecture.
NOTE 2. Max. values for IDD currents considering worst case conditions of process, temperature and voltage.
NOTE 3. Applicable for MR2 settings A6=0 and A7=0.
NOTE 4. Supplier data sheets include a max value for IDD6.
NOTE 5. Applicable for MR2 settings A6=0 and A7=1. IDD6ET is only specified for devices which support the Extended Temperature Range feature.
NOTE 6. Refer to the supplier data sheet for the value specification method (e.g. max, typical) for IDD6ET and IDD6TC
NOTE 7. Applicable for MR2 settings A6=1 and A7=0. IDD6TC is only specified for devices which support the Auto Self Refresh feature.
NOTE 8. The number of discrete temperature ranges supported and the associated Ta - Tz values are supplier/design specific. Temperature ranges are specified for all supported values of TOPER. Refer to supplier data sheet for more information.</td></tr></table>

This page left blank. 

# 11 Input/Output Capacitance

# 11.1 Input/Output Capacitance


Table 58 — Input / Output Capacitance


<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>Input/output capacitance (DQ, DM, DQS, DQS#, TDQS, TDQS#)</td><td>CIO</td><td>1.5</td><td>3.0</td><td>1.5</td><td>2.7</td><td>1.5</td><td>2.5</td><td>1.5</td><td>2.3</td><td>pF</td><td>1,2,3</td></tr><tr><td>Input capacitance, CK and CK#</td><td>CK</td><td>0.8</td><td>1.6</td><td>0.8</td><td>1.6</td><td>0.8</td><td>1.4</td><td>0.8</td><td>1.4</td><td>pF</td><td>2,3</td></tr><tr><td>Input capacitance delta, CK and CK#</td><td>CDCK</td><td>0</td><td>0.15</td><td>0</td><td>0.15</td><td>0</td><td>0.15</td><td>0</td><td>0.15</td><td>pF</td><td>2,3,4</td></tr><tr><td>Input/output capacitance delta DQS and DQS#</td><td>CDDQS</td><td>0</td><td>0.2</td><td>0</td><td>0.2</td><td>0</td><td>0.15</td><td>0</td><td>0.15</td><td>pF</td><td>2,3,5</td></tr><tr><td>Input capacitance, (CTRL, ADD, CMD input-only pins)</td><td>CI</td><td>0.75</td><td>1.4</td><td>0.75</td><td>1.35</td><td>0.75</td><td>1.3</td><td>0.75</td><td>1.3</td><td>pF</td><td>2,3,6</td></tr><tr><td>Input capacitance delta, (All CTRL input-only pins</td><td>CDI_CTRL</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>-0.4</td><td>0.2</td><td>-0.4</td><td>0.2</td><td>pF</td><td>2,3,7,8</td></tr><tr><td>Input capacitance delta, (All ADD/ CMD input-only pins)</td><td>CDI_ADD_CMD</td><td>-0.5</td><td>0.5</td><td>-0.5</td><td>0.5</td><td>-0.4</td><td>0.4</td><td>-0.4</td><td>0.4</td><td>pF</td><td>2,3,9, 10</td></tr><tr><td>Input/output capacitance delta, DQ, DM, DQS, DQS#, TDQS, TDQS#</td><td>CDIO</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>pF</td><td>2,3,11</td></tr><tr><td>Input/output capacitance of ZQ pin</td><td>CZQ</td><td>-</td><td>3</td><td>-</td><td>3</td><td>-</td><td>3</td><td>-</td><td>3</td><td>pF</td><td>2,3,12</td></tr><tr><td colspan="12">NOTE 1. Although the DM, TDQS and TDQS# pins have different functions, the loading matches DQ and DQSNOTE 2. This parameter is not subject to production test. It is verified by design and characterization. The capacitance is measured according to JEP147(&quot;PROCEDURE FOR MEASURING INPUT CAPACITANCE USING A VEC-TOR NETWORK ANALYZER(VNA)) with VDD, VDDQ, VSS, VSSQ applied and all other pins floating (except the pin under test, CKE, RESET# and ODT as necessary). VDD=VDDQ=1.5V, VBIAS=VDD/2 and on-die termination off.NOTE 3. This parameter applies to monolithic devices only; stacked/dual-die devices are not covered hereNOTE 4. Absolute value of CCK-CCK#NOTE 5. Absolute value of CIO(DQS)-CIO(DQS#)NOTE 6. CI applies to ODT, CS#, CKE, A0-A15, BA0-BA2, RAS#, CAS#, WE#.NOTE 7. CDI_CTRL applies to ODT, CS# and CKENOTE 8. CDI_CTRL=CIO(CTRL)-0.5*(CIO(CLK)+CIO(CLK#))NOTE 9. CDI_ADD_CMD applies to A0-A15, BA0-BA2, RAS#, CAS# and WE#.NOTE 10. CDI_ADD_CMD=CIO(ADD_CMD)-0.5*(CIO(CLK)+CIO(CLK#))NOTE 11. CDIO=CIO(DQ,DM)-0.5*(CIO(DQS)+CIO(DQS#))NOTE 12. Maximum external load capacitance on ZQ pin: 5 pF.</td></tr></table>

This page left blank. 

# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133

# 12.1 Clock Specification

The jitter specified is a random jitter meeting a Gaussian distribution. Input clocks violating the min/max values may result in malfunction of the DDR3 SDRAM device. 

# 12.1.1 Definition for tCK(avg)

tCK(avg) is calculated as the average clock period across any consecutive 200 cycle window, where each clock period is calculated from rising edge to rising edge. 

$$
t C K (a v g) = \left(\sum_ {j = 1} ^ {N} t C K _ {j}\right) / N
$$

$$
w h e r e \quad N = 2 0 0
$$

# 12.1.2 Definition for tCK(abs)

tCK(abs) is defined as the absolute clock period, as measured from one rising edge to the next consecutive rising edge. tCK(abs) is not subject to production test. 

# 12.1.3 Definition for tCH(avg) and tCL(avg)

tCH(avg) is defined as the average high pulse width, as calculated across any consecutive 200 high pulses. 

$$
t C H (a v g) = \left(\sum_ {j = 1} ^ {N} t C H _ {j}\right) / (N \times t C K (a v g))
$$

$$
w h e r e N = 2 0 0
$$

tCL(avg) is defined as the average low pulse width, as calculated across any consecutive 200 low pulses. 

$$
t C L (a v g) = \left(\sum_ {j = 1} ^ {N} t C L _ {j}\right) / (N \times t C K (a v g))
$$

$$
w h e r e \quad N = 2 0 0
$$

# 12.1.4 Definition for tJIT(per) and tJIT(per,lck)

tJIT(per) is defined as the largest deviation of any signal tCK from tCK(avg). 

# 12.1 Clock Specification (Cont’d)

# 12.1.4 Definition for tJIT(per) and tJIT(per,lck) (Cont’d)

tJIT(per) $=$ Min/max of {tCKi - tCK(avg) where $\dot { 1 } = 1$ to $2 0 0 \}$ . 

tJIT(per) defines the single period jitter when the DLL is already locked. 

tJIT(per,lck) uses the same definition for single period jitter, during the DLL locking period only. 

tJIT(per) and tJIT(per,lck) are not subject to production test. 

# 12.1.5 Definition for tJIT(cc) and tJIT(cc,lck)

tJIT(cc) is defined as the absolute difference in clock period between two consecutive clock cycles. 

tJIT(cc) = Max of $| \{ \mathrm { t C K } _ { \mathrm { i } + 1 } - \mathrm { t C K } _ { \mathrm { i } } \} |$ . 

tJIT(cc) defines the cycle to cycle jitter when the DLL is already locked. 

tJIT(cc,lck) uses the same definition for cycle to cycle jitter, during the DLL locking period only. 

tJIT(cc) and tJIT(cc,lck) are not subject to production test. 

# 12.1.6 Definition for tERR(nper)

tERR is defined as the cumulative error across n multiple consecutive cycles from tCK(avg). tERR is not subject to production test. 

# 12.2 Refresh parameters by device density


Table 59 — Refresh parameters by device density


<table><tr><td>Parameter</td><td colspan="2">Symbol</td><td>512Mb</td><td>1Gb</td><td>2Gb</td><td>4Gb</td><td>8Gb</td><td>Units</td><td>Notes</td></tr><tr><td>REF command to ACT or REF command time</td><td colspan="2">tRFC</td><td>90</td><td>110</td><td>160</td><td>300</td><td>350</td><td>ns</td><td></td></tr><tr><td rowspan="2">Average periodic refresh interval</td><td rowspan="2">tREFI</td><td>0 °C ≤ TCASE ≤ 85 °C</td><td>7.8</td><td>7.8</td><td>7.8</td><td>7.8</td><td>7.8</td><td>μs</td><td></td></tr><tr><td>85 °C &lt; TCASE ≤ 95 °C</td><td>3.9</td><td>3.9</td><td>3.9</td><td>3.9</td><td>3.9</td><td>μs</td><td>1</td></tr></table>


NOTE 1. Users should refer to the DRAM supplier data sheet and/or the DIMM SPD to determine if DDR3 SDRAM devices support the following options or requirements referred to in this material. 


# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133 (Cont’d)

# 12.3 Standard Speed Bins

DDR3 SDRAM Standard Speed Bins include tCK, tRCD, tRP, tRAS and tRC for each corresponding bin. 


Table 60 — DDR3-800 Speed Bins and Operating Conditions


<table><tr><td colspan="9">For specific Notes See 12.3.1 “Speed Bin Table Notes” on page 165.</td></tr><tr><td colspan="3">Speed Bin</td><td colspan="2">DDR3-800D</td><td colspan="2">DDR3-800E</td><td rowspan="3">Unit</td><td rowspan="3">Notes</td></tr><tr><td colspan="3">CL - nRCD - nRP</td><td colspan="2">5-5-5</td><td colspan="2">6-6-6</td></tr><tr><td colspan="2">Parameter</td><td>Symbol</td><td>min</td><td>max</td><td>min</td><td>max</td></tr><tr><td colspan="2">Internal read command to first data</td><td>tAA</td><td>12.5</td><td>20</td><td>15</td><td>20</td><td>ns</td><td></td></tr><tr><td colspan="2">ACT to internal read or write delay time</td><td>tRCD</td><td>12.5</td><td>—</td><td>15</td><td>—</td><td>ns</td><td></td></tr><tr><td colspan="2">PRE command period</td><td>tRP</td><td>12.5</td><td>—</td><td>15</td><td>—</td><td>ns</td><td></td></tr><tr><td colspan="2">ACT to ACT or REF command period</td><td>tRC</td><td>50</td><td>—</td><td>52.5</td><td>—</td><td>ns</td><td></td></tr><tr><td colspan="2">ACT to PRE command period</td><td>tRAS</td><td>37.5</td><td>9 * tREFI</td><td>37.5</td><td>9 * tREFI</td><td>ns</td><td></td></tr><tr><td>CL = 5</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>3.0</td><td>3.3</td><td>ns</td><td>1, 2, 3, 4, 12, 13</td></tr><tr><td>CL = 6</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>ns</td><td>1, 2, 3</td></tr><tr><td colspan="3">Supported CL Settings</td><td colspan="2">5, 6</td><td colspan="2">5, 6</td><td>nCK</td><td>13</td></tr><tr><td colspan="3">Supported CWL Settings</td><td colspan="2">5</td><td colspan="2">5</td><td>nCK</td><td></td></tr></table>

# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133 (Cont’d)

# 12.3 Standard Speed Bins (Cont’d)


Table 61 — DDR3-1066 Speed Bins and Operating Conditions


<table><tr><td colspan="10">For specific Notes See 12.3.1 “Speed Bin Table Notes” on page 165.</td><td></td></tr><tr><td colspan="2">Speed Bin</td><td colspan="2">DDR3-1066E</td><td colspan="2">DDR3-1066F</td><td colspan="2">DDR3-1066G</td><td rowspan="3">Unit</td><td rowspan="3">Note</td><td></td></tr><tr><td colspan="2">CL - nRCD - nRP</td><td colspan="2">6-6-6</td><td colspan="2">7-7-7</td><td colspan="2">8-8-8</td><td></td></tr><tr><td>Parameter</td><td>Symbol</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td><td></td></tr><tr><td>Internal read command to first data</td><td>tAA</td><td>11.25</td><td>20</td><td>13.125</td><td>20</td><td>15</td><td>20</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to internal read or write delay time</td><td>tRCD</td><td>11.25</td><td>—</td><td>13.125</td><td>—</td><td>15</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td>PRE command period</td><td>tRP</td><td>11.25</td><td>—</td><td>13.125</td><td>—</td><td>15</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to ACT or REF command period</td><td>tRC</td><td>48.75</td><td>—</td><td>50.625</td><td>—</td><td>52.5</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to PRE command period</td><td>tRAS</td><td>37.5</td><td>9 * tREFI</td><td>37.5</td><td>9 * tREFI</td><td>37.5</td><td>9 * tREFI</td><td>ns</td><td></td><td></td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>3.0</td><td>3.3</td><td>3.0</td><td>3.3</td><td>ns</td><td>1,2,3,4,6,12,13</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4,</td></tr><tr><td rowspan="2">CL = 6</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>ns</td><td>1,2,3,6,</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,</td></tr><tr><td rowspan="2">CL = 7</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4,</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,</td></tr><tr><td rowspan="2">CL = 8</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4,</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>1,2,3,</td></tr><tr><td colspan="3">Supported CL Settings</td><td colspan="2">5, 6, 7, 8</td><td colspan="2">5, 6, 7, 8</td><td colspan="2">5, 6, 8</td><td>nCK</td><td>13</td></tr><tr><td colspan="3">Supported CWL Settings</td><td colspan="2">5, 6</td><td colspan="2">5, 6</td><td colspan="2">5, 6</td><td>nCK</td><td></td></tr></table>

# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133 (Cont’d)

# 12.3 Standard Speed Bins (Cont’d)


Table 62 — DDR3-1333 Speed Bins and Operating Conditions


<table><tr><td colspan="12">For specific Notes See 12.3.1 &quot;Speed Bin Table Notes&quot; on page 165.</td><td></td></tr><tr><td colspan="2">Speed Bin</td><td colspan="2">DDR3-1333F(optional)</td><td colspan="2">DDR3-1333G</td><td colspan="2">DDR3-1333H</td><td colspan="2">DDR3-1333J(optional)</td><td rowspan="3">Unit</td><td rowspan="3">Note</td><td></td></tr><tr><td colspan="2">CL - nRCD - nRP</td><td colspan="2">7-7-7</td><td colspan="2">8-8-8</td><td colspan="2">9-9-9</td><td colspan="2">10-10-10</td><td></td></tr><tr><td>Parameter</td><td>Symbol</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td><td></td></tr><tr><td>Internal read command to first data</td><td>tAA</td><td>10.5</td><td>20</td><td>12</td><td>20</td><td>13.5(13.125)5,11</td><td>20</td><td>15</td><td>20</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to internal read or write delay time</td><td>tRCD</td><td>10.5</td><td>—</td><td>12</td><td>—</td><td>13.5(13.125)5,11</td><td>—</td><td>15</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td>PRE command period</td><td>tRP</td><td>10.5</td><td>—</td><td>12</td><td>—</td><td>13.5(13.125)5,11</td><td>—</td><td>15</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to ACT or REF command period</td><td>tRC</td><td>46.5</td><td>—</td><td>48</td><td>—</td><td>49.5(49.125)5,11</td><td>—</td><td>51</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to PRE command period</td><td>tRAS</td><td>36</td><td>9*tREFI</td><td>36</td><td>9*tREFI</td><td>36</td><td>9*tREFI</td><td>36</td><td>9*tREFI</td><td>ns</td><td></td><td></td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>3.0</td><td>3.3</td><td>3.0</td><td>3.3</td><td>ns</td><td>1,2,3,4,7,12,13</td></tr><tr><td>CWL = 6, 7</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="3">CL = 6</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>ns</td><td>1,2,3,7</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,7</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="4">CL = 7</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CWL = 6</td><td rowspan="2">tCK(AVG)</td><td rowspan="2">1.875</td><td rowspan="2">&lt;2.5</td><td rowspan="2">1.875</td><td rowspan="2">&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td rowspan="2" colspan="2">Reserved</td><td rowspan="2">ns</td><td rowspan="2">1,2,3,4,7</td></tr><tr><td colspan="2">(Optional)5,11</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4</td></tr><tr><td rowspan="3">CL = 8</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>1,2,3,7</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4</td></tr><tr><td rowspan="2">CL = 9</td><td>CWL = 5, 6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4</td></tr><tr><td rowspan="3">CL = 10</td><td>CWL = 5, 6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CWL = 7</td><td rowspan="2">tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td rowspan="2">1.5</td><td rowspan="2">&lt;1.875</td><td>ns</td><td>1,2,3</td></tr><tr><td colspan="2">(Optional)</td><td colspan="2">(Optional)</td><td colspan="2">(Optional)</td><td>ns</td><td>5</td></tr><tr><td colspan="3">Supported CL Settings</td><td colspan="2">5, 6, 7, 8, 9, (10)</td><td colspan="2">5, 6, 7, 8, 9, (10)</td><td colspan="2">5, 6, 8, (7), 9, (10)</td><td colspan="2">5, 6, 8, 10</td><td>nCK</td><td></td></tr><tr><td colspan="3">Supported CWL Settings</td><td colspan="2">5, 6, 7</td><td colspan="2">5, 6, 7</td><td colspan="2">5, 6, 7</td><td colspan="2">5, 6, 7</td><td>nCK</td><td></td></tr></table>

# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133 (Cont’d)

# 12.3 Standard Speed Bins (Cont’d)


Table 63 — DDR3-1600 Speed Bins and Operating Conditions



For specific Notes See 12.3.1 “Speed Bin Table Notes” on page 165.


<table><tr><td colspan="3">Speed Bin</td><td colspan="2">DDR3-1600G(optional)</td><td colspan="2">DDR3-1600H</td><td colspan="2">DDR3-1600J</td><td colspan="2">DDR3-1600K</td><td rowspan="3">Unit</td><td rowspan="3">Note</td></tr><tr><td colspan="3">CL - nRCD - nRP</td><td colspan="2">8-8-8</td><td colspan="2">9-9-9</td><td colspan="2">10-10-10</td><td colspan="2">11-11-11</td></tr><tr><td colspan="2">Parameter</td><td>Symbol</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td></tr><tr><td colspan="2">Internal read command to first data</td><td>tAA</td><td>10</td><td>20</td><td>11.25</td><td>20</td><td>12.5</td><td>20</td><td>13.75(13.125)5,11</td><td>20</td><td>ns</td><td></td></tr><tr><td colspan="2">ACT to internal read or write delay time</td><td>tRCD</td><td>10</td><td>—</td><td>11.25</td><td>—</td><td>12.5</td><td>—</td><td>13.75(13.125)5,11</td><td>—</td><td>ns</td><td></td></tr><tr><td colspan="2">PRE command period</td><td>tRP</td><td>10</td><td>—</td><td>11.25</td><td>—</td><td>12.5</td><td>—</td><td>13.75(13.125)5,11</td><td>—</td><td>ns</td><td></td></tr><tr><td colspan="2">ACT to ACT or REF command period</td><td>tRC</td><td>45</td><td>—</td><td>46.25</td><td>—</td><td>47.5</td><td>—</td><td>48.75(48.125)5,11</td><td>—</td><td>ns</td><td></td></tr><tr><td colspan="2">ACT to PRE command period</td><td>tRAS</td><td>35</td><td>9*tREFI</td><td>35</td><td>9*tREFI</td><td>35</td><td>9*tREFI</td><td>35</td><td>9*tREFI</td><td>ns</td><td></td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>3.0</td><td>3.3</td><td>ns</td><td>1,2,3,4,8,12,13</td></tr><tr><td>CWL = 6, 7, 8</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="3">CL = 6</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>ns</td><td>1,2,3,8</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,8</td></tr><tr><td>CWL = 7, 8</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="5">CL = 7</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CWL = 6</td><td rowspan="2">tCK(AVG)</td><td rowspan="2">1.875</td><td rowspan="2">&lt;2.5</td><td rowspan="2">1.875</td><td rowspan="2">&lt;2.5</td><td rowspan="2">1.875</td><td rowspan="2">&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td rowspan="2">ns</td><td rowspan="2">1,2,3,4,8</td></tr><tr><td colspan="2">(Optional)5,11</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,8</td></tr><tr><td>CWL = 8</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="4">CL = 8</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>1,2,3,8</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,8</td></tr><tr><td>CWL = 8</td><td>tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4</td></tr><tr><td rowspan="4">CL = 9</td><td>CWL = 5, 6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CWL = 7</td><td rowspan="2">tCK(AVG)</td><td rowspan="2">1.5</td><td rowspan="2">&lt;1.875</td><td rowspan="2">1.5</td><td rowspan="2">&lt;1.875</td><td rowspan="2">1.5</td><td rowspan="2">&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td rowspan="2">ns</td><td rowspan="2">1,2,3,4,8</td></tr><tr><td colspan="2">(Optional)5,11</td></tr><tr><td>CWL = 8</td><td>tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4</td></tr><tr><td rowspan="3">CL = 10</td><td>CWL = 5, 6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>1,2,3,8</td></tr><tr><td>CWL = 8</td><td>tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4</td></tr><tr><td rowspan="3">CL = 11</td><td>CWL = 5, 6, 7</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CWL = 8</td><td rowspan="2">tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td rowspan="2">1.25</td><td rowspan="2">&lt;1.5</td><td>ns</td><td>1,2,3</td></tr><tr><td colspan="2">(Optional)</td><td colspan="2">(Optional)</td><td colspan="2">(Optional)</td><td>ns</td><td>5</td></tr></table>

# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133 (Cont’d)

# 12.3 Standard Speed Bins (Cont’d)

<table><tr><td>Supported CL Settings</td><td>5, 6, 7, 8, 9, 10,(11)</td><td>5, 6, 7, 8, 9, 10,(11)</td><td>5, 6, 7, 8, 9, 10,(11)</td><td>5, 6, (7), 8, (9), 10, 11</td><td>nCK</td><td></td></tr><tr><td>Supported CWL Settings</td><td>5, 6, 7, 8</td><td>5, 6, 7, 8</td><td>5, 6, 7, 8</td><td>5, 6, 7, 8</td><td>nCK</td><td></td></tr></table>

# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133 (Cont’d)

# 12.3 Standard Speed Bins (Cont’d)


Table 64 — DDR3-1866 Speed Bins and Operating Conditions


<table><tr><td colspan="12">For specific Notes See 12.3.1 &quot;Speed Bin Table Notes&quot; on page 165.</td><td></td></tr><tr><td colspan="2">Speed Bin</td><td colspan="2">DDR3-1866J(optional)</td><td colspan="2">DDR3-1866K</td><td colspan="2">DDR3-1866L</td><td colspan="2">DDR3-1866M(optional)</td><td rowspan="3">Unit</td><td rowspan="3">Note</td><td></td></tr><tr><td colspan="2">CL - nRCD - nRP</td><td colspan="2">10-10-10</td><td colspan="2">11-11-11</td><td colspan="2">12-12-12</td><td colspan="2">13-13-13</td><td></td></tr><tr><td>Parameter</td><td>Symbol</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td><td></td></tr><tr><td>Internal read command to first data</td><td>tAA</td><td>10.7</td><td>20.0</td><td>11.77</td><td>20.0</td><td>12.84</td><td>20.0</td><td>13.91</td><td>20.0</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to internal read or write delay time</td><td>tRCD</td><td>10.7</td><td>—</td><td>11.77</td><td>—</td><td>12.84</td><td>—</td><td>13.91</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td>PRE command period</td><td>tRP</td><td>10.7</td><td>—</td><td>11.77</td><td>—</td><td>12.84</td><td>—</td><td>13.91</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to PRE command period</td><td>tRAS</td><td>35.0</td><td>9 x tREFI</td><td>35.0</td><td>9 x tREFI</td><td>35.0</td><td>9 x tREFI</td><td>35.0</td><td>9 x tREFI</td><td>ns</td><td></td><td></td></tr><tr><td>ACT to ACT or REF command period</td><td>tRC</td><td>45.7</td><td>—</td><td>46.77</td><td>—</td><td>47.84</td><td>—</td><td>48.91</td><td>—</td><td>ns</td><td></td><td></td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,9</td><td></td></tr><tr><td>CWL = 6,7,8,9</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td rowspan="3">CL = 6</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>ns</td><td>1,2,3,9</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,9</td><td></td></tr><tr><td>CWL = 7,8,9</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td rowspan="4">CL = 7</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>Reserved</td><td>ns</td><td>1,2,3,4,9</td><td></td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,9</td><td></td></tr><tr><td>CWL = 8,9</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td rowspan="4">CL = 9</td><td>CWL = 5,6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>Reserved</td><td>ns</td><td>1,2,3,4,9</td><td></td></tr><tr><td>CWL = 8</td><td>tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,9</td><td></td></tr><tr><td>CWL = 9</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td>CL = 10</td><td>CWL = 5,6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td></td><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>1,2,3,9</td></tr><tr><td></td><td>CWL = 8</td><td>tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4,9</td><td></td></tr><tr><td rowspan="3">CL = 11</td><td>CWL = 5,6,7</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td>CWL = 8</td><td rowspan="2">tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>Reserved</td><td>ns</td><td>1,2,3,4,9</td><td></td></tr><tr><td>CWL = 9</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>1,2,3,4</td><td></td></tr><tr><td rowspan="2">CL = 12</td><td>CWL = 5,6,7,8</td><td>tCK.AVG</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td>CWL = 9</td><td>tCK.AVG</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td>Reserved</td><td>ns</td><td>1,2,3,4</td><td></td></tr><tr><td rowspan="3">CL = 13</td><td>CWL = 5,6,7,8</td><td>tCK.AVG</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td><td></td></tr><tr><td rowspan="2">CWL = 9</td><td rowspan="2">tCK.AVG</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td rowspan="2">1.07</td><td rowspan="2">&lt;1.25</td><td>ns</td><td>1,2,3</td></tr><tr><td colspan="2">(Optional)</td><td colspan="2">(Optional)</td><td colspan="2">(Optional)</td><td>ns</td><td>5</td></tr><tr><td colspan="3">Supported CL Settings</td><td colspan="2">5,6,7,8,9,10,11,12,(13)</td><td colspan="2">5,6,7,8,9,10,11,12,(13)</td><td colspan="2">6,7,8,9,10,11,12,(13)</td><td colspan="2">6,8,10,12,13</td><td>nCK</td><td></td></tr><tr><td colspan="3">Supported CWL Settings</td><td colspan="2">5,6,7,8,9</td><td colspan="2">5,6,7,8,9</td><td colspan="2">5,6,7,8,9</td><td colspan="2">5,6,7,8,9</td><td>nCK</td><td></td></tr></table>

# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133 (Cont’d)

# 12.3 Standard Speed Bins (Cont’d)


Table 65 — DDR3-2133 Speed Bins and Operating Conditions


<table><tr><td colspan="12">For specific Notes See 12.3.1 &quot;Speed Bin Table Notes&quot; on page 165.</td></tr><tr><td colspan="2">Speed Bin</td><td colspan="2">DDR3-2133K(optional)</td><td colspan="2">DDR3-2133L</td><td colspan="2">DDR3-2133M</td><td colspan="2">DDR3-2133N(optional)</td><td rowspan="3">Unit</td><td rowspan="3">Note</td></tr><tr><td colspan="2">CL - nRCD - nRP</td><td colspan="2">11-11-11</td><td colspan="2">12-12-12</td><td colspan="2">13-13-13</td><td colspan="2">14-14-14</td></tr><tr><td>Parameter</td><td>Symbol</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td><td>min</td><td>max</td></tr><tr><td>Internal read command to first data</td><td>tAA</td><td>10.285</td><td>20.0</td><td>11.22</td><td>20.0</td><td>12.155</td><td>20.0</td><td>13.09</td><td>20.0</td><td>ns</td><td></td></tr><tr><td>ACT to internal read or write delay time</td><td>tRCD</td><td>10.285</td><td>—</td><td>11.22</td><td>—</td><td>12.155</td><td>—</td><td>13.09</td><td>—</td><td>ns</td><td></td></tr><tr><td>PRE command period</td><td>tRP</td><td>10.285</td><td>—</td><td>11.22</td><td>—</td><td>12.155</td><td>—</td><td>13.09</td><td>—</td><td>ns</td><td></td></tr><tr><td>ACT to PRE command period</td><td>tRAS</td><td>35.0</td><td>9 x tREFI</td><td>35.0</td><td>9 x tREFI</td><td>35.0</td><td>9 x tREFI</td><td>35.0</td><td>9 x tREFI</td><td>ns</td><td></td></tr><tr><td>ACT to ACT or REF command period</td><td>tRC</td><td>45.285</td><td>—</td><td>46.22</td><td>—</td><td>47.155</td><td>—</td><td>48.09</td><td>—</td><td>ns</td><td></td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 6,7,8,9,10</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td rowspan="3">CL = 6</td><td>CWL = 5</td><td>tCK(AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>ns, 1, 2, 3, 10</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 7,8,9,10</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td rowspan="4">CL = 7</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>ns, 1, 2, 3, 10</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 8,9,10</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td rowspan="4">CL = 8</td><td>CWL = 5</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td>CWL = 6</td><td>tCK(AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>ns, 1, 2, 3.10</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 8,9,10</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td rowspan="4">CL = 9</td><td>CWL = 5,6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>ns, 1, 2, 3, 10</td></tr><tr><td>CWL = 8</td><td>tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 9,10</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td rowspan="5">CL = 10</td><td>CWL = 5,6</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td>CWL = 7</td><td>tCK(AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>ns, 1, 2,3, 10</td></tr><tr><td>CWL = 8</td><td>tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 9</td><td>tCK(AVG)</td><td>1.07</td><td>&lt;1.25</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 10</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td rowspan="4">CL = 11</td><td>CWL = 5,6,7</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td>CWL = 8</td><td>tCK(AVG)</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>1.25</td><td>&lt;1.5</td><td>ns, 1, 2, 3, 10</td></tr><tr><td>CWL = 9</td><td>tCK(AVG)</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 10</td><td>tCK(AVG)</td><td>0.935</td><td>&lt;1.07</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4</td></tr><tr><td rowspan="3">CL = 12</td><td>CWL = 5,6,7,8</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td>CWL = 9</td><td>tCK(AVG)</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4, 10</td></tr><tr><td>CWL = 10</td><td>tCK(AVG)</td><td>0.935</td><td>&lt;1.07</td><td>0.935</td><td>&lt;1.07</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4</td></tr><tr><td rowspan="3">CL = 13</td><td>CWL = 5,6,7,8</td><td>tCK(AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns, 4</td></tr><tr><td>CWL = 9</td><td>tCK(AVG)</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td>1.07</td><td>&lt;1.25</td><td>ns, 1, 2, 3, 10</td></tr><tr><td>CWL = 10</td><td>tCK(AVG)</td><td>0.935</td><td>&lt;1.07</td><td>0.935</td><td>&lt;1.07</td><td>0.935</td><td>&lt;1.07</td><td colspan="2">Reserved</td><td>ns, 1, 2, 3, 4</td></tr></table>

# 13 Electrical Characteristics and AC Timing (Cont’d)

<table><tr><td rowspan="3">CL = 14</td><td>CWL = 5,6,7,8,9</td><td>tCK.AVG</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CWL = 10</td><td rowspan="2">tCK.AVG</td><td>0.935</td><td>&lt; 1.07</td><td>0.935</td><td>&lt; 1.07</td><td>0.935</td><td>&lt; 1.07</td><td rowspan="2">0.935</td><td rowspan="2">&lt; 1.07</td><td>ns</td><td>1,2,3</td></tr><tr><td colspan="2">(Optional)</td><td colspan="2">(Optional)</td><td colspan="2">(Optional)</td><td>ns</td><td>5</td></tr><tr><td colspan="3">Supported CL Settings</td><td colspan="2">5,6,7,8,9,10,11,12,13, (14)</td><td colspan="2">5,6,7,8,9,10,11,12,13, (14)</td><td colspan="2">5,6,7,8,9,10,11,12,13, (14)</td><td colspan="2">5,6,7,8,9,10,11,12,13,14</td><td>nCK</td><td></td></tr><tr><td colspan="3">Supported CWL Settings</td><td colspan="2">5,6,7,8,9,10</td><td colspan="2">5,6,7,8,9,10</td><td colspan="2">5,6,7,8,9,10</td><td colspan="2">5,6,7,8,9,10</td><td>nCK</td><td></td></tr></table>

# 12 Electrical Characteristics & AC Timing for DDR3-800 to DDR3-2133 (Cont’d)

# 12.3 Standard Speed Bins (Cont’d)

# 12.3.1 Speed Bin Table Notes

Absolute Specification (TOPER; $\mathrm { \Delta V _ { D D Q } = \Delta V _ { D D } = 1 . 5 V + / - 0 . 0 7 5 \Delta V ) } .$ 

NOTE 1. The CL setting and CWL setting result in tCK(AVG).MIN and tCK(AVG).MAX requirements. When making a selection of tCK(AVG), both need to be fulfilled: Requirements from CL setting as well as requirements from CWL setting. 

NOTE 2. tCK(AVG).MIN limits: Since CAS Latency is not purely analog - data and strobe output are synchronized by the DLL - all possible intermediate frequencies may not be guaranteed. An application should use the next smaller JEDEC standard tCK(AVG) value (3.0, 2.5, 1.875, 1.5, 1.25, 1.07, or 0.935 ns) when calculating CL [nCK] = tAA [ns] / tCK(AVG) [ns], rounding up to the next ‘Supported CL’, where $\mathrm { t C K } ( \mathrm { A V G } ) = 3 . 0$ ns should only be used for $\mathrm { C L } = 5$ calculation. 

NOTE 3. tCK(AVG).MAX limits: Calculate tCK(AVG) $=$ tAA.MAX / CL SELECTED and round the resulting tCK(AVG) down to the next valid speed bin (i.e. 3.3ns or 2.5ns or 1.875 ns or 1.5 ns or 1.25 ns or 1.07 ns or 0.935 ns). This result is tCK(AVG).MAX corresponding to CL SELECTED. 

NOTE 4. ‘Reserved’ settings are not allowed. User must program a different value. 

NOTE 5. ‘Optional’ settings allow certain devices in the industry to support this setting, however, it is not a mandatory feature. Refer to supplier’s data sheet and/or the DIMM SPD information if and how this setting is supported. 

NOTE 6. Any DDR3-1066 speed bin also supports functional operation at lower frequencies as shown in the table which are not subject to Production Tests but verified by Design/Characterization. 

NOTE 7. Any DDR3-1333 speed bin also supports functional operation at lower frequencies as shown in the table which are not subject to Production Tests but verified by Design/Characterization. 

NOTE 8. Any DDR3-1600 speed bin also supports functional operation at lower frequencies as shown in the table which are not subject to Production Tests but verified by Design/Characterization. 

NOTE 9. Any DDR3-1866 speed bin also supports functional operation at lower frequencies as shown in the table which are not subject to Production Tests but verified by Design/Characterization. 

NOTE 10.Any DDR3-2133 speed bin also supports functional operation at lower frequencies as shown in the table which are not subject to Production Tests but verified by Design/Characterization. 

NOTE 11.For devices supporting optional down binning to $\mathrm { C L } = 7$ and $\mathrm { C L } { = } 9$ , tAA/tRCD/tRPmin must be 13.125 ns or lower. SPD settings must be programmed to match. For example, DDR3-1333H devices supporting down binning to DDR3-1066F should program 13.125 ns in SPD bytes for tAAmin (Byte 16), tRCDmin (Byte 18), and tRPmin (Byte 20). DDR3-1600K devices supporting down binning to DDR3-1333H or DDR3-1066F should program 13.125 ns in SPD bytes for tAAmin (Byte16), tRCDmin (Byte 18), and tRPmin (Byte 20). Once tRP (Byte 20) is programmed to 13.125ns, tRCmin (Byte 21,23) also should be programmed accodingly. For example, 49.125ns (tRASmin $^ +$ tRPmin = 36 ns + 13.125 ns) for DDR3-1333H and 48.125ns $( \mathrm { t R A S m i n } + \mathrm { t R P m i n } = 3 5 \ \mathrm { n s } + 1 3 . 1 2 5 \ \mathrm { n s } )$ for DDR3-1600K. 

NOTE 12.DDR3 800 AC timing apply if DRAM operates at lower than 800 MT/s data rate. 

NOTE 13.For CL5 support, refer to DIMM SPD information. DRAM is required to support CL5. CL5 is not mandatory in SPD coding. 

This page left blank. 

# 1 3 E lectrical C haracteristics and AC Ti m i ng

# 1 3. 1 Ti m i ng Parameters for D D R3-800, D D R3-1 067, D D R3-1 333, and D D R3-1 600


Table 66 — Ti m i ng Parameters by Speed Bi n



NOTE : The following general notes from page 1 79 apply to Table 66 : Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$


<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td colspan="12"></td></tr><tr><td colspan="12">Clock Timing</td></tr><tr><td>Minimum Clock Cycle Time (DLL off mode)</td><td>tCK(DLL_OFF)</td><td>8</td><td>-</td><td>8</td><td>-</td><td>8</td><td>-</td><td>8</td><td>-</td><td>ns</td><td>6</td></tr><tr><td>Average Clock Period</td><td>tCK(avg)</td><td colspan="8">See 12.3 &quot;Standard Speed Bins&quot; on page 157</td><td>ps</td><td></td></tr><tr><td>Average high pulse width</td><td>tCH(avg)</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>tCK(avg)</td><td></td></tr><tr><td>Average low pulse width</td><td>tCL(avg)</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>tCK(avg)</td><td></td></tr><tr><td>Absolute Clock Period</td><td>tCK(abs)</td><td>tCK(avg)min+tJIT(per)min</td><td>tCK(avg)max+tJIT(per)max</td><td>tCK(avg)min+tJIT(per)min</td><td>tCK(avg)max+tJIT(per)min</td><td>tCK(avg)min+tJIT(per)min</td><td>tCK(avg)max+tJIT(per)min</td><td>tCK(avg)min+tJIT(per)min</td><td>tCK(avg)max+tJIT(per)min</td><td>ps</td><td></td></tr><tr><td>Absolute clock HIGH pulse width</td><td>tCH(abs)</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>tCK(avg)</td><td>25</td></tr><tr><td>Absolute clock LOW pulse width</td><td>tCL(abs)</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>tCK(avg)</td><td>26</td></tr><tr><td>Clock Period Jitter</td><td>JIT(per)</td><td>-100</td><td>100</td><td>-90</td><td>90</td><td>-80</td><td>80</td><td>-70</td><td>70</td><td>ps</td><td></td></tr><tr><td>Clock Period Jitter during DLL locking period</td><td>tJIT(per, lck)</td><td>-90</td><td>90</td><td>-80</td><td>80</td><td>-70</td><td>70</td><td>-60</td><td>60</td><td>ps</td><td></td></tr><tr><td>Cycle to Cycle Period Jitter</td><td>tJIT(cc)</td><td colspan="2">200</td><td colspan="2">180</td><td colspan="2">160</td><td colspan="2">140</td><td>ps</td><td></td></tr><tr><td>Cycle to Cycle Period Jitter during DLL locking period</td><td>tJIT(cc, lck)</td><td colspan="2">180</td><td colspan="2">160</td><td colspan="2">140</td><td colspan="2">120</td><td>ps</td><td></td></tr><tr><td>Duty Cycle Jitter</td><td>tJIT(duty)</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 2 cycles</td><td>tERR(2per)</td><td>-147</td><td>147</td><td>-132</td><td>132</td><td>-118</td><td>118</td><td>-103</td><td>103</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 3 cycles</td><td>tERR(3per)</td><td>-175</td><td>175</td><td>-157</td><td>157</td><td>-140</td><td>140</td><td>-122</td><td>122</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 4 cycles</td><td>tERR(4per)</td><td>-194</td><td>194</td><td>-175</td><td>175</td><td>-155</td><td>155</td><td>-136</td><td>136</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 5 cycles</td><td>tERR(5per)</td><td>-209</td><td>209</td><td>-188</td><td>188</td><td>-168</td><td>168</td><td>-147</td><td>147</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 6 cycles</td><td>tERR(6per)</td><td>-222</td><td>222</td><td>-200</td><td>200</td><td>-177</td><td>177</td><td>-155</td><td>155</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 7 cycles</td><td>tERR(7per)</td><td>-232</td><td>232</td><td>-209</td><td>209</td><td>-186</td><td>186</td><td>-163</td><td>163</td><td>ps</td><td></td></tr></table>


Table 66 — Ti m i ng Parameters by Speed B i n (Cont’d)


NOTE : The following general notes from page 1 79 apply to Table 66 : Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$ 

<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>Cumulative error across 8 cycles</td><td>tERR(8per)</td><td>-241</td><td>241</td><td>-217</td><td>217</td><td>-193</td><td>193</td><td>-169</td><td>169</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 9 cycles</td><td>tERR(9per)</td><td>-249</td><td>249</td><td>-224</td><td>224</td><td>-200</td><td>200</td><td>-175</td><td>175</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 10 cycles</td><td>tERR(10per)</td><td>-257</td><td>257</td><td>-231</td><td>231</td><td>-205</td><td>205</td><td>-180</td><td>180</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 11 cycles</td><td>tERR(11per)</td><td>-263</td><td>263</td><td>-237</td><td>237</td><td>-210</td><td>210</td><td>-184</td><td>184</td><td>ps</td><td></td></tr><tr><td>Cumulative error across 12 cycles</td><td>tERR(12per)</td><td>-269</td><td>269</td><td>-242</td><td>242</td><td>-215</td><td>215</td><td>-188</td><td>188</td><td>ps</td><td></td></tr><tr><td>Cumulative error across n = 13, 14 . . . 49, 50 cycles</td><td>tERR(nper)</td><td colspan="8">\({}^{t}\text{ERR}(nper)\min=(1+0.68ln(n))*{}^{t}\text{JIT(per)}\min\) \({}^{t}\text{ERR}(nper)\max=(1+0.68ln(n))*{}^{t}\text{JIT(per)}\max\)</td><td>ps</td><td>24</td></tr><tr><td colspan="12">Data Timing</td></tr><tr><td>DQS, DQS# to DQ skew, per group, per access</td><td>tDQSQ</td><td>-</td><td>200</td><td>-</td><td>150</td><td>-</td><td>125</td><td>-</td><td>100</td><td>ps</td><td>13</td></tr><tr><td>DQ output hold time from DQS, DQS#</td><td>tQH</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>tCK(avg)</td><td>13, g</td></tr><tr><td>DQ low-impedance time from CK, CK#</td><td>tLZ(DQ)</td><td>-800</td><td>400</td><td>-600</td><td>300</td><td>-500</td><td>250</td><td>-450</td><td>225</td><td>ps</td><td>13, 14, f</td></tr><tr><td>DQ high impedance time from CK, CK#</td><td>tHZ(DQ)</td><td>-</td><td>400</td><td>-</td><td>300</td><td>-</td><td>250</td><td>-</td><td>225</td><td>ps</td><td>13, 14, f</td></tr><tr><td>Data setup time to DQS, DQS# referenced to Vih(ac) / Vil(ac) levels</td><td>tDS(base) AC175</td><td>75</td><td></td><td>25</td><td></td><td>-</td><td></td><td>-</td><td></td><td>ps</td><td>d, 17</td></tr><tr><td>Data setup time to DQS, DQS# referenced to Vih(ac) / Vil(ac) levels</td><td>tDS(base) AC150</td><td>125</td><td></td><td>75</td><td></td><td>30</td><td></td><td>10</td><td></td><td>ps</td><td>d, 17</td></tr><tr><td>Data hold time from DQS, DQS# referenced to Vih(dc) / Vil(dc) levels</td><td>tDH(base) DC100</td><td>150</td><td></td><td>100</td><td></td><td>65</td><td></td><td>45</td><td></td><td>ps</td><td>d, 17</td></tr><tr><td>DQ and DM Input pulse width for each input</td><td>tDIPW</td><td>600</td><td>-</td><td>490</td><td>-</td><td>400</td><td>-</td><td>360</td><td>-</td><td>ps</td><td>28</td></tr><tr><td colspan="12">Data Strobe Timing</td></tr><tr><td>DQS,DQS# differential READ Preamble</td><td>tRPRE</td><td>0.9</td><td>Note 19</td><td>0.9</td><td>Note 19</td><td>0.9</td><td>Note 19</td><td>0.9</td><td>Note 19</td><td>tCK(avg)</td><td>13, 19, g</td></tr><tr><td>DQS, DQS# differential READ Postamble</td><td>tRPST</td><td>0.3</td><td>Note 11</td><td>0.3</td><td>Note 11</td><td>0.3</td><td>Note 11</td><td>0.3</td><td>Note 11</td><td>tCK(avg)</td><td>11, 13, g</td></tr><tr><td>DQS, DQS# differential output high time</td><td>tQSH</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>0.40</td><td>-</td><td>0.40</td><td>-</td><td>tCK(avg)</td><td>13, g</td></tr><tr><td>DQS, DQS# differential output low time</td><td>tQSL</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>0.40</td><td>-</td><td>0.40</td><td>-</td><td>tCK(avg)</td><td>13, g</td></tr><tr><td>DQS, DQS# differential WRITE Preamble</td><td>tWPRE</td><td>0.9</td><td>-</td><td>0.9</td><td>-</td><td>0.9</td><td>-</td><td>0.9</td><td>-</td><td>tCK(avg)</td><td></td></tr><tr><td>DQS, DQS# differential WRITE Postamble</td><td>tWPST</td><td>0.3</td><td>-</td><td>0.3</td><td>-</td><td>0.3</td><td>-</td><td>0.3</td><td>-</td><td>tCK(avg)</td><td></td></tr><tr><td>DQS, DQS# rising edge output access time from rising CK, CK#</td><td>tDQSCK</td><td>-400</td><td>400</td><td>-300</td><td>300</td><td>-255</td><td>255</td><td>-225</td><td>225</td><td>ps</td><td>13, f</td></tr></table>


rical Characteristics and AC Timing 13.3.1 Timing Parameters 
for DDR3-800, DDR3-1067, DDR3-1333, and DDR3-1600 (Cont’d 



Table 66 — Ti m i ng Parameters by Speed B i n (Cont’d)


NOTE : The following general notes from page 1 79 apply to Table 66 : Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$ 

<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>DQS and DQS# low-impedance time(Referenced from RL - 1)</td><td>tLZ(DQS)</td><td>- 800</td><td>400</td><td>- 600</td><td>300</td><td>- 500</td><td>250</td><td>- 450</td><td>225</td><td>ps</td><td>13, 14, f</td></tr><tr><td>DQS and DQS# high-impedance time(Referenced from RL + BL/2)</td><td>tHZ(DQS)</td><td>-</td><td>400</td><td>-</td><td>300</td><td>-</td><td>250</td><td>-</td><td>225</td><td>ps</td><td>13, 14, f</td></tr><tr><td>DQS, DQS# differential input low pulse width</td><td>tDQSL</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>tCK(avg)</td><td>29, 31</td></tr><tr><td>DQS, DQS# differential input high pulse width</td><td>tDQSH</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>tCK(avg)</td><td>30, 31</td></tr><tr><td>DQS, DQS# rising edge to CK, CK# rising edge</td><td>tDQSS</td><td>- 0.25</td><td>0.25</td><td>- 0.25</td><td>0.25</td><td>- 0.25</td><td>0.25</td><td>- 0.27</td><td>0.27</td><td>tCK(avg)</td><td>c</td></tr><tr><td>DQS, DQS# falling edge setup time to CK, CK# rising edge</td><td>tDSS</td><td>0.2</td><td>-</td><td>0.2</td><td>-</td><td>0.2</td><td>-</td><td>0.18</td><td>-</td><td>tCK(avg)</td><td>c, 32</td></tr><tr><td>DQS, DQS# falling edge hold time from CK, CK# rising edge</td><td>tDSH</td><td>0.2</td><td>-</td><td>0.2</td><td>-</td><td>0.2</td><td>-</td><td>0.18</td><td>-</td><td>tCK(avg)</td><td>c, 32</td></tr><tr><td colspan="12">Command and Address Timing</td></tr><tr><td>DLL locking time</td><td>tDLLK</td><td>512</td><td>-</td><td>512</td><td>-</td><td>512</td><td>-</td><td>512</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Internal READ Command to PRECHARGE Command delay</td><td>tRTP</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td></td><td>e</td></tr><tr><td>Delay from start of internal write transaction to internal read command</td><td>tWTR</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td></td><td>e, 18</td></tr><tr><td>WRITE recovery time</td><td>tWR</td><td>15</td><td>-</td><td>15</td><td>-</td><td>15</td><td>-</td><td>15</td><td>-</td><td>ns</td><td>e, 18</td></tr><tr><td>Mode Register Set command cycle time</td><td>tMRD</td><td>4</td><td>-</td><td>4</td><td>-</td><td>4</td><td>-</td><td>4</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Mode Register Set command update delay</td><td>tMOD</td><td>max(12nCK, 15ns)</td><td>-</td><td>max(12nCK, 15ns)</td><td>-</td><td>max(12nCK, 15ns)</td><td>-</td><td>max(12nCK, 15ns)</td><td>-</td><td></td><td></td></tr><tr><td>ACT to internal read or write delay time</td><td>tRCD</td><td colspan="2">See Table 60 on page 157</td><td colspan="2">See Table 61 on page 158</td><td colspan="2">See Table 62 on page 159</td><td colspan="2">See Table 63 on page 160</td><td></td><td>e</td></tr><tr><td>PRE command period</td><td>tRP</td><td colspan="2">See Table 60 on page 157</td><td colspan="2">See Table 61 on page 158</td><td colspan="2">See Table 62 on page 159</td><td colspan="2">See Table 63 on page 160</td><td></td><td>e</td></tr><tr><td>ACT to ACT or REF command period</td><td>tRC</td><td colspan="2">See Table 60 on page 157</td><td colspan="2">See Table 61 on page 158</td><td colspan="2">See Table 62 on page 159</td><td colspan="2">See Table 63 on page 160</td><td></td><td>e</td></tr><tr><td>CAS# to CAS# command delay</td><td>tCCD</td><td>4</td><td>-</td><td>4</td><td>-</td><td>4</td><td>-</td><td>4</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Auto precharge write recovery + precharge time</td><td>tDAL(min)</td><td colspan="8">WR + roundup(tRP / tCK(avg))</td><td>nCK</td><td></td></tr><tr><td>Multi-Purpose Register Recovery Time</td><td>tMPRR</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>nCK</td><td>22</td></tr></table>


rical Characteristics and AC Timing 13.3.1 Timing Parameters 
for DDR3-800, DDR3-1067, DDR3-1333, and DDR3-1600 (Cont’d 



Table 66 — Ti m i ng Parameters by Speed B i n (Cont’d)


NOTE : The following general notes from page 1 79 apply to Table 66 : Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$ 

<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>ACTIVE to PRECHARGE command period</td><td>tRAS</td><td colspan="2">See Table 60 on page 157</td><td colspan="2">See Table 61 on page 158</td><td colspan="2">See Table 62 on page 159</td><td colspan="2">See Table 63 on page 160</td><td></td><td>e</td></tr><tr><td>ACTIVE to ACTIVE command period for 1KB page size</td><td>tRRD</td><td>max(4nCK, 10ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 6ns)</td><td>-</td><td>max(4nCK, 6ns)</td><td>-</td><td></td><td>e</td></tr><tr><td>ACTIVE to ACTIVE command period for 2KB page size</td><td>tRRD</td><td>max(4nCK, 10ns)</td><td>-</td><td>max(4nCK, 10ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td></td><td>e</td></tr><tr><td>Four activate window for 1KB page size</td><td>tFAW</td><td>40</td><td>-</td><td>37.5</td><td>-</td><td>30</td><td>-</td><td>30</td><td>-</td><td>ns</td><td>e</td></tr><tr><td>Four activate window for 2KB page size</td><td>tFAW</td><td>50</td><td>-</td><td>50</td><td>-</td><td>45</td><td>-</td><td>40</td><td>-</td><td>ns</td><td>e</td></tr><tr><td>Command and Address setup time to CK, CK# referenced to Vih(ac) / Vil(ac) levels</td><td>tIS(base) AC175</td><td>200</td><td></td><td>125</td><td></td><td>65</td><td></td><td>45</td><td></td><td>ps</td><td>b, 16</td></tr><tr><td>Command and Address setup time to CK, CK# referenced to Vih(ac) / Vil(ac) levels</td><td>tIS(base) AC150</td><td>350</td><td></td><td>275</td><td></td><td>190</td><td></td><td>170</td><td></td><td>ps</td><td>b, 16, 27</td></tr><tr><td>Command and Address hold time from CK, CK# referenced to Vih(dc) / Vil(dc) levels</td><td>tIH(base) DC100</td><td>275</td><td></td><td>200</td><td></td><td>140</td><td></td><td>120</td><td></td><td>ps</td><td>b, 16</td></tr><tr><td>Control and Address Input pulse width for each input</td><td>tIPW</td><td>900</td><td>-</td><td>780</td><td>-</td><td>620</td><td>-</td><td>560</td><td>-</td><td>ps</td><td>28</td></tr><tr><td colspan="12">Calibration Timing</td></tr><tr><td>Power-up and RESET calibration time</td><td>tZQinit</td><td>max(512nCK, 640ns)</td><td>-</td><td>max(512nCK, 640ns)</td><td>-</td><td>max(512nCK, 640ns)</td><td>-</td><td>max(512nCK, 640ns)</td><td>-</td><td></td><td></td></tr><tr><td>Normal operation Full calibration time</td><td>tZQoper</td><td>max(256nCK, 320ns)</td><td>-</td><td>max(256nCK, 320ns)</td><td>-</td><td>max(256nCK, 320ns)</td><td>-</td><td>max(256nCK, 320ns)</td><td>-</td><td></td><td></td></tr><tr><td>Normal operation Short calibration time</td><td>tZQCS</td><td>max(64nCK, 80ns)</td><td>-</td><td>max(64nCK, 80ns)</td><td>-</td><td>max(64nCK, 80ns)</td><td>-</td><td>max(64nCK, 80ns)</td><td>-</td><td></td><td>23</td></tr><tr><td colspan="12">Reset Timing</td></tr><tr><td>Exit Reset from CKE HIGH to a valid command</td><td>tXPR</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td></td><td></td></tr><tr><td colspan="12">Self Refresh Timings</td></tr><tr><td>Exit Self Refresh to commands not requiring a locked DLL</td><td>tXS</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td></td><td></td></tr></table>


rical Characteristics and AC Timing 13.3.1 Timing Parameters 
for DDR3-800, DDR3-1067, DDR3-1333, and DDR3-1600 (Cont’d 



Table 66 — Ti m i ng Parameters by Speed B i n (Cont’d)


NOTE : The following general notes from page 1 79 apply to Table 66 : Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$ 

<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>Exit Self Refresh to commands requiring a locked DLL</td><td>tXSDLL</td><td>tDLLK(min)</td><td>-</td><td>tDLLK(min)</td><td>-</td><td>tDLLK(min)</td><td>-</td><td>tDLLK(min)</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Minimum CKE low width for Self Refresh entry to exit timing</td><td>tCKESR</td><td>tCKE(min) + 1 nCK</td><td>-</td><td>tCKE(min) + 1 nCK</td><td>-</td><td>tCKE(min) + 1 nCK</td><td>-</td><td>tCKE(min) + 1 nCK</td><td>-</td><td></td><td></td></tr><tr><td>Valid Clock Requirement after Self Refresh Entry (SRE) or Power-Down Entry (PDE)</td><td>tCKSRE</td><td>max(5 nCK, 10 ns)</td><td>-</td><td>max(5 nCK, 10 ns)</td><td>-</td><td>max(5 nCK, 10 ns)</td><td>-</td><td>max(5 nCK, 10 ns)</td><td>-</td><td></td><td></td></tr><tr><td>Valid Clock Requirement before Self Refresh Exit (SRX) or Power-Down Exit (PDX) or Reset Exit</td><td>tCKSRX</td><td>max(5 nCK, 10 ns)</td><td>-</td><td>max(5 nCK, 10 ns)</td><td>-</td><td>max(5 nCK, 10 ns)</td><td>-</td><td>max(5 nCK, 10 ns)</td><td>-</td><td></td><td></td></tr><tr><td colspan="12">Power Down Timings</td></tr><tr><td>Exit Power Down with DLL on to any valid command; Exit Precharge Power Down with DLL frozen to commands not requiring a locked DLL</td><td>tXP</td><td>max(3nCK, 7.5ns)</td><td>-</td><td>max(3nCK, 7.5ns)</td><td>-</td><td>max(3nCK, 6ns)</td><td>-</td><td>max(3nCK, 6ns)</td><td>-</td><td></td><td></td></tr><tr><td>Exit Precharge Power Down with DLL frozen to commands requiring a locked DLL</td><td>tXPDLL</td><td>max(10nCK, 24ns)</td><td>-</td><td>max(10nCK, 24ns)</td><td>-</td><td>max(10nCK, 24ns)</td><td>-</td><td>max(10nCK, 24ns)</td><td>-</td><td></td><td>2</td></tr><tr><td>CKE minimum pulse width</td><td>tCKE</td><td>max(3nCK 7.5ns)</td><td>-</td><td>max(3nCK, 5.625ns)</td><td>-</td><td>max(3nCK, 5.625ns)</td><td>-</td><td>max(3nCK, 5ns)</td><td>-</td><td></td><td></td></tr><tr><td>Command pass disable delay</td><td>tCPDED</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Power Down Entry to Exit Timing</td><td>tPD</td><td>tCKE(min)</td><td>9 * tREFI</td><td>tCKE(min)</td><td>9 * tREFI</td><td>tCKE(min)</td><td>9 * tREFI</td><td>tCKE(min)</td><td>9 * tREFI</td><td></td><td>15</td></tr><tr><td>Timing of ACT command to Power Down entry</td><td>tACTPDEN</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>nCK</td><td>20</td></tr><tr><td>Timing of PRE or PREA command to Power Down entry</td><td>tPRPDEN</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>nCK</td><td>20</td></tr><tr><td>Timing of RD/RDA command to Power Down entry</td><td>tRDPDEN</td><td>RL + 4 + 1</td><td>-</td><td>RL + 4 + 1</td><td>-</td><td>RL + 4 + 1</td><td>-</td><td>RL + 4 + 1</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Timing of WR command to Power Down entry (BL8OTF, BL8MRS, BC4OTF)</td><td>tWRPDEN</td><td>WL + 4 + (tWR / tCK(avg))</td><td>-</td><td>WL + 4 + (tWR / tCK(avg))</td><td>-</td><td>WL + 4 + (tWR / tCK(avg))</td><td>-</td><td>WL + 4 + (tWR / tCK(avg))</td><td>-</td><td>nCK</td><td>9</td></tr></table>


rical Characteristics and AC Timing 13.3.1 Timing Parameters 
for DDR3-800, DDR3-1067, DDR3-1333, and DDR3-1600 (Cont’d 



Table 66 — Ti m i ng Parameters by Speed B i n (Cont’d)


NOTE : The following general notes from page 1 79 apply to Table 66 : Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$ 

<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>Timing of WRA command to Power Down entry (BL8OTF, BL8MRS, BC4OTF)</td><td>tWRAPDEN</td><td>WL + 4 + WR + 1</td><td>-</td><td>WL + 4 + WR + 1</td><td>-</td><td>WL + 4 + WR + 1</td><td>-</td><td>WL + 4 + WR + 1</td><td>-</td><td>nCK</td><td>10</td></tr><tr><td>Timing of WR command to Power Down entry (BC4MRS)</td><td>tWRPDEN</td><td>WL + 2 + (tWR / tCK(avg))</td><td>-</td><td>WL + 2 + (tWR / tCK(avg))</td><td>-</td><td>WL + 2 + (tWR / tCK(avg))</td><td>-</td><td>WL + 2 + (tWR / tCK(avg))</td><td>-</td><td>nCK</td><td>9</td></tr><tr><td>Timing of WRA command to Power Down entry (BC4MRS)</td><td>tWRAPDEN</td><td>WL + 2 + WR + 1</td><td>-</td><td>WL + 2 + WR + 1</td><td>-</td><td>WL + 2 + WR + 1</td><td>-</td><td>WL + 2 + WR + 1</td><td>-</td><td>nCK</td><td>10</td></tr><tr><td>Timing of REF command to Power Down entry</td><td>tREFPDEN</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>1</td><td>-</td><td>nCK</td><td>20, 21</td></tr><tr><td>Timing of MRS command to Power Down entry</td><td>tMRSPDEN</td><td>tMOD(min)</td><td>-</td><td>tMOD(min)</td><td>-</td><td>tMOD(min)</td><td>-</td><td>tMOD(min)</td><td>-</td><td></td><td></td></tr><tr><td colspan="12">ODT Timings</td></tr><tr><td>ODT turn on Latency</td><td>ODTLon</td><td colspan="8">WL - 2 = CWL + AL - 2</td><td>nCK</td><td></td></tr><tr><td>ODT turn off Latency</td><td>ODTLoff</td><td colspan="8">WL - 2 = CWL + AL - 2</td><td>nCK</td><td></td></tr><tr><td>ODT high time without write command or with write command and BC4</td><td>ODTH4</td><td>4</td><td>-</td><td>4</td><td>-</td><td>4</td><td>-</td><td>4</td><td>-</td><td>nCK</td><td></td></tr><tr><td>ODT high time with Write command and BL8</td><td>ODTH8</td><td>6</td><td>-</td><td>6</td><td>-</td><td>6</td><td>-</td><td>6</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Asynchronous RTT turn-on delay (Power-Down with DLL frozen)</td><td>tAONPD</td><td>2</td><td>8.5</td><td>2</td><td>8.5</td><td>2</td><td>8.5</td><td>2</td><td>8.5</td><td>ns</td><td></td></tr><tr><td>Asynchronous RTT turn-off delay (Power-Down with DLL frozen)</td><td>tAOFPD</td><td>2</td><td>8.5</td><td>2</td><td>8.5</td><td>2</td><td>8.5</td><td>2</td><td>8.5</td><td>ns</td><td></td></tr><tr><td>RTT turn-on</td><td>tAON</td><td>-400</td><td>400</td><td>-300</td><td>300</td><td>-250</td><td>250</td><td>-225</td><td>225</td><td>ps</td><td>7, f</td></tr><tr><td>RTT_Nom and RTT_WR turn-off time from ODTLoff reference</td><td>tAOF</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>tCK(avg)</td><td>8, f</td></tr><tr><td>RTT dynamic change skew</td><td>tADC</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>tCK(avg)</td><td>f</td></tr><tr><td colspan="12">Write Leveling Timings</td></tr><tr><td>First DQS/DQS# rising edge after write leveling mode is programmed</td><td>tWLMRD</td><td>40</td><td>-</td><td>40</td><td>-</td><td>40</td><td>-</td><td>40</td><td>-</td><td>nCK</td><td>3</td></tr><tr><td>DQS/DQS# delay after write leveling mode is programmed</td><td>tWLDQSEN</td><td>25</td><td>-</td><td>25</td><td>-</td><td>25</td><td>-</td><td>25</td><td>-</td><td>nCK</td><td>3</td></tr></table>


rical Characteristics and AC Timing 13.3.1 Timing Parameters 
for DDR3-800, DDR3-1067, DDR3-1333, and DDR3-1600 (Cont’d 



Table 66 — Ti m i ng Parameters by Speed B i n (Cont’d)


NOTE : The following general notes from page 1 79 apply to Table 66 : Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$ 

<table><tr><td colspan="2"></td><td colspan="2">DDR3-800</td><td colspan="2">DDR3-1066</td><td colspan="2">DDR3-1333</td><td colspan="2">DDR3-1600</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>Write leveling setup time from rising CK, CK# crossing to rising DQS, DQS# crossing</td><td>tWLS</td><td>325</td><td>-</td><td>245</td><td>-</td><td>195</td><td>-</td><td>165</td><td>-</td><td>ps</td><td></td></tr><tr><td>Write leveling hold time from rising DQS, DQS# crossing to rising CK, CK# crossing</td><td>tWLH</td><td>325</td><td>-</td><td>245</td><td>-</td><td>195</td><td>-</td><td>165</td><td>-</td><td>ps</td><td></td></tr><tr><td>Write leveling output delay</td><td>tWLO</td><td>0</td><td>9</td><td>0</td><td>9</td><td>0</td><td>9</td><td>0</td><td>7.5</td><td>ns</td><td></td></tr><tr><td>Write leveling output error</td><td>tWLOE</td><td>0</td><td>2</td><td>0</td><td>2</td><td>0</td><td>2</td><td>0</td><td>2</td><td>ns</td><td></td></tr></table>

# 13.2 Timing Paramters for DDR3-1866 and DDR3-2133 Speed Bins


Table 67 — Timing Parameters by Speed Bin



NOTE: The following general notes from page 179 apply to Table 67: Note a. V $\mathrm { \Delta ) D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$


<table><tr><td colspan="2"></td><td colspan="2">DDR3-1866</td><td colspan="2">DDR3-2133</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td colspan="8"></td></tr><tr><td colspan="8">Clock Timing</td></tr><tr><td>Minimum Clock Cycle Time (DLL off mode)</td><td>tCK(DLL_OFF)</td><td></td><td></td><td></td><td></td><td>ns</td><td>6</td></tr><tr><td>Average Clock Period</td><td>tCK(avg)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Average high pulse width</td><td>tCH(avg)</td><td></td><td></td><td></td><td></td><td>tCK(avg)</td><td></td></tr><tr><td>Average low pulse width</td><td>tCL(avg)</td><td></td><td></td><td></td><td></td><td>tCK(avg)</td><td></td></tr><tr><td>Absolute Clock Period</td><td>tCK(abs)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Absolute clock HIGH pulse width</td><td>tCH(abs)</td><td></td><td></td><td></td><td></td><td>tCK(avg)</td><td>25</td></tr><tr><td>Absolute clock LOW pulse width</td><td>tCL(abs)</td><td></td><td></td><td></td><td></td><td>tCK(avg)</td><td>26</td></tr><tr><td>Clock Period Jitter</td><td>JIT(per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Clock Period Jitter during DLL locking period</td><td>tJIT(per, lck)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cycle to Cycle Period Jitter</td><td>tJIT(cc)</td><td colspan="2"></td><td colspan="2"></td><td>ps</td><td></td></tr><tr><td>Cycle to Cycle Period Jitter during DLL locking period</td><td>tJIT(cc, lck)</td><td colspan="2"></td><td colspan="2"></td><td>ps</td><td></td></tr><tr><td>Duty Cycle Jitter</td><td>tJIT(duty)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 2 cycles</td><td>tERR(2per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 3 cycles</td><td>tERR(3per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 4 cycles</td><td>tERR(4per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 5 cycles</td><td>tERR(5per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 6 cycles</td><td>tERR(6per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 7 cycles</td><td>tERR(7per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 8 cycles</td><td>tERR(8per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 9 cycles</td><td>tERR(9per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 10 cycles</td><td>tERR(10per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 11 cycles</td><td>tERR(11per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across 12 cycles</td><td>tERR(12per)</td><td></td><td></td><td></td><td></td><td>ps</td><td></td></tr><tr><td>Cumulative error across n = 13, 14 . . . 49, 50 cycles</td><td>tERR(nper)</td><td></td><td></td><td></td><td></td><td>ps</td><td>24</td></tr><tr><td colspan="8">Data Timing</td></tr><tr><td>DQS, DQS# to DQ skew, per group, per access</td><td>tDQSQ</td><td>-</td><td>85</td><td>-</td><td>75</td><td>ps</td><td>13</td></tr><tr><td>DQ output hold time from DQS, DQS#</td><td>tQH</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>tCK(avg)</td><td>13, g</td></tr><tr><td>DQ low-impedance time from CK, CK#</td><td>tLZ(DQ)</td><td>- 390</td><td>195</td><td>- 360</td><td>180</td><td>ps</td><td>13, 14, f</td></tr><tr><td>DQ high impedance time from CK, CK#</td><td>tHZ(DQ)</td><td>-</td><td>195</td><td>-</td><td>180</td><td>ps</td><td>13, 14, f</td></tr><tr><td>Data setup time to DQS, DQS# referenced to Vih(ac) / Vil(ac) levels</td><td>tDS(base) AC150</td><td>TBD</td><td></td><td>TBD</td><td></td><td>ps</td><td>d, 17</td></tr><tr><td>Data setup time to DQS, DQS# referenced to Vih(ac) / Vil(ac) levels</td><td>tDS(base) AC125</td><td>TBD</td><td></td><td>TBD</td><td></td><td>ps</td><td>d, 17</td></tr><tr><td>Data hold time from DQS, DQS# referenced to Vih(dc) / Vil(dc) levels</td><td>tDH(base) DC100</td><td>TBD</td><td></td><td>TBD</td><td></td><td>ps</td><td>d, 17</td></tr></table>

# 13 Electrical Characteristics and AC Timing (Cont’d)

# 13.2 Timing Paramters for DDR3-1866 and DDR3-2133 Speed Bins (Cont’d)


Table 67 — Timing Parameters by Speed Bin (Cont’d)



NOTE: The following general notes from page 179 apply to Table 67: Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$


<table><tr><td colspan="2"></td><td colspan="2">DDR3-1866</td><td colspan="2">DDR3-2133</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>DQ and DM Input pulse width for each input</td><td>tDIPW</td><td>TBD</td><td>-</td><td>TBD</td><td>-</td><td>ps</td><td>28</td></tr><tr><td colspan="8">Data Strobe Timing</td></tr><tr><td>DQS,DQS# differential READ Preamble</td><td>tRPRE</td><td>0.9</td><td>Note 19</td><td>0.9</td><td>Note 19</td><td>tCK(avg)</td><td>13, 19, g</td></tr><tr><td>DQS, DQS# differential READ Postamble</td><td>tRPST</td><td>0.3</td><td>Note 11</td><td>0.3</td><td>Note 11</td><td>tCK(avg)</td><td>11, 13, g</td></tr><tr><td>DQS, DQS# differential output high time</td><td>tQSH</td><td>0.4</td><td>-</td><td>0.4</td><td>-</td><td>tCK(avg)</td><td>13, g</td></tr><tr><td>DQS, DQS# differential output low time</td><td>tQSL</td><td>0.4</td><td>-</td><td>0.4</td><td>-</td><td>tCK(avg)</td><td>13, g</td></tr><tr><td>DQS, DQS# differential WRITE Preamble</td><td>tWPRE</td><td>0.9</td><td>-</td><td>0.9</td><td>-</td><td>tCK(avg)</td><td></td></tr><tr><td>DQS, DQS# differential WRITE Postamble</td><td>tWPST</td><td>0.3</td><td>-</td><td>0.3</td><td>-</td><td>tCK(avg)</td><td></td></tr><tr><td>DQS, DQS# rising edge output access time from rising CK, CK#</td><td>tDQSCK</td><td>- 195</td><td>195</td><td>- 180</td><td>180</td><td>ps</td><td>13, f</td></tr><tr><td>DQS and DQS# low-impedance time (Referenced from RL - 1)</td><td>tLZ(DQS)</td><td>- 390</td><td>195</td><td>- 360</td><td>180</td><td>ps</td><td>13, 14, f</td></tr><tr><td>DQS and DQS# high-impedance time (Referenced from RL + BL/2)</td><td>tHZ(DQS)</td><td>-</td><td>195</td><td>-</td><td>180</td><td>ps</td><td>13, 14, f</td></tr><tr><td>DQS, DQS# differential input low pulse width</td><td>tDQSL</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>tCK(avg)</td><td>29, 31</td></tr><tr><td>DQS, DQS# differential input high pulse width</td><td>tDQSH</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>tCK(avg)</td><td>30, 31</td></tr><tr><td>DQS, DQS# rising edge to CK, CK# rising edge</td><td>tDQSS</td><td>- 0.27</td><td>0.27</td><td>- 0.27</td><td>0.27</td><td>tCK(avg)</td><td>c</td></tr><tr><td>DQS, DQS# falling edge setup time to CK, CK# rising edge</td><td>tDSS</td><td>0.18</td><td>-</td><td>0.18</td><td>-</td><td>tCK(avg)</td><td>c, 32</td></tr><tr><td>DQS, DQS# falling edge hold time from CK, CK# rising edge</td><td>tDSH</td><td>0.18</td><td>-</td><td>0.18</td><td>-</td><td>tCK(avg)</td><td>c, 32</td></tr><tr><td colspan="8">Command and Address Timing</td></tr><tr><td>DLL locking time</td><td>tDLLK</td><td>512</td><td>-</td><td>512</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Internal READ Command to PRECHARGE Command delay</td><td>tRTP</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td></td><td>e</td></tr><tr><td>Delay from start of internal write transaction to internal read command</td><td>tWTR</td><td>max(4nCK, 7.5ns)</td><td>-</td><td>max(4nCK, 7.5ns)</td><td>-</td><td></td><td>e, 18</td></tr><tr><td>WRITE recovery time</td><td>tWR</td><td>15</td><td>-</td><td>15</td><td>-</td><td>ns</td><td>e, 18</td></tr><tr><td>Mode Register Set command cycle time</td><td>tMRD</td><td>4</td><td>-</td><td>4</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Mode Register Set command update delay</td><td>tMOD</td><td>max(12nCK, 15ns)</td><td>-</td><td>max(12nCK, 15ns)</td><td>-</td><td></td><td></td></tr><tr><td>ACT to internal read or write delay time</td><td>tRCD</td><td colspan="2">See Table 64 on page 162</td><td colspan="2">See Table 65 on page 163</td><td></td><td>e</td></tr><tr><td>PRE command period</td><td>tRP</td><td colspan="2">See Table 64 on page 162</td><td colspan="2">See Table 65 on page 163</td><td></td><td>e</td></tr><tr><td>ACT to ACT or REF command period</td><td>tRC</td><td colspan="2">See Table 64 on page 162</td><td colspan="2">See Table 65 on page 163</td><td></td><td>e</td></tr><tr><td>CAS# to CAS# command delay</td><td>tCCD</td><td>4</td><td>-</td><td>4</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Auto precharge write recovery + precharge time</td><td>tDAL(min)</td><td colspan="4">WR + roundup(tRP / tCK(avg))</td><td>nCK</td><td></td></tr><tr><td>Multi-Purpose Register Recovery Time</td><td>tMPRR</td><td>1</td><td>-</td><td>1</td><td>-</td><td>nCK</td><td>22</td></tr><tr><td>ACTIVE to PRECHARGE command period</td><td>tRAS</td><td colspan="2">See Table 64 on page 162</td><td colspan="2">See Table 65 on page 163</td><td></td><td>e</td></tr><tr><td>ACTIVE to ACTIVE command period for 1KB page size</td><td>tRRD</td><td>TBD</td><td>-</td><td>TBD</td><td>-</td><td></td><td>e</td></tr></table>

# 13 Electrical Characteristics and AC Timing (Cont’d)

13.2 Timing Paramters for DDR3-1866 and DDR3-2133 Speed Bins (Cont’d) 


Table 67 — Timing Parameters by Speed Bin (Cont’d)



NOTE: The following general notes from page 179 apply to Table 67: Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$


<table><tr><td colspan="2"></td><td colspan="2">DDR3-1866</td><td colspan="2">DDR3-2133</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>ACTIVE to ACTIVE command period for 2KB page size</td><td>tRRD</td><td>TBD</td><td>-</td><td>TBD</td><td>-</td><td></td><td>e</td></tr><tr><td>Four activate window for 1KB page size</td><td>tFAW</td><td>TBD</td><td>-</td><td>TBD</td><td>-</td><td>ns</td><td>e</td></tr><tr><td>Four activate window for 2KB page size</td><td>tFAW</td><td>TBD</td><td>-</td><td>TBD</td><td>-</td><td>ns</td><td>e</td></tr><tr><td>Command and Address setup time to CK, CK# referenced to Vih(ac) / Vil(ac) levels</td><td>tIS(base) AC150</td><td>TBD</td><td></td><td>TBD</td><td></td><td>ps</td><td>b, 16</td></tr><tr><td>Command and Address setup time to CK, CK# referenced to Vih(ac) / Vil(ac) levels</td><td>tIS(base) AC125</td><td>TBD</td><td></td><td>TBD</td><td></td><td>ps</td><td>b, 16, 27</td></tr><tr><td>Command and Address hold time from CK, CK# referenced to Vih(dc) / Vil(dc) levels</td><td>tIH(base) DC100</td><td>TBD</td><td></td><td>TBD</td><td></td><td>ps</td><td>b, 16</td></tr><tr><td>Control and Address Input pulse width for each input</td><td>tIPW</td><td>535</td><td>-</td><td>470</td><td>-</td><td>ps</td><td>28</td></tr><tr><td colspan="8">Calibration Timing</td></tr><tr><td>Power-up and RESET calibration time</td><td>tZQinit</td><td>max(512nCK, 640ns)</td><td>-</td><td>max(512nCK, 640ns)</td><td>-</td><td></td><td></td></tr><tr><td>Normal operation Full calibration time</td><td>tZQoper</td><td>max(256nCK, 320ns)</td><td>-</td><td>max(256nCK, 320ns)</td><td>-</td><td></td><td></td></tr><tr><td>Normal operation Short calibration time</td><td>tZQCS</td><td>max(64nCK, 80ns)</td><td>-</td><td>max(64nCK, 80ns)</td><td>-</td><td></td><td>23</td></tr><tr><td colspan="8">Reset Timing</td></tr><tr><td>Exit Reset from CKE HIGH to a valid command</td><td>tXPR</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td></td><td></td></tr><tr><td colspan="8">Self Refresh Timings</td></tr><tr><td>Exit Self Refresh to commands not requiring a locked DLL</td><td>tXS</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td>max(5nCK, tRFC(min) + 10ns)</td><td>-</td><td></td><td></td></tr><tr><td>Exit Self Refresh to commands requiring a locked DLL</td><td>tXSDLL</td><td>tDLLK(min)</td><td>-</td><td>tDLLK(min)</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Minimum CKE low width for Self Refresh entry to exit timing</td><td>tCKESR</td><td>tCKE(min) + 1 nCK</td><td>-</td><td>tCKE(min) + 1 nCK</td><td>-</td><td></td><td></td></tr><tr><td>Valid Clock Requirement after Self Refresh Entry (SRE) or Power-Down Entry (PDE)</td><td>tCKSRE</td><td>max(5 nCK, 10ns)</td><td>-</td><td>max(5 nCK, 10 ns)</td><td>-</td><td></td><td></td></tr><tr><td>Valid Clock Requirement before Self Refresh Exit (SRX) or Power-Down Exit (PDX) or Reset Exit</td><td>tCKSRX</td><td>max(5 nCK, 10 ns)</td><td>-</td><td>max(5 nCK, 10 ns)</td><td>-</td><td></td><td></td></tr><tr><td colspan="8">Power Down Timings</td></tr><tr><td>Exit Power Down with DLL on to any valid command; Exit Precharge Power Down with DLL frozen to commands not requiring a locked DLL</td><td>tXP</td><td>max(3nCK, 6ns)</td><td>-</td><td>max(3nCK, 6ns)</td><td>-</td><td></td><td></td></tr><tr><td>Exit Precharge Power Down with DLL frozen to commands requiring a locked DLL</td><td>tXPDLL</td><td>max(10nCK, 24ns)</td><td>-</td><td>max(10nCK, 24ns)</td><td>-</td><td></td><td>2</td></tr><tr><td>CKE minimum pulse width</td><td>tCKE</td><td>max(3nCK 5ns)</td><td>-</td><td>max(3nCK, 5ns)</td><td>-</td><td></td><td></td></tr></table>

# 13 Electrical Characteristics and AC Timing (Cont’d)

# 13.2 Timing Paramters for DDR3-1866 and DDR3-2133 Speed Bins (Cont’d)


Table 67 — Timing Parameters by Speed Bin (Cont’d)



NOTE: The following general notes from page 179 apply to Table 67: Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$


<table><tr><td colspan="2"></td><td colspan="2">DDR3-1866</td><td colspan="2">DDR3-2133</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>Command pass disable delay</td><td>tCPDED</td><td>2</td><td>-</td><td>2</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Power Down Entry to Exit Timing</td><td>tPD</td><td>tCKE(min)</td><td>9 * tREFI</td><td>tCKE(min)</td><td>9 * tREFI</td><td></td><td>15</td></tr><tr><td>Timing of ACT command to Power Down entry</td><td>tACTPDEN</td><td>1</td><td>-</td><td>2</td><td>-</td><td>nCK</td><td>20</td></tr><tr><td>Timing of PRE or PREA command to Power Down entry</td><td>tPRPDEN</td><td>1</td><td>-</td><td>2</td><td>-</td><td>nCK</td><td>20</td></tr><tr><td>Timing of RD/RDA command to Power Down entry</td><td>tRDPDEN</td><td>RL + 4 + 1</td><td>-</td><td>RL + 4 + 1</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Timing of WR command to Power Down entry (BL8OTF, BL8MRS, BC4OTF)</td><td>tWRPDEN</td><td>WL + 4 + (tWR / tCK(avg))</td><td>-</td><td>WL + 4 + (tWR / tCK(avg))</td><td>-</td><td>nCK</td><td>9</td></tr><tr><td>Timing of WRA command to Power Down entry (BL8OTF, BL8MRS, BC4OTF)</td><td>tWRAPDEN</td><td>WL + 4 + WR + 1</td><td>-</td><td>WL + 4 + WR + 1</td><td>-</td><td>nCK</td><td>10</td></tr><tr><td>Timing of WR command to Power Down entry (BC4MRS)</td><td>tWRPDEN</td><td>WL + 2 + (tWR / tCK(avg))</td><td>-</td><td>WL + 2 + (tWR / tCK(avg))</td><td>-</td><td>nCK</td><td>9</td></tr><tr><td>Timing of WRA command to Power Down entry (BC4MRS)</td><td>tWRAPDEN</td><td>WL + 2 + WR + 1</td><td>-</td><td>WL + 2 + WR + 1</td><td>-</td><td>nCK</td><td>10</td></tr><tr><td>Timing of REF command to Power Down entry</td><td>tREFPDEN</td><td>1</td><td>-</td><td>2</td><td>-</td><td>nCK</td><td>20, 21</td></tr><tr><td>Timing of MRS command to Power Down entry</td><td>tMRSPDEN</td><td>tMOD(min)</td><td>-</td><td>tMOD(min)</td><td>-</td><td></td><td></td></tr><tr><td colspan="8">ODT Timings</td></tr><tr><td>ODT turn on Latency</td><td>ODTLon</td><td colspan="4">WL - 2 = CWL + AL - 2</td><td>nCK</td><td></td></tr><tr><td>ODT turn off Latency</td><td>ODTLoff</td><td colspan="4">WL - 2 = CWL + AL - 2</td><td>nCK</td><td></td></tr><tr><td>ODT high time without write command or with write command and BC4</td><td>ODTH4</td><td>4</td><td>-</td><td>4</td><td>-</td><td>nCK</td><td></td></tr><tr><td>ODT high time with Write command and BL8</td><td>ODTH8</td><td>6</td><td>-</td><td>6</td><td>-</td><td>nCK</td><td></td></tr><tr><td>Asynchronous RTT turn-on delay (Power-Down with DLL frozen)</td><td>tAONPD</td><td>2</td><td>8.5</td><td>2</td><td>8.5</td><td>ns</td><td></td></tr><tr><td>Asynchronous RTT turn-off delay (Power-Down with DLL frozen)</td><td>tAOFPD</td><td>2</td><td>8.5</td><td>2</td><td>8.5</td><td>ns</td><td></td></tr><tr><td>RTT turn-on</td><td>tAON</td><td>- 195</td><td>195</td><td>- 180</td><td>180</td><td>ps</td><td>7, f</td></tr><tr><td>RTT_Nom and RTT_WR turn-off time from ODTLoff reference</td><td>tAOF</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>tCK(avg)</td><td>8, f</td></tr><tr><td>RTT dynamic change skew</td><td>tADC</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>tCK(avg)</td><td>f</td></tr><tr><td colspan="8">Write Leveling Timings</td></tr><tr><td>First DQS/DQS# rising edge after write leveling mode is programmed</td><td>tWLMRD</td><td>40</td><td>-</td><td>40</td><td>-</td><td>nCK</td><td>3</td></tr><tr><td>DQS/DQS# delay after write leveling mode is programmed</td><td>tWLDQSEN</td><td>25</td><td>-</td><td>25</td><td>-</td><td>nCK</td><td>3</td></tr><tr><td>Write leveling setup time from rising CK, CK# crossing to rising DQS, DQS# crossing</td><td>tWLS</td><td>140</td><td>0</td><td>125</td><td>-</td><td>ps</td><td></td></tr></table>

# 13 Electrical Characteristics and AC Timing (Cont’d)

13.2 Timing Paramters for DDR3-1866 and DDR3-2133 Speed Bins (Cont’d) 


Table 67 — Timing Parameters by Speed Bin (Cont’d)



NOTE: The following general notes from page 179 apply to Table 67: Note a. $\mathrm { \Delta V D D = V D D Q = 1 . 5 V + / - 0 . 0 7 5 V }$


<table><tr><td colspan="2"></td><td colspan="2">DDR3-1866</td><td colspan="2">DDR3-2133</td><td colspan="2"></td></tr><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>Write leveling hold time from rising DQS, DQS# crossing to rising CK, CK# crossing</td><td>tWLH</td><td>140</td><td>-</td><td>125</td><td>-</td><td>ps</td><td></td></tr><tr><td>Write leveling output delay</td><td>tWLO</td><td>0</td><td>7.5</td><td>0</td><td>7.5</td><td>ns</td><td></td></tr><tr><td>Write leveling output error</td><td>tWLOE</td><td>0</td><td>2</td><td>0</td><td>2</td><td>ns</td><td></td></tr></table>

# 13 Electrical Characteristics and AC Timing (Cont’d)

# 13.3 Jitter Notes

<table><tr><td>Specific Note a</td><td>Unit &#x27;tCK(avg)&#x27; represents the actual tCK(avg) of the input clock under operation. Unit &#x27;nCK&#x27; represents one clock cycle of the input clock, counting the actual clock edges.ex) tMRD = 4 [nCK] means; if one Mode Register Set command is registered at Tm, another Mode Register Set command may be registered at Tm+4, even if (Tm+4 - Tm) is 4 x tCK(avg) + tERR(4per),min.</td></tr><tr><td>Specific Note b</td><td>These parameters are measured from a command/address signal (CKE, CS#, RAS#, CAS#, WE#, ODT, BA0, A0, A1, etc.) transition edge to its respective clock signal (CK/CK#) crossing. The spec values are not affected by the amount of clock jitter applied (i.e. tJIT(per), tJIT(cc), etc.), as the setup and hold are relative to the clock signal crossing that latches the command/address. That is, these parameters should be met whether clock jitter is present or not.</td></tr><tr><td>Specific Note c</td><td>These parameters are measured from a data strobe signal (DQS(L/U), DQS(L/U)#) crossing to its respective clock signal (CK, CK#) crossing. The spec values are not affected by the amount of clock jitter applied (i.e. tJIT(per), tJIT(cc), etc.), as these are relative to the clock signal crossing. That is, these parameters should be met whether clock jitter is present or not.</td></tr><tr><td>Specific Note d</td><td>These parameters are measured from a data signal (DM(L/U), DQ(L/U)0, DQ(L/U)1, etc.) transition edge to its respective data strobe signal (DQS(L/U), DQS(L/U)#) crossing.</td></tr><tr><td>Specific Note e</td><td>For these parameters, the DDR3 SDRAM device supports tnPARAM [nCK] = RU{ tPARAM [ns] / tCK(avg) [ns]}, which is in clock cycles, assuming all input clock jitter specifications are satisfied. For example, the device will support tnRP = RU{tRP / tCK(avg)}, which is in clock cycles, if all input clock jitter specifications are met. This means: For DDR3-800 6-6-6, of which tRP = 15ns, the device will support tnRP = RU{tRP / tCK(avg)} = 6, as long as the input clock jitter specifications are met, i.e. Precharge command at Tm and Active command at Tm+6 is valid even if (Tm+6 - Tm) is less than 15ns due to input clock jitter.</td></tr><tr><td>Specific Note f</td><td>When the device is operated with input clock jitter, this parameter needs to be derated by the actual tERR(mper),act of the input clock, where 2 &lt;= m &lt;= 12. (output deratings are relative to the SDRAM input clock.) For example, if the measured jitter into a DDR3-800 SDRAM has tERR(mper),act,min = -172 ps and tERR(mper),act,max = +193 ps, then tDQSCK,min(derated) = tDQSCK,min - tERR(mper),act,max = -400 ps - 193 ps = -593 ps and tDQSCK,max(derated) = tDQSCK,max - tERR(mper),act,min = 400 ps + 172 ps = +572 ps. Similarly, tLZ(DQ) for DDR3-800 derates to tLZ(DQ),min(derated) = -800 ps - 193 ps = -993 ps and tLZ(DQ),max(derated) = 400 ps + 172 ps = +572 ps. (Caution on the min/max usage!) Note that tERR(mper),act,min is the minimum measured value of tERR(nper) where 2 &lt;= n &lt;= 12, and tERR(mper),act,max is the maximum measured value of tERR(nper) where 2 &lt;= n &lt;= 12.</td></tr><tr><td>Specific Note g</td><td>When the device is operated with input clock jitter, this parameter needs to be derated by the actual tJIT(per),act of the input clock. (output deratings are relative to the SDRAM input clock.) For example, if the measured jitter into a DDR3-800 SDRAM has tCK(avg),act = 2500 ps, tJIT(per),act,min = -72 ps and tJIT(per),act,max = +93 ps, then tRPRE,min(derated) = tRPRE,min + tJIT(per),act,min = 0.9 x tCK(avg),act + tJIT(per),act,min = 0.9 x 2500 ps - 72 ps = +2178 ps. Similarly, tQH,min(derated) = tQH,min + tJIT(per),act,min = 0.38 x tCK(avg),act + tJIT(per),act,min = 0.38 x 2500 ps - 72 ps = +878 ps. (Caution on the min/max usage!)</td></tr></table>

# 13 Electrical Characteristics and AC Timing (Cont’d)

# 13.4 Timing Parameter Notes

NOTE 1. Actual value dependant upon measurement level definitions which are TBD. 

NOTE 2. Commands requiring a locked DLL are: READ (and RAP) and synchronous ODT commands. 

NOTE 3. The max values are system dependent. 

NOTE 4. WR as programmed in mode register 

NOTE 5. Value must be rounded-up to next higher integer value 

NOTE 6. There is no maximum cycle time limit besides the need to satisfy the refresh interval, tREFI. 

NOTE 7. For definition of RTT turn-on time tAON See 5.2.2 “Timing Parameters” on page 92. 

NOTE 8. For definition of RTT turn-off time tAOF See 5.2.2 “Timing Parameters” on page 92. 

NOTE 9. tWR is defined in ns, for calculation of tWRPDEN it is necessary to round up tWR / tCK to the next integer. 

NOTE 10. WR in clock cycles as programmed in MR0. 

NOTE 11. The maximum read postamble is bound by tDQSCK(min) plus tQSH(min) on the left side and tHZ(DQS)max on the right side. See Figure 28 — “Clock to Data Strobe Relationship” on page 58 

NOTE 12. Output timing deratings are relative to the SDRAM input clock. When the device is operated with input clock jitter, this parameter needs to be derated by t.b.d. 

NOTE 13. Value is only valid for RON34 

NOTE 14. Single ended signal parameter. Refer to chapter <t.b.d.> for definition and measurement method. 

NOTE 15. tREFI depends on TOPER 

NOTE 16. tIS(base) and tIH(base) values are for 1V/ns CMD/ADD single-ended slew rate and 2V/ns CK, CK# differential slew rate. Note for DQ and DM signals, VREF(DC) $=$ VRefDQ(DC). For input only pins except RESET#, VRef(DC) $=$ VRefCA(DC). See 13.5 “Address / Command Setup, Hold and Derating” on page 182 

NOTE 17. tDS(base) and tDH(base) values are for 1V/ns DQ single-ended slew rate and 2V/ns DQS, DQS# differential slew rate. Note for DQ and DM signals, VREF(DC) $=$ VRefDQ(DC). For input only pins except RESET#, VRef(DC) $=$ VRefCA(DC). See 13.6 “Data Setup, Hold and Slew Rate Derating” on page 189. 

NOTE 18. Start of internal write transaction is defined as follows: 

For BL8 (fixed by MRS and on- the-fly): Rising clock edge 4 clock cycles after WL. 

For BC4 (on- the- fly): Rising clock edge 4 clock cycles after WL. 

For BC4 (fixed by MRS): Rising clock edge 2 clock cycles after WL. 

NOTE 19. The maximum read preamble is bound by tLZ(DQS)min on the left side and tDQSCK(max) on the right side. See Figure 28 — “Clock to Data Strobe Relationship” on page 58 

NOTE 20. CKE is allowed to be registered low while operations such as row activation, precharge, autoprecharge or refresh are in progress, but power-down IDD spec will not be applied until finishing those operations. 

NOTE 21. Although CKE is allowed to be registered LOW after a REFRESH command once tREFP-DEN(min) is satisfied, there are cases where additional time such as tXPDLL(min) is also required. See 4.17.3 “Power-Down clarifications - Case $2 ^ { \circ }$ on page 87 

NOTE 22. Defined between end of MPR read burst and MRS which reloads MPR or disables MPR function. 

# 13 Electrical Characteristics and AC Timing (Cont’d)

# 13.4 Data Setup, Hold and Slew Rate Derating (Cont’d)

NOTE 23. One ZQCS command can effectively correct a minimum of $0 . 5 ~ \%$ (ZQ Correction) of RON and RTT impedance error within 64 nCK for all speed bins assuming the maximum sensitivities specified in the ‘Output Driver Voltage and Temperature Sensitivity’ and ‘ODT Voltage and Temperature Sensitivity’ tables. The appropriate interval between ZQCS commands can be determined from these tables and other application-specific parameters. 

One method for calculating the interval between ZQCS commands, given the temperature (Tdriftrate) and voltage (Vdriftrate) drift rates that the SDRAM is subject to in the application, is illustrated. The interval could be defined by the following formula: 

$$
\frac {Z Q C o r r e c t i o n}{(T S e n s \times T d r i f t r a t e) + (V S e n s \times V d r i f t r a t e)}
$$

where TSens $=$ max(dRTTdT, dRONdTM) and VSens $=$ max(dRTTdV, dRONdVM) define the SDRAM temperature and voltage sensitivities. 

For example, if TSens $= 1 . 5 \% / ^ { 0 } \mathrm { C }$ , VSens $= 0 . 1 5 \%$ / mV, Tdriftrate $= 1 ~ ^ { \mathrm { { o } } } \mathrm { { C } }$ / sec and Vdriftrate $= 1 5 \mathrm { m V }$ / sec, then the interval between ZQCS commands is calculated as: 

$$
\frac {0 . 5}{(1 . 5 \times 1) + (0 . 1 5 \times 1 5)} = 0. 1 3 3 \approx 1 2 8 m s
$$

NOTE 24. $\mathrm { n } = \mathrm { f r o m } \ 1 3 $ $\mathbf { n } =$ cycles to 50 cycles. This row defines 38 parameters. 

NOTE 25. tCH(abs) is the absolute instantaneous clock high pulse width, as measured from one rising edge to the following falling edge. 

NOTE 26. tCL(abs) is the absolute instantaneous clock low pulse width, as measured from one falling edge to the following rising edge. 

NOTE 27. The tIS(base) AC150 specifications are adjusted from the tIS(base) specification by adding an additional 100 ps of derating to accommodate for the lower alternate threshold of $1 5 0 \mathrm { m V }$ and another 25 ps to account for the earlier reference point $( 1 7 5 \mathrm { { m v } - 1 5 0 \mathrm { { m V } ) / 1 \mathrm { { V } / \mathrm { { n s } } ] } } }$ . 

NOTE 28. Pulse width of a input signal is defined as the width between the first crossing of Vref(dc) and the consecutive crossing of Vref(dc). 

NOTE 29. tDQSL describes the instantaneous differential input low pulse width on DQS - DQS#, as measured from one falling edge to the next consecutive rising edge. 

NOTE 30. tDQSH describes the instantaneous differential input high pulse width on DQS - DQS#, as measured from one rising edge to the next consecutive falling edge. 

NOTE 31. tDQSH,act $^ +$ tDQSL,act $= 1$ tCK,act ; with tXYZ,act being the actual measured value of the respective timing parameter in the application. 

NOTE 32. tDSH,act $^ +$ tDSS,act = 1 tCK,act ; with tXYZ,act being the actual measured value of the respective timing parameter in the application. 

# 13 Electrical Characteristics and AC Timing (Cont’d)

# 13.5 Address / Command Setup, Hold and Derating

For all input signals the total tIS (setup time) and tIH (hold time) required is calculated by adding the data sheet tIS(base) and tIH(base) value (see Table 68) to the ΔtIS and ΔtIH derating value (see Table 69) respectively. Example: tIS (total setup time) $) = \mathrm { t I S } ( \mathrm { b a s e } ) + \Delta \mathrm { t I S }$ $=$ 

Setup (tIS) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V _ { R E F ( d c ) } }$ and the first crossing of $\mathrm { V _ { I H ( a c ) } m i n }$ . Setup (tIS) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of $\mathrm { V _ { R E F ( d c ) } }$ and the first crossing of Vil(ac)max. If the actual signal is always earlier than the nominal slew rate line between shaded ${ } ^ { \mathrm { { } ^ { \circ } V _ { R E F ( d c ) } } }$ to ac region’, use nominal slew rate for derating value (see Figure 110). If the actual signal is later than the nominal slew rate line anywhere between shaded ${ } ^ { \mathrm { { } ^ { \circ } V _ { R E F ( d c ) } } }$ to ac region’, the slew rate of a tangent line to the actual signal from the ac level to $\mathrm { V _ { R E F ( d c ) } }$ level is used for derating value (see Figure 112). 

Hold (tIH) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of Vil(dc)max and the first crossing of $\mathrm { V } _ { \mathrm { R E F ( d c ) } }$ . Hold (tIH) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of Vih(dc)min and the first crossing of $\mathrm { V } _ { \mathrm { R E F ( d c ) } }$ . If the actual signal is always later than the nominal slew rate line between shaded ‘dc to $\mathrm { V } _ { \mathrm { R E F ( d c ) } }$ region’, use nominal slew rate for derating value (see Figure 111). If the actual signal is earlier than the nominal slew rate line anywhere between shaded ‘dc to VREF(dc) region’, the slew rate of a tangent line to the actual signal from the dc level to $\mathrm { V _ { R E F ( d c ) } }$ level is used for derating value (see Figure 113). 

For a valid transition the input signal has to remain above/below $\mathrm { V _ { I H / I L ( a c ) } }$ for some time tVAC (see Table 71). 

Although for slow slew rates the total setup time might be negative (i.e. a valid input signal will not have reached $\mathrm { V _ { I H / I L ( a c ) } }$ at the time of the rising clock transition, a valid input signal is still required to complete the transition and reach VIH/IL(ac). $\mathrm { V _ { I H / I L ( a c ) } }$ 

For slew rates in between the values listed in Table 69, the derating values may obtained by linear interpolation. 

These values are typically not subject to production test. They are verified by design and characterization. 


Table 68 — ADD/CMD Setup and Hold Base-Values for 1V/ns


<table><tr><td>Symbol</td><td>Reference</td><td>DDR3-800</td><td>DDR3-1066</td><td>DDR3-1333</td><td>DDR3-1600</td><td>Units</td></tr><tr><td>tIS(base) AC175</td><td>VIH/L(ac)</td><td>200</td><td>125</td><td>65</td><td>45</td><td>ps</td></tr><tr><td>tIS(base) AC150</td><td>VIH/L(ac)</td><td>350</td><td>275</td><td>190</td><td>170</td><td>ps</td></tr><tr><td>tIH(base) DC100</td><td>VIH/L(dc)</td><td>275</td><td>200</td><td>140</td><td>120</td><td>ps</td></tr></table>


NOTE 1. (ac/dc referenced for 1V/ns Address/Command slew rate and 2 V/ns differential CK-CK# slew rate) 



NOTE 2. The tIS(base) AC150 specifications are adjusted from the tIS(base) AC175 specification by adding an additional 125 ps for DDR3-800/1066 or 100ps for DDR3-1333/1600 of derating to accommodate for the lower alternate threshold of $1 5 0 ~ \mathrm { m V }$ and another 25 ps to account for the earlier reference point [(175 mv - 150 mV) / 1 V/ns]. 


13 Electrical Characteristics and AC Timing (Cont’d) 

13.5 Address / Command Setup, Hold and Derating (Cont’d) 


Table 69 — Derating values DDR3-800/1066/1333/1600 tIS/tIH - ac/dc based AC175 Threshold


<table><tr><td colspan="16">ΔtIS, ΔtIH derating in [ps] AC/DC based AC175 Threshold -&gt; VIH(ac)=VREF(dc)+175mV, VIL(ac)=VREF(dc)-175mV</td><td></td><td></td></tr><tr><td rowspan="3" colspan="2"></td><td colspan="14">CK,CK# Differential Slew Rate</td><td></td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td colspan="2">1.0 V/ns</td></tr><tr><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td></tr><tr><td rowspan="9">CMD/ADD Slew rate V/ns</td><td>2.0</td><td>88</td><td>50</td><td>88</td><td>50</td><td>88</td><td>50</td><td>96</td><td>58</td><td>104</td><td>66</td><td>112</td><td>74</td><td>120</td><td>84</td><td>128</td><td>100</td></tr><tr><td>1.5</td><td>59</td><td>34</td><td>59</td><td>34</td><td>59</td><td>34</td><td>67</td><td>42</td><td>75</td><td>50</td><td>83</td><td>58</td><td>91</td><td>68</td><td>99</td><td>84</td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td>24</td><td>24</td><td>32</td><td>34</td><td>40</td><td>50</td></tr><tr><td>0.9</td><td>-2</td><td>-4</td><td>-2</td><td>-4</td><td>-2</td><td>-4</td><td>6</td><td>4</td><td>14</td><td>12</td><td>22</td><td>20</td><td>30</td><td>30</td><td>38</td><td>46</td></tr><tr><td>0.8</td><td>-6</td><td>-10</td><td>-6</td><td>-10</td><td>-6</td><td>-10</td><td>2</td><td>-2</td><td>10</td><td>6</td><td>18</td><td>14</td><td>26</td><td>24</td><td>34</td><td>40</td></tr><tr><td>0.7</td><td>-11</td><td>-16</td><td>-11</td><td>-16</td><td>-11</td><td>-16</td><td>-3</td><td>-8</td><td>5</td><td>0</td><td>13</td><td>8</td><td>21</td><td>18</td><td>29</td><td>34</td></tr><tr><td>0.6</td><td>-17</td><td>-26</td><td>-17</td><td>-26</td><td>-17</td><td>-26</td><td>-9</td><td>-18</td><td>-1</td><td>-10</td><td>7</td><td>-2</td><td>15</td><td>8</td><td>23</td><td>24</td></tr><tr><td>0.5</td><td>-35</td><td>-40</td><td>-35</td><td>-40</td><td>-35</td><td>-40</td><td>-27</td><td>-32</td><td>-19</td><td>-24</td><td>-11</td><td>-16</td><td>-2</td><td>-6</td><td>5</td><td>10</td></tr><tr><td>0.4</td><td>-62</td><td>-60</td><td>-62</td><td>-60</td><td>-62</td><td>-60</td><td>-54</td><td>-52</td><td>-46</td><td>-44</td><td>-38</td><td>-36</td><td>-30</td><td>-26</td><td>-22</td><td>-10</td></tr></table>


Table 70 — Derating values DDR3-800/1066/1333/1600 tIS/tIH - ac/dc based - Alternate AC150 Threshold


<table><tr><td colspan="16">ΔtIS, ΔtIH derating in [ps] AC/DC based
Alternate AC150 Threshold -&gt; VIH(ac)=VREF(dc)+150mV, VIL(ac)=VREF(dc)-150mV</td><td></td><td></td></tr><tr><td rowspan="3" colspan="2"></td><td colspan="14">CK,CK# Differential Slew Rate</td><td></td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td>1.0 V/ns</td><td></td></tr><tr><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td></tr><tr><td rowspan="9">CMD/
ADD
Slew
rate
V/ns</td><td>2.0</td><td>75</td><td>50</td><td>75</td><td>50</td><td>75</td><td>50</td><td>83</td><td>58</td><td>91</td><td>66</td><td>99</td><td>74</td><td>107</td><td>84</td><td>115</td><td>100</td></tr><tr><td>1.5</td><td>50</td><td>34</td><td>50</td><td>34</td><td>50</td><td>34</td><td>58</td><td>42</td><td>66</td><td>50</td><td>74</td><td>58</td><td>82</td><td>68</td><td>90</td><td>84</td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td>24</td><td>24</td><td>32</td><td>34</td><td>40</td><td>50</td></tr><tr><td>0.9</td><td>0</td><td>-4</td><td>0</td><td>-4</td><td>0</td><td>-4</td><td>8</td><td>4</td><td>16</td><td>12</td><td>24</td><td>20</td><td>32</td><td>30</td><td>40</td><td>46</td></tr><tr><td>0.8</td><td>0</td><td>-10</td><td>0</td><td>-10</td><td>0</td><td>-10</td><td>8</td><td>-2</td><td>16</td><td>6</td><td>24</td><td>14</td><td>32</td><td>24</td><td>40</td><td>40</td></tr><tr><td>0.7</td><td>0</td><td>-16</td><td>0</td><td>-16</td><td>0</td><td>-16</td><td>8</td><td>-8</td><td>16</td><td>0</td><td>24</td><td>8</td><td>32</td><td>18</td><td>40</td><td>34</td></tr><tr><td>0.6</td><td>-1</td><td>-26</td><td>-1</td><td>-26</td><td>-1</td><td>-26</td><td>7</td><td>-18</td><td>15</td><td>-10</td><td>23</td><td>-2</td><td>31</td><td>8</td><td>39</td><td>24</td></tr><tr><td>0.5</td><td>-10</td><td>-40</td><td>-10</td><td>-40</td><td>-10</td><td>-40</td><td>-2</td><td>-32</td><td>6</td><td>-24</td><td>14</td><td>-16</td><td>22</td><td>-6</td><td>30</td><td>10</td></tr><tr><td>0.4</td><td>-25</td><td>-60</td><td>-25</td><td>-60</td><td>-25</td><td>-60</td><td>-17</td><td>-52</td><td>-9</td><td>-44</td><td>-1</td><td>-36</td><td>7</td><td>-26</td><td>15</td><td>-10</td></tr></table>

# 13 Electrical Characteristics and AC Timing (Cont’d)

13.5 Address / Command Setup, Hold and Derating (Cont’d) 


Table 71 — Required time tVAC above VIH(ac) {below VIL(ac)} for valid transition


<table><tr><td>Slew Rate [V/ns]</td><td colspan="2">\(t_{\text{VAC}}@ \text{AC175 [ps]}\)</td><td colspan="2">\(t_{\text{VAC}}@ \text{AC150 [ps]}\)</td></tr><tr><td></td><td>min</td><td>max</td><td>min</td><td>max</td></tr><tr><td>&gt;2.0</td><td>75</td><td>-</td><td>175</td><td>-</td></tr><tr><td>2.0</td><td>57</td><td>-</td><td>170</td><td>-</td></tr><tr><td>1.5</td><td>50</td><td>-</td><td>167</td><td>-</td></tr><tr><td>1.0</td><td>38</td><td>-</td><td>163</td><td>-</td></tr><tr><td>0.9</td><td>34</td><td>-</td><td>162</td><td>-</td></tr><tr><td>0.8</td><td>29</td><td>-</td><td>161</td><td>-</td></tr><tr><td>0.7</td><td>22</td><td>-</td><td>159</td><td>-</td></tr><tr><td>0.6</td><td>13</td><td>-</td><td>155</td><td>-</td></tr><tr><td>0.5</td><td>0</td><td>-</td><td>150</td><td>-</td></tr><tr><td>&lt;0.5</td><td>0</td><td>-</td><td>150</td><td>-</td></tr></table>

13 Electrical Characteristics and AC Timing (Cont’d) 

13.5 Address / Command Setup, Hold and Derating (Cont’d) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/8328e62701ee882c3ebd4fb7fbed23f4a3729adb70c4e1fe54d72b2debcde69f.jpg)



Figure 110 — Illustration of nominal slew rate and tVAC for setup time tIS (for ADD/CMD with respect to clock).


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/332128c4a917cd9c8ad3ba3ea8485cacb6e0e2357a32f397e2ce24b14ac5f7a3.jpg)



Figure 111 — Illustration of nominal slew rate for hold time $\mathbf { t _ { I H } }$ (for ADD/CMD with respect to clock).


13 Electrical Characteristics and AC Timing (Cont’d) 

13.5 Address / Command Setup, Hold and Derating (Cont’d) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/baff6770d5818f70c2783309b2c6019b118aa33538ba23414aaf2130d0ac2fa5.jpg)



Figure 112 — Illustration of tangent line for setup time tIS (for ADD/CMD with respect to clock)


13 Electrical Characteristics and AC Timing (Cont’d) 

13.5 Address / Command Setup, Hold and Derating (Cont’d) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/2140c4d3afeebb4e08f9c1ba7a2f3c0baaa239c43d11f0f6ba8998fc27a5c978.jpg)



Figure 113 — Illustration of tangent line for for hold time $\mathbf { t _ { I H } }$ (for ADD/CMD with respect to clock)


# 13 Electrical Characteristics and AC Timing (Cont’d)

# 13.6 Data Setup, Hold and Slew Rate Derating

For all input signals the total tDS (setup time) and tDH (hold time) required is calculated by adding the data sheet tDS(base) and tDH(base) value (see Table 72) to the $\Delta { \sf t D } \mathrm { S }$ and $\Delta { \sf t D H }$ (see Table 73) derating value respectively. Example: tDS (total setup time) $= \mathrm { t D S } ( \mathrm { b a s e } ) + \Delta \mathrm { t D S }$ $=$ . 

Setup (tDS) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V _ { R E F ( d c ) } }$ and the first crossing of $\mathrm { V _ { I H ( a c ) } m i n }$ . Setup (tDS) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of ${ \mathrm { V } } _ { \mathrm { R E F ( d c ) } }$ and the first crossing of $\mathrm { V _ { I L ( a c ) } m a x }$ (see Figure 114). If the actual signal is always earlier than the nominal slew rate line between shaded ${ } ^ { \mathrm { { } ^ { \circ } V _ { R E F ( d c ) } } }$ to ac region’, use nominal slew rate for derating value. If the actual signal is later than the nominal slew rate line anywhere between shaded ${ } ^ { \mathrm { { } ^ { \circ } V _ { R E F ( d c ) } } }$ to ac region’, the slew rate of a tangent line to the actual signal from the ac level to $\mathrm { V _ { R E F ( d c ) } }$ level is used for derating value (see Figure 116). 

Hold (tDH) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V _ { I L ( d c ) } m a x }$ and the first crossing of $\mathrm { V _ { R E F ( d c ) } }$ . Hold (tDH) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of $\mathrm { V _ { I H ( d c ) } m i n }$ and the first crossing of $\mathrm { V _ { R E F ( d c ) } }$ (see Figure 115). If the actual signal is always later than the nominal slew rate line between shaded ‘dc level to VREF(dc) region’, use nominal slew rate for derating value. If the actual signal is earlier than the nominal slew rate line anywhere between shaded ‘dc to $\mathrm { V _ { R E F ( d c ) } }$ region’, the slew rate of a tangent line to the actual signal from the dc level to $\mathrm { V } _ { \mathrm { R E F ( d c ) } }$ level is used for derating value (see Figure 117). 

For a valid transition the input signal has to remain above/below $\mathrm { V _ { I H / I L ( a c ) } }$ for some time tVAC (see Table 75). 

Although for slow slew rates the total setup time might be negative (i.e. a valid input signal will not have reached $\mathrm { V _ { I H / I L ( a c ) } }$ at the time of the rising clock transition) a valid input signal is still required to complete the transition and reach VIH/IL(ac). $\mathrm { V _ { I H / I L ( a c ) } }$ 

For slew rates in between the values listed in the tables the derating values may obtained by linear interpolation. 

These values are typically not subject to production test. They are verified by design and characterization. 


Table 72 — Data Setup and Hold Base-Values


<table><tr><td>Symbol</td><td>Reference</td><td>DDR3-800</td><td>DDR3-1066</td><td>DDR3-1333</td><td>DDR3-1600</td><td>Units</td></tr><tr><td>tDS(base) AC175</td><td>VIH/L(ac)</td><td>75</td><td>25</td><td>-</td><td>-</td><td>ps</td></tr><tr><td>tDS(base) AC150</td><td>VIH/L(ac)</td><td>125</td><td>75</td><td>30</td><td>10</td><td>ps</td></tr><tr><td>tDH(base) DC100</td><td>VIH/L(dc)</td><td>150</td><td>100</td><td>65</td><td>45</td><td>ps</td></tr></table>


NOTE: (ac/dc referenced for 1V/ns DQ-slew rate and 2 V/ns DQS slew rate) 


13 Electrical Characteristics and AC Timing (Cont’d) 

13.6 Data Setup, Hold and Slew Rate Derating (Cont’d) 


Table 73 — Derating values DDR3-800/1066 tDS/tDH - (AC175)


<table><tr><td colspan="17">ΔtDS, ΔDH derating in [ps] AC/DC based1</td><td></td></tr><tr><td rowspan="3" colspan="2"></td><td colspan="15">DQS, DQS# Differential Slew Rate</td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td>1.0 V/ns</td><td></td></tr><tr><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td></tr><tr><td rowspan="9">DQ Slew rate V/ns</td><td>2.0</td><td>88</td><td>50</td><td>88</td><td>50</td><td>88</td><td>50</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>1.5</td><td>59</td><td>34</td><td>59</td><td>34</td><td>59</td><td>34</td><td>67</td><td>42</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>0.9</td><td>-</td><td>-</td><td>-2</td><td>-4</td><td>-2</td><td>-4</td><td>6</td><td>4</td><td>14</td><td>12</td><td>22</td><td>20</td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>0.8</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-6</td><td>-10</td><td>2</td><td>-2</td><td>10</td><td>6</td><td>18</td><td>14</td><td>26</td><td>24</td><td>-</td><td>-</td></tr><tr><td>0.7</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-3</td><td>-8</td><td>5</td><td>0</td><td>13</td><td>8</td><td>21</td><td>18</td><td>29</td><td>34</td></tr><tr><td>0.6</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-1</td><td>-10</td><td>7</td><td>-2</td><td>15</td><td>8</td><td>23</td><td>24</td></tr><tr><td>0.5</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-11</td><td>-16</td><td>-2</td><td>-6</td><td>5</td><td>10</td></tr><tr><td>0.4</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-30</td><td>-26</td><td>-22</td><td>-10</td></tr></table>


NOTE 1. Cell contents shaded in red are defined as ‘not supported’. 



Table 74 — Derating values for DDR3-800/1066/1333/1600 tDS/tDH - (AC150)


<table><tr><td colspan="17">ΔtDS, ΔDH derating in [ps] AC/DC based1</td><td></td></tr><tr><td rowspan="3" colspan="2"></td><td colspan="15">DQS, DQS# Differential Slew Rate</td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td>1.0 V/ns</td><td></td></tr><tr><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td></tr><tr><td rowspan="9">DQ Slew rate V/ns</td><td>2.0</td><td>75</td><td>50</td><td>75</td><td>50</td><td>75</td><td>50</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>1.5</td><td>50</td><td>34</td><td>50</td><td>34</td><td>50</td><td>34</td><td>58</td><td>42</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>0.9</td><td>-</td><td>-</td><td>0</td><td>-4</td><td>0</td><td>-4</td><td>8</td><td>4</td><td>16</td><td>12</td><td>24</td><td>20</td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>0.8</td><td>-</td><td>-</td><td>-</td><td>-</td><td>0</td><td>-10</td><td>8</td><td>-2</td><td>16</td><td>6</td><td>24</td><td>14</td><td>32</td><td>24</td><td>-</td><td>-</td></tr><tr><td>0.7</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>8</td><td>-8</td><td>16</td><td>0</td><td>24</td><td>8</td><td>32</td><td>18</td><td>40</td><td>34</td></tr><tr><td>0.6</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>15</td><td>-10</td><td>23</td><td>-2</td><td>31</td><td>8</td><td>39</td><td>24</td></tr><tr><td>0.5</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>14</td><td>-16</td><td>22</td><td>-6</td><td>30</td><td>10</td></tr><tr><td>0.4</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>7</td><td>-26</td><td>15</td><td>-10</td></tr></table>


NOTE 1. Cell contents shaded in red are defined as ‘not supported’. 


# 13 Electrical Characteristics and AC Timing (Cont’d)

# 13.6 Data Setup, Hold and Slew Rate Derating (Cont’d)


Table 75 — Required time tVAC above VIH(ac) {below VIL(ac)} for valid transition


<table><tr><td>Slew Rate [V/ns]</td><td colspan="2">DDR3-800/1066 (AC175)</td><td colspan="2">DDR3-800/1066/1333/1600 (AC150)</td></tr><tr><td>Slew Rate [V/ns]</td><td colspan="2">tVAC [ps]</td><td colspan="2">tVAC [ps]</td></tr><tr><td></td><td>min</td><td>max</td><td>min</td><td>max</td></tr><tr><td>&gt;2.0</td><td>75</td><td>-</td><td>175</td><td>-</td></tr><tr><td>2.0</td><td>57</td><td>-</td><td>170</td><td>-</td></tr><tr><td>1.5</td><td>50</td><td>-</td><td>167</td><td>-</td></tr><tr><td>1.0</td><td>38</td><td>-</td><td>163</td><td>-</td></tr><tr><td>0.9</td><td>34</td><td>-</td><td>162</td><td>-</td></tr><tr><td>0.8</td><td>29</td><td>-</td><td>161</td><td>-</td></tr><tr><td>0.7</td><td>22</td><td>-</td><td>159</td><td>-</td></tr><tr><td>0.6</td><td>13</td><td>-</td><td>155</td><td>-</td></tr><tr><td>0.5</td><td>0</td><td>-</td><td>155</td><td>-</td></tr><tr><td>&lt;0.5</td><td>0</td><td>-</td><td>150</td><td>-</td></tr></table>

13 Electrical Characteristics and AC Timing (Cont’d) 

13.6 Data Setup, Hold and Slew Rate Derating (Cont’d) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/829e6dce5740077fca9570b2d4d49f2582866416890d3c10aa5052adc0d3a051.jpg)



Figure 114 — Illustration of nominal slew rate and tVAC for setup time tDS (for DQ with respect to strobe)


13 Electrical Characteristics and AC Timing (Cont’d) 

13.6 Data Setup, Hold and Slew Rate Derating (Cont’d) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/5d2b90910ed88eff141563fefcbf8d4d38cb3e347e7cfaccf401af294b917af9.jpg)



Figure 115 — Illustration of nominal slew rate for hold time $\mathbf { t _ { D H } }$ (for DQ with respect to strobe)


13 Electrical Characteristics and AC Timing (Cont’d) 

13.6 Data Setup, Hold and Slew Rate Derating (Cont’d) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/35a7eb94419030f4e61ce1355fd4c6719f4293a6be8a97ea6fb743523dbea37f.jpg)



Figure 116 — Illustration of tangent line for setup time $\bf { t _ { D S } }$ (for DQ with respect to strobe)


13 Electrical Characteristics and AC Timing (Cont’d) 

13.6 Data Setup, Hold and Slew Rate Derating (Cont’d) 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/8269a0c8ecbb3961257de32cb76dd6b89ce88f720711b1b1d4a24706a15d8017.jpg)


$$
\begin{array}{l} \frac {\text {H o l d S l e w R a t e}}{\text {R i s i n g S i g n a l}} = \frac {\text {t a n g e n t l i n e} [ V _ {\text {R E F (d c)}} - V _ {\text {I L (d c)}} \max ]}{\Delta \text {T R}} \\ \frac {\text {H o l d S l e w R a t e}}{\text {F a l l i n g S i g n a l}} = \frac {\text {t a n g e n t l i n e} [ V _ {\mathrm {I H (d c)}} \min  - V _ {\mathrm {R E F (d c)}} ]}{\Delta \mathrm {T F}} \\ \end{array}
$$


Figure 117 — Illustration of tangent line for for hold time $\mathbf { t _ { D H } }$ (for DQ with respect to strobe)


This page left blank. 

# Annex A (informative) Differences between JESD79-3D, and JESD79-3C.

This table briefly describes most of the changes made to this standard, JESD79-3D, compared to its predecessor, JESD79-3C. Some editorial changes are not included. 

<table><tr><td>Page</td><td>Description of Change</td></tr><tr><td>23, 29, 161-165</td><td>DDR3 1866/2133 latency value encodings and speed bins(added speed bin notes 9 and 10)</td></tr><tr><td>34, 36, 79</td><td>VrefDQ supply OFF in self-refresh(note 9 in Table 6, note in 16 Table 7, text updated in section 4.16)</td></tr><tr><td>58</td><td>tDQSCK clarification (added new note 2 to Fig-28)</td></tr><tr><td>70</td><td>n 4.14.2.3, 2nd par. update Fig 43 reference to Fig 51</td></tr><tr><td>77</td><td>DDR3 postponed refresh upon self-refresh entry clarification (/w edit)</td></tr><tr><td>79</td><td>DDR3 ZQ clarification</td></tr><tr><td>92, 163+</td><td>1866/2133 ac timing spec; deleted ODT Table 16, added into Table 67/68</td></tr><tr><td>115</td><td>Table 24 (Data input levels) removed first part of note1, updated VIH/IL AC175 entry</td></tr><tr><td>142</td><td>Table47 updated x4x8 / x16 to 1KB / 2KB page size</td></tr><tr><td>143</td><td>DDR3 Reset Current IDD8 definition</td></tr><tr><td>153</td><td>DDR3 Ci for 800/1066 speed bins</td></tr><tr><td>159</td><td>updated Supported CL row adding &#x27;5&#x27; to 1333H and 1333J bins</td></tr><tr><td>159, 165</td><td>DDR3-1333 Speed Bin modification</td></tr><tr><td>160</td><td>updated Supported CL row adding &#x27;5&#x27; to 1600K bin</td></tr><tr><td>160</td><td>DDR3-1333/1600 Speed Bin modification</td></tr><tr><td>161</td><td>updated note11 &quot;downshift&quot; to &quot;down binning&quot; and units/operand spacing</td></tr><tr><td>161-164, 166</td><td>DDR3 CL5 update (added speed bin notes 12 and 13)</td></tr><tr><td>163</td><td>1866/2133 ODT and Write Leveling timing; added to Table 68</td></tr><tr><td>163</td><td>1866/2133 data timing; added to Table 68</td></tr><tr><td>163+</td><td>1866/2133 data strobe timing; added to Table 68</td></tr><tr><td>163+</td><td>1866/2133 command/address timing; added to Table 68</td></tr><tr><td>163+</td><td>1866/2133 power-down timing</td></tr><tr><td>166</td><td>1866/2133 reset timing spec; added to Table 68</td></tr><tr><td>173</td><td>updated 800-1600 ZQ parameters to match 1866/2133 using max[nCK,ns] formula</td></tr><tr><td>179</td><td>1866/2133 tZQinit, tZQoper, tZQCS(added speed bin note 11)</td></tr><tr><td>180</td><td>1866/2133 tCCDmin</td></tr><tr><td>186</td><td>updated typo&#x27;s in section 13.5 and Table 68 heading format-columns</td></tr><tr><td>189-192</td><td>deleted DQS, DQS#, tDS, tDH from Figures 110-113</td></tr><tr><td>193</td><td>updated typo&#x27;s in section 13.6 and Table 72 heading format-columns</td></tr><tr><td>196-199</td><td>deleted CK, CK#, tIS, tIH from Figures 114-117</td></tr><tr><td>mult</td><td>DDR3 800/1066 DQ input level and tDS (updated tables 25,67,73,74,75)</td></tr></table>

# Annex A.1 (informative) Differences between JESD79-3C, and JESD79-3B.

This table briefly describes most of the changes made to this standard, JESD79-3C, compared to its predecessor, JESD79-3B. Some editorial changes are not included. 

<table><tr><td>Page</td><td>Description of Change</td></tr><tr><td>22</td><td>Updated Figure 7, tMRD Timing
Updated Figure 8, tMOD Timing</td></tr><tr><td>26</td><td>Updated Figure 10, MR1 Definition</td></tr><tr><td>33</td><td>Updated Table 6, Command Truth Table</td></tr><tr><td>63</td><td>Updated Figure 35, READ (BL8) to WRITE (BL8)
Updated Figure 36, READ (BC4) to WRITE (BC4) ETF</td></tr><tr><td>65</td><td>Updated Figure 39, READ (BL4) to WRITE (BL8) ETF
Updated Figure 40, READ (BL8) to WRITE (BC4) ETF</td></tr><tr><td>66</td><td>Updated Section 4.13.3, Burst REad Operation followed by a Precharge
Added Figure 41, READ to Precharge, RL=5, AL=0, CL=5, tRTP=4, tRP=5
Renumbered subsequent figures.</td></tr><tr><td>67</td><td>Added Figure 42, READ to Precharge, RL=8, AL=CL-2, CL=5, tRTP=6, tRP=5
Renumbered subsequent figures.</td></tr><tr><td>72</td><td>Updated Figure 48, WRITE (BC4) to READ (BC4) Operation
Updated Figure 49, WRITE (BC4) to PRECHARGE Operation
Added Figure 50, WRITE (BC4) ETF to PRECHARGE Operation
Renumbered subsequent figures.</td></tr><tr><td>73</td><td>Updated Figure 51, WRITE (BL8) to WRITE (BL8) Operation
Updated Figure 52, WRITE (BC4) to WRITE (BC4) ETF</td></tr><tr><td>74</td><td>Updated Figure 53, WRITE (BL8) to READ (BC4/BL8) ETF
Updated Figure 54, WRITE (BC4) to WRITE (BC4) ETF</td></tr><tr><td>75</td><td>Added Figure 55, WRITE (BC4) to READ (BC4)
Renumbered subsequent figures
Updated Figure 56, WRITE (BL8) to WRITE (BC4) ETF</td></tr><tr><td>76</td><td>Updated Figure 57, WRITE (BC4) to WRITE (BL8) ETF</td></tr><tr><td>77</td><td>Updated Section 4.15, Refresh Command</td></tr><tr><td>79</td><td>Updated Section 4.16, Self Refresh Operation</td></tr><tr><td>102</td><td>Updated Table 19, Asynchronous ODT Timing Paramaters for all Speed Bins</td></tr><tr><td>113</td><td>Updated Table 24, Single-Ended AC and DC Input Levels for Command and Address</td></tr><tr><td>128</td><td>Updated Table 39, Output Driver DC Electrical Characteristics</td></tr><tr><td>129</td><td>Updated Table 41, Output Driver Voltage and Temperature Sensitivity</td></tr><tr><td>39</td><td>Updated Section 10, IDD and IDDQ Specification Parameters and Test Conditions</td></tr><tr><td>140</td><td>Removed Figures 104, IDD1 Example
Removed Figures 105, IDD2N/IDD3N Example
Removed Figures 106, IDD4 Example
Added Figure 108, Measurement Setup and Test Load for IDD and IDDQ (option) Measurements
Added Figure 109, Correlation from Simulated Channel IO Power to Actual Channel IO Power supported by IDDQ Measurements</td></tr></table>

# Annex A.1 (informative) Differences between JESD79-3C, and JESD79-3B.

This table briefly describes most of the changes made to this standard, JESD79-3C, compared to its predecessor, JESD79-3B. Some editorial changes are not included. 

<table><tr><td>Page</td><td>Description of Change</td></tr><tr><td>141</td><td>Updated Table 47, Timings used for IDD and IDDQ Measurement-Loop Patterns
Updated Table 48, Basic IDD and IDDQ Measurement Conditions</td></tr><tr><td>144</td><td>Updated Table 49, IDD0 Measurement-Loop Pattern</td></tr><tr><td>145</td><td>Updated Table 50, IDD1 Measurement-Loop Pattern</td></tr><tr><td>146</td><td>Updated Table 51, IDD2N and IDD3N Measurement-Loop Pattern
Updated Table 52, IDD2NT and IDDQ2NT Measurement-Loop Pattern</td></tr><tr><td>147</td><td>Updated Table 53, IDD4R and IDDQ4R Measurement-Loop Pattern
Updated Table 54, IDD4W Measurement-Loop Pattern</td></tr><tr><td>148</td><td>Updated Table 55, IDD5B Measurement-Loop Pattern</td></tr><tr><td>149</td><td>Updated Table 56, IDD7 Measurement-Loop Pattern</td></tr><tr><td>150</td><td>Updated Table 57 IDD Specification Example 512M DDR3</td></tr><tr><td>153</td><td>Updated Table 59, Input/Output Capacitance</td></tr><tr><td>163-169</td><td>Updated Table 65, Timing Paramaters by Speed Bin</td></tr><tr><td>173</td><td>Updated Table 66, ADD/CMD Setup and Hold Base-Values for 1V/ns</td></tr><tr><td>174</td><td>Updated Table 68, Derating Values DDR3-800/1066/1333/1600 tIS/tIH ac/dc based - Alternate AC150 Threshold</td></tr></table>

# Annex A.2 (informative) Differences between JESD79-3B, and JESD79-3A.

This table briefly describes most of the changes made to this standard, JESD79-3B, compared to its predecessor, JESD79-3A. Some editorial changes and format-updates of figures are not included. 

<table><tr><td>Page</td><td>Description of Change</td></tr><tr><td>3-8</td><td>Updated bailout diagrams</td></tr><tr><td>9-11</td><td>Added bailouts for Quad-Stacked/Quadl-die DDR3 SDRAM in x4, x8, x16 bailout. Renumbered subsequent figures.</td></tr><tr><td>13</td><td>Updated Table 1, Input/Output Functional Description</td></tr><tr><td>17</td><td>Updated Figure 4, Simplified State Diagram</td></tr><tr><td>29</td><td>Updated Figure 11, MR2 Definition</td></tr><tr><td>44</td><td>Updated Figure 18, Timing Details of Write Leveling Sequence</td></tr><tr><td>45</td><td>Updated Figure 19, Timing Details of Write Leveling Exit</td></tr><tr><td>58</td><td>Updated Figure 28, Clock to Data Strobe Relationship</td></tr><tr><td>60</td><td>Updated Figure 30, tLZ and tHZ Method for Calculating Transitions and Endpoints</td></tr><tr><td>66</td><td>Updated Section 4.14.2.3; Strobe to Strobe and Strobe to Clock Violations</td></tr><tr><td>67</td><td>Added Section 4.14.3, Write Data Mask Updated Figure-41, Write Timing Definition and Parameters</td></tr><tr><td>74</td><td>Added Section 4.15, Refresh Command. Subsequent sections renumbered accordingly.</td></tr><tr><td>83</td><td>Updated Figure 67, MRS Command to Power Down Entry</td></tr><tr><td>89</td><td>Updated Figure 72, Sync ODT Timing Example.</td></tr><tr><td>99</td><td>Updated second paragraph in Section 5.4.2, Sync to Async ODT Mode Transition During Power-Down Entry</td></tr><tr><td>100</td><td>Updated Figure 81, Sync to async transition during Precharge Power Down (with DLL frozen)</td></tr><tr><td>101</td><td>updated Figures 82, Sync to async transition after Refresh command</td></tr><tr><td>111</td><td>Split Table 24 into two tables: Table 24, Single-Ended AC and DC Input Levels for Command and Address Table 25, Single-ended AC and DC Input Levels for DQ and DM</td></tr><tr><td>112</td><td>Added Section, 8.2, Vref Tolerances</td></tr><tr><td>113</td><td>Updated Figure 87, Definition of differential ac-swing and &quot;time above ac-level&quot;.</td></tr><tr><td>115</td><td>Updated Table 28, Single-ended levels for CK, DQS, DQSL, DQSU, CK#, DQS#, DQS#, DQSL# or DQSU#</td></tr><tr><td>116</td><td>Updated Table 29, Cross point voltage for differential input signals (CD, DQS).</td></tr><tr><td>117</td><td>Replaced Table 29, Single-Ended INput Slew Rate Definition Figure 83, Input NOMinal Slew RAte Definition for Singe-Ended Signals Section 8.4.1, Input Slew Rate for Input Setup Time and Data Setup Time Section 8.4.2 Input Slew Rate for Input Hold Time and Data Hold Time with reference to existing definitions of single-ended signals in Sections 13.3 and 13.4.</td></tr><tr><td>117</td><td>Updated Table 30, Differential Input Slew Rate Definition</td></tr><tr><td>139</td><td>Added summary Table 51, IDD Measurement Conditions, to replace existing Tables 51-54,56-57</td></tr><tr><td>147</td><td>Updated Table 55, Input/Output Capacitance</td></tr><tr><td>153</td><td>Updated Table 59, DDR3-1333 Speed Bins and Operating Conditions.</td></tr><tr><td>154</td><td>Updated Table 60, DDR3-1333 Speed Bins and Operating Conditions.</td></tr></table>

# Annex A.2 (informative) Differences between JESD79-3B, and JESD79-3A.

This table briefly describes most of the changes made to this standard, JESD79-3B, compared to its predecessor, JESD79-3A. Some editorial changes and format-updates of figures are not included. 

<table><tr><td>Page</td><td>Description of Change</td></tr><tr><td>157</td><td>Updated Table 61, Timing Parameters by Speed Bin</td></tr><tr><td>164</td><td>Updated and reordered Specific Notes a - g</td></tr><tr><td>165</td><td>Updated notes 11 and 19 for read tRPRE and tRPST and added reference to Fig-28.</td></tr><tr><td>A-1</td><td>Added Annex A (Informative) Differences between JESD79-3B and JESD79-3A.</td></tr></table>

# Annex A.3 (informative) Differences between JESD79-3A, and JESD79-3.

This table briefly describes most of the changes made to this standard, JESD79-3A, compared to its predecessor, JESD79-3. Some editorial changes and format-updates of figures are not included. 

<table><tr><td>Page</td><td>Description of Change</td></tr><tr><td>13</td><td>Per JCB-07-070, DDR3 SpecificationUpdated Figure 1 – Simplified State DiagramUpdated Table 2 – State Diagram Command Definitions</td></tr><tr><td>54</td><td>Per JCB-07-070, DDR3 SpecificationUpdated Section 4.13.2.1 – READ Timing; Clock to Data Strobe relationship</td></tr><tr><td>55</td><td>Per JCB-07-070, DDR3 SpecificationUpdated Section 4.13.2.2 – READ Timing; Data Strobe to Data Strobe relationship</td></tr><tr><td>57</td><td>Per JCB-07-070, DDR3 SpecificationAdded Figure 28 – Method for calculationtRPRE transitions and endpoints</td></tr><tr><td>63</td><td>Per JCB-07-070, DDR3 SpecificationRemoved Figure 40 – Write Timing ParametersMoved Figure 45, renamed as Write Timing Definition and Parameters, to page 63, as Figure 38</td></tr><tr><td>64</td><td>Per JCB-07-034, tWPRE, tWPSTAdded Section 4.14.3 – tWPRE CalculationAdded Section 4.14.4 – tWPST Calculation</td></tr><tr><td>72-79</td><td>Per JCB-07-070, DDR3 SpecificationReorganized subsections 4.16.1 and 4.16.2, moving Figures 52-61 into 4.16.1 and making one subsection each (4.16.2, 3, and 4) for the power-down entry/exit clarification cases (1-3).</td></tr><tr><td>75</td><td>Per JCB-07-070, DDR3 SpecificationRemoved Figure 57 – Active Power-Down Entry and Exit Timing Diagram</td></tr><tr><td>79</td><td>Per JCB-07-070, DDR3 SpecificationRemoved Table 15 – Timing Values tXXXPDEN Parameters</td></tr><tr><td>84</td><td>Per JCB-07-036, ODT Read TimingUpdated Figure 68 – OCT must be disabled...during Reads...</td></tr><tr><td>86</td><td>Per JCB-07-036, ODT Read TimingUpdated Section 5.2.3 – ODT During READs</td></tr><tr><td>96, 97</td><td>Per JCB-07-067, ZQ Input CapacitanceUpdated Section 5.5.1 – ZQ Calibration DescriptionReplaced Section 5.5.3. Is now: ZQ External Resistor Value, Tolerance, and Capacitance Loading</td></tr><tr><td>97</td><td>Per JCB-07-070, DDR3 SpecificationRemoved Table 22 – ZQ Calibration Command Truth Table</td></tr><tr><td>101</td><td>Per JCB-07-065, Vih(dc)max, Vil(dc)minUpdated Table 24 – Single Ended AC and DC Input Levels</td></tr><tr><td>103-106</td><td>Per JCB-07-068, Differentiation Signal Input SpecificationAdded Section 8.2 – AC and CD Logic Input Levels for Differential Signals</td></tr><tr><td>128</td><td>Per JCB-07-070, DDR3 SpecificationUpdated Table 50 – For IDD testing the followign parameters are utilized</td></tr></table>

# Annex A.3 (informative) Differences between JESD79-3A, and JESD79-3.

This table briefly describes most of the changes made to this standard, JESD79-3A, compared to its predecessor, JESD79-3. Some editorial changes and format-updates of figures are not included. 

<table><tr><td>Page</td><td>Description of Change</td></tr><tr><td>141</td><td>Per JCB-07-038, Capacitance
Updated Table 61 – Input/Output Capacitance</td></tr><tr><td>141</td><td>Per JCB-07-067, ZQ Input Capacitance
Updated Table 61 – Input/Output Capacitance</td></tr><tr><td>142, 143</td><td>Per JCB-07-070, DDR3 Specification
Removed unnumbered tables from subsection 12.1. Moved subsection 12.2 material into 12.1. Renumbered subsequent subsections.</td></tr><tr><td>149</td><td>Per JCB-07-041, tJIT (duty) note modification
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>149, 150</td><td>Per JCB-07-032, Cumulative Jitter
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>150</td><td>Per JCB-07-034, tWPRE, tWPST
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>150</td><td>Per JCB-07-040, Jitter Values for DDR3-1600
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>150</td><td>Per JCB-07-029, Jitter Output Derating
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>150</td><td>Per JCB-07-031, tDQSCK tQH
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>150</td><td>Per JCB-07-066, tQSH, tQSL values
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>152</td><td>Per JCB-07-042, tIS, tIH, DDR3-1333
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>154</td><td>Per JCB-07-035, tWLS, tWLH
Updated Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>156-158</td><td>Per JCB-07-033, tCH (abs) and tCL (abs)
Removed Specific Note F from Table 67 – Timing Parameters by Speed Bin. This action included removing the Table – Min and Max SPEC values.
Removed Note 22 from Table 67 – Timing Parameters by Speed Bin
Added Notes 25 and 26 to Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>157</td><td>Per JCB-07-039, tZQCS
Added Note 23</td></tr><tr><td>157, 158</td><td>Per JCB-07-039, tZQCS
Updated Note 23 of Table 67 – Timing Parameters by Speed Bin</td></tr><tr><td>158</td><td>Per JCB-07-042, tIS, tIH, DDR3-1333
Added Note 27</td></tr><tr><td>159</td><td>Per JCB-07-027
Updated Table 68 – ADD/CMD Setup and Hold Base-Values for 1V/ns</td></tr></table>

# Annex A.3 (informative) Differences between JESD79-3A, and JESD79-3.

This table briefly describes most of the changes made to this standard, JESD79-3A, compared to its predecessor, JESD79-3. Some editorial changes and format-updates of figures are not included. 

<table><tr><td>Page</td><td>Description of Change</td></tr><tr><td>160</td><td>Per JCB-07-027
Updated Table 69 – Derating values DDR3-800/1066/1333/1600 tS/tIH - ac/dc based
Added Table 70 – Derating values DDR3-1333/1600 tS/tIH - ac/dc based - Alternate AC150 Threshold</td></tr><tr><td>161</td><td>Per JCB-07-027
Updated Table 71 – Required time TVAC above VIH(ac) [below VIL(ac)] for valid transition</td></tr><tr><td>166</td><td>Per JCB-07-037, tDS, tDH 1333
Updated Table 72 – Data Setup and Hold Base-Values</td></tr><tr><td>A-1</td><td>Added Annex A (Informative) Differences between JESD79-3A and JESD79-3.</td></tr></table>

# Standard Improvement Form

JEDEC JESD79-3D 

The purpose of this form is to provide the Technical Committees of JEDEC with input from the industry regarding usage of the subject standard. Individuals or companies are invited to submit comments to JEDEC. All comments will be collected and dispersed to the appropriate committee(s). 

If you can provide input, please complete this form and return to: 

JEDEC 

Fax: 703.907.7583 

Attn: Publications Department 

3103 North 10th Street 

Suite 240 South 

Arlington, VA 22201-2107 

1. I recommend changes to the following: 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/f470ce531488e018908b2ce3cb9c66e4f241c532117d79f8fce829f147e18f2e.jpg)


Requirement, clause number 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/c739eb91b72102289b185a4f4f57b172470b805e199f81ff97aa510eb169911f.jpg)


Test method number 

Clause number 

The referenced clause number has proven to be: 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/a92b056100bc280f750b23ed5566ca5c2d1496e2fd3ca210c1c932fda0d3a2e7.jpg)


Unclear 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/a5701475004a556013bd44e44797238588d450278c519483d5f064920566d3fe.jpg)


Too Rigid 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/e0c64b674d8b246e29d9b315578d5939156a444b70f6e518cb522c1e29bcae3f.jpg)


In Error 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/48f9bb20-be46-4d6e-8406-be82d9b539f5/36d3d42f8d81b013205135d33690cd51a1af51d4ec9856796246d0d62269c95c.jpg)


Other 

2. Recommendations for correction: 

3. Other suggestions for document improvement: 

Submitted by 

Name: 

Phone: 

Company: 

E-mail: 

Address: 

City/State/Zip: 

Date: 

# JEDEC