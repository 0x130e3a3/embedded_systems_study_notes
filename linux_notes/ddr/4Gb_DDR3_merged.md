# DDR3L SDRAM

# MT41K1G4 – 128 Meg x 4 x 8 banks

# MT41K512M8 – 64 Meg x 8 x 8 banks

# MT41K256M16 – 32 Meg x 16 x 8 banks

# Description

DDR3L SDRAM (1.35V) is a low voltage version of the DDR3 (1.5V) SDRAM. Refer to DDR3 (1.5V) SDRAM (Die Rev :E) data sheet specifications when running in $1 . 5 \mathrm { V }$ compatible mode. 

# Features

• $\mathrm { V _ { D D } } = \mathrm { V _ { D D Q } } = 1 . 3 5 \mathrm { V }$ (1.283–1.45V) 

• Backward compatible to $\mathrm { V _ { D D } = V _ { D D Q } = 1 . 5 V \pm 0 . 0 7 5 V }$ – Supports DDR3L devices to be backward compatible in 1.5V applications 

• Differential bidirectional data strobe 

• $_ { 8 n }$ -bit prefetch architecture 

• Differential clock inputs (CK, CK#) 

• 8 internal banks 

• Nominal and dynamic on-die termination (ODT) for data, strobe, and mask signals 

• Programmable CAS (READ) latency (CL) 

• Programmable posted CAS additive latency (AL) 

• Programmable CAS (WRITE) latency (CWL) 

• Fixed burst length (BL) of 8 and burst chop (BC) of 4 (via the mode register set [MRS]) 

• Selectable BC4 or BL8 on-the-fly (OTF) 

• Self refresh mode 

• $\mathrm { T _ { C } }$ of $0 ^ { \circ } \mathrm { C }$ to $+ 9 5 ^ { \circ } \mathrm { C }$ – 64ms, 8192-cycle refresh at $0 ^ { \circ } \mathrm { C }$ to $+ 8 5 ^ { \circ } \mathrm { C }$ 

– 32ms at $+ 8 5 ^ { \circ } \mathrm { C }$ to $+ 9 5 ^ { \circ } \mathrm { C }$ 

• Self refresh temperature (SRT) 

• Automatic self refresh (ASR) 

• Write leveling 

• Multipurpose register 

• Output driver calibration 

<table><tr><td>Options</td><td>Marking</td></tr><tr><td>• Configuration</td><td></td></tr><tr><td>- 1 Gig x 4</td><td>1G4</td></tr><tr><td>- 512 Meg x 8</td><td>512M8</td></tr><tr><td>- 256 Meg x 16</td><td>256M16</td></tr><tr><td>• FBGA package (Pb-free) - x4, x8</td><td></td></tr><tr><td>- 78-ball (9mm x 10.5mm) Rev. E</td><td>RH</td></tr><tr><td>- 78-ball (7.5mm x 10.6mm) Rev. N</td><td>RG</td></tr><tr><td>- 78-ball (8mm x 10.5mm) Rev. P</td><td>DA</td></tr><tr><td>• FBGA package (Pb-free) - x16</td><td></td></tr><tr><td>- 96-ball (9mm x 14mm) Rev. E</td><td>HA</td></tr><tr><td>- 96-ball (7.5mm x 13.5mm) Rev. N</td><td>LY</td></tr><tr><td>- 96-ball (8mm x 14mm) Rev. P</td><td>TW</td></tr><tr><td>• Timing - cycle time</td><td></td></tr><tr><td>- 938ps @ CL = 14 (DDR3-2133)</td><td>-093</td></tr><tr><td>- 1.07ns @ CL = 13 (DDR3-1866)</td><td>-107</td></tr><tr><td>- 1.25ns @ CL = 11 (DDR3-1600)</td><td>-125</td></tr><tr><td>• Operating temperature</td><td></td></tr><tr><td>- Commercial (0°C ≤ TC ≤ +95°C)</td><td>None</td></tr><tr><td>- Industrial (-40°C ≤ TC ≤ +95°C)</td><td>IT</td></tr><tr><td>• Revision</td><td>:E/:N/:P</td></tr></table>


Table 1: Key Timing Parameters


<table><tr><td>Speed Grade</td><td>Data Rate (MT/s)</td><td>Target tRCD-tRP-CL</td><td>tRCD (ns)</td><td>tRP (ns)</td><td>CL (ns)</td></tr><tr><td>-093 1, 2</td><td>2133</td><td>14-14-14</td><td>13.09</td><td>13.09</td><td>13.09</td></tr><tr><td>-107 1</td><td>1866</td><td>13-13-13</td><td>13.91</td><td>13.91</td><td>13.91</td></tr><tr><td>-125</td><td>1600</td><td>11-11-11</td><td>13.75</td><td>13.75</td><td>13.75</td></tr></table>


Notes: 1. Backward compatible to 1600, $\mathsf { C L } = 1 1$ (-125). 



2. Backward compatible to 1866, CL = 13 (-107). 



Table 2: Addressing


<table><tr><td>Parameter</td><td>1 Gig x 4</td><td>512 Meg x 8</td><td>256 Meg x 16</td></tr><tr><td>Configuration</td><td>128 Meg x 4 x 8 banks</td><td>64 Meg x 8 x 8 banks</td><td>32 Meg x 16 x 8 banks</td></tr><tr><td>Refresh count</td><td>8K</td><td>8K</td><td>8K</td></tr><tr><td>Row address</td><td>64K (A[15:0])</td><td>64K (A[15:0])</td><td>32K (A[14:0])</td></tr><tr><td>Bank address</td><td>8 (BA[2:0])</td><td>8 (BA[2:0])</td><td>8 (BA[2:0])</td></tr><tr><td>Column address</td><td>2K (A[11, 9:0])</td><td>1K (A[9:0])</td><td>1K (A[9:0])</td></tr><tr><td>Page size</td><td>1KB</td><td>1KB</td><td>2KB</td></tr></table>


Figure 1: DDR3L Part Numbers


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/c10d6cd97cb856708542749e6ce65d71533e3005b96e55be86152137ee7fe032.jpg)



Note: 1. Not all options listed can be combined to define an offered product. Use the part catalog search on http://www.micron.com for available offerings.


# FBGA Part Marking Decoder

Due to space limitations, FBGA-packaged components have an abbreviated part marking that is different from the part number. For a quick conversion of an FBGA code, see the FBGA Part Marking Decoder on Micron’s Web site: http://www.micron.com. 

# Contents

State Diagram ......... 11 

Functional Description 12 

Industrial Temperature ....... 12 

General Notes 12 

Functional Block Diagrams ......... 14 

Ball Assignments and Descriptions .......... 16 

Package Dimensions ......... 22 

Electrical Specifications 28 

Absolute Ratings ........... 28 

Input/Output Capacitance ....... 29 

Thermal Characteristics ...... .. 30 

Electrical Specifications – IDD Specifications and Conditions ... 32 

Electrical Characteristics – Operating IDD Specifications . 4 3 

Electrical Specifications – DC and AC 47 

DC Operating Conditions ...... 47 

Input Operating Conditions ...... 48 

DDR3L 1.35V AC Overshoot/Undershoot Specification ........ 5 2 

DDR3L 1.35V Slew Rate Definitions for Single-Ended Input Signals 5 5 

DDR3L 1.35V Slew Rate Definitions for Differential Input Signals ... 5 7 

ODT Characteristics 58 

1.35V ODT Resistors .... 59 

ODT Sensitivity ..... 60 

ODT Timing Definitions .... 60 

Output Driver Impedance ....... 64 

34 Ohm Output Driver Impedance 65 

DDR3L 34 Ohm Driver ...... 66 

DDR3L 34 Ohm Output Driver Sensitivity ..... 67 

DDR3L Alternative 40 Ohm Driver .... 68 

DDR3L 40 Ohm Output Driver Sensitivity ........... 68 

Output Characteristics and Operating Conditions .... 7 0 

Reference Output Load . 73 

Slew Rate Definitions for Single-Ended Output Signals ........ 73 

Slew Rate Definitions for Differential Output Signals ........ 75 

Speed Bin Tables 76 

Electrical Characteristics and AC Operating Conditions 81 

Command and Address Setup, Hold, and Derating ..... 101 

Data Setup, Hold, and Derating ........... .... 108 

Commands – Truth Tables 116 

Commands . . 119 

DESELECT . 119 

NO OPERATION 119 

ZQ CALIBRATION LONG 119 

ZQ CALIBRATION SHORT . 119 

ACTIVATE 119 

READ . 119 

WRITE . 120 

PRECHARGE . 121 

REFRESH . 121 

SELF REFRESH . . 122 

DLL Disable Mode . . 123 

Input Clock Frequency Change ..... 127 

Write Leveling 129 

Write Leveling Procedure .. . 131 

Write Leveling Mode Exit Procedure . 133 

Initialization 134 

Voltage Initialization / Change ... .. 136 

$\mathrm { V _ { D D } }$ Voltage Switching ...... 137 

Mode Registers ......... 138 

Mode Register 0 (MR0) . . 139 

Burst Length ......... ...... 139 

Burst Type ....... . 140 

DLL RESET . . 141 

Write Recovery ......... ..... 142 

Precharge Power-Down (Precharge PD) ....... ..... 142 

CAS Latency (CL) .. . 142 

Mode Register 1 (MR1) .. .. 144 

DLL Enable/DLL Disable . . 144 

Output Drive Strength . 145 

OUTPUT ENABLE/DISABLE . . 145 

TDQS Enable .. . 145 

On-Die Termination . 146 

WRITE LEVELING . 146 

POSTED CAS ADDITIVE Latency ... . 146 

Mode Register 2 (MR2) . 147 

CAS Write Latency (CWL) .... ... 148 

AUTO SELF REFRESH (ASR) . . 148 

SELF REFRESH TEMPERATURE (SRT) . 148 

SRT vs. ASR . 149 

DYNAMIC ODT . 149 

Mode Register 3 (MR3) . . 149 

MULTIPURPOSE REGISTER (MPR) . 150 

MPR Functional Description . . 151 

MPR Register Address Definitions and Bursting Order ...... ...... 152 

MPR Read Predefined Pattern . 157 

MODE REGISTER SET (MRS) Command 157 

ZQ CALIBRATION Operation . 158 

ACTIVATE Operation ......... 159 

READ Operation . 161 

WRITE Operation .......... 172 

DQ Input Timing .... 180 

PRECHARGE Operation 182 

SELF REFRESH Operation .......... 182 

Extended Temperature Usage 184 

Power-Down Mode 185 

RESET Operation .... . 193 

On-Die Termination (ODT) . 195 

Functional Representation of ODT . ...... 195 

Nominal ODT . . 195 

Dynamic ODT 197 

Dynamic ODT Special Use Case .. . 197 

Functional Description .. . 197 

Synchronous ODT Mode ..... . 203 

ODT Latency and Posted ODT . . 203 

Timing Parameters . . 203 

ODT Off During READs . . 206 

Asynchronous ODT Mode 208 

Synchronous to Asynchronous ODT Mode Transition (Power-Down Entry) . . 210 

Asynchronous to Synchronous ODT Mode Transition (Power-Down Exit) 212 

Asynchronous to Synchronous ODT Mode Transition (Short CKE Pulse) ..... .... 214 

# List of Figures

Figure 1: DDR3L Part Numbers 2 

Figure 2: Simplified State Diagram ........... .... 11 

Figure 3: 1 Gig x 4 Functional Block Diagram .......... .... 14 

Figure 4: 512 Meg x 8 Functional Block Diagram .......... ... 15 

Figure 5: 256 Meg x 16 Functional Block Diagram .......... ... 15 

Figure 6: 78-Ball FBGA – x4, x8 (Top View) ....... 16 

Figure 7: 96-Ball FBGA – x16 (Top View) ...... 17 

Figure 8: 78-Ball FBGA – x4, x8 (RH) 2 2 

Figure 9: 78-Ball FBGA – x4, x8 (RG) 2 3 

Figure 10: 78-Ball FBGA – x4, x8 (DA) ........ 24 

Figure 11: 96-Ball FBGA – x16 (HA) ..... 2 5 

Figure 12: 96-Ball FBGA – x16 (LY) . 2 6 

Figure 13: 96-Ball FBGA – x16 (TW) ....... 2 7 

Figure 14: Thermal Measurement Point 30 

Figure 15: DDR3L 1.35V Input Signal ....... .... 51 

Figure 16: Overshoot ......... 52 

Figure 17: Undershoot ........ 53 

Figure 18: $\mathrm { V _ { I X } }$ for Differential Signals ....... 53 

Figure 19: Single-Ended Requirements for Differential Signals .......... .... 5 3 

Figure 20: Definition of Differential AC-Swing and t DVAC 5 4 

Figure 21: Nominal Slew Rate Definition for Single-Ended Input Signals . 5 6 

Figure 22: DDR3L 1.35V Nominal Differential Input Slew Rate Definition for DQS, DQS# and CK, CK# .............. 57 

Figure 23: ODT Levels and I-V Characteristics .. 5 8 

Figure 24: ODT Timing Reference Load .. 61 

Figure 25: t AON and t AOF Definitions ... 62 

Figure 26: t AONPD and t AOFPD Definitions .... 62 

Figure 27: t ADC Definition ...... 63 

Figure 28: Output Driver ... 64 

Figure 29: DQ Output Signal . 71 

Figure 30: Differential Output Signal . 7 2 

Figure 31: Reference Output Load for AC Timing and Output Slew Rate .......... 7 3 

Figure 32: Nominal Slew Rate Definition for Single-Ended Output Signals ...... 74 

Figure 33: Nominal Differential Output Slew Rate Definition for DQS, DQS# ......... 75 

Figure 34: Nominal Slew Rate and t VAC for t IS (Command and Address – Clock) 104 

Figure 35: Nominal Slew Rate for t IH (Command and Address – Clock) .. . 105 

Figure 36: Tangent Line for t IS (Command and Address – Clock) . 106 

Figure 37: Tangent Line for t IH (Command and Address – Clock) ... . 107 

Figure 38: Nominal Slew Rate and t VAC for t DS (DQ – Strobe) ....... 112 

Figure 39: Nominal Slew Rate for t DH (DQ – Strobe) ........ 113 

Figure 40: Tangent Line for t DS (DQ – Strobe) ........... .... 114 

Figure 41: Tangent Line for t DH (DQ – Strobe) . 115 

Figure 42: Refresh Mode . 122 

Figure 43: DLL Enable Mode to DLL Disable Mode 124 

Figure 44: DLL Disable Mode to DLL Enable Mode 125 

Figure 45: DLL Disable t DQSCK .. 126 

Figure 46: Change Frequency During Precharge Power-Down ............ 128 

Figure 47: Write Leveling Concept . 129 

Figure 48: Write Leveling Sequence .... 132 

Figure 49: Write Leveling Exit Procedure ....... 133 

Figure 50: Initialization Sequence .......... .... 135 

Figure 51: $\mathrm { V _ { D D } }$ Voltage Switching ........... . 137 

Figure 52: MRS to MRS Command Timing (t MRD) . ..... 138 

Figure 53: MRS to nonMRS Command Timing (t MOD) . 139 

Figure 54: Mode Register 0 (MR0) Definitions .. 140 

Figure 55: READ Latency .. .. 143 

Figure 56: Mode Register 1 (MR1) Definition ....... 144 

Figure 57: READ Latency $( \mathrm { A L } = 5 $ , $\mathrm { C L } = 6 $ ) ......... . 147 

Figure 58: Mode Register 2 (MR2) Definition ....... .... 147 

Figure 59: CAS Write Latency ......... ... 148 

Figure 60: Mode Register 3 (MR3) Definition 150 

Figure 61: Multipurpose Register (MPR) Block Diagram . 151 

Figure 62: MPR System Read Calibration with BL8: Fixed Burst Order Single Readout . . 153 

Figure 63: MPR System Read Calibration with BL8: Fixed Burst Order, Back-to-Back Readout .............. ...... 154 

Figure 64: MPR System Read Calibration with BC4: Lower Nibble, Then Upper Nibble ....... .... 155 

Figure 65: MPR System Read Calibration with BC4: Upper Nibble, Then Lower Nibble . 156 

Figure 66: ZQ CALIBRATION Timing (ZQCL and ZQCS) . 158 

Figure 67: Example: Meeting t RRD (MIN) and t RCD (MIN) . . 159 

Figure 68: Example: t FAW . 160 

Figure 69: READ Latency ... .. 161 

Figure 70: Consecutive READ Bursts (BL8) 163 

Figure 71: Consecutive READ Bursts (BC4) . . 163 

Figure 72: Nonconsecutive READ Bursts 164 

Figure 73: READ (BL8) to WRITE (BL8) . 164 

Figure 74: READ (BC4) to WRITE (BC4) OTF . 165 

Figure 75: READ to PRECHARGE (BL8) . 165 

Figure 76: READ to PRECHARGE (BC4) . 166 

Figure 77: READ to PRECHARGE $( \mathrm { A L } = 5 $ , $\mathrm { C L } = 6 $ ) . 166 

Figure 78: READ with Auto Precharge $\mathrm { ( A L = 4 }$ , $\mathrm { C L } = 6 $ ) . 166 

Figure 79: Data Output Timing – t DQSQ and Data Valid Window ...... .. 168 

Figure 80: Data Strobe Timing – READs . 169 

Figure 81: Method for Calculating t LZ and t HZ . . 170 

Figure 82: t RPRE Timing .......... 170 

Figure 83: t RPST Timing .......... 171 

Figure 84: t WPRE Timing ........... 173 

Figure 85: t WPST Timing ........... 173 

Figure 86: WRITE Burst .. 174 

Figure 87: Consecutive WRITE (BL8) to WRITE (BL8) . 175 

Figure 88: Consecutive WRITE (BC4) to WRITE (BC4) via OTF . 175 

Figure 89: Nonconsecutive WRITE to WRITE . 176 

Figure 90: WRITE (BL8) to READ (BL8) . 176 

Figure 91: WRITE to READ (BC4 Mode Register Setting) . 177 

Figure 92: WRITE (BC4 OTF) to READ (BC4 OTF) . 178 

Figure 93: WRITE (BL8) to PRECHARGE . 179 

Figure 94: WRITE (BC4 Mode Register Setting) to PRECHARGE . 179 

Figure 95: WRITE (BC4 OTF) to PRECHARGE 180 

Figure 96: Data Input Timing . .. 181 

Figure 97: Self Refresh Entry/Exit Timing ........... 183 

Figure 98: Active Power-Down Entry and Exit . 187 

Figure 99: Precharge Power-Down (Fast-Exit Mode) Entry and Exit . . 187 

Figure 100: Precharge Power-Down (Slow-Exit Mode) Entry and Exit . 188 

Figure 101: Power-Down Entry After READ or READ with Auto Precharge (RDAP) . . 188 

Figure 102: Power-Down Entry After WRITE 189 

Figure 103: Power-Down Entry After WRITE with Auto Precharge (WRAP) . 189 

Figure 104: REFRESH to Power-Down Entry .......... .... 190 

Figure 105: ACTIVATE to Power-Down Entry ........ .... 190 

Figure 106: PRECHARGE to Power-Down Entry ..... . 191 

Figure 107: MRS Command to Power-Down Entry . . 191 

Figure 108: Power-Down Exit to Refresh to Power-Down Entry . . 192 

Figure 109: RESET Sequence ..... .. 194 

Figure 110: On-Die Termination 195 

Figure 111: Dynamic ODT: ODT Asserted Before and After the WRITE, BC4 .. .. 200 

Figure 112: Dynamic ODT: Without WRITE Command . 200 

Figure 113: Dynamic ODT: ODT Pin Asserted Together with WRITE Command for 6 Clock Cycles, BL8 ............ 201 

Figure 114: Dynamic ODT: ODT Pin Asserted with WRITE Command for 6 Clock Cycles, BC4 .......... .... 202 

Figure 115: Dynamic ODT: ODT Pin Asserted with WRITE Command for 4 Clock Cycles, BC4 .......... .... 202 

Figure 116: Synchronous ODT . . 204 

Figure 117: Synchronous ODT (BC4) . 205 

Figure 118: ODT During READs . 207 

Figure 119: Asynchronous ODT Timing with Fast ODT Transition . 209 

Figure 120: Synchronous to Asynchronous Transition During Precharge Power-Down (DLL Off) Entry ............ 211 

Figure 121: Asynchronous to Synchronous Transition During Precharge Power-Down (DLL Off) Exit ............... 213 

Figure 122: Transition Period for Short CKE LOW Cycles with Entry and Exit Period Overlapping ..................... 215 

Figure 123: Transition Period for Short CKE HIGH Cycles with Entry and Exit Period Overlapping ................... 215 

# List of Tables

Table 1: Key Timing Parameters .......... .... 

Table 2: Addressing .. 

Table 3: 78-Ball FBGA – x4, x8 Ball Descriptions 18 

Table 4: 96-Ball FBGA – x16 Ball Descriptions .... . 20 

Table 5: Absolute Maximum Ratings ........... 28 

Table 6: DDR3L Input/Output Capacitance ........... 2 9 

Table 7: Thermal Characteristics . . 30 

Table 8: Thermal Impedance .... .. 31 

Table 9: Timing Parameters Used for IDD Measurements – Clock Units ........ 32 

Table 10: IDD0 Measurement Loop ........... 33 

Table 11: IDD1 Measurement Loop ........... .... 34 

Table 12: IDD Measurement Conditions for Power-Down Currents ... 3 5 

Table 13: IDD2N and IDD3N Measurement Loop ........... .... 36 

Table 14: IDD2NT Measurement Loop 36 

Table 15: IDD4R Measurement Loop ........... .. 37 

Table 16: IDD4W Measurement Loop ........ . 38 

Table 17: IDD5B Measurement Loop ............ . 39 

Table 18: IDD Measurement Conditions for IDD6, IDD6ET, and IDD8 .......... .. 4 0 

Table 19: IDD7 Measurement Loop ........... .. 41 

Table 20: IDD Maximum Limits Die Rev. E for 1.35/1.5V Operation . 43 

Table 21: IDD Maximum Limits Die Rev. N for 1.35V/1.5V Operation . . 44 

Table 22: IDD Maximum Limits Die Rev. P for 1.35V/1.5V Operation .. 46 

Table 23: DDR3L 1.35V DC Electrical Characteristics and Operating Conditions . 47 

Table 24: DDR3L 1.35V DC Electrical Characteristics and Input Conditions 4 8 

Table 25: DDR3L 1.35V Input Switching Conditions – Command and Address 4 9 

Table 26: DDR3L 1.35V Differential Input Operating Conditions (CK, CK# and DQS, DQS#) ... . 50 

Table 27: DDR3L Control and Address Pins .... 52 

Table 28: DDR3L 1.35V Clock, Data, Strobe, and Mask Pins 52 

Table 29: DDR3L 1.35V – Minimum Required Time t DVAC for CK/CK#, DQS/DQS# Differential for AC Ringback ... 54 

Table 30: Single-Ended Input Slew Rate Definition 55 

Table 31: DDR3L 1.35V Differential Input Slew Rate Definition 57 

Table 32: On-Die Termination DC Electrical Characteristics 58 

Table 33: 1.35V RTT Effective Impedance ......... 59 

Table 34: ODT Sensitivity Definition . 60 

Table 35: ODT Temperature and Voltage Sensitivity 60 

Table 36: ODT Timing Definitions 61 

Table 37: DDR3L(1.35V) Reference Settings for ODT Timing Measurements ....... 6 1 

Table 38: DDR3L 34 Ohm Driver Impedance Characteristics ....... 65 

Table 39: DDR3L 34 Ohm Driver Pull-Up and Pull-Down Impedance Calculations .......... 66 

Table 40: DDR3L 34 Ohm Driver $\mathrm { I _ { O H } / I _ { O L } }$ Characteristics: $\mathrm { V _ { D D } = V _ { D D Q } = D D R 3 L @ 1 . 3 5 V }$ .. ... 66 

Table 41: DDR3L 34 Ohm Driver $\mathrm { I _ { O H } / I _ { O L } }$ Characteristics: $\mathrm { V _ { D D } = V _ { D D Q } = D D R 3 L @ 1 . 4 5 V }$ . 66 

Table 42: DDR3L 34 Ohm Driver $\mathrm { I _ { O H } / I _ { O L } }$ Characteristics: $\mathrm { V _ { D D } = V _ { D D Q } = D D R 3 L } @ 1 . 2 8 3$ . .... 67 

Table 43: DDR3L 34 Ohm Output Driver Sensitivity Definition 67 

Table 44: DDR3L 34 Ohm Output Driver Voltage and Temperature Sensitivity ............ 6 7 

Table 45: DDR3L 40 Ohm Driver Impedance Characteristics 68 

Table 46: DDR3L 40 Ohm Output Driver Sensitivity Definition . 68 

Table 47: 40 Ohm Output Driver Voltage and Temperature Sensitivity . 69 

Table 48: DDR3L Single-Ended Output Driver Characteristics 70 

Table 49: DDR3L Differential Output Driver Characteristics . . 71 

Table 50: DDR3L Differential Output Driver Characteristics VOX(AC) ..... 72 

Table 51: Single-Ended Output Slew Rate Definition . 73 

Table 52: Differential Output Slew Rate Definition ........ 75 

Table 53: DDR3L-1066 Speed Bins . 7 6 

Table 54: DDR3L-1333 Speed Bins . 77 

Table 55: DDR3L-1600 Speed Bins . 78 

Table 56: DDR3L-1866 Speed Bins ......... 7 9 

Table 57: DDR3L-2133 Speed Bins ......... 8 0 

Table 58: Electrical Characteristics and AC Operating Conditions ......... 81 

Table 59: Electrical Characteristics and AC Operating Conditions for Speed Extensions ............ 91 

Table 60: DDR3L Command and Address Setup and Hold Values 1 V/ns Referenced – AC/DC-Based ............... 101 

Table 61: DDR3L-800/1066 Derating Values t IS/t IH – AC160/DC90-Based 102 

Table 62: DDR3L-800/1066/1333/1600 Derating Values for t IS/t IH – AC135/DC90-Based 102 

Table 63: DDR3L-1866/2133 Derating Values for t IS/t IH – AC125/DC90-Based . 102 

Table 64: DDR3L Minimum Required Time t VAC Above $\mathrm { V _ { I H ( A C ) } }$ (Below $\mathrm { { V } _ { I L [ A C ] } } ,$ ) for Valid ADD/CMD Transition . 103 

Table 65: DDR3L Data Setup and Hold Values at 1 V/ns (DQS, DQS# at 2 V/ns) – AC/DC-Based . 108 

Table 66: DDR3L Derating Values for t DS/t DH – AC160/DC90-Based . 109 

Table 67: DDR3L Derating Values for t DS/t DH – AC135/DC90-Based . 109 

Table 68: DDR3L Derating Values for t DS/t DH – AC130/DC90-Based at 2V/ns . 110 

Table 69: DDR3L Minimum Required Time t VAC Above $\mathrm { V _ { I H ( A C ) } }$ (Below $\mathrm { V _ { I L ( A C ) } } )$ for Valid DQ Transition ............. 111 

Table 70: Truth Table – Command 116 

Table 71: Truth Table – CKE 118 

Table 72: READ Command Summary .... . 120 

Table 73: WRITE Command Summary . 120 

Table 74: READ Electrical Characteristics, DLL Disable Mode . 126 

Table 75: Write Leveling Matrix . . 130 

Table 76: Burst Order . . 141 

Table 77: MPR Functional Description of MR3 Bits 151 

Table 78: MPR Readouts and Burst Order Bit Mapping .. . 152 

Table 79: Self Refresh Temperature and Auto Self Refresh Description ... 184 

Table 80: Self Refresh Mode Summary . . 184 

Table 81: Command to Power-Down Entry Parameters . 185 

Table 82: Power-Down Modes . 186 

Table 83: Truth Table – ODT (Nominal) ...... 196 

Table 84: ODT Parameters 196 

Table 85: Write Leveling with Dynamic ODT Special Case . . 197 

Table 86: Dynamic ODT Specific Parameters . 198 

Table 87: Mode Registers for $\mathrm { R _ { T T , n o m } }$ ........... 198 

Table 88: Mode Registers for $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ ....... 199 

Table 89: Timing Diagrams for Dynamic ODT .. 199 

Table 90: Synchronous ODT Parameters ....... . 204 

Table 91: Asynchronous ODT Timing Parameters for All Speed Bins ......... . 209 

Table 92: ODT Parameters for Power-Down (DLL Off) Entry and Exit Transition Period . . 211 

# State Diagram


Figure 2: Simplified State Diagram


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/007ce72ff4eae4b51d227aa643f4c680b7c4fed05260e26f9680a6179f626e36.jpg)


# Functional Description

DDR3 SDRAM uses a double data rate architecture to achieve high-speed operation. The double data rate architecture is an $_ { 8 n }$ -prefetch architecture with an interface designed to transfer two data words per clock cycle at the I/O pins. A single read or write operation for the DDR3 SDRAM effectively consists of a single $_ { 8 n }$ -bit-wide, four-clockcycle data transfer at the internal DRAM core and eight corresponding $n$ -bit-wide, onehalf-clock-cycle data transfers at the I/O pins. 

The differential data strobe (DQS, DQS#) is transmitted externally, along with data, for use in data capture at the DDR3 SDRAM input receiver. DQS is center-aligned with data for WRITEs. The read data is transmitted by the DDR3 SDRAM and edge-aligned to the data strobes. 

The DDR3 SDRAM operates from a differential clock (CK and CK#). The crossing of CK going HIGH and CK# going LOW is referred to as the positive edge of CK. Control, command, and address signals are registered at every positive edge of CK. Input data is registered on the first rising edge of DQS after the WRITE preamble, and output data is referenced on the first rising edge of DQS after the READ preamble. 

Read and write accesses to the DDR3 SDRAM are burst-oriented. Accesses start at a selected location and continue for a programmed number of locations in a programmed sequence. Accesses begin with the registration of an ACTIVATE command, which is then followed by a READ or WRITE command. The address bits registered coincident with the ACTIVATE command are used to select the bank and row to be accessed. The address bits registered coincident with the READ or WRITE commands are used to select the bank and the starting column location for the burst access. 

The device uses a READ and WRITE BL8 and BC4. An auto precharge function may be enabled to provide a self-timed row precharge that is initiated at the end of the burst access. 

As with standard DDR SDRAM, the pipelined, multibank architecture of DDR3 SDRAM allows for concurrent operation, thereby providing high bandwidth by hiding row precharge and activation time. 

A self refresh mode is provided, along with a power-saving, power-down mode. 

# Industrial Temperature

The industrial temperature (IT) device requires that the case temperature not exceed $- 4 0 ^ { \circ } \mathrm { C }$ or $9 5 ^ { \circ } \mathrm { C }$ . JEDEC specifications require the refresh rate to double when $\mathrm { T _ { C } }$ exceeds $8 5 ^ { \circ } \mathrm { C }$ ; this also requires use of the high-temperature self refresh option. Additionally, ODT resistance and the input/output impedance must be derated when TC is $< 0 ^ { \circ } \mathrm { C }$ or ${ } _ { > 9 5 ^ { \circ } \mathrm { C } }$ . 

# General Notes

• The functionality and the timing specifications discussed in this data sheet are for the DLL enable mode of operation (normal operation). 

• Throughout this data sheet, various figures and text refer to DQs as “DQ.” DQ is to be interpreted as any and all DQ collectively, unless specifically stated otherwise. 

• The terms “DQS” and “CK” found throughout this data sheet are to be interpreted as DQS, DQS# and CK, CK# respectively, unless specifically stated otherwise. 

• Complete functionality may be described throughout the document; any page or diagram may have been simplified to convey a topic and may not be inclusive of all requirements. 

• Any specific requirement takes precedence over a general statement. 

• Any functionality not specifically stated is considered undefined, illegal, and not supported, and can result in unknown operation. 

• Row addressing is denoted as A[n:0]. For example, 1Gb: $n = 1 2$ (x16); 1Gb: $n = 1 3$ (x4, x8); 2Gb: $n = 1 3$ (x16) and 2Gb: $n = 1 4$ (x4, x8); 4Gb: $n = 1 4$ (x16); and 4Gb: $n = 1 5$ (x4, x8). 

• Dynamic ODT has a special use case: when DDR3 devices are architected for use in a single rank memory array, the ODT ball can be wired HIGH rather than routed. Refer to the Dynamic ODT Special Use Case section. 

• A x16 device's DQ bus is comprised of two bytes. If only one of the bytes needs to be used, use the lower byte for data transfers and terminate the upper byte as noted: 

– Connect UDQS to ground via $1 \mathrm { k } \Omega ^ { * }$ resistor. 

– Connect UDQS# to $\mathrm { V _ { D D } }$ via $1 \mathrm { k } \Omega ^ { * }$ resistor. 

– Connect UDM to $\mathrm { V _ { D D } }$ via $1 \mathrm { k } \Omega ^ { * }$ resistor. 

– Connect DQ[15:8] individually to either $\mathrm { \Delta V _ { S S } , V _ { D D } }$ , or $\mathrm { V _ { R E F } }$ via 1kΩ resistors,* or float DQ[15:8]. 

*If ODT is used, 1kΩ resistor should be changed to 4x that of the selected ODT. 

# Functional Block Diagrams

DDR3 SDRAM is a high-speed, CMOS dynamic random access memory. It is internally configured as an 8-bank DRAM. 


Figure 3: 1 Gig x 4 Functional Block Diagram


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/d5cb935de7a621ab310754af41795705d71c8bbf67e020c31de6ca623b72388a.jpg)



Figure 4: 512 Meg x 8 Functional Block Diagram


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/6c923370a7f46dfec1d8e78f5d8245c0f09fdf65a922b2352784635922a25db4.jpg)



Figure 5: 256 Meg x 16 Functional Block Diagram


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/63698ed2d155dc4928627069cdb247deee62794fc13da4bc03f879d7dc48b74e.jpg)


# Ball Assignments and Descriptions


Figure 6: 78-Ball FBGA – x4, x8 (Top View)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/064ef40c737bfc7253d012744027efc98598b7e1d2fa3ea2732017b81ba139b0.jpg)


Notes: 1. Ball descriptions listed in Table 3 (page 18) are listed as $" \times 4 ,$ , $\times 8 ^ { \prime \prime }$ if unique; otherwise, x4 and x8 are the same. 

2. A comma separates the configuration; a slash defines a selectable function. Example ${ \mathsf { D } } 7 = { \mathsf { N } } { \mathsf { F } } ,$ NF/TDQS#. NF applies to the x4 configuration only. NF/TDQS# applies to the x8 configuration only—selectable between NF or TDQS# via MRS (symbols are defined in Table 3). 


Figure 7: 96-Ball FBGA – x16 (Top View)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/2d5fb2e0acb7a93255708ae5afc4cd92c39e97c5296e6f7cc7c6f31063675492.jpg)



Notes: 1. Ball descriptions listed in Table 4 (page 20) are listed as “x4, $\times 8 ^ { \prime \prime }$ if unique; otherwise, x4 and x8 are the same.



2. A comma separates the configuration; a slash defines a selectable function. Example ${ \mathsf { D } } 7 = { \mathsf { N } } { \mathsf { F } } ,$ , NF/TDQS#. NF applies to the x4 configuration only. NF/TDQS# applies to the x8 configuration only—selectable between NF or TDQS# via MRS (symbols are defined in Table 3).



Table 3: 78-Ball FBGA – x4, x8 Ball Descriptions


<table><tr><td>Symbol</td><td>Type</td><td>Description</td></tr><tr><td>A[15:13], A12/BC#, A11, A10/AP, A[9:0]</td><td>Input</td><td>Address inputs: Provide the row address for ACTIVATE commands, and the column address and auto precharge bit (A10) for READ/WRITE commands, to select one location out of the memory array in the respective bank. A10 sampled during a PRECHARGE command determines whether the PRECHARGE applies to one bank (A10 LOW, bank selected by BA[2:0]) or all banks (A10 HIGH). The address inputs also provide the op-code during a LOAD MODE command. Address inputs are referenced to VREFCA. A12/BC#: When enabled in the mode register (MR), A12 is sampled during READ and WRITE commands to determine whether burst chop (on-the-fly) will be performed (HIGH = BL8 or no burst chop, LOW = BC4). See Table 70 (page 116).</td></tr><tr><td>BA[2:0]</td><td>Input</td><td>Bank address inputs: BA[2:0] define the bank to which an ACTIVATE, READ, WRITE, or PRECHARGE command is being applied. BA[2:0] define which mode register (MR0, MR1, MR2, or MR3) is loaded during the LOAD MODE command. BA[2:0] are referenced to VREFCA.</td></tr><tr><td>CK, CK#</td><td>Input</td><td>Clock: CK and CK# are differential clock inputs. All control and address input signals are sampled on the crossing of the positive edge of CK and the negative edge of CK#. Output data strobe (DQS, DQS#) is referenced to the crossings of CK and CK#.</td></tr><tr><td>CKE</td><td>Input</td><td>Clock enable: CKE enables (registered HIGH) and disables (registered LOW) internal circuitry and clocks on the DRAM. The specific circuitry that is enabled/disabled is dependent upon the DDR3 SDRAM configuration and operating mode. Taking CKE LOW provides PRECHARGE POWER-DOWN and SELF REFRESH operations (all banks idle), or active power-down (row active in any bank). CKE is synchronous for power-down entry and exit and for self refresh entry. CKE is asynchronous for self refresh exit. Input buffers (excluding CK, CK#, CKE, RESET#, and ODT) are disabled during POWER-DOWN. Input buffers (excluding CKE and RESET#) are disabled during SELF REFRESH. CKE is referenced to VREFCA.</td></tr><tr><td>CS#</td><td>Input</td><td>Chip select: CS# enables (registered LOW) and disables (registered HIGH) the command decoder. All commands are masked when CS# is registered HIGH. CS# provides for external rank selection on systems with multiple ranks. CS# is considered part of the command code. CS# is referenced to VREFCA.</td></tr><tr><td>DM</td><td>Input</td><td>Input data mask: DM is an input mask signal for write data. Input data is masked when DM is sampled HIGH along with the input data during a write access. Although the DM ball is input-only, the DM loading is designed to match that of the DQ and DQS balls. DM is referenced to VREFDQ. DM has an optional use as TDQS on the x8.</td></tr><tr><td>ODT</td><td>Input</td><td>On-die termination: ODT enables (registered HIGH) and disables (registered LOW) termination resistance internal to the DDR3 SDRAM. When enabled in normal operation, ODT is only applied to each of the following balls: DQ[7:0], DQS, DQS#, and DM for the x8; DQ[3:0], DQS, DQS#, and DM for the x4. The ODT input is ignored if disabled via the LOAD MODE command. ODT is referenced to VREFCA.</td></tr><tr><td>RAS#, CAS#, WE#</td><td>Input</td><td>Command inputs: RAS#, CAS#, and WE# (along with CS#) define the command being entered and are referenced to VREFCA.</td></tr><tr><td>RESET#</td><td>Input</td><td>Reset: RESET# is an active LOW CMOS input referenced to VSS. The RESET# input receiver is a CMOS input defined as a rail-to-rail signal with DC HIGH ≥ 0.8 × VDD and DC LOW ≤ 0.2 × VDDQ. RESET# assertion and desertion are asynchronous.</td></tr><tr><td>DQ[3:0]</td><td>I/O</td><td>Data input/output: Bidirectional data bus for the x4 configuration. DQ[3:0] are referenced to VREFDQ.</td></tr><tr><td>DQ[7:0]</td><td>I/O</td><td>Data input/output: Bidirectional data bus for the x8 configuration. DQ[7:0] are referenced to VREFDQ.</td></tr><tr><td>DQS, DQS#</td><td>I/O</td><td>Data strobe: Output with read data. Edge-aligned with read data. Input with write data. Center-aligned to write data.</td></tr><tr><td>TDQS, TDQS#</td><td>Output</td><td>Termination data strobe: Applies to the x8 configuration only. When TDQS is enabled, DM is disabled, and the TDQS and TDQS# balls provide termination resistance.</td></tr><tr><td>VDD</td><td>Supply</td><td>Power supply: 1.5V ±0.075V.</td></tr><tr><td>VDDQ</td><td>Supply</td><td>DQ power supply: 1.5V ±0.075V. Isolated on the device for improved noise immuni-ty.</td></tr><tr><td>VREFCA</td><td>Supply</td><td>Reference voltage for control, command, and address: VREFCA must be maintained at all times (including self refresh) for proper device operation.</td></tr><tr><td>VREFDQ</td><td>Supply</td><td>Reference voltage for data: VREFDQ must be maintained at all times (excluding self refresh) for proper device operation.</td></tr><tr><td>VSS</td><td>Supply</td><td>Ground.</td></tr><tr><td>VSSQ</td><td>Supply</td><td>DQ ground: Isolated on the device for improved noise immunity.</td></tr><tr><td>ZQ</td><td>Reference</td><td>External reference ball for output drive calibration: This ball is tied to an external 240Ω resistor (RZQ), which is tied to VSSQ.</td></tr><tr><td>NC</td><td>-</td><td>No connect: These balls should be left unconnected (the ball has no connection to the DRAM or to other balls).</td></tr><tr><td>NF</td><td>-</td><td>No function: When configured as a x4 device, these balls are NF. When configured as a x8 device, these balls are defined as TDQS#, DQ[7:4].</td></tr></table>


Table 4: 96-Ball FBGA – x16 Ball Descriptions


<table><tr><td>Symbol</td><td>Type</td><td>Description</td></tr><tr><td>A[14:13], A12/BC#, A11, A10/AP, A[9:0]</td><td>Input</td><td>Address inputs: Provide the row address for ACTIVATE commands, and the column address and auto precharge bit (A10) for READ/WRITE commands, to select one location out of the memory array in the respective bank. A10 sampled during a PRECHARGE command determines whether the PRECHARGE applies to one bank (A10 LOW, bank selected by BA[2:0]) or all banks (A10 HIGH). The address inputs also provide the op-code during a LOAD MODE command. Address inputs are referenced to VREFCA. A12/BC#: When enabled in the mode register (MR), A12 is sampled during READ and WRITE commands to determine whether burst chop (on-the-fly) will be performed (HIGH = BL8 or no burst chop, LOW = BC4). See Table 70 (page 116).</td></tr><tr><td>BA[2:0]</td><td>Input</td><td>Bank address inputs: BA[2:0] define the bank to which an ACTIVATE, READ, WRITE, or PRECHARGE command is being applied. BA[2:0] define which mode register (MR0, MR1, MR2, or MR3) is loaded during the LOAD MODE command. BA[2:0] are referenced to VREFCA.</td></tr><tr><td>CK, CK#</td><td>Input</td><td>Clock: CK and CK# are differential clock inputs. All control and address input signals are sampled on the crossing of the positive edge of CK and the negative edge of CK#. Output data strobe (DQS, DQS#) is referenced to the crossings of CK and CK#.</td></tr><tr><td>CKE</td><td>Input</td><td>Clock enable: CKE enables (registered HIGH) and disables (registered LOW) internal circuitry and clocks on the DRAM. The specific circuitry that is enabled/disabled is dependent upon the DDR3 SDRAM configuration and operating mode. Taking CKE LOW provides PRECHARGE POWER-DOWN and SELF REFRESH operations (all banks idle), or active power-down (row active in any bank). CKE is synchronous for power-down entry and exit and for self refresh entry. CKE is asynchronous for self refresh exit. Input buffers (excluding CK, CK#, CKE, RESET#, and ODT) are disabled during POWER-DOWN. Input buffers (excluding CKE and RESET#) are disabled during SELF REFRESH. CKE is referenced to VREFCA.</td></tr><tr><td>CS#</td><td>Input</td><td>Chip select: CS# enables (registered LOW) and disables (registered HIGH) the command decoder. All commands are masked when CS# is registered HIGH. CS# provides for external rank selection on systems with multiple ranks. CS# is considered part of the command code. CS# is referenced to VREFCA.</td></tr><tr><td>LDM</td><td>Input</td><td>Input data mask: LDM is a lower-byte, input mask signal for write data. Lower-byte input data is masked when LDM is sampled HIGH along with the input data during a write access. Although the LDM ball is input-only, the LDM loading is designed to match that of the DQ and DQS balls. LDM is referenced to VREFDQ.</td></tr><tr><td>ODT</td><td>Input</td><td>On-die termination: ODT enables (registered HIGH) and disables (registered LOW) termination resistance internal to the DDR3 SDRAM. When enabled in normal operation, ODT is only applied to each of the following balls: DQ[15:0], LDQS, LDQS#, UDQS, UDQS#, LDM, and UDM for the x16; DQ0[7:0], DQS, DQS#, DM/TDQS, and NF/TDQS# (when TDQS is enabled) for the x8; DQ[3:0], DQS, DQS#, and DM for the x4. The ODT input is ignored if disabled via the LOAD MODE command. ODT is referenced to VREFCA.</td></tr><tr><td>RAS#, CAS#, WE#</td><td>Input</td><td>Command inputs: RAS#, CAS#, and WE# (along with CS#) define the command being entered and are referenced to VREFCA.</td></tr><tr><td>RESET#</td><td>Input</td><td>Reset: RESET# is an active LOW CMOS input referenced to VSS. The RESET# input receiver is a CMOS input defined as a rail-to-rail signal with DC HIGH ≥ 0.8 × VDD and DC LOW ≤ 0.2 × VDDQ. RESET# assertion and desertion are asynchronous.</td></tr><tr><td>UDM</td><td>Input</td><td>Input data mask: UDM is an upper-byte, input mask signal for write data. Upper-byte input data is masked when UDM is sampled HIGH along with that input data during a WRITE access. Although the UDM ball is input-only, the UDM loading is designed to match that of the DQ and DQS balls. UDM is referenced to VREFDQ.</td></tr><tr><td>DQ[7:0]</td><td>I/O</td><td>Data input/output: Lower byte of bidirectional data bus for the x16 configuration. DQ[7:0] are referenced to VREFDQ.</td></tr><tr><td>DQ[15:8]</td><td>I/O</td><td>Data input/output: Upper byte of bidirectional data bus for the x16 configuration. DQ[15:8] are referenced to VREFDQ.</td></tr><tr><td>LDQS, LDQS#</td><td>I/O</td><td>Lower byte data strobe: Output with read data. Edge-aligned with read data. Input with write data. Center-aligned to write data.</td></tr><tr><td>UDQS, UDQS#</td><td>I/O</td><td>Upper byte data strobe: Output with read data. Edge-aligned with read data. Input with write data. DQS is center-aligned to write data.</td></tr><tr><td>VDD</td><td>Supply</td><td>Power supply: 1.5V ±0.075V.</td></tr><tr><td>VDDQ</td><td>Supply</td><td>DQ power supply: 1.5V ±0.075V. Isolated on the device for improved noise immuni-ty.</td></tr><tr><td>VREFCA</td><td>Supply</td><td>Reference voltage for control, command, and address: VREFCA must be maintained at all times (including self refresh) for proper device operation.</td></tr><tr><td>VREFDQ</td><td>Supply</td><td>Reference voltage for data: VREFDQ must be maintained at all times (excluding self refresh) for proper device operation.</td></tr><tr><td>VSS</td><td>Supply</td><td>Ground.</td></tr><tr><td>VSSQ</td><td>Supply</td><td>DQ ground: Isolated on the device for improved noise immunity.</td></tr><tr><td>ZQ</td><td>Reference</td><td>External reference ball for output drive calibration: This ball is tied to an external 240Ω resistor (RZQ), which is tied to VSSQ.</td></tr><tr><td>NC</td><td>-</td><td>No connect: These balls should be left unconnected (the ball has no connection to the DRAM or to other balls).</td></tr></table>

# Package Dimensions


Figure 8: 78-Ball FBGA – x4, x8 (RH)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/feff60fe80b5f3ad8c05918ff29a3e7ec1fdc904675bbfc91ab0257ba50fb2e0.jpg)



Notes: 1. All dimensions are in millimeters.



2. Solder ball material: SAC305 ( $9 6 . 5 \%$ Sn, $3 \%$ Ag, $0 . 5 \%$ Cu).



Figure 9: 78-Ball FBGA – x4, x8 (RG)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/0a89a6c9499c5c26384ff962f9303c786677f81b8e012c56a0d1fd63ff92cbd9.jpg)



1.8 CTR nonconductive overmold


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/39d51ab31154be0c7becdcf816238a5357b68dbe2323c87565bf9f0c26b7b592.jpg)



Notes: 1. All dimensions are in millimeters.



2. Solder ball material: SAC302 ( $9 6 . 8 \%$ Sn, $3 \%$ Ag, 0.2% Cu).



Figure 10: 78-Ball FBGA – x4, x8 (DA)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/17c29351e5f1e134f8a8ed224e3ebbbef3505ec51e34058c90b0b96ec24b4bcb.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/bbc4d74dfe6eb251c784bd0c564ed64909772c45cb46e13a5d6195dae4f532de.jpg)



Notes: 1. All dimensions are in millimeters.



2. Solder ball material: SAC302 $9 6 . 8 \%$ Sn, $3 \%$ Ag, 0.2% Cu).



Figure 11: 96-Ball FBGA – x16 (HA)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/6db4d1bd94e3e575b989e4867e15aefd4ddbdace55bb41b3d5554975be1c461c.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/2d5c542df0a4c214660c8ce9327c195396083625af67af586e4ebcb1322b84b0.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/a5309be3b6326a1c064c43c72d919b6ffb3bc2782471337ea538c106f1c13c9d.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/efaa7fd97ec495571438bac7fcd7a909537d77f414909e779779dd2fc75a9d9f.jpg)



Notes: 1. All dimensions are in millimeters.



2. Solder ball material: SAC305 $9 6 . 5 \%$ Sn, $3 \%$ Ag, $0 . 5 \%$ Cu).



Figure 12: 96-Ball FBGA – x16 (LY)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/44cc2d719b080f26e42f20a8d74bcbf3e5331c46bd9f2bd73ed4e62092f97e79.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/b71d107ca6076617f6049999e15b96906b5b194e3a673100f84d14abfa795531.jpg)



Notes: 1. All dimensions are in millimeters.



2. Solder ball material: SAC302 ( $9 6 . 8 \%$ Sn, $3 \%$ Ag, 0.2% Cu).



Figure 13: 96-Ball FBGA – x16 (TW)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/785233d98bfeab5b4e69a0ff376e3ef9a4b3d2cbadcf459007ebb4b8626a902f.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/5cd5c9ce87e349b2c74a28ec3580d8dc04b3c108017f4fb088ed798e282cc77a.jpg)



Notes: 1. All dimensions are in millimeters.



2. Material composition: Pb-free SAC302 $9 6 . 8 \%$ Sn, $3 \%$ Ag, 0.2% Cu).


# Electrical Specifications

# Absolute Ratings

Stresses greater than those listed may cause permanent damage to the device. This is a stress rating only, and functional operation of the device at these or any other conditions outside those indicated in the operational sections of this specification is not implied. Exposure to absolute maximum rating conditions for extended periods may adversely affect reliability. 


Table 5: Absolute Maximum Ratings


<table><tr><td>Symbol</td><td>Parameter</td><td>Min</td><td>Max</td><td>Unit</td><td>Notes</td></tr><tr><td>VDD</td><td>VDD supply voltage relative to VSS</td><td>-0.4</td><td>1.975</td><td>V</td><td>1</td></tr><tr><td>VDDQ</td><td>VDD supply voltage relative to VSSQ</td><td>-0.4</td><td>1.975</td><td>V</td><td></td></tr><tr><td>VIN, VOUT</td><td>Voltage on any pin relative to VSS</td><td>-0.4</td><td>1.975</td><td>V</td><td></td></tr><tr><td rowspan="2">TC</td><td>Operating case temperature – Commercial</td><td>0</td><td>95</td><td>°C</td><td>2,3</td></tr><tr><td>Operating case temperature – Industrial</td><td>-40</td><td>95</td><td>°C</td><td>2,3</td></tr><tr><td>TSTG</td><td>Storage temperature</td><td>-55</td><td>150</td><td>°C</td><td></td></tr></table>


Notes: 1. $V _ { \mathsf { D D } }$ and $V _ { \mathsf { D D Q } }$ must be within $3 0 0 \mathsf { m } \mathsf { V }$ of each other at all times, and $V _ { R E F }$ must not be greater than $0 . 6 \times \mathsf { V } _ { \mathsf { D D Q } }$ . When $V _ { \mathsf { D D } }$ and $V _ { \mathsf { D D Q } }$ are $< 5 0 0 \mathsf { m V } _ { \iota }$ , $V _ { R E F }$ can be $\leq 3 0 0 \mathsf { m V } .$ . 



2. MAX operating case temperature. ${ { \sf T } _ { \mathsf { C } } }$ is measured in the center of the package. 



3. Device functionality is not guaranteed if the DRAM device exceeds the maximum ${ { \sf T } _ { \mathsf { C } } }$ during operation. 


# Input/Output Capacitance


Table 6: DDR3L Input/Output Capacitance



Note 1 applies to the entire table


<table><tr><td rowspan="2">Capacitance Parameters</td><td rowspan="2">Sym</td><td colspan="2">DDR3L -800</td><td colspan="2">DDR3L -1066</td><td colspan="2">DDR3L -1333</td><td colspan="2">DDR3L -1600</td><td colspan="2">DDR3L -1866</td><td colspan="2">DDR3L -2133</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td>CK and CK#</td><td>CCK</td><td>0.8</td><td>1.6</td><td>0.8</td><td>1.6</td><td>0.8</td><td>1.4</td><td>0.8</td><td>1.4</td><td>0.8</td><td>1.3</td><td>0.8</td><td>1.3</td><td>pF</td><td></td></tr><tr><td>ΔC: CK to CK#</td><td>CDCK</td><td>0.0</td><td>0.15</td><td>0.0</td><td>0.15</td><td>0.0</td><td>0.15</td><td>0.0</td><td>0.15</td><td>0.0</td><td>0.15</td><td>0.0</td><td>0.15</td><td>pF</td><td></td></tr><tr><td>Single-end I/O: DQ, DM</td><td>CIO</td><td>1.4</td><td>2.5</td><td>1.4</td><td>2.5</td><td>1.4</td><td>2.3</td><td>1.4</td><td>2.2</td><td>1.4</td><td>2.1</td><td>1.4</td><td>2.1</td><td>pF</td><td>2</td></tr><tr><td>Differential I/O: DQS, DQS#, TDQS, TDQS#</td><td>CIO</td><td>1.4</td><td>2.5</td><td>1.4</td><td>2.5</td><td>1.4</td><td>2.3</td><td>1.4</td><td>2.2</td><td>1.4</td><td>2.1</td><td>1.4</td><td>2.1</td><td>pF</td><td>3</td></tr><tr><td>ΔC: DQS to DQS#, TDQS, TDQS#</td><td>CDDQS</td><td>0.0</td><td>0.2</td><td>0.0</td><td>0.2</td><td>0.0</td><td>0.15</td><td>0.0</td><td>0.15</td><td>0.0</td><td>0.15</td><td>0.0</td><td>0.15</td><td>pF</td><td>3</td></tr><tr><td>ΔC: DQ to DQS</td><td>CDIO</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>pF</td><td>4</td></tr><tr><td>Inputs (CTRL, CMD, ADDR)</td><td>CI</td><td>0.75</td><td>1.3</td><td>0.75</td><td>1.3</td><td>0.75</td><td>1.3</td><td>0.75</td><td>1.2</td><td>0.75</td><td>1.2</td><td>0.75</td><td>1.2</td><td>pF</td><td>5</td></tr><tr><td>ΔC: CTRL to CK</td><td>CDI_CTRL</td><td>-0.5</td><td>0.3</td><td>-0.5</td><td>0.3</td><td>-0.4</td><td>0.2</td><td>-0.4</td><td>0.2</td><td>-0.4</td><td>0.2</td><td>-0.4</td><td>0.2</td><td>pF</td><td>6</td></tr><tr><td>ΔC: CMD_ADDR to CK</td><td>CDI_CMD_ADDR</td><td>-0.5</td><td>0.5</td><td>-0.5</td><td>0.5</td><td>-0.4</td><td>0.4</td><td>-0.4</td><td>0.4</td><td>-0.4</td><td>0.4</td><td>-0.4</td><td>0.4</td><td>pF</td><td>7</td></tr><tr><td>ZQ pin capacitance</td><td>CZQ</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>pF</td><td></td></tr><tr><td>Reset pin capacitance</td><td>CRE</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>-</td><td>3.0</td><td>pF</td><td></td></tr></table>

Notes: 1. $\mathsf { V } _ { \mathsf { D D } } = 1 . 3 5 \mathsf { V }$ (1.283–1.45V), VDDQ = VDD, VREF = VSS, f = 100 MHz, $T _ { \mathsf { C } } = 2 5 ^ { \circ } { \mathsf { C } }$ . $\mathsf { V } _ { \mathsf { O U T } ( \mathsf { D C } ) } = 0 . 5$ $\mathsf { \nabla } \times \mathsf { V } _ { \mathsf { D D Q } } , \mathsf { V } _ { \mathsf { O U T } } = 0 . 1 \mathsf { V }$ (peak-to-peak). 

2. DM input is grouped with I/O pins, reflecting the fact that they are matched in loading. 

3. Includes TDQS, TDQS#. CDDQS is for DQS vs. DQS# and TDQS vs. TDQS# separately. 

4. $\mathsf C _ { \mathsf D 1 0 } = \mathsf C _ { \mathsf { I O } ( \mathsf { D Q } ) } - 0 . 5 \times \left( \mathsf C _ { \mathsf { I O } ( \mathsf { D Q 5 } ) } + \mathsf C _ { \mathsf { I O } ( \mathsf { D Q 5 } \# ) } \right)$ 

5. Excludes CK, CK#; CTRL $=$ ODT, CS#, and CKE; CMD $=$ RAS#, CAS#, and WE#; ADDR $=$ A[n:0], BA[2:0]. 

6. $\mathsf { C } _ { \mathsf { D } \mathsf { I } _ { - } \mathsf { C } \mathsf { T } \mathsf { R } \mathsf { L } } = \mathsf { C } _ { \mathsf { I } ( \mathsf { C } \mathsf { T } \mathsf { R } \mathsf { L } ) } - 0 . 5 \times \bigl ( \mathsf { C } _ { \mathsf { C } \mathsf { K } ( \mathsf { C } \mathsf { K } ) } + \mathsf { C } _ { \mathsf { C } \mathsf { K } ( \mathsf { C } \mathsf { K } \mathsf { \# } ) } \bigr ) .$ 

7. CDI_CMD_ADDR $=$ CI(CMD_ADDR) - 0.5 × (CCK(CK) + CCK(CK#)). 

# Thermal Characteristics


Table 7: Thermal Characteristics



Notes 1–3 apply to entire table


<table><tr><td>Parameter</td><td>Symbol</td><td>Value</td><td>Units</td><td>Notes</td></tr><tr><td rowspan="2">Operating temperature</td><td rowspan="2">Tc</td><td>0 to 85</td><td>°C</td><td></td></tr><tr><td>0 to 95</td><td>°C</td><td>4</td></tr></table>

Notes: 1. MAX operating case temperature ${ { \sf T } _ { \mathsf { C } } }$ is measured in the center of the package, as shown below. 

2. A thermal solution must be designed to ensure that the device does not exceed the maximum ${ { \sf T } _ { \mathsf { C } } }$ during operation. 

3. Device functionality is not guaranteed if the device exceeds maximum ${ { \sf T } _ { \mathsf { C } } }$ during operation. 

4. If ${ { \sf T } _ { \mathsf { C } } }$ exceeds $8 5 ^ { \circ } \mathsf { C } ,$ the DRAM must be refreshed externally at 2x refresh, which is a $3 . 9 \mu \ s$ interval refresh rate. The use of self refresh temperature (SRT) or automatic self refresh (ASR), must be enabled. 


Figure 14: Thermal Measurement Point


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/ef38326017e013e0d5360ec872acbbc0d3c9e7f1495ee27f29b8d4b77bb08c56.jpg)



Table 8: Thermal Impedance


<table><tr><td>Die Rev.</td><td>Package</td><td>Substrate</td><td>Θ JA (°C/W) Airflow = 0m/s</td><td>Θ JA (°C/W) Airflow = 1m/s</td><td>Θ JA (°C/W) Airflow = 2m/s</td><td>Θ JB (°C/W)</td><td>Θ JC (°C/W)</td></tr><tr><td rowspan="4">E</td><td rowspan="2">78-ball</td><td>Low conduc-tivity</td><td>63.7</td><td>49.6</td><td>44.0</td><td>N/A</td><td>4.0</td></tr><tr><td>High con-ductivity</td><td>42.3</td><td>35.7</td><td>32.9</td><td>29.7</td><td>N/A</td></tr><tr><td rowspan="2">96-ball</td><td>Low conduc-tivity</td><td>50.4</td><td>39.2</td><td>35.1</td><td>N/A</td><td>3.9</td></tr><tr><td>High con-ductivity</td><td>31.3</td><td>26.1</td><td>24.3</td><td>19.2</td><td>N/A</td></tr><tr><td rowspan="4">N</td><td rowspan="2">78-ball</td><td>Low conduc-tivity</td><td>61.7</td><td>47.6</td><td>42.6</td><td>N/A</td><td>5.7</td></tr><tr><td>High con-ductivity</td><td>40.6</td><td>33.4</td><td>31.2</td><td>19.1</td><td>N/A</td></tr><tr><td rowspan="2">96-ball</td><td>Low conduc-tivity</td><td>52.1</td><td>42.1</td><td>38.4</td><td>N/A</td><td>5.6</td></tr><tr><td>High con-ductivity</td><td>32.6</td><td>27.9</td><td>26.5</td><td>12.6</td><td>N/A</td></tr><tr><td rowspan="4">P</td><td rowspan="2">78-ball</td><td>Low conduc-tivity</td><td>88.3</td><td>70.6</td><td>64.1</td><td>N/A</td><td>10.8</td></tr><tr><td>High con-ductivity</td><td>56.5</td><td>48.4</td><td>45.7</td><td>25.5</td><td>N/A</td></tr><tr><td rowspan="2">96-ball</td><td>Low conduc-tivity</td><td>54.3</td><td>42.1</td><td>37.3</td><td>N/A</td><td>4.6</td></tr><tr><td>High con-ductivity</td><td>34.8</td><td>29.0</td><td>26.9</td><td>16.9</td><td>N/A</td></tr></table>


Note: 1. Thermal resistance data is based on a number of samples from multiple lots and should be viewed as a typical number. 


# Electrical Specifications – IDD Specifications and Conditions

Within the following $\mathrm { I _ { D D } }$ measurement tables, the following definitions and conditions are used, unless stated otherwise: 

• LOW: $\mathrm { V _ { I N } \leq V _ { I L ( A C ) m a x } }$ ; HIGH: VIN ≥ VIH(AC)min. 

• Midlevel: Inputs are $\mathrm { V _ { R E F } } { = } \mathrm { V _ { D D } } / 2$ . 

• $\mathrm { R _ { O N } }$ set to RZQ/7 (34Ω). 

• $\mathrm { R _ { T T , n o m } }$ set to RZQ/6 (40Ω). 

• RTT(WR) set to RZQ/2 (120Ω). 

• QOFF is enabled in MR1. 

• ODT is enabled in MR1 $( \mathrm { R _ { T T , n o m } } )$ and MR2 (RTT(WR)). 

• TDQS is disabled in MR1. 

• External DQ/DQS/DM load resistor is 25Ω to $\mathrm { V _ { D D Q } } / 2$ 

• Burst lengths are BL8 fixed. 

• AL equals 0 (except in $\mathrm { I _ { D D 7 } }$ ). 

• IDD specifications are tested after the device is properly initialized. 

• Input slew rate is specified by AC parametric test conditions. 

• Optional ASR is disabled. 

• Read burst type uses nibble sequential $( \mathrm { M R } 0 [ 3 ] = 0 )$ 

• Loop patterns must be executed at least once before current measurements begin. 


Table 9: Timing Parameters Used for IDD Measurements – Clock Units


<table><tr><td rowspan="3" colspan="2">IDDParameter</td><td colspan="2">DDR3L-800</td><td colspan="2">DDR3L-1066</td><td colspan="2">DDR3L-1333</td><td colspan="2">DDR3L-1600</td><td>DDR3L-1866</td><td>DDR3L-2133</td><td rowspan="3">Unit</td></tr><tr><td>-25E</td><td>-25</td><td>-187E</td><td>-187</td><td>-15E</td><td>-15</td><td>-125E</td><td>-125</td><td>-107</td><td>-093</td></tr><tr><td>5-5-5</td><td>6-6-6</td><td>7-7-7</td><td>8-8-8</td><td>9-9-9</td><td>10-10-10</td><td>10-10-10</td><td>11-11-11</td><td>13-13-13</td><td>14-14-14</td></tr><tr><td colspan="2">tCK (MIN) I_DD</td><td colspan="2">2.5</td><td colspan="2">1.875</td><td colspan="2">1.5</td><td colspan="2">1.25</td><td>1.07</td><td>0.938</td><td>ns</td></tr><tr><td colspan="2">CL I_DD</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td><td>10</td><td>11</td><td>13</td><td>14</td><td>CK</td></tr><tr><td colspan="2">tRCD (MIN) I_DD</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td><td>10</td><td>11</td><td>13</td><td>14</td><td>CK</td></tr><tr><td colspan="2">tRC (MIN) I_DD</td><td>20</td><td>21</td><td>27</td><td>28</td><td>33</td><td>34</td><td>38</td><td>39</td><td>45</td><td>50</td><td>CK</td></tr><tr><td colspan="2">tRAS (MIN) I_DD</td><td>15</td><td>15</td><td>20</td><td>20</td><td>24</td><td>24</td><td>28</td><td>28</td><td>32</td><td>36</td><td>CK</td></tr><tr><td colspan="2">tRP (MIN)</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td><td>10</td><td>11</td><td>13</td><td>14</td><td>CK</td></tr><tr><td rowspan="2">tFAW</td><td>x4, x8</td><td>16</td><td>16</td><td>20</td><td>20</td><td>20</td><td>20</td><td>24</td><td>24</td><td>26</td><td>27</td><td>CK</td></tr><tr><td>x16</td><td>20</td><td>20</td><td>27</td><td>27</td><td>30</td><td>30</td><td>32</td><td>32</td><td>33</td><td>38</td><td>CK</td></tr><tr><td rowspan="2">tRRD I_DD</td><td>x4, x8</td><td>4</td><td>4</td><td>4</td><td>4</td><td>4</td><td>4</td><td>5</td><td>5</td><td>5</td><td>6</td><td>CK</td></tr><tr><td>x16</td><td>4</td><td>4</td><td>6</td><td>6</td><td>5</td><td>5</td><td>6</td><td>6</td><td>6</td><td>7</td><td>CK</td></tr><tr><td rowspan="4">tRFC</td><td>1Gb</td><td>44</td><td>44</td><td>59</td><td>59</td><td>74</td><td>74</td><td>88</td><td>88</td><td>103</td><td>118</td><td>CK</td></tr><tr><td>2Gb</td><td>64</td><td>64</td><td>86</td><td>86</td><td>107</td><td>107</td><td>128</td><td>128</td><td>150</td><td>172</td><td>CK</td></tr><tr><td>4Gb</td><td>104</td><td>104</td><td>139</td><td>139</td><td>174</td><td>174</td><td>208</td><td>208</td><td>243</td><td>279</td><td>CK</td></tr><tr><td>8Gb</td><td>140</td><td>140</td><td>187</td><td>187</td><td>234</td><td>234</td><td>280</td><td>280</td><td>328</td><td>375</td><td>CK</td></tr></table>


Table 10: IDD0 Measurement Loop


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data</td></tr><tr><td rowspan="23">Toggling</td><td rowspan="23">Static HIGH</td><td rowspan="16">0</td><td>0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>4</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td></td><td colspan="13">Repeat cycles 1 through 4 until nRAS - 1; truncate if needed</td></tr><tr><td>nRAS</td><td>PRE</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td></td><td colspan="13">Repeat cycles 1 through 4 until nRC - 1; truncate if needed</td></tr><tr><td>nRC</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRC + 1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRC + 2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRC + 3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRC + 4</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td></td><td colspan="13">Repeat cycles nRC + 1 through nRC + 4 until nRC - 1 + nRAS -1; truncate if needed</td></tr><tr><td>nRC + nRAS</td><td>PRE</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td></td><td colspan="13">Repeat cycles nRC + 1 through nRC + 4 until 2 × RC - 1; truncate if needed</td></tr><tr><td>1</td><td>2 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 1</td></tr><tr><td>2</td><td>4 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 2</td></tr><tr><td>3</td><td>6 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 3</td></tr><tr><td>4</td><td>8 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 4</td></tr><tr><td>5</td><td>10 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 5</td></tr><tr><td>6</td><td>12 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 6</td></tr><tr><td>7</td><td>14 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 7</td></tr></table>


Notes: 1. DQ, DQS, DQS# are midlevel. 



2. DM is LOW. 



3. Only selected bank (single) active. 



Table 11: IDD1 Measurement Loop


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data2</td></tr><tr><td rowspan="27">Tooggling</td><td rowspan="27">Static HIGH</td><td rowspan="20">0</td><td>0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>4</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td></td><td colspan="13">Repeat cycles 1 through 4 until nRCD - 1; truncate if needed</td></tr><tr><td>nRCD</td><td>RD</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td></td><td colspan="13">Repeat cycles 1 through 4 until nRAS - 1; truncate if needed</td></tr><tr><td>nRAS</td><td>PRE</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td></td><td colspan="13">Repeat cycles 1 through 4 until nRC - 1; truncate if needed</td></tr><tr><td>nRC</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRC + 1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRC + 2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRC + 3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRC + 4</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td></td><td colspan="13">Repeat cycles nRC + 1 through nRC + 4 until nRC + nRCD - 1; truncate if needed</td></tr><tr><td>nRC + nRCD</td><td>RD</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td></td><td colspan="13">Repeat cycles nRC + 1 through nRC + 4 until nRC + nRAS - 1; truncate if needed</td></tr><tr><td>nRC + nRAS</td><td>PRE</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td></td><td colspan="13">Repeat cycle nRC + 1 through nRC + 4 until 2 × nRC - 1; truncate if needed</td></tr><tr><td>1</td><td>2 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 1</td></tr><tr><td>2</td><td>4 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 2</td></tr><tr><td>3</td><td>6 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 3</td></tr><tr><td>4</td><td>8 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 4</td></tr><tr><td>5</td><td>10 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 5</td></tr><tr><td>6</td><td>12 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 6</td></tr><tr><td>7</td><td>14 × nRC</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 7</td></tr></table>

Notes: 1. DQ, DQS, DQS# are midlevel unless driven as required by the RD command. 

2. DM is LOW. 

3. Burst sequence is driven on each DQ signal by the RD command. 

4. Only selected bank (single) active. 


Table 12: IDD Measurement Conditions for Power-Down Currents


<table><tr><td>Name</td><td>IDD2P0 Precharge Power-Down Current (Slow Exit)1</td><td>IDD2P1 Precharge Power-Down Current (Fast Exit)1</td><td>IDD2Q Precharge Quiet Standby Current</td><td>IDD3P Active Power-Down Current</td></tr><tr><td>Timing pattern</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>CKE</td><td>LOW</td><td>LOW</td><td>HIGH</td><td>LOW</td></tr><tr><td>External clock</td><td>Toggling</td><td>Toggling</td><td>Toggling</td><td>Toggling</td></tr><tr><td>tCK</td><td>tCK (MIN) I_DD</td><td>tCK (MIN) I_DD</td><td>tCK (MIN) I_DD</td><td>tCK (MIN) I_DD</td></tr><tr><td>tRC</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRAS</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRCD</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRRD</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRC</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>CL</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>AL</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>CS#</td><td>HIGH</td><td>HIGH</td><td>HIGH</td><td>HIGH</td></tr><tr><td>Command inputs</td><td>LOW</td><td>LOW</td><td>LOW</td><td>LOW</td></tr><tr><td>Row/column addr</td><td>LOW</td><td>LOW</td><td>LOW</td><td>LOW</td></tr><tr><td>Bank addresses</td><td>LOW</td><td>LOW</td><td>LOW</td><td>LOW</td></tr><tr><td>DM</td><td>LOW</td><td>LOW</td><td>LOW</td><td>LOW</td></tr><tr><td>Data I/O</td><td>Midlevel</td><td>Midlevel</td><td>Midlevel</td><td>Midlevel</td></tr><tr><td>Output buffer DQ, DQS</td><td>Enabled</td><td>Enabled</td><td>Enabled</td><td>Enabled</td></tr><tr><td>ODT2</td><td>Enabled, off</td><td>Enabled, off</td><td>Enabled, off</td><td>Enabled, off</td></tr><tr><td>Burst length</td><td>8</td><td>8</td><td>8</td><td>8</td></tr><tr><td>Active banks</td><td>None</td><td>None</td><td>None</td><td>All</td></tr><tr><td>Idle banks</td><td>All</td><td>All</td><td>All</td><td>None</td></tr><tr><td>Special notes</td><td>N/A</td><td>N/A</td><td>N/A</td><td>N/A</td></tr></table>


Notes: 1. MR0[12] defines DLL on/off behavior during precharge power-down only; DLL on (fast exit, MR0[12] $= 1$ ) and DLL off (slow exit, $\mathsf { M R O } [ 1 2 ] = 0 )$ . 



2. “Enabled, off” means the MR bits are enabled, but the signal is LOW. 



Table 13: IDD2N and IDD3N Measurement Loop


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data</td></tr><tr><td rowspan="11">Toggling</td><td rowspan="11">Static HIGH</td><td rowspan="4">0</td><td>0</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1</td><td>4-7</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 1</td></tr><tr><td>2</td><td>8-11</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 2</td></tr><tr><td>3</td><td>12-15</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 3</td></tr><tr><td>4</td><td>16-19</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 4</td></tr><tr><td>5</td><td>20-23</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 5</td></tr><tr><td>6</td><td>24-27</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 6</td></tr><tr><td>7</td><td>28-31</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 7</td></tr></table>


Notes: 1. DQ, DQS, DQS# are midlevel. 



2. DM is LOW. 



3. All banks closed during IDD2N; all banks open during IDD3N. 



Table 14: IDD2NT Measurement Loop


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data</td></tr><tr><td rowspan="11">Toggling</td><td rowspan="11">Static HIGH</td><td rowspan="4">0</td><td>0</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1</td><td>4-7</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 1; ODT = 0</td></tr><tr><td>2</td><td>8-11</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 2; ODT = 1</td></tr><tr><td>3</td><td>12-15</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 3; ODT = 1</td></tr><tr><td>4</td><td>16-19</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 4; ODT = 0</td></tr><tr><td>5</td><td>20-23</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 5; ODT = 0</td></tr><tr><td>6</td><td>24-27</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 6; ODT = 1</td></tr><tr><td>7</td><td>28-31</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 7; ODT = 1</td></tr></table>


Notes: 1. DQ, DQS, DQS# are midlevel. 



2. DM is LOW. 



3. All banks closed. 



Table 15: IDD4R Measurement Loop


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data3</td></tr><tr><td rowspan="15">Toggling</td><td rowspan="15">Static HIGH</td><td rowspan="8">0</td><td>0</td><td>RD</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>4</td><td>RD</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td>5</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>6</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>7</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1</td><td>8-15</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 1</td></tr><tr><td>2</td><td>16-23</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 2</td></tr><tr><td>3</td><td>24-31</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 3</td></tr><tr><td>4</td><td>32-39</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 4</td></tr><tr><td>5</td><td>40-47</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 5</td></tr><tr><td>6</td><td>48-55</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 6</td></tr><tr><td>7</td><td>56-63</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 7</td></tr></table>


Notes: 1. DQ, DQS, DQS# are midlevel when not driving in burst sequence. 



2. DM is LOW. 



3. Burst sequence is driven on each DQ signal by the RD command. 



4. All banks open. 



Table 16: IDD4W Measurement Loop


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data4</td></tr><tr><td rowspan="15">Toggling</td><td rowspan="15">Static HIGH</td><td rowspan="8">0</td><td>0</td><td>WR</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>4</td><td>WR</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td>5</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>6</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>7</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1</td><td>8-15</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 1</td></tr><tr><td>2</td><td>16-23</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 2</td></tr><tr><td>3</td><td>24-31</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 3</td></tr><tr><td>4</td><td>32-39</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 4</td></tr><tr><td>5</td><td>40-47</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 5</td></tr><tr><td>6</td><td>48-55</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 6</td></tr><tr><td>7</td><td>56-63</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 7</td></tr></table>


Notes: 1. DQ, DQS, DQS# are midlevel when not driving in burst sequence. 



2. DM is LOW. 



3. Burst sequence is driven on each DQ signal by the WR command. 



4. All banks open. 



Table 17: IDD5B Measurement Loop


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data</td></tr><tr><td rowspan="13">Toggling</td><td rowspan="13">Static HIGH</td><td>0</td><td>0</td><td>REF</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td rowspan="4">1a</td><td>1</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>4</td><td>D#</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>1b</td><td>5-8</td><td colspan="13">Repeat sub-loop 1a, use BA[2:0] = 1</td></tr><tr><td>1c</td><td>9-12</td><td colspan="13">Repeat sub-loop 1a, use BA[2:0] = 2</td></tr><tr><td>1d</td><td>13-16</td><td colspan="13">Repeat sub-loop 1a, use BA[2:0] = 3</td></tr><tr><td>1e</td><td>17-20</td><td colspan="13">Repeat sub-loop 1a, use BA[2:0] = 4</td></tr><tr><td>1f</td><td>21-24</td><td colspan="13">Repeat sub-loop 1a, use BA[2:0] = 5</td></tr><tr><td>1g</td><td>25-28</td><td colspan="13">Repeat sub-loop 1a, use BA[2:0] = 6</td></tr><tr><td>1h</td><td>29-32</td><td colspan="13">Repeat sub-loop 1a, use BA[2:0] = 7</td></tr><tr><td>2</td><td>33-nRFC - 1</td><td colspan="13">Repeat sub-loop 1a through 1h until nRFC - 1; truncate if needed</td></tr></table>


Notes: 1. DQ, DQS, DQS# are midlevel. 



2. DM is LOW. 



Table 18: IDD Measurement Conditions for IDD6, IDD6ET, and IDD8


<table><tr><td>IDD Test</td><td>IDD6: Self Refresh Current Normal Temperature Range TC = 0°C to +85°C</td><td>IDD6ET: Self Refresh Current Extended Temperature Range TC = 0°C to +95°C</td><td>IDD8: Reset2</td></tr><tr><td>CKE</td><td>LOW</td><td>LOW</td><td>Midlevel</td></tr><tr><td>External clock</td><td>Off, CK and CK# = LOW</td><td>Off, CK and CK# = LOW</td><td>Midlevel</td></tr><tr><td>tCK</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRC</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRAS</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRCD</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRRD</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>tRC</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>CL</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>AL</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>CS#</td><td>Midlevel</td><td>Midlevel</td><td>Midlevel</td></tr><tr><td>Command inputs</td><td>Midlevel</td><td>Midlevel</td><td>Midlevel</td></tr><tr><td>Row/column addresses</td><td>Midlevel</td><td>Midlevel</td><td>Midlevel</td></tr><tr><td>Bank addresses</td><td>Midlevel</td><td>Midlevel</td><td>Midlevel</td></tr><tr><td>Data I/O</td><td>Midlevel</td><td>Midlevel</td><td>Midlevel</td></tr><tr><td>Output buffer DQ, DQS</td><td>Enabled</td><td>Enabled</td><td>Midlevel</td></tr><tr><td>ODT1</td><td>Enabled, midlevel</td><td>Enabled, midlevel</td><td>Midlevel</td></tr><tr><td>Burst length</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>Active banks</td><td>N/A</td><td>N/A</td><td>None</td></tr><tr><td>Idle banks</td><td>N/A</td><td>N/A</td><td>All</td></tr><tr><td>SRT</td><td>Disabled (normal)</td><td>Enabled (extended)</td><td>N/A</td></tr><tr><td>ASR</td><td>Disabled</td><td>Disabled</td><td>N/A</td></tr></table>


Notes: 1. “Enabled, midlevel” means the MR command is enabled, but the signal is midlevel. 



2. During a cold boot RESET (initialization), current reading is valid after power is stable and RESET has been LOW for 1ms; During a warm boot RESET (while operating), current reading is valid after RESET has been LOW for 200ns + t RFC. 



Table 19: IDD7 Measurement Loop


<table><tr><td>CK, CK#</td><td>CKE</td><td>Sub-Loop</td><td>Cycle Number</td><td>Command</td><td>CS#</td><td>RAS#</td><td>CAS#</td><td>WE#</td><td>ODT</td><td>BA[2:0]</td><td>A[15:11]</td><td>A[10]</td><td>A[9:7]</td><td>A[6:3]</td><td>A[2:0]</td><td>Data3</td></tr><tr><td rowspan="31">Toggling</td><td rowspan="31">Static HIGH</td><td rowspan="4">0</td><td>0</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>1</td><td>RDA</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td>2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3</td><td colspan="13">Repeat cycle 2 until nRRD - 1</td></tr><tr><td rowspan="4">1</td><td>nRRD</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRRD + 1</td><td>RDA</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td>nRRD + 2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nRRD + 3</td><td colspan="13">Repeat cycle nRRD + 2 until 2 × nRRD - 1</td></tr><tr><td>2</td><td>2 × nRRD</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 2</td></tr><tr><td>3</td><td>3 × nRRD</td><td colspan="13">Repeat sub-loop 1, use BA[2:0] = 3</td></tr><tr><td rowspan="2">4</td><td>4 × nRRD</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>3</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>4 × nRRD + 1</td><td colspan="13">Repeat cycle 4 × nRRD until nFAW - 1, if needed</td></tr><tr><td>5</td><td>nFAW</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 4</td></tr><tr><td>6</td><td>nFAW + nRRD</td><td colspan="13">Repeat sub-loop 1, use BA[2:0] = 5</td></tr><tr><td>7</td><td>nFAW + 2 × nRRD</td><td colspan="13">Repeat sub-loop 0, use BA[2:0] = 6</td></tr><tr><td>8</td><td>nFAW + 3 × nRRD</td><td colspan="13">Repeat sub-loop 1, use BA[2:0] = 7</td></tr><tr><td rowspan="2">9</td><td>nFAW + 4 × nRRD</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>7</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>nFAW + 4 × nRRD + 1</td><td colspan="13">Repeat cycle nFAW + 4 × nRRD until 2 × nFAW - 1, if needed</td></tr><tr><td rowspan="4">10</td><td>2 × nFAW</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>2 × nFAW + 1</td><td>RDA</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>F</td><td>0</td><td>00110011</td></tr><tr><td>2 × nFAW + 2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>F</td><td>0</td><td>-</td></tr><tr><td>2 × nFAW + 3</td><td colspan="13">Repeat cycle 2 × nFAW + 2 until 2 × nFAW + nRRD - 1</td></tr><tr><td rowspan="4">11</td><td>2 × nFAW + nRRD</td><td>ACT</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2 × nFAW + nRRD + 1</td><td>RDA</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>00000000</td></tr><tr><td>2 × nFAW + nRRD + 2</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2 × nFAW + nRRD + 3</td><td colspan="13">Repeat cycle 2 × nFAW + nRRD + 2 until 2 × nFAW + 2 × nRRD - 1</td></tr><tr><td>12</td><td>2 × nFAW + 2 × nRRD</td><td colspan="13">Repeat sub-loop 10, use BA[2:0] = 2</td></tr><tr><td>13</td><td>2 × nFAW + 3 × nRRD</td><td colspan="13">Repeat sub-loop 11, use BA[2:0] = 3</td></tr><tr><td rowspan="2">14</td><td>2 × nFAW + 4 × nRRD</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>3</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>2 × nFAW + 4 × nRRD + 1</td><td colspan="13">Repeat cycle 2 × nFAW + 4 × nRRD until 3 × nFAW - 1, if needed</td></tr><tr><td>15</td><td>3 × nFAW</td><td colspan="13">Repeat sub-loop 10, use BA[2:0] = 4</td></tr><tr><td rowspan="5">Toggling</td><td rowspan="5">Static HIGH</td><td>16</td><td>3 × nFAW + nRRD</td><td colspan="13">Repeat sub-loop 11, use BA[2:0] = 5</td></tr><tr><td>17</td><td>3 × nFAW + 2 × nRRD</td><td colspan="13">Repeat sub-loop 10, use BA[2:0] = 6</td></tr><tr><td>18</td><td>3 × nFAW + 3 × nRRD</td><td colspan="13">Repeat sub-loop 11, use BA[2:0] = 7</td></tr><tr><td rowspan="2">19</td><td>3 × nFAW + 4 × nRRD</td><td>D</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>7</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-</td></tr><tr><td>3 × nFAW + 4 × nRRD + 1</td><td colspan="13">Repeat cycle 3 × nFAW + 4 × nRRD until 4 × nFAW - 1, if needed</td></tr></table>


Notes: 1. DQ, DQS, DQS# are midlevel unless driven as required by the RD command. 



2. DM is LOW. 



3. Burst sequence is driven on each DQ signal by the RD command. 



4. $\mathsf { A L } = \mathsf { C L } - 1$ . 


# Electrical Characteristics – Operating IDD Specifications


Table 20: IDD Maximum Limits Die Rev. E for 1.35/1.5V Operation


<table><tr><td colspan="3">Speed Bin</td><td rowspan="2">DDR3/3L -1066</td><td rowspan="2">DDR3/3L -1333</td><td rowspan="2">DDR3/3L -1600</td><td rowspan="2">DDR3/3L -1866</td><td rowspan="2">Units</td><td rowspan="2">Notes</td></tr><tr><td>Parameter</td><td>Symbol</td><td>Width</td></tr><tr><td rowspan="2">Operating current 0: One bank ACTIVATE-to-PRECHARGE</td><td rowspan="2">IDD0</td><td>x4, x8</td><td>44</td><td>47</td><td>55</td><td>62</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>55</td><td>58</td><td>66</td><td>73</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="3">Operating current 1: One bank ACTIVATE-to-READ-to-PRECHARGE</td><td rowspan="3">IDD1</td><td>x4</td><td>53</td><td>57</td><td>61</td><td>65</td><td>mA</td><td>1, 2</td></tr><tr><td>x8</td><td>59</td><td>62</td><td>66</td><td>70</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>80</td><td>84</td><td>87</td><td>91</td><td>mA</td><td>1, 2</td></tr><tr><td>Precharge power-down current: Slow exit</td><td>IDD2P0</td><td>All</td><td>18</td><td>18</td><td>18</td><td>18</td><td>mA</td><td>1, 2</td></tr><tr><td>Precharge power-down current: Fast exit</td><td>IDD2P1</td><td>All</td><td>26</td><td>28</td><td>32</td><td>37</td><td>mA</td><td>1, 2</td></tr><tr><td>Precharge quiet standby current</td><td>IDD2Q</td><td>All</td><td>27</td><td>28</td><td>32</td><td>35</td><td>mA</td><td>1, 2</td></tr><tr><td>Precharge standby current</td><td>IDD2N</td><td>All</td><td>28</td><td>29</td><td>32</td><td>35</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="2">Precharge standby ODT current</td><td rowspan="2">IDD2NT</td><td>x4, x8</td><td>32</td><td>35</td><td>39</td><td>42</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>35</td><td>39</td><td>42</td><td>45</td><td>mA</td><td>1, 2</td></tr><tr><td>Active power-down current</td><td>IDD3P</td><td>All</td><td>32</td><td>35</td><td>38</td><td>41</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="2">Active standby current</td><td rowspan="2">IDD3N</td><td>x4, x8</td><td>32</td><td>35</td><td>38</td><td>41</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>41</td><td>45</td><td>47</td><td>49</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="3">Burst read operating current</td><td rowspan="3">IDD4R</td><td>x4</td><td>113</td><td>130</td><td>147</td><td>164</td><td>mA</td><td>1, 2</td></tr><tr><td>x8</td><td>123</td><td>140</td><td>157</td><td>174</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>185</td><td>202</td><td>235</td><td>252</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="3">Burst write operating current</td><td rowspan="3">IDD4W</td><td>x4</td><td>87</td><td>103</td><td>118</td><td>133</td><td>mA</td><td>1, 2</td></tr><tr><td>x8</td><td>95</td><td>110</td><td>125</td><td>141</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>137</td><td>152</td><td>171</td><td>190</td><td>mA</td><td>1, 2</td></tr><tr><td>Burst refresh current</td><td>IDD5B</td><td>All</td><td>224</td><td>228</td><td>235</td><td>242</td><td>mA</td><td>1, 2</td></tr><tr><td>Room temperature self refresh</td><td>IDD6</td><td>All</td><td>20</td><td>20</td><td>20</td><td>20</td><td>mA</td><td>1, 2, 3</td></tr><tr><td>Extended temperature self refresh</td><td>IDD6ET</td><td>All</td><td>25</td><td>25</td><td>25</td><td>25</td><td>mA</td><td>2, 4</td></tr><tr><td rowspan="2">All banks interleaved read current</td><td rowspan="2">IDD7</td><td>x4, x8</td><td>160</td><td>190</td><td>220</td><td>251</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>198</td><td>217</td><td>243</td><td>274</td><td>mA</td><td>1, 2</td></tr><tr><td>Reset current</td><td>IDD8</td><td>All</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>mA</td><td>1, 2</td></tr></table>

Notes: 1. ${ \mathsf { T } } _ { \mathsf { C } } = 8 5 ^ { \circ } { \mathsf { C } } ;$ SRT and ASR are disabled. 

2. Enabling ASR could increase $\mathsf { I } _ { \mathsf { D D } x }$ by up to an additional 2mA. 

3. Restricted to $T _ { \mathsf { C } } \left( { \mathsf { M A X } } \right) = 8 5 ^ { \circ } { \mathsf { C } }$ . 

4. ${ \mathsf { T } } _ { \mathsf { C } } = 8 5 ^ { \circ } { \mathsf { C } } ;$ ASR and ODT are disabled; SRT is enabled. 

5. The $1 _ { \mathsf { D D } }$ values must be derated (increased) on IT-option devices when operated outside of the range $0 ^ { \circ } \mathsf { C } \le \mathsf { T } _ { \mathsf { C } } \le + 8 5 ^ { \circ } \mathsf { C } ;$ 

5a. When ${ \mathsf { T } } _ { \mathsf { C } } < 0 ^ { \circ } { \mathsf { C } } \colon$ IDD2P0, IDD2P1 and IDD3P must be derated by $4 \%$ ; IDD4R and IDD4W must be derated by $2 \%$ ; and IDD6, IDD6ET and IDD7 must be derated by $7 \%$ . 

5b. When ${ \mathsf { T } } _ { \mathsf { C } } > 8 5 ^ { \circ } { \mathsf { C } } \mathrm { : }$ IDD0, IDD1, IDD2N, IDD2NT, IDD2Q, IDD3N, IDD3P, IDD4R, IDD4W, and IDD5B must be derated by $2 \%$ ; $\mathsf { I } _ { \mathsf { D D } 2 \mathsf { P } \mathsf { x } }$ must be derated by $30 \%$ . 


Table 21: IDD Maximum Limits Die Rev. N for 1.35V/1.5V Operation


<table><tr><td colspan="3">Speed Bin</td><td rowspan="2">DDR3/3L -1066</td><td rowspan="2">DDR3/3L -1333</td><td rowspan="2">DDR3/3L -1600</td><td rowspan="2">DDR3/3L -1866</td><td rowspan="2">DDR3/3L -2133</td><td rowspan="2">Units</td><td rowspan="2">Notes</td></tr><tr><td>Parameter</td><td>Symbol</td><td>Width</td></tr><tr><td rowspan="2">Operating current 0: One bank ACTIVATE-to-PRECHARGE</td><td rowspan="2">IDD0</td><td>x4, x8</td><td>42</td><td>45</td><td>47</td><td>49</td><td>51</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>52</td><td>55</td><td>57</td><td>59</td><td>61</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="3">Operating current 1: One bank ACTIVATE-to-READ-to-PRE-CHARGE</td><td rowspan="3">IDD1</td><td>x4</td><td>50</td><td>53</td><td>56</td><td>59</td><td>62</td><td>mA</td><td>1, 2</td></tr><tr><td>x8</td><td>55</td><td>58</td><td>61</td><td>64</td><td>67</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>75</td><td>78</td><td>81</td><td>84</td><td>87</td><td>mA</td><td>1, 2</td></tr><tr><td>Precharge power-down cur- rent: Slow exit</td><td>IDD2P0</td><td>All</td><td>8</td><td>8</td><td>8</td><td>8</td><td>8</td><td>mA</td><td>1, 2</td></tr><tr><td>Precharge power-down cur- rent: Fast exit</td><td>IDD2P1</td><td>All</td><td>10</td><td>12</td><td>14</td><td>16</td><td>18</td><td>mA</td><td>1, 2</td></tr><tr><td>Precharge quiet standby cur- rent</td><td>IDD2Q</td><td>All</td><td>20</td><td>22</td><td>24</td><td>26</td><td>28</td><td>mA</td><td>1, 2</td></tr><tr><td>Precharge standby current</td><td>IDD2N</td><td>All</td><td>20</td><td>22</td><td>24</td><td>26</td><td>28</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="2">Precharge standby ODT current</td><td rowspan="2">IDD2NT</td><td>x4, x8</td><td>24</td><td>26</td><td>28</td><td>30</td><td>32</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>27</td><td>29</td><td>31</td><td>33</td><td>35</td><td>mA</td><td>1, 2</td></tr><tr><td>Active power-down current</td><td>IDD3P</td><td>All</td><td>22</td><td>24</td><td>26</td><td>28</td><td>30</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="2">Active standby current</td><td rowspan="2">IDD3N</td><td>x4, x8</td><td>26</td><td>28</td><td>30</td><td>32</td><td>34</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>34</td><td>36</td><td>38</td><td>40</td><td>42</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="3">Burst read operating current</td><td rowspan="3">IDD4R</td><td>x4</td><td>65</td><td>75</td><td>85</td><td>95</td><td>105</td><td>mA</td><td>1, 2</td></tr><tr><td>x8</td><td>75</td><td>85</td><td>95</td><td>105</td><td>115</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>135</td><td>145</td><td>155</td><td>165</td><td>175</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="3">Burst write operating current</td><td rowspan="3">IDD4W</td><td>x4</td><td>65</td><td>75</td><td>85</td><td>95</td><td>105</td><td>mA</td><td>1, 2</td></tr><tr><td>x8</td><td>75</td><td>85</td><td>95</td><td>105</td><td>115</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>135</td><td>145</td><td>155</td><td>165</td><td>175</td><td>mA</td><td>1, 2</td></tr><tr><td>Burst refresh current</td><td>IDD5B</td><td>All</td><td>165</td><td>170</td><td>175</td><td>180</td><td>185</td><td>mA</td><td>1, 2</td></tr><tr><td>Room temperature self refresh</td><td>IDD6</td><td>All</td><td>12</td><td>12</td><td>12</td><td>12</td><td>12</td><td>mA</td><td>1, 2, 3</td></tr><tr><td>Extended temperature self re- fresh</td><td>IDD6ET</td><td>All</td><td>16</td><td>16</td><td>16</td><td>16</td><td>16</td><td>mA</td><td>2, 4</td></tr><tr><td rowspan="2">All banks interleaved read cur- rent</td><td rowspan="2">IDD7</td><td>x4, x8</td><td>110</td><td>120</td><td>130</td><td>140</td><td>150</td><td>mA</td><td>1, 2</td></tr><tr><td>x16</td><td>170</td><td>180</td><td>190</td><td>200</td><td>210</td><td>mA</td><td>1, 2</td></tr><tr><td>Reset current</td><td>IDD8</td><td>All</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>mA</td><td>1, 2</td></tr></table>


Notes: 1. ${ \mathsf { T } } _ { \mathsf { C } } = 8 5 ^ { \circ } { \mathsf { C } } ;$ SRT and ASR are disabled. 



2. Enabling ASR could increase $\mathsf { I } _ { \mathsf { D D } x }$ by up to an additional 2mA. 



3. Restricted to $T _ { \mathsf { C } } \left( { \mathsf { M A X } } \right) = 8 5 ^ { \circ } { \mathsf { C } }$ . 



4. ${ \mathsf { T } } _ { \mathsf { C } } = 8 5 ^ { \circ } { \mathsf { C } } ;$ ASR and ODT are disabled; SRT is enabled. 


5. The $1 _ { \mathsf { D D } }$ values must be derated (increased) on IT-option devices when operated outside of the range $0 ^ { \circ } \mathsf { C } \le \mathsf { T } _ { \mathsf { C } } \le 8 5 ^ { \circ } \mathsf { C }$ : 

5a. When ${ \bar { \mathsf { T } } } _ { \mathsf { C } } < 0 ^ { \circ } { \mathsf { C } } :$ : IDD2P0, IDD2P1 and IDD3P must be derated by $4 \%$ ; IDD4R and IDD4W must be derated by $2 \%$ ; and IDD6, IDD6ET and IDD7 must be derated by $7 \%$ . 

5b. When ${ \mathsf { T } } _ { \mathsf { C } } > 8 5 ^ { \circ } { \mathsf { C } } \mathrm { : }$ IDD0, IDD1, IDD2N, IDD2NT, IDD2Q, IDD3N, IDD3P, IDD4R, IDD4W, and IDD5B must be derated by $2 \%$ ; $\mathsf { I } _ { \mathsf { D D } 2 \mathsf { P } \mathsf { x } }$ must be derated by $30 \%$ . 


Table 22: IDD Maximum Limits Die Rev. P for 1.35V/1.5V Operation


<table><tr><td colspan="3">Speed Bin</td><td rowspan="2">DDR3/3L -1600</td><td rowspan="2">DDR3/3L -1866</td><td rowspan="2">DDR3/3L -2133</td><td rowspan="2">Units</td><td rowspan="2">Notes</td></tr><tr><td>Parameter</td><td>Symbol</td><td>Width</td></tr><tr><td rowspan="2">Operating current 0: One bank ACTI-VATE-to-PRECHARGE</td><td rowspan="2">IDD0</td><td>x4, x8</td><td>28</td><td>29</td><td>31</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>X16</td><td>32</td><td>32</td><td>34</td></tr><tr><td rowspan="2">Operating current 1: One bank ACTI-VATE-to-READ-to-PRECHARGE</td><td rowspan="2">IDD1</td><td>x4, x8</td><td>43</td><td>44</td><td>47</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>45</td><td>46</td><td>54</td></tr><tr><td rowspan="2">Precharge power-down current: Slow exit</td><td rowspan="2">IDD2P0</td><td>x4, x8</td><td>10</td><td>11</td><td>12</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>12</td><td>12</td><td>12</td></tr><tr><td rowspan="2">Precharge power-down current: Fast exit</td><td rowspan="2">IDD2P1</td><td>x4, x8</td><td>11</td><td>11</td><td>13</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>12</td><td>12</td><td>14</td></tr><tr><td>Precharge quiet standby current</td><td>IDD2Q</td><td>ALL</td><td>15</td><td>15</td><td>17</td><td>mA</td><td>1, 2</td></tr><tr><td rowspan="2">Precharge standby current</td><td rowspan="2">IDD2N</td><td>x4, x8</td><td>16</td><td>17</td><td>22</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>17</td><td>17</td><td>22</td></tr><tr><td rowspan="2">Precharge standby ODT current</td><td rowspan="2">IDD2NT</td><td>x4, x8</td><td>20</td><td>22</td><td>27</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>22</td><td>23</td><td>28</td></tr><tr><td rowspan="2">Active power-down current</td><td rowspan="2">IDD3P</td><td>x4,x8</td><td>15</td><td>15</td><td>17</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>17</td><td>17</td><td>19</td></tr><tr><td rowspan="2">Active standby current</td><td rowspan="2">IDD3N</td><td>x4, x8</td><td>20</td><td>21</td><td>23</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>22</td><td>23</td><td>25</td></tr><tr><td rowspan="2">Burst read operating current</td><td rowspan="2">IDD4R</td><td>x4, x8</td><td>90</td><td>90</td><td>110</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>110</td><td>120</td><td>130</td></tr><tr><td rowspan="2">Burst write operating current</td><td rowspan="2">IDD4W</td><td>x4, x8</td><td>90</td><td>90</td><td>110</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>16</td><td>120</td><td>130</td><td>140</td></tr><tr><td rowspan="2">Burst refresh current</td><td rowspan="2">IDD5B</td><td>x4, x8</td><td>152</td><td>152</td><td>160</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>156</td><td>156</td><td>160</td></tr><tr><td>Self refresh</td><td>IDD6</td><td>ALL</td><td>15</td><td>15</td><td>15</td><td>mA</td><td>1, 2, 3</td></tr><tr><td>Extended temperature self refresh</td><td>IDD6ET</td><td>ALL</td><td>23</td><td>23</td><td>23</td><td>mA</td><td>2, 4</td></tr><tr><td rowspan="2">All banks interleaved read current</td><td rowspan="2">IDD7</td><td>x4, x8</td><td>130</td><td>146</td><td>150</td><td rowspan="2">mA</td><td rowspan="2">1, 2</td></tr><tr><td>x16</td><td>132</td><td>147</td><td>160</td></tr><tr><td>Reset current</td><td>IDD8</td><td>ALL</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>IDD2P + 2mA</td><td>mA</td><td>1, 2</td></tr></table>


Notes: 1. ${ \mathsf { T } } _ { \mathsf { C } } = 8 5 ^ { \circ } { \mathsf { C } } ;$ SRT and ASR are disabled. 



2. Enabling ASR could increase $\mathsf { I } _ { \mathsf { D D } x }$ by up to an additional 2mA. 



3. Restricted to $T _ { \mathsf { C } } \left( { \mathsf { M A X } } \right) = 8 5 ^ { \circ } { \mathsf { C } }$ . 



4. ${ \mathsf { T } } _ { \mathsf { C } } = 8 5 ^ { \circ } { \mathsf { C } } ;$ ASR and ODT are disabled; SRT is enabled. 


# Electrical Specifications – DC and AC

# DC Operating Conditions


Table 23: DDR3L 1.35V DC Electrical Characteristics and Operating Conditions



All voltages are referenced to $\mathsf { V } _ { \mathsf { S } \mathsf { S } }$


<table><tr><td>Parameter/Condition</td><td>Symbol</td><td>Min</td><td>Nom</td><td>Max</td><td>Unit</td><td>Notes</td></tr><tr><td>Supply voltage</td><td>VDD</td><td>1.283</td><td>1.35</td><td>1.45</td><td>V</td><td>1-7</td></tr><tr><td>I/O supply voltage</td><td>VDDQ</td><td>1.283</td><td>1.35</td><td>1.45</td><td>V</td><td>1-7</td></tr><tr><td>Input leakage current
Any input 0V ≤ VIN ≤ VDD, VREF pin 0V ≤ VIN ≤ 1.1V
(All other pins not under test = 0V)</td><td>Ii</td><td>-2</td><td>-</td><td>2</td><td>μA</td><td></td></tr><tr><td>VREF supply leakage current
VREFDQ = VDD/2 or VREFCA = VDD/2
(All other pins not under test = 0V)</td><td>IVREF</td><td>-1</td><td>-</td><td>1</td><td>μA</td><td>8, 9</td></tr></table>

Notes: 1. $V _ { \mathsf { D D } }$ and $V _ { \mathsf { D D Q } }$ must track one another. VDDQ must be $\leq V _ { \mathsf { D D } }$ . $\mathsf { V } _ { 5 \mathsf { S } } = \mathsf { V } _ { 5 \mathsf { S } \mathsf { Q } }$ 

2. $V _ { \mathsf { D D } }$ and $V _ { \mathsf { D D Q } }$ may include AC noise of $\pm 5 0 \mathsf { m V }$ $2 5 0 ~ \mathsf { k H z }$ to 20 MHz) in addition to the DC (0 Hz to $2 5 0 \mathsf { k H z } )$ ) specifications. $V _ { \mathsf { D D } }$ and $V _ { \mathsf { D D Q } }$ must be at same level for valid AC timing parameters. 

3. Maximum DC value may not be greater than 1.425V. The DC value is the linear average of $\mathsf { V } _ { \mathsf { D D } } / \mathsf { V } _ { \mathsf { D D Q } } ( \mathsf { t } )$ over a very long period of time (for example, 1 second). 

4. Under these supply voltages, the device operates to this DDR3L specification. 

5. If the maximum limit is exceeded, input levels shall be governed by DDR3 specifications. 

6. Under 1.5V operation, this DDR3L device operates in accordance with the DDR3 specifications under the same speed timings as defined for this device. 

7. Once initialized for DDR3L operation, DDR3 operation may only be used if the device is in reset while $V _ { \mathsf { D D } }$ and $V _ { \mathsf { D D Q } }$ are changed for DDR3 operation (see VDD Voltage Switching (page 137)). 

8. The minimum limit requirement is for testing purposes. The leakage current on the $V _ { \mathsf { R E F } }$ pin should be minimal. 

9. $V _ { R E F }$ (see Table 24). 

# Input Operating Conditions


Table 24: DDR3L 1.35V DC Electrical Characteristics and Input Conditions



All voltages are referenced to $\mathsf { V } _ { \mathsf { S } \mathsf { S } }$


<table><tr><td>Parameter/Condition</td><td>Symbol</td><td>Min</td><td>Nom</td><td>Max</td><td>Unit</td><td>Notes</td></tr><tr><td>VINlow; DC/comands/address busses</td><td>VIL</td><td>VSS</td><td>N/A</td><td>See Table 25</td><td>V</td><td></td></tr><tr><td>VINhigh; DC/comands/address busses</td><td>VIH</td><td>See Table 25</td><td>N/A</td><td>VDD</td><td>V</td><td></td></tr><tr><td>Input reference voltage command/address bus</td><td>VREFCA(DC)</td><td>0.49 × VDD</td><td>0.5 × VDD</td><td>0.51 × VDD</td><td>V</td><td>1,2</td></tr><tr><td>I/O reference voltage DQ bus</td><td>VREFDQ(DC)</td><td>0.49 × VDD</td><td>0.5 × VDD</td><td>0.51 × VDD</td><td>V</td><td>2,3</td></tr><tr><td>I/O reference voltage DQ bus in SELF REFRESH</td><td>VREFDQ(SR)</td><td>VSS</td><td>0.5 × VDD</td><td>VDD</td><td>V</td><td>4</td></tr><tr><td>Command/address termination voltage (system level, not direct DRAM input)</td><td>VTT</td><td>-</td><td>0.5 × VDDQ</td><td>-</td><td>V</td><td>5</td></tr></table>

Notes: 1. VREFCA(DC) is expected to be approximately $0 . 5 \times \mathsf { V } _ { \mathsf { D } \mathsf { D } }$ and to track variations in the DC level. Externally generated peak noise (non-common mode) on VREFCA may not exceed $\pm 1 \% \times \mathsf { V } _ { \mathsf { D D } }$ around the VREFCA(DC) value. Peak-to-peak AC noise on VREFCA should not exceed ±2% of VREFCA(DC). $\pm 2 \%$ 

2. DC values are determined to be less than $2 0 ~ \mathsf { M H z }$ in frequency. DRAM must meet specifications if the DRAM induces additional AC noise greater than 20 MHz in frequency. 

3. VREFDQ(DC) is expected to be approximately $0 . 5 \times \mathsf { V } _ { \mathsf { D D } }$ and to track variations in the DC level. Externally generated peak noise (non-common mode) on VREFDQ may not exceed $\pm 1 \% \times \mathsf { V } _ { \mathsf { D D } }$ around the VREFDQ(DC) value. Peak-to-peak AC noise on VREFDQ should not exceed ±2% of VREFDQ(DC). $\pm 2 \%$ 

4. VREFDQ(DC) may transition to VREFDQ(SR) and back to VREFDQ(DC) when in SELF REFRESH, within restrictions outlined in the SELF REFRESH section. 

5. $\mathsf { V } _ { \Pi }$ is not applied directly to the device. $\mathsf { V } _ { \Pi }$ is a system supply for signal termination resistors. Minimum and maximum values are system-dependent. 


Table 25: DDR3L 1.35V Input Switching Conditions – Command and Address


<table><tr><td>Parameter/Condition</td><td>Symbol</td><td>DDR3L-800/1066</td><td>DDR3L-1333/1600</td><td>DDR3L-1866/2133</td><td>Units</td></tr><tr><td colspan="6">Command and Address</td></tr><tr><td rowspan="3">Input high AC voltage: Logic 1</td><td>VIH(AC160),min5</td><td>160</td><td>160</td><td>-</td><td>mV</td></tr><tr><td>VIH(AC135),min5</td><td>135</td><td>135</td><td>135</td><td>mV</td></tr><tr><td>VIH(AC125),min5</td><td>-</td><td>-</td><td>125</td><td>mV</td></tr><tr><td>Input high DC voltage: Logic 1</td><td>VIH(DC90),min</td><td>90</td><td>90</td><td>90</td><td>mV</td></tr><tr><td>Input low DC voltage: Logic 0</td><td>VIL(DC90),min</td><td>-90</td><td>-90</td><td>-90</td><td>mV</td></tr><tr><td rowspan="3">Input low AC voltage: Logic 0</td><td>VIL(AC125),min5</td><td>-</td><td>-</td><td>-125</td><td>mV</td></tr><tr><td>VIL(AC135),min5</td><td>-135</td><td>-135</td><td>-135</td><td>mV</td></tr><tr><td>VIL(AC160),min5</td><td>-160</td><td>-160</td><td>-</td><td>mV</td></tr><tr><td colspan="6">DQ and DM</td></tr><tr><td rowspan="3">Input high AC voltage: Logic 1</td><td>VIH(AC160),min5</td><td>160</td><td>160</td><td>-</td><td>mV</td></tr><tr><td>VIH(AC135),min5</td><td>135</td><td>135</td><td>135</td><td>mV</td></tr><tr><td>VIH(AC125),min5</td><td>-</td><td>-</td><td>130</td><td>mV</td></tr><tr><td>Input high DC voltage: Logic 1</td><td>VIH(DC90),min</td><td>90</td><td>90</td><td>90</td><td>mV</td></tr><tr><td>Input low DC voltage: Logic 0</td><td>VIL(DC90),min</td><td>-90</td><td>-90</td><td>-90</td><td>mV</td></tr><tr><td rowspan="3">Input low AC voltage: Logic 0</td><td>VIL(AC125),min5</td><td>-</td><td>-</td><td>-130</td><td>mV</td></tr><tr><td>VIL(AC135),min5</td><td>-135</td><td>-135</td><td>-135</td><td>mV</td></tr><tr><td>VIL(AC160),min5</td><td>-160</td><td>-160</td><td>-</td><td>mV</td></tr></table>

Notes: 1. All voltages are referenced to $V _ { R E F }$ . $V _ { \mathsf { R E F } }$ is $V _ { R E F C A }$ for control, command, and address. All slew rates and setup/hold times are specified at the DRAM ball. $V _ { \mathsf { R E F } }$ is VREFDQ for DQ and DM inputs. 

2. Input setup timing parameters (t IS and ${ } ^ { \mathrm { t } } \mathsf { D } { \mathsf { S } }$ ) are referenced at $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) } / \mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) } ,$ not VREF(DC). 

3. Input hold timing parameters (t IH and t DH) are referenced at $\mathsf { V } _ { \mathsf { I L ( D C ) } } / \mathsf { V } _ { \mathsf { I H ( D C ) } } ,$ not VREF(DC). 

4. Single-ended input slew rate $=$ 1 V/ns; maximum input voltage swing under test is $9 0 0 \mathsf { m } \mathsf { V }$ (peak-to-peak). 

5. When two $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ values (and two corresponding $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ values) are listed for a specific speed bin, the user may choose either value for the input AC level. Whichever value is used, the associated setup time for that AC level must also be used. Additionally, one $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ value may be used for address/command inputs and the other $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ value may be used for data inputs. 

For example, for DDR3-800, two input AC levels are defined: $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 6 0 ) , \mathsf { m i n } }$ and $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 3 5 ) , \mathsf { m i n } }$ (corresponding $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C 1 6 0 } ) , \mathsf { m i n } }$ and $\mathsf { V } _ { 1 \mathsf { L } ( \mathsf { A C } 1 3 5 ) , \mathsf { m i n } } )$ . For DDR3-800, the address/ command inputs must use either $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 6 0 ) , \mathsf { m i n } }$ with t IS(AC160) of 210ps or $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } }$ with t IS(AC135) of 365ps; independently, the data inputs must use either VIH(AC160),min with t DS(AC160) of 75ps or $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } }$ with t DS(AC150) of 125ps. 


Table 26: DDR3L 1.35V Differential Input Operating Conditions (CK, CK# and DQS, DQS#)


<table><tr><td>Parameter/Condition</td><td>Symbol</td><td>Min</td><td>Max</td><td>Units</td><td>Notes</td></tr><tr><td>Differential input logic high – slew</td><td>VIH,diff(AC)slew</td><td>180</td><td>N/A</td><td>mV</td><td>4</td></tr><tr><td>Differential input logic low – slew</td><td>VIL,diff(AC)slew</td><td>N/A</td><td>-180</td><td>mV</td><td>4</td></tr><tr><td>Differential input logic high</td><td>VIH,diff(AC)</td><td>2 × (VIH(AC) - VREF)</td><td>VDD/VDDQ</td><td>mV</td><td>5</td></tr><tr><td>Differential input logic low</td><td>VIL,diff(AC)</td><td>VSS/VSSQ</td><td>2 × (VIL(AC) - VREF)</td><td>mV</td><td>6</td></tr><tr><td>Differential input crossing voltage relative to VDD/2 for DQS, DQS#, CK, CK#</td><td>VIX</td><td>VREF(DC) - 150</td><td>VREF(DC) + 150</td><td>mV</td><td>5, 7, 9</td></tr><tr><td>Differential input crossing voltage relative to VDD/2 for CK, CK#</td><td>VIX (175)</td><td>VREF(DC) - 175</td><td>VREF(DC) + 175</td><td>mV</td><td>5, 7–9</td></tr><tr><td>Single-ended high level for strobes</td><td rowspan="2">VSEH</td><td>VDDQ/2 + 160</td><td>VDDQ</td><td>mV</td><td>5</td></tr><tr><td>Single-ended high level for CK, CK#</td><td>VDD/2 + 160</td><td>VDD</td><td>mV</td><td>5</td></tr><tr><td>Single-ended low level for strobes</td><td rowspan="2">VSEL</td><td>VSSQ</td><td>VDDQ/2 - 160</td><td>mV</td><td>6</td></tr><tr><td>Single-ended low level for CK, CK#</td><td>VSS</td><td>VDD/2 - 160</td><td>mV</td><td>6</td></tr></table>

Notes: 1. Clock is referenced to $V _ { \mathsf { D D } }$ and $\mathsf { V } _ { \mathsf { S } \mathsf { S } }$ . Data strobe is referenced to $V _ { \mathsf { D D Q } }$ and $\mathsf { V } _ { \mathsf { S S Q } }$ 

2. Reference is VREFCA(DC) for clock and VREFDQ(DC) for strobe. 

3. Differential input slew rate $^ { = 2 }$ V/ns. 

4. Defines slew rate reference points, relative to input crossing voltages. 

5. Minimum DC limit is relative to single-ended signals; overshoot specifications are applicable. 

6. Maximum DC limit is relative to single-ended signals; undershoot specifications are applicable. 

7. The typical value of $\mathsf { V } _ { \mathsf { I X } ( \mathsf { A C } ) }$ is expected to be about $0 . 5 \times \mathsf { V } _ { \mathsf { D } \mathsf { D } }$ of the transmitting device, and $\mathsf { V } _ { \mathsf { I X } ( \mathsf { A C } ) }$ is expected to track variations in $\mathsf { V } _ { \mathsf { D D } } . \mathsf { V } _ { \mathsf { I X } ( \mathsf { A C } ) }$ indicates the voltage at which differential input signals must cross. 

8. The $\mathsf { V } _ { \mathsf { I X } }$ extended range $( \pm 1 7 5 \mathrm { m V } )$ is allowed only for the clock; this $\mathsf { V } _ { \mathsf { I X } }$ extended range is only allowed when the following conditions are met: The single-ended input signals are monotonic, have the single-ended swing $\mathsf { V } _ { \mathsf { S E L } } , \mathsf { V } _ { \mathsf { S E H } }$ of at least $\mathsf { V } _ { \mathsf { D D } } / 2 \pm 2 5 0 \mathsf { m V } ,$ and the differential slew rate of CK, CK# is greater than 3 V/ns. 

9. $\mathsf { V } _ { \mathsf { I X } }$ must provide $2 5 \mathsf { m V }$ (single-ended) of the voltages separation. 


Figure 15: DDR3L 1.35V Input Signal


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/4e4b32a07443b9c89913c847d2f53f9db7192b3e63cc9234b3e26041183c14a4.jpg)



Note: 1. Numbers in diagrams reflect nominal values.


# DDR3L 1.35V AC Overshoot/Undershoot Specification


Table 27: DDR3L Control and Address Pins


<table><tr><td>Parameter</td><td>DDR3L-800</td><td>DRR3L-1066</td><td>DDR3L-1333</td><td>DDR3L-1600</td><td>DDR3L-1866</td><td>DDR3L-2133</td></tr><tr><td>Maximum peak amplitude allowed for overshoot area (see Figure 16)</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td></tr><tr><td>Maximum peak amplitude allowed for undershoot area (see Figure 17)</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td></tr><tr><td>Maximum overshoot area above VDD (see Figure 16)</td><td>0.67 V/ns</td><td>0.5 V/ns</td><td>0.4 V/ns</td><td>0.33 V/ns</td><td>0.28 V/ns</td><td>0.25 V/ns</td></tr><tr><td>Maximum undershoot area below VSS (see Figure 17)</td><td>0.67 V/ns</td><td>0.5 V/ns</td><td>0.4 V/ns</td><td>0.33 V/ns</td><td>0.28 V/ns</td><td>0.25 V/ns</td></tr></table>


Table 28: DDR3L 1.35V Clock, Data, Strobe, and Mask Pins


<table><tr><td>Parameter</td><td>DDR3L-800</td><td>DDR3L-1066</td><td>DDR3L-1333</td><td>DDR3L-1600</td><td>DDR3L-1866</td><td>DDR3L-2133</td></tr><tr><td>Maximum peak amplitude allowed for overshoot area (see Figure 16)</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td></tr><tr><td>Maximum peak amplitude allowed for undershoot area (see Figure 17)</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td><td>0.4V</td></tr><tr><td>Maximum overshoot area above VDD/VDDQ (see Figure 16)</td><td>0.25 V/ns</td><td>0.19 V/ns</td><td>0.15 V/ns</td><td>0.13 V/ns</td><td>0.11 V/ns</td><td>0.10 V/ns</td></tr><tr><td>Maximum undershoot area below VSS/VSSQ (see Figure 17)</td><td>0.25 V/ns</td><td>0.19 V/ns</td><td>0.15 V/ns</td><td>0.13 V/ns</td><td>0.11 V/ns</td><td>0.10 V/ns</td></tr></table>


Figure 16: Overshoot


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/50f5af50a9af8ac87df37758730ec26708f107ac8fba6e51da6e934d01fabf74.jpg)



Figure 17: Undershoot


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/517c61ca8eb75f6587f73a5813a4afc94b8fd70cd5ab2224c90bb60c7ae7ca47.jpg)



Figure 18: $\mathsf { \mathbf { v } } _ { \parallel \mathbf { x } }$ for Differential Signals


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/d6bc95563262559b87cb031d4b08d47b324b3d8515c0085be9b2704aa98c4faa.jpg)



Figure 19: Single-Ended Requirements for Differential Signals


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/43a75bb6fb420f381aa09d581484e1e957af9a57dbe7ed61b1c7fd372e10431d.jpg)



Figure 20: Definition of Differential AC-Swing and t DVAC


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/460f81e4752431871b82ce5e8c7008c31a20af60311a52d4cdbcd63c4eba17b7.jpg)



Table 29: DDR3L 1.35V – Minimum Required Time t DVAC for CK/CK#, DQS/DQS# Differential for AC Ringback


<table><tr><td rowspan="2">Slew Rate (V/ns)</td><td colspan="2">DDR3L-800/1066/1333/1600</td><td colspan="3">DDR3L-1866/2133</td></tr><tr><td>\( ^t \)DVAC at 320mV (ps)</td><td>\( ^t \)DVAC at 270mV (ps)</td><td>\( ^t \)DVAC at 270mV (ps)</td><td>\( ^t \)DVAC at 250mV (ps)</td><td>\( ^t \)DVAC at 260mV (ps)</td></tr><tr><td>&gt;4.0</td><td>189</td><td>201</td><td>163</td><td>168</td><td>176</td></tr><tr><td>4.0</td><td>189</td><td>201</td><td>163</td><td>168</td><td>176</td></tr><tr><td>3.0</td><td>162</td><td>179</td><td>140</td><td>147</td><td>154</td></tr><tr><td>2.0</td><td>109</td><td>134</td><td>95</td><td>105</td><td>111</td></tr><tr><td>1.8</td><td>91</td><td>119</td><td>80</td><td>91</td><td>97</td></tr><tr><td>1.6</td><td>69</td><td>100</td><td>62</td><td>74</td><td>78</td></tr><tr><td>1.4</td><td>40</td><td>76</td><td>37</td><td>52</td><td>55</td></tr><tr><td>1.2</td><td>Note 1</td><td>44</td><td>5</td><td>22</td><td>24</td></tr><tr><td>1.0</td><td colspan="5">Note 1</td></tr><tr><td>&lt;1.0</td><td colspan="5">Note 1</td></tr></table>


Note: 1. Rising input signal shall become equal to or greater than $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ level and Falling input signal shall become equal to or less than $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ level. 


# DDR3L 1.35V Slew Rate Definitions for Single-Ended Input Signals

Setup (t IS and $^ \mathrm { t } \mathrm { D } S$ ) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V } _ { \mathrm { R E F } }$ and the first crossing of $\mathrm { V _ { I H ( A C ) m i n } }$ . Setup (t IS and t DS) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of $\mathrm { V _ { R E F } }$ and the first crossing of $\mathrm { V _ { I L ( A C ) m a x } }$ . 

Hold (t IH and t DH) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V _ { I L ( D C ) m a x } }$ and the first crossing of $\mathrm { V } _ { \mathrm { R E F } }$ . Hold (t IH and t DH) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of $ { \mathrm { V } _ { \mathrm { I H ( D C ) m i n } } }$ and the first crossing of $\mathrm { V _ { R E F } }$ (see Figure 21 (page 56)). 


Table 30: Single-Ended Input Slew Rate Definition


<table><tr><td colspan="2">Input Slew Rates (Linear Signals)</td><td colspan="2">Measured</td><td rowspan="2">Calculation</td></tr><tr><td>Input</td><td>Edge</td><td>From</td><td>To</td></tr><tr><td rowspan="2">Setup</td><td>Rising</td><td>VREF</td><td>VIH(AC),min</td><td>VIH(AC),min - VREF ΔTRSse</td></tr><tr><td>Falling</td><td>VREF</td><td>VIL(AC),max</td><td>VREF - VIL(AC),max ΔTFSse</td></tr><tr><td rowspan="2">Hold</td><td>Rising</td><td>VIL(DC),max</td><td>VREF</td><td>VREF - VIL(DC),max ΔTFHse</td></tr><tr><td>Falling</td><td>VIH(DC),min</td><td>VREF</td><td>VIH(DC),min - VREF ΔTRSHse</td></tr></table>


Figure 21: Nominal Slew Rate Definition for Single-Ended Input Signals


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/4646e609dae6d581b0fc37dffd12a6f68b75fc26e0f06c8163ca705a2be2b7a9.jpg)



Hold


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/6196f0b8ea4d4b7bf6a6efffecf5019c5e932438c19e3f214dd3f20adaa614b7.jpg)


# DDR3L 1.35V Slew Rate Definitions for Differential Input Signals

Input slew rate for differential signals (CK, CK# and DQS, DQS#) are defined and measured, as shown in Table 31 and Figure 22. The nominal slew rate for a rising signal is defined as the slew rate between $\mathrm { V _ { I L , d i f f , m a x } }$ and $ { \mathrm { V } } _ { \mathrm { I H , d i f f , m i n } }$ . The nominal slew rate for a falling signal is defined as the slew rate between $ { \mathrm { V } } _ { \mathrm { I H , d i f f , m i n } }$ and $\mathrm { V _ { I L , d i f f , m a x } }$ . 


Table 31: DDR3L 1.35V Differential Input Slew Rate Definition


<table><tr><td colspan="2">Differential Input Slew Rates (Linear Signals)</td><td colspan="2">Measured</td><td rowspan="2">Calculation</td></tr><tr><td>Input</td><td>Edge</td><td>From</td><td>To</td></tr><tr><td rowspan="2">CK and DQS reference</td><td>Rising</td><td>VIL,diff,max</td><td>VIH,diff,min</td><td>VIH,diff,min - VIL,diff,max ΔTRdiff</td></tr><tr><td>Falling</td><td>VIH,diff,min</td><td>VIL,diff,max</td><td>VIH,diff,min - VIL,diff,max ΔTFdiff</td></tr></table>


Figure 22: DDR3L 1.35V Nominal Differential Input Slew Rate Definition for DQS, DQS# and CK, CK#


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/ec1965b8b922a39a056f4107960923bb0071a23a77e14c162bae803a1c1f7390.jpg)


# ODT Characteristics

The ODT effective resistance $\mathrm { R } _ { \mathrm { T T } }$ is defined by MR1[9, 6, and 2]. ODT is applied to the DQ, DM, DQS, DQS#, and TDQS, TDQS# balls (x8 devices only). The ODT target values and a functional representation are listed in Table 32 and Table 33 (page 59). The individual pull-up and pull-down resistors $\mathrm { ( R _ { T T ( P U ) } }$ and ${ \mathrm { R } } _ { \mathrm { T T } ( { \mathrm { P D } } ) }$ ) are defined as follows: 

• $R _ { T T ( P U ) } = ( V _ { D D Q } - V _ { O U T } ) / | I _ { O U T } | ,$ , under the condition that ${ \mathrm { R } } _ { \mathrm { T T } ( \mathrm { P D } ) }$ is turned off 

• $R _ { T T ( P D ) } = ( V _ { O U T } ) / | I _ { O U T } |$ , under the condition that $\mathrm { R _ { T T ( P U ) } }$ is turned off 


Figure 23: ODT Levels and I-V Characteristics


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/d068832d13e7d040d7090a9190a8781c6f21fc9b9859e252d347286ce821c448.jpg)



Table 32: On-Die Termination DC Electrical Characteristics


<table><tr><td>Parameter/Condition</td><td>Symbol</td><td>Min</td><td>Nom</td><td>Max</td><td>Unit</td><td>Notes</td></tr><tr><td>RTT effective impedance</td><td>RTT(EFF)</td><td colspan="4">See Table 33 (page 59)</td><td>1, 2</td></tr><tr><td>Deviation of VM with respect to VDDQ/2</td><td>ΔVM</td><td>-5</td><td></td><td>5</td><td>%</td><td>1, 2, 3</td></tr></table>

Notes: 1. Tolerance limits are applicable after proper ZQ calibration has been performed at a stable temperature and voltage $( \mathsf { V } _ { \mathsf { D D Q } } = \mathsf { V } _ { \mathsf { D D } } , \mathsf { V } _ { 5 5 \mathsf { Q } } = \mathsf { V } _ { 5 5 } )$ . Refer to ODT Sensitivity (page 60) if either the temperature or voltage changes after calibration. 

2. Measurement definition for $\mathsf { R } _ { \mathsf { T T } }$ : Apply $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ to pin under test and measure current $\begin{array} { r } { \mathbb { I } [ \mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) } ] , } \end{array}$ then apply $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ to pin under test and measure current $\mathsf { I } [ \mathsf { V } _ { 1 \mathsf { L } ( \mathsf { A C } ) } ]$ : 

$$
R _ {T T} = \frac {V _ {I H (A C)} - V _ {I L (A C)}}{I \left(V _ {I H (A C)} - I \left(V _ {I L (A C)}\right) \right.}
$$

3. Measure voltage (VM) at the tested pin with no load: 

$$
\Delta \mathrm {V M} = \left(\frac {2 \times \mathrm {V M}}{\mathrm {V} _ {\mathrm {D D Q}}} - 1\right) \times 1 0 0
$$

4. For IT and AT devices, the minimum values are derated by $6 \%$ when the device operates between $\angle 4 0 ^ { \circ } \mathsf { C }$ and $0 ^ { \circ } \mathsf { C }$ (TC). 

# 1.35V ODT Resistors

Table 33 provides an overview of the ODT DC electrical characteristics. The values provided are not specification requirements; however, they can be used as design guidelines to indicate what $\mathrm { R } _ { \mathrm { T T } }$ is targeted to provide: 

• $\mathrm { R } _ { \mathrm { T T } } 1 2 0 \Omega$ is made up of RTT120(PD240) and RTT120(PU240) 

• $\mathrm { R } _ { \mathrm { T T } } 6 0 \Omega$ is made up of RTT60(PD120) and RTT60(PU120) 

• $\mathrm { R } _ { \mathrm { T T } } 4 0 \Omega$ is made up of RTT40(PD80) and RTT40(PU80) 

• $\mathrm { R } _ { \mathrm { T T } } 3 0 \Omega$ is made up of RTT30(PD60) and RTT30(PU60) 

• $\mathrm { R } _ { \mathrm { T T } } 2 0 \Omega$ is made up of RTT20(PD40) and RTT20(PU40) 


Table 33: 1.35V $\scriptstyle { \mathsf { R } } _ { \mathsf { T } \mathsf { T } }$ Effective Impedance


<table><tr><td>MR1[9, 6, 2]</td><td>RTT</td><td>Resistor</td><td>VOUT</td><td>Min</td><td>Nom</td><td>Max</td><td>Units</td></tr><tr><td rowspan="7">0, 1, 0</td><td rowspan="6">120Ω</td><td rowspan="3">RTT,120PD240</td><td>0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/1</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/1</td></tr><tr><td>0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/1</td></tr><tr><td rowspan="3">RTT,120PU240</td><td>0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/1</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/1</td></tr><tr><td>0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/1</td></tr><tr><td colspan="2">120Ω</td><td>VIL(AC) to VIH(AC)</td><td>0.9</td><td>1.0</td><td>1.65</td><td>RZQ/2</td></tr><tr><td rowspan="7">0, 0, 1</td><td rowspan="6">60Ω</td><td rowspan="3">RTT,60PD120</td><td>0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/2</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/2</td></tr><tr><td>0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/2</td></tr><tr><td rowspan="3">RTT,60PU120</td><td>0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/2</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/2</td></tr><tr><td>0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/2</td></tr><tr><td colspan="2">60Ω</td><td>VIL(AC) to VIH(AC)</td><td>0.9</td><td>1.0</td><td>1.65</td><td>RZQ/4</td></tr><tr><td rowspan="7">0, 1, 1</td><td rowspan="6">40Ω</td><td rowspan="3">RTT,40PD80</td><td>0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/3</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/3</td></tr><tr><td>0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/3</td></tr><tr><td rowspan="3">RTT,40PU80</td><td>0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/3</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/3</td></tr><tr><td>0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/3</td></tr><tr><td colspan="2">40Ω</td><td>VIL(AC) to VIH(AC)</td><td>0.9</td><td>1.0</td><td>1.65</td><td>RZQ/6</td></tr><tr><td rowspan="7">1, 0, 1</td><td rowspan="6">30Ω</td><td rowspan="3">RTT,30PD60</td><td>0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/4</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/4</td></tr><tr><td>0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/4</td></tr><tr><td rowspan="3">RTT,30PU60</td><td>0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/4</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/4</td></tr><tr><td>0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/4</td></tr><tr><td colspan="2">30Ω</td><td>VIL(AC) to VIH(AC)</td><td>0.9</td><td>1.0</td><td>1.65</td><td>RZQ/8</td></tr><tr><td rowspan="7">1, 0, 0</td><td rowspan="6">20Ω</td><td rowspan="3">RTT,20PD40</td><td>0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/6</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/6</td></tr><tr><td>0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/6</td></tr><tr><td rowspan="3">RTT,20PU40</td><td>0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/6</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/6</td></tr><tr><td>0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/6</td></tr><tr><td colspan="2">20Ω</td><td>VIL(AC) to VIH(AC)</td><td>0.9</td><td>1.0</td><td>1.65</td><td>RZQ/12</td></tr></table>

# ODT Sensitivity

If either the temperature or voltage changes after I/O calibration, then the tolerance limits listed in Table 32 and Table 33 can be expected to widen according to Table 34 and Table 35. 


Table 34: ODT Sensitivity Definition


<table><tr><td>Symbol</td><td>Min</td><td>Max</td><td>Unit</td></tr><tr><td>RTT</td><td>0.9 - dRTTdT × |DT| - dRTTdV × |DV|</td><td>1.6 + dRTTdT × |DT| + dRTTdV × |DV|</td><td>RZQ/(2, 4, 6, 8, 12)</td></tr></table>


Note: 1. $\Delta \mathsf { T } = \mathsf { T } - \mathsf { T } ( \mathscr { Q }$ calibration), $\Delta \mathsf { V } = \mathsf { V } _ { \mathsf { D D Q } } - \mathsf { V } _ { \mathsf { D D Q } } ( \ @$ calibration) and $\mathsf { V } _ { \mathsf { D D } } = \mathsf { V } _ { \mathsf { D D Q } }$ 



Table 35: ODT Temperature and Voltage Sensitivity


<table><tr><td>Change</td><td>Min</td><td>Max</td><td>Unit</td></tr><tr><td>dRTTdT</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRTTdV</td><td>0</td><td>0.15</td><td>%/mV</td></tr></table>


Note: 1. $\Delta \mathsf { T } = \mathsf { T } - \mathsf { T } ( \mathscr { Q }$ $@$ calibration), $\Delta \mathsf { V } = \mathsf { V } _ { \mathsf { D D Q } } - \mathsf { V } _ { \mathsf { D D Q } } ( \ @$ calibration) and $\mathsf { V } _ { \mathsf { D D } } = \mathsf { V } _ { \mathsf { D D Q } }$ 


# ODT Timing Definitions

ODT loading differs from that used in AC timing measurements. The reference load for ODT timings is shown in Figure 24. Two parameters define when ODT turns on or off synchronously, two define when ODT turns on or off asynchronously, and another defines when ODT turns on or off dynamically. Table 36 and Table 37 (page 61) outline and provide definition and measurement references settings for each parameter. 

ODT turn-on time begins when the output leaves High-Z and ODT resistance begins to turn on. ODT turn-off time begins when the output leaves Low-Z and ODT resistance begins to turn off. 


Figure 24: ODT Timing Reference Load


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/9d666289d3552df1a8c0038ce439d321f3220fb804f295bd0040e630789e4066.jpg)



Table 36: ODT Timing Definitions


<table><tr><td>Symbol</td><td>Begin Point Definition</td><td>End Point Definition</td><td>Figure</td></tr><tr><td>tAON</td><td>Rising edge of CK - CK# defined by the end point of ODTLon</td><td>Extrapolated point at VSSQ</td><td>Figure 25 (page 62)</td></tr><tr><td>tAOF</td><td>Rising edge of CK - CK# defined by the end point of ODTLoff</td><td>Extrapolated point at VRTT,nom</td><td>Figure 25 (page 62)</td></tr><tr><td>tAONPD</td><td>Rising edge of CK - CK# with ODT first being registered HIGH</td><td>Extrapolated point at VSSQ</td><td>Figure 26 (page 62)</td></tr><tr><td>tAOFPD</td><td>Rising edge of CK - CK# with ODT first being registered LOW</td><td>Extrapolated point at VRTT,nom</td><td>Figure 26 (page 62)</td></tr><tr><td>tADC</td><td>Rising edge of CK - CK# defined by the end point of ODTLcnw, ODTLcwn4, or ODTLcwn8</td><td>Extrapolated points at VRTT(WR) and VRTT,nom</td><td>Figure 27 (page 63)</td></tr></table>


Table 37: DDR3L(1.35V) Reference Settings for ODT Timing Measurements


<table><tr><td>Measured Parameter</td><td>RTT,nom Setting</td><td>RTT(WR) Setting</td><td>VSW1</td><td>VSW2</td></tr><tr><td rowspan="2">tAON</td><td>RZQ/4 (60Ω)</td><td>N/A</td><td>50mV</td><td>100mV</td></tr><tr><td>RZQ/12 (20Ω)</td><td>N/A</td><td>100mV</td><td>200mV</td></tr><tr><td rowspan="2">tAOF</td><td>RZQ/4 (60Ω)</td><td>N/A</td><td>50mV</td><td>100mV</td></tr><tr><td>RZQ/12 (20Ω)</td><td>N/A</td><td>100mV</td><td>200mV</td></tr><tr><td rowspan="2">tAONPD</td><td>RZQ/4 (60Ω)</td><td>N/A</td><td>50mV</td><td>100mV</td></tr><tr><td>RZQ/12 (20Ω)</td><td>N/A</td><td>100mV</td><td>200mV</td></tr><tr><td rowspan="2">tAOFPD</td><td>RZQ/4 (60Ω)</td><td>N/A</td><td>50mV</td><td>100mV</td></tr><tr><td>RZQ/12 (20Ω)</td><td>N/A</td><td>100mV</td><td>200mV</td></tr><tr><td>tADC</td><td>RZQ/12 (20Ω)</td><td>RZQ/2 (20Ω)</td><td>200mV</td><td>250mV</td></tr></table>


Figure 25: t AON and t AOF Definitions


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/8415aa563f525f66a59e759f55cc461ae9d13589467d33fef8276c5ac745c0a6.jpg)



Figure 26: t AONPD and t AOFPD Definitions


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/794faef4c4c5ce6d784a11c5866fe29be1765a6c34fec0a18b085a0e423fa5cc.jpg)



Figure 27: t ADC Definition


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/6875d62428aafc486c0e10c259f4d772ccf52048f6d2f8c2720ae74873446688.jpg)


# Output Driver Impedance

The output driver impedance is selected by MR1[5,1] during initialization. The selected value is able to maintain the tight tolerances specified if proper ZQ calibration is performed. Output specifications refer to the default output driver unless specifically stated otherwise. A functional representation of the output buffer is shown below. The output driver impedance $\operatorname { R o n }$ is defined by the value of the external reference resistor RZQ as follows: 

• $R _ { O N , x } = R Z Q / y$ (with $\mathrm { R Z Q } = 2 4 0 \Omega \pm 1 \%$ ; $x = 3 4 \Omega$ or $4 0 \Omega$ with $y = 7$ or 6, respectively) 

The individual pull-up and pull-down resistors RON(PU) and RON(PD) are defined as follows: 

• $R _ { O N ( P U ) } = ( V _ { D D Q } - V _ { O U T } ) / | I _ { O U T } | ,$ , when RON(PD) is turned off 

• $R _ { O N ( P D ) } = ( V _ { O U T } ) / | I _ { O U T } |$ , when $\mathrm { R _ { O N ( P U ) } }$ is turned off 


Figure 28: Output Driver


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/a312b44dd6d758d4944c7ecc497cc7d42e05b9df41baa75fe049401d9806c959.jpg)


# 34 Ohm Output Driver Impedance

The 34Ω driver $( \mathrm { M R 1 } [ 5 , 1 ] = 0 1 )$ ) is the default driver. Unless otherwise stated, all timings and specifications listed herein apply to the 34Ω driver only. Its impedance $\mathrm { R _ { O N } }$ is defined by the value of the external reference resistor RZQ as follows: $\mathrm { R _ { O N 3 4 } } = \mathrm { R Z Q } / 7$ (with nominal $\mathrm { R Z Q } = 2 4 0 \Omega \pm 1 \% )$ and is actually $3 4 . 3 \Omega \pm 1 \%$ . 


Table 38: DDR3L 34 Ohm Driver Impedance Characteristics


<table><tr><td>MR1
[5, 1]</td><td>RON</td><td>Resistor</td><td>VOUT</td><td>Min</td><td>Nom</td><td>Max</td><td>Units</td></tr><tr><td rowspan="6">0, 1</td><td rowspan="6">34.3Ω</td><td rowspan="3">RON,34PD</td><td>0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/7</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/7</td></tr><tr><td>0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/7</td></tr><tr><td rowspan="3">RON,34PU</td><td>0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/7</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/7</td></tr><tr><td>0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/7</td></tr><tr><td colspan="3">Pull-up/pull-down mismatch (MMPUPD)</td><td>VIL(AC) to VIH(AC)</td><td>-10</td><td>N/A</td><td>10</td><td>%</td></tr></table>

Notes: 1. Tolerance limits assume RZQ of $2 4 0 \Omega \pm 1 \%$ and are applicable after proper ZQ calibration has been performed at a stable temperature and voltage: $V _ { D D Q } = V _ { D D } ; V _ { S S Q } = V _ { S S } )$ . Refer to DDR3L 34 Ohm Output Driver Sensitivity (page 67) if either the temperature or the voltage changes after calibration. 

2. Measurement definition for mismatch between pull-up and pull-down $( \mathsf { M M } _ { \mathsf { P U P D } } )$ . Measure both RON(PU) and ${ \mathsf { R } } _ { \mathsf { O N } ( { \mathsf { P D } } ) }$ at $0 . 5 \times \mathsf { V } _ { \mathsf { D D Q } }$ : 

$$
M M _ {P U P D} = \frac {R _ {O N (P U)} - R _ {O N (P D)}}{R _ {O N , n o m}} \times 1 0 0
$$

3. For IT and AT (1Gb only) devices, the minimum values are derated by $6 \%$ when the device operates between $\ - 4 0 ^ { \circ } \mathsf { C }$ and $0 \%$ (TC). 

A larger maximum limit will result in slightly lower minimum currents. 

# DDR3L 34 Ohm Driver

Using Table 39, the 34Ω driver’s current range has been calculated and summarized in Table 40 (page 66) $\mathrm { V _ { D D } } = 1 . 3 5 \mathrm { V } ,$ Table 41 for $\mathrm { V _ { D D } } = 1 . 4 5 \mathrm { V } ,$ and Table 42 (page 67) for $\mathrm { V _ { D D } } = 1 . 2 8 3 \mathrm { V } .$ The individual pull-up and pull-down resistors RON34(PD) and RON34(PU) are defined as follows: 

• RON34(PD) = (VOUT)/|IOUT|; RON34(PU) is turned off 

• RON34(PU) = (VDDQ - VOUT)/|IOUT|; RON34(PD) is turned off 


Table 39: DDR3L 34 Ohm Driver Pull-Up and Pull-Down Impedance Calculations


<table><tr><td colspan="4">RON</td><td>Min</td><td>Nom</td><td>Max</td><td>Unit</td></tr><tr><td colspan="4">RZQ = 240Ω ±1%</td><td>237.6</td><td>240</td><td>242.4</td><td>Ω</td></tr><tr><td colspan="4">RZQ/7 = (240Ω ±1%)/7</td><td>33.9</td><td>34.3</td><td>34.6</td><td>Ω</td></tr><tr><td>MR1[5,1]</td><td>RON</td><td>Resistor</td><td>VOUT</td><td>Min</td><td>Nom</td><td>Max</td><td>Unit</td></tr><tr><td rowspan="6">0,1</td><td rowspan="6">34.3Ω</td><td rowspan="3">RON34(PD)</td><td>0.2 × VDDQ</td><td>20.4</td><td>34.3</td><td>38.1</td><td>Ω</td></tr><tr><td>0.5 × VDDQ</td><td>30.5</td><td>34.3</td><td>38.1</td><td>Ω</td></tr><tr><td>0.8 × VDDQ</td><td>30.5</td><td>34.3</td><td>48.5</td><td>Ω</td></tr><tr><td rowspan="3">RON34(PU)</td><td>0.2 × VDDQ</td><td>30.5</td><td>34.3</td><td>48.5</td><td>Ω</td></tr><tr><td>0.5 × VDDQ</td><td>30.5</td><td>34.3</td><td>38.1</td><td>Ω</td></tr><tr><td>0.8 × VDDQ</td><td>20.4</td><td>34.3</td><td>38.1</td><td>Ω</td></tr></table>


Table 40: DDR3L 34 Ohm Driver $\boldsymbol { \mathbf { I _ { O H } } } \boldsymbol { \Lambda _ { \mathbf { O L } } }$ Characteristics: VDD = VDDQ = DDR3L@1.35V


<table><tr><td>MR1[5,1]</td><td>RON</td><td>Resistor</td><td>VOUT</td><td>Max</td><td>Nom</td><td>Min</td><td>Unit</td></tr><tr><td rowspan="6">0,1</td><td rowspan="6">34.3Ω</td><td rowspan="3">RON34(PD)</td><td>IOL@ 0.2 × VDDQ</td><td>13.3</td><td>7.9</td><td>7.1</td><td>mA</td></tr><tr><td>IOL@ 0.5 × VDDQ</td><td>22.1</td><td>19.7</td><td>17.7</td><td>mA</td></tr><tr><td>IOL@ 0.8 × VDDQ</td><td>35.4</td><td>31.5</td><td>22.3</td><td>mA</td></tr><tr><td rowspan="3">RON34(PU)</td><td>IOH@ 0.2 × VDDQ</td><td>35.4</td><td>31.5</td><td>22.3</td><td>mA</td></tr><tr><td>IOH@ 0.5 × VDDQ</td><td>22.1</td><td>19.7</td><td>17.7</td><td>mA</td></tr><tr><td>IOH@ 0.8 × VDDQ</td><td>13.3</td><td>7.9</td><td>7.1</td><td>mA</td></tr></table>


Table 41: DDR3L 34 Ohm Driver $\boldsymbol { \mathbf { I _ { O H } } } \boldsymbol { \Lambda _ { \mathbf { O L } } }$ Characteristics: $\begin{array} { r } { \mathbf { V _ { D D } } = \mathbf { V _ { D D Q } } = } \end{array}$ DDR3L@1.45V


<table><tr><td>MR1[5,1]</td><td>RON</td><td>Resistor</td><td>VOUT</td><td>Max</td><td>Nom</td><td>Min</td><td>Unit</td></tr><tr><td rowspan="6">0,1</td><td rowspan="6">34.3Ω</td><td rowspan="3">RON34(PD)</td><td>IOL@ 0.2 × VDDQ</td><td>14.2</td><td>8.5</td><td>7.6</td><td>mA</td></tr><tr><td>IOL@ 0.5 × VDDQ</td><td>23.7</td><td>21.1</td><td>19.0</td><td>mA</td></tr><tr><td>IOL@ 0.8 × VDDQ</td><td>38.0</td><td>33.8</td><td>23.9</td><td>mA</td></tr><tr><td rowspan="3">RON34(PU)</td><td>IOH@ 0.2 × VDDQ</td><td>38.0</td><td>33.8</td><td>23.9</td><td>mA</td></tr><tr><td>IOH@ 0.5 × VDDQ</td><td>23.7</td><td>21.1</td><td>19.0</td><td>mA</td></tr><tr><td>IOH@ 0.8 × VDDQ</td><td>14.2</td><td>8.5</td><td>7.6</td><td>mA</td></tr></table>


Table 42: DDR3L 34 Ohm Driver $\pmb { \mathrm { I o } } _ { \pmb { \mathrm { H } } } / \pmb { \mathrm { I l } } _ { \pmb { \mathrm { O } } \pmb { \mathrm { L } } }$ Characteristics: VDD = VDDQ $=$ DDR3L@1.283


<table><tr><td>MR1[5,1]</td><td>RON</td><td>Resistor</td><td>VOUT</td><td>Max</td><td>Nom</td><td>Min</td><td>Unit</td></tr><tr><td rowspan="6">0,1</td><td rowspan="6">34.3Ω</td><td rowspan="3">RON34(PD)</td><td>IOL@ 0.2 × VDDQ</td><td>12.6</td><td>7.5</td><td>6.7</td><td>mA</td></tr><tr><td>IOL@ 0.5 × VDDQ</td><td>21.0</td><td>18.7</td><td>16.8</td><td>mA</td></tr><tr><td>IOL@ 0.8 × VDDQ</td><td>33.6</td><td>29.9</td><td>21.2</td><td>mA</td></tr><tr><td rowspan="3">RON34(PU)</td><td>IOH@ 0.2 × VDDQ</td><td>33.6</td><td>29.9</td><td>21.2</td><td>mA</td></tr><tr><td>IOH@ 0.5 × VDDQ</td><td>21.0</td><td>18.7</td><td>16.8</td><td>mA</td></tr><tr><td>IOH@ 0.8 × VDDQ</td><td>12.6</td><td>7.5</td><td>6.7</td><td>mA</td></tr></table>

# DDR3L 34 Ohm Output Driver Sensitivity

If either the temperature or the voltage changes after ZQ calibration, then the tolerance limits listed in Table 38 (page 65) can be expected to widen according to Table 43 and Table 44. 


Table 43: DDR3L 34 Ohm Output Driver Sensitivity Definition


<table><tr><td>Symbol</td><td>Min</td><td>Max</td><td>Unit</td></tr><tr><td>RON(PD) @ 0.2 × VDDQ</td><td>0.6 - dRONdTL × |ΔT| - dRONdVL × |ΔV|</td><td>1.1 + dRONdTL × |ΔT| + dRONdVL × |ΔV|</td><td>RZQ/7</td></tr><tr><td>RON(PD) @ 0.5 × VDDQ</td><td>0.9 - dRONdTM × |ΔT| - dRONdVM × |ΔV|</td><td>1.1 + dRONdTM × |ΔT| + dRONdVM × |ΔV|</td><td>RZQ/7</td></tr><tr><td>RON(PD) @ 0.8 × VDDQ</td><td>0.9 - dRONdTH × |ΔT| - dRONdVH × |ΔV|</td><td>1.4 + dRONdTH × |ΔT| + dRONdVH × |ΔV|</td><td>RZQ/7</td></tr><tr><td>RON(PU) @ 0.2 × VDDQ</td><td>0.9 - dRONdTL × |ΔT| - dRONdVL × |ΔV|</td><td>1.4 + dRONdTL × |ΔT| + dRONdVL × |ΔV|</td><td>RZQ/7</td></tr><tr><td>RON(PU) @ 0.5 × VDDQ</td><td>0.9 - dRONdTM × |ΔT| - dRONdVM × |ΔV|</td><td>1.1 + dRONdTM × |ΔT| + dRONdVM × |ΔV|</td><td>RZQ/7</td></tr><tr><td>RON(PU) @ 0.8 × VDDQ</td><td>0.6 - dRONdTH × |ΔT| - dRONdVH × |ΔV|</td><td>1.1 + dRONdTH × |ΔT| + dRONdVH × |ΔV|</td><td>RZQ/7</td></tr></table>


Note: 1. $\Delta T = T$ - T(@CALIBRATION)ΔV = VDDQ - VDDQ(@CALIBRATION); and $V _ { D D } = V _ { D D Q }$ . 



Table 44: DDR3L 34 Ohm Output Driver Voltage and Temperature Sensitivity


<table><tr><td>Change</td><td>Min</td><td>Max</td><td>Unit</td></tr><tr><td>dRONdTM</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVM</td><td>0</td><td>0.13</td><td>%/mV</td></tr><tr><td>dRONdTL</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVL</td><td>0</td><td>0.13</td><td>%/mV</td></tr><tr><td>dRONdTH</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVH</td><td>0</td><td>0.13</td><td>%/mV</td></tr></table>

# DDR3L Alternative 40 Ohm Driver


Table 45: DDR3L 40 Ohm Driver Impedance Characteristics


<table><tr><td>MR1 [5, 1]</td><td>RON</td><td>Resistor</td><td>VOUT</td><td>Min</td><td>Nom</td><td>Max</td><td>Units</td></tr><tr><td rowspan="6">0, 0</td><td rowspan="6">40Ω</td><td rowspan="3">RON,40PD</td><td>0.2 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/6</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/6</td></tr><tr><td>0.8 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/6</td></tr><tr><td rowspan="3">RON,40PU</td><td>0.2 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.45</td><td>RZQ/6</td></tr><tr><td>0.5 × VDDQ</td><td>0.9</td><td>1.0</td><td>1.15</td><td>RZQ/6</td></tr><tr><td>0.8 × VDDQ</td><td>0.6</td><td>1.0</td><td>1.15</td><td>RZQ/6</td></tr><tr><td colspan="3">Pull-up/pull-down mismatch (MMPUPD)</td><td>VIL(AC) to VIH(AC)</td><td>-10</td><td>N/A</td><td>10</td><td>%</td></tr></table>


Notes: 1. Tolerance limits assume RZQ of $2 4 0 \Omega \pm 1 \%$ and are applicable after proper ZQ calibration has been performed at a stable temperature and voltage $( V _ { D D Q } = V _ { D D } ; V _ { S S Q } = V _ { S S } )$ . Refer to DDR3L 40 Ohm Output Driver Sensitivity (page 68) if either the temperature or the voltage changes after calibration. 



2. Measurement definition for mismatch between pull-up and pull-down $( M M _ { \mathsf { P U P D } } )$ . Measure both RON(PU) and ${ \mathsf { R } } _ { \mathsf { O N } ( { \mathsf { P D } } ) }$ at $0 . 5 \times \mathsf { V } _ { \mathsf { D D Q } }$ : 



$\mathsf { M M } _ { \mathsf { P U P D } } = \frac { \mathsf { R } _ { \mathsf { O N ( P U ) } } - \mathsf { R } _ { \mathsf { O N ( P D ) } } } { \mathsf { R } _ { \mathsf { O N , n o m } } } \times 1 0 0 $ × 100RON(PU) - RON(PD) RON,nom 



3. For IT and AT (1Gb only) devices, the minimum values are derated by $6 \%$ when the device operates between $\ - 4 0 ^ { \circ } \mathsf { C }$ and $0 \%$ (TC). 



A larger maximum limit will result in slightly lower minimum currents. 


# DDR3L 40 Ohm Output Driver Sensitivity

If either the temperature or the voltage changes after I/O calibration, then the tolerance limits listed in Table 45 can be expected to widen according to Table 46 and Table 47 (page 69). 


Table 46: DDR3L 40 Ohm Output Driver Sensitivity Definition


<table><tr><td>Symbol</td><td>Min</td><td>Max</td><td>Unit</td></tr><tr><td>RON(PD) @ 0.2 × VDDQ</td><td>0.6 - dRONdTL × |ΔT| - dRONdVL × |ΔV|</td><td>1.1 + dRONdTL × |ΔT| + dRONdVL × |ΔV|</td><td>RZQ/6</td></tr><tr><td>RON(PD) @ 0.5 × VDDQ</td><td>0.9 - dRONdTM × |ΔT| - dRONdVM × |ΔV|</td><td>1.1 + dRONdTM × |ΔT| + dRONdVM × |ΔV|</td><td>RZQ/6</td></tr><tr><td>RON(PD) @ 0.8 × VDDQ</td><td>0.9 - dRONdTH × |ΔT| - dRONdVH × |ΔV|</td><td>1.4 + dRONdTH × |ΔT| + dRONdVH × |ΔV|</td><td>RZQ/6</td></tr><tr><td>RON(PU) @ 0.2 × VDDQ</td><td>0.9 - dRONdTL × |ΔT| - dRONdVL × |ΔV|</td><td>1.4 + dRONdTL × |ΔT| + dRONdVL × |ΔV|</td><td>RZQ/6</td></tr><tr><td>RON(PU) @ 0.5 × VDDQ</td><td>0.9 - dRONdTM × |ΔT| - dRONdVM × |ΔV|</td><td>1.1 + dRONdTM × |ΔT| + dRONdVM × |ΔV|</td><td>RZQ/6</td></tr><tr><td>RON(PU) @ 0.8 × VDDQ</td><td>0.6 - dRONdTH × |ΔT| - dRONdVH × |ΔV|</td><td>1.1 + dRONdTH × |ΔT| + dRONdVH × |ΔV|</td><td>RZQ/6</td></tr></table>


Note: 1. $\Delta T = T$ - T(@CALIBRATION)ΔV = VDDQ - VDDQ(@CALIBRATION); and $V _ { D D } = V _ { D D Q }$ . 



Table 47: 40 Ohm Output Driver Voltage and Temperature Sensitivity


<table><tr><td>Change</td><td>Min</td><td>Max</td><td>Unit</td></tr><tr><td>dRONdTM</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVM</td><td>0</td><td>0.15</td><td>%/mV</td></tr><tr><td>dRONdTL</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVL</td><td>0</td><td>0.15</td><td>%/mV</td></tr><tr><td>dRONdTH</td><td>0</td><td>1.5</td><td>%/°C</td></tr><tr><td>dRONdVH</td><td>0</td><td>0.15</td><td>%/mV</td></tr></table>

# Output Characteristics and Operating Conditions


Table 48: DDR3L Single-Ended Output Driver Characteristics



All voltages are referenced to $\mathsf { V } _ { \mathsf { S } \mathsf { S } }$


<table><tr><td>Parameter/Condition</td><td>Symbol</td><td>Min</td><td>Max</td><td>Unit</td><td>Notes</td></tr><tr><td>Output leakage current: DQ are disabled; 0V ≤ VOUT ≤ VDDQ; ODT is disabled; ODT is HIGH</td><td>IOZ</td><td>-5</td><td>5</td><td>μA</td><td>1</td></tr><tr><td>Output slew rate: Single-ended; For rising and falling edges, measure between VOL(AC) = VREF - 0.09 × VDDQ and VOH(AC) = VREF + 0.09 × VDDQ</td><td>SRQse</td><td>1.75</td><td>6</td><td>V/ns</td><td>1, 2, 3, 4</td></tr><tr><td>Single-ended DC high-level output voltage</td><td>VOH(DC)</td><td colspan="2">0.8 × VDDQ</td><td>V</td><td>1, 2, 5</td></tr><tr><td>Single-ended DC mid-point level output voltage</td><td>VOM(DC)</td><td colspan="2">0.5 × VDDQ</td><td>V</td><td>1, 2, 5</td></tr><tr><td>Single-ended DC low-level output voltage</td><td>VOL(DC)</td><td colspan="2">0.2 × VDDQ</td><td>V</td><td>1, 2, 5</td></tr><tr><td>Single-ended AC high-level output voltage</td><td>VOH(AC)</td><td colspan="2">VTT + 0.1 × VDDQ</td><td>V</td><td>1, 2, 3, 6</td></tr><tr><td>Single-ended AC low-level output voltage</td><td>VOL(AC)</td><td colspan="2">VTT - 0.1 × VDDQ</td><td>V</td><td>1, 2, 3, 6</td></tr><tr><td>Delta RON between pull-up and pull-down for DQ/DQS</td><td>MMPUPD</td><td>-10</td><td>10</td><td>%</td><td>1, 7</td></tr><tr><td>Test load for AC timing and output slew rates</td><td colspan="4">Output to VTT (VDDQ/2) via 25Ω resistor</td><td>3</td></tr></table>


Notes: 1. RZQ of $2 4 0 \Omega \pm 1 \%$ with RZQ/7 enabled (default 34Ω driver) and is applicable after proper ZQ calibration has been performed at a stable temperature and voltage $( V _ { D D Q } = V _ { D D } ;$ $V _ { S S Q } = V _ { S S } )$ . 



2. $V _ { T T } = V _ { D D Q } / 2$ 



3. See Figure 31 (page 73) for the test load configuration. 



4. The 6 V/ns maximum is applicable for a single DQ signal when it is switching either from HIGH to LOW or LOW to HIGH while the remaining DQ signals in the same byte lane are either all static or all switching in the opposite direction. For all other DQ signal switching combinations, the maximum limit of 6 V/ns is reduced to 5 V/ns. 



5. See Figure 28 (page 64) for IV curve linearity. Do not use AC test load. 



6. See Slew Rate Definitions for Single-Ended Output Signals (page 73) for output slew rate. 



7. See Figure 28 (page 64) for additional information. 



8. See Figure 29 (page 71) for an example of a single-ended output signal. 



Figure 29: DQ Output Signal


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/9e0c1e8bac59d147892f6118ab291834ff4f27fff848cc08a096072139aa2bfc.jpg)



Table 49: DDR3L Differential Output Driver Characteristics



All voltages are referenced to $\mathsf { V } _ { \mathsf { S } \mathsf { S } }$


<table><tr><td>Parameter/Condition</td><td>Symbol</td><td>Min</td><td>Max</td><td>Unit</td><td>Notes</td></tr><tr><td>Output leakage current: DQ are disabled; 0V ≤ VOUT ≤ VDDQ; ODT is disabled; ODT is HIGH</td><td>IOZ</td><td>-5</td><td>5</td><td>μA</td><td>1</td></tr><tr><td>DDR3L Output slew rate: Differential; For rising and fall-ing edges, measure between VOL,diff(AC) = -0.18 × VDDQ and VOH,diff(AC) = 0.18 × VDDQ</td><td>SRQdiff</td><td>3.5</td><td>12</td><td>V/ns</td><td>1</td></tr><tr><td>Differential high-level output voltage</td><td>VOH,diff(AC)</td><td colspan="2">+0.2 × VDDQ</td><td>V</td><td>1,4</td></tr><tr><td>Differential low-level output voltage</td><td>VOL,diff(AC)</td><td colspan="2">-0.2 × VDDQ</td><td>V</td><td>1,4</td></tr><tr><td>Delta Ron between pull-up and pull-down for DQ/DQS</td><td>MMPUPD</td><td>-10</td><td>10</td><td>%</td><td>1,5</td></tr><tr><td>Test load for AC timing and output slew rates</td><td colspan="4">Output to VTT(VDDQ/2) via 25Ω resistor</td><td>3</td></tr></table>

Notes: 1. RZQ of $2 4 0 \Omega \pm 1 \%$ with RZQ/7 enabled (default 34Ω driver) and is applicable after proper ZQ calibration has been performed at a stable temperature and voltage $( V _ { D D Q } = V _ { D D } ;$ $V _ { S S Q } = V _ { S S } )$ . 

2. $V _ { R E F } = V _ { D D Q } / 2 ;$ slew rate $ @ ~ 5 ~ \mathsf { V } / \mathsf { n s } ,$ interpolate for faster slew rate. 

3. See Figure 31 (page 73) for the test load configuration. 

4. See Table 52 (page 75) for the output slew rate. 

5. See Table 38 (page 65) for additional information. 

6. See Figure 30 (page 72) for an example of a differential output signal. 


Table 50: DDR3L Differential Output Driver Characteristics VOX(AC)



All voltages are referenced to $\mathsf { V } _ { \mathsf { S } \mathsf { S } }$


<table><tr><td rowspan="2">Parameter/Condition</td><td rowspan="2" colspan="2">Symbol</td><td colspan="9">DDR3L- 800/1066/1333 DQS/DQS# Differential Slew Rate</td><td rowspan="2">Unit</td></tr><tr><td>3.5V/ns</td><td>4V/ns</td><td>5V/ns</td><td>6V/ns</td><td>7V/ns</td><td>8V/ns</td><td>9V/ns</td><td>10V/ns</td><td>12V/ns</td></tr><tr><td rowspan="2">Output differential crosspoint voltage</td><td rowspan="2">\( V_{OX(AC)} \)</td><td>Max</td><td>115</td><td>130</td><td>135</td><td>195</td><td>205</td><td>205</td><td>205</td><td>205</td><td>205</td><td>mV</td></tr><tr><td>Min</td><td>-115</td><td>-130</td><td>-135</td><td>-195</td><td>-205</td><td>-205</td><td>-205</td><td>-205</td><td>-205</td><td>mV</td></tr><tr><td rowspan="2">Parameter/Condition</td><td rowspan="2" colspan="2">Symbol</td><td colspan="9">DDR3L-1600/1866/2133 DQS/DQS# Differential Slew Rate</td><td rowspan="2">Unit</td></tr><tr><td>3.5V/ns</td><td>4V/ns</td><td>5v/ns</td><td>6V/ns</td><td>7V/ns</td><td>8V/ns</td><td>9V/ns</td><td>10V/ns</td><td>12V/ns</td></tr><tr><td rowspan="2">Output differential crosspoint voltage</td><td rowspan="2">\( V_{OX(AC)} \)</td><td>Max</td><td>90</td><td>105</td><td>135</td><td>155</td><td>180</td><td>205</td><td>205</td><td>205</td><td>205</td><td>mV</td></tr><tr><td>Min</td><td>-90</td><td>-105</td><td>-135</td><td>-155</td><td>-180</td><td>-205</td><td>-205</td><td>-205</td><td>-205</td><td>mV</td></tr></table>

Notes: 1. RZQ of $2 4 0 \Omega \pm 1 \%$ with RZQ/7 enabled (default 34Ω driver) and is applicable after proper ZQ calibration has been performed at a stable temperature and voltage $( V _ { D D Q } = V _ { D D } ;$ $V _ { S S Q } = V _ { S S } )$ . 

2. See Figure 31 (page 73) for the test load configuration. 

3. See Figure 30 (page 72) for an example of a differential output signal. 

4. For a differential slew rate between the list values, the $\mathsf { V } _ { \mathsf { O X } ( \mathsf { A C } ) }$ value may be obtained by linear interpolation. 


Figure 30: Differential Output Signal


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/575f93ea60670c7d7e99084494cfec388d649e63e48162a52f13b5f40c0c5ef3.jpg)


# Reference Output Load

Figure 31 (page 73) represents the effective reference load of 25Ω used in defining the relevant device AC timing parameters (except ODT reference timing) as well as the output slew rate measurements. It is not intended to be a precise representation of a particular system environment or a depiction of the actual load presented by a production tester. System designers should use IBIS or other simulation tools to correlate the timing reference load to a system environment. 


Figure 31: Reference Output Load for AC Timing and Output Slew Rate


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/6715b443b2b1036f9cc9e20f7b97ed03e0930998c7e014972b22205e7b890834.jpg)


# Slew Rate Definitions for Single-Ended Output Signals

The single-ended output driver is summarized in Table 48 (page 70). With the reference load for timing measurements, the output slew rate for falling and rising edges is defined and measured between VOL(AC) and VOH(AC) for single-ended signals. 


Table 51: Single-Ended Output Slew Rate Definition


<table><tr><td colspan="2">Single-Ended Output Slew Rates (Linear Signals)</td><td colspan="2">Measured</td><td rowspan="2">Calculation</td></tr><tr><td>Output</td><td>Edge</td><td>From</td><td>To</td></tr><tr><td rowspan="2">DQ</td><td>Rising</td><td>VOL(AC)</td><td>VOH(AC)</td><td>VOH(AC) - VOL(AC)/ΔTRse</td></tr><tr><td>Falling</td><td>VOH(AC)</td><td>VOL(AC)</td><td>VOH(AC) - VOL(AC)/ΔTFse</td></tr></table>


Figure 32: Nominal Slew Rate Definition for Single-Ended Output Signals


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/87733f20c0e54ae0af3262bc39b12918dbe2670bf704fecb8a35aed9abc79464.jpg)


# Slew Rate Definitions for Differential Output Signals

The differential output driver is summarized in Table 49 (page 71). With the reference load for timing measurements, the output slew rate for falling and rising edges is defined and measured between VOL(AC) and VOH(AC) for differential signals. 


Table 52: Differential Output Slew Rate Definition


<table><tr><td colspan="2">Differential Output Slew Rates (Linear Signals)</td><td colspan="2">Measured</td><td rowspan="2">Calculation</td></tr><tr><td>Output</td><td>Edge</td><td>From</td><td>To</td></tr><tr><td rowspan="2">DQS, DQS#</td><td>Rising</td><td>VOL,diff(AC)</td><td>VOH,diff(AC)</td><td>VOH,diff(AC) - VOL,diff(AC) / ΔTRdiff</td></tr><tr><td>Falling</td><td>VOH,diff(AC)</td><td>VOL,diff(AC)</td><td>VOH,diff(AC) - VOL,diff(AC) / ΔTFdiff</td></tr></table>


Figure 33: Nominal Differential Output Slew Rate Definition for DQS, DQS#


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/381eff89f28f468c9fcfdb6fdc3f48a8f0bf3634cfe21cc3283cf35976899d04.jpg)


# Speed Bin Tables


Table 53: DDR3L-1066 Speed Bins


<table><tr><td colspan="3">DDR3L-1066 Speed Bin</td><td colspan="2">-187E</td><td colspan="2">-187</td><td rowspan="3">Unit</td><td rowspan="3">Notes</td></tr><tr><td colspan="3">CL-tRCD-tRP</td><td colspan="2">7-7-7</td><td colspan="2">8-8-8</td></tr><tr><td colspan="2">Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">Internal READ command to first data</td><td>tAA</td><td>13.125</td><td>-</td><td>15</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE to internal READ or WRITE delay time</td><td>tRCD</td><td>13.125</td><td>-</td><td>15</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">PRECHARGE command period</td><td>tRP</td><td>13.125</td><td>-</td><td>15</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-ACTIVATE or REFRESH command period</td><td>tRC</td><td>50.625</td><td>-</td><td>52.5</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-PRECHARGE command period</td><td>tRAS</td><td>37.5</td><td>9 x tREFI</td><td>37.5</td><td>9 x tREFI</td><td>ns</td><td>1</td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK (AVG)</td><td>3.0</td><td>3.3</td><td>3.0</td><td>3.3</td><td>ns</td><td>2</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>3</td></tr><tr><td rowspan="2">CL = 6</td><td>CWL = 5</td><td>tCK (AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>ns</td><td>2</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>3</td></tr><tr><td rowspan="2">CL = 7</td><td>CWL = 5</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>3</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td colspan="2">Reserved</td><td>ns</td><td>2, 3</td></tr><tr><td rowspan="2">CL = 8</td><td>CWL = 5</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>3</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>2</td></tr><tr><td colspan="3">Supported CL settings</td><td colspan="2">5, 6, 7, 8</td><td colspan="2">5, 6, 8</td><td>CK</td><td></td></tr><tr><td colspan="3">Supported CWL settings</td><td colspan="2">5, 6</td><td colspan="2">5, 6</td><td>CK</td><td></td></tr></table>


Notes: 1. t REFI depends on TOPER. 



2. The CL and CWL settings result in $\mathsf { t } _ { \mathsf { C K } }$ requirements. When making a selection of ${ } ^ { \mathrm { t } } { \mathsf { C K } } ,$ both CL and CWL requirement settings need to be fulfilled. 



3. Reserved settings are not allowed. 



Table 54: DDR3L-1333 Speed Bins


<table><tr><td colspan="3">DDR3L-1333 Speed Bin</td><td colspan="2">-15E1</td><td colspan="2">-152</td><td rowspan="3">Unit</td><td rowspan="3">Notes</td></tr><tr><td colspan="3">CL-tRCD-tRP</td><td colspan="2">9-9-9</td><td colspan="2">10-10-10</td></tr><tr><td colspan="2">Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">Internal READ command to first data</td><td>tAA</td><td>13.5</td><td>-</td><td>15</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE to internal READ or WRITE delay time</td><td>tRCD</td><td>13.5</td><td>-</td><td>15</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">PRECHARGE command period</td><td>tRP</td><td>13.5</td><td>-</td><td>15</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-ACTIVATE or REFRESH command period</td><td>tRC</td><td>49.5</td><td>-</td><td>51</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-PRECHARGE command period</td><td>tRAS</td><td>36</td><td>9 x tREFI</td><td>36</td><td>9 x tREFI</td><td>ns</td><td>3</td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK (AVG)</td><td>3.0</td><td>3.3</td><td>3.0</td><td>3.3</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6, 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td rowspan="3">CL = 6</td><td>CWL = 5</td><td>tCK (AVG)</td><td>2.5</td><td>3.3</td><td>2.5</td><td>3.3</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td rowspan="3">CL = 7</td><td>CWL = 5</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td colspan="2">Reserved</td><td>ns</td><td>4, 5</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td rowspan="3">CL = 8</td><td>CWL = 5</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td rowspan="2">CL = 9</td><td>CWL = 5, 6</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td>1.5</td><td>&lt;1.875</td><td colspan="2">Reserved</td><td>ns</td><td>4, 5</td></tr><tr><td rowspan="2">CL = 10</td><td>CWL = 5, 6</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td colspan="2">Reserved</td><td>ns</td><td>5</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td>1.5</td><td>&lt;1.875</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>4</td></tr><tr><td colspan="3">Supported CL settings</td><td colspan="2">5, 6, 7, 8, 9, 10</td><td colspan="2">5, 6, 8, 10</td><td>CK</td><td></td></tr><tr><td colspan="3">Supported CWL settings</td><td colspan="2">5, 6, 7</td><td colspan="2">5, 6, 7</td><td>CK</td><td></td></tr></table>


Notes: 1. The -15E speed grade is backward compatible with 1066, $\mathrm { { C L } } = 7$ (-187E). 



2. The -15 speed grade is backward compatible with 1066, $\mathtt { C L } = 8$ (-187). 



3. t REFI depends on TOPER. 



4. The CL and CWL settings result in $^ \mathrm { t } \mathsf { C K }$ requirements. When making a selection of $^ \mathrm { t } \mathsf { C K } ,$ both CL and CWL requirement settings need to be fulfilled. 



5. Reserved settings are not allowed. 



Table 55: DDR3L-1600 Speed Bins


<table><tr><td colspan="3">DDR3L-1600 Speed Bin</td><td colspan="2">-1251</td><td rowspan="3">Unit</td><td rowspan="3">Notes</td></tr><tr><td colspan="3">CL-tRCD-tRP</td><td colspan="2">11-11-11</td></tr><tr><td colspan="2">Parameter</td><td>Symbol</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">Internal READ command to first data</td><td>tAA</td><td>13.75</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE to internal READ or WRITE delay time</td><td>tRCD</td><td>13.75</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">PRECHARGE command period</td><td>tRP</td><td>13.75</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-ACTIVATE or REFRESH command period</td><td>tRC</td><td>48.75</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-PRECHARGE command period</td><td>tRAS</td><td>35</td><td>9 x tREFI</td><td>ns</td><td>2</td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK (AVG)</td><td>3.0</td><td>3.3</td><td>ns</td><td>3</td></tr><tr><td>CWL = 6, 7, 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="3">CL = 6</td><td>CWL = 5</td><td>tCK (AVG)</td><td>2.5</td><td>3.3</td><td>ns</td><td>3</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7, 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="4">CL = 7</td><td>CWL = 5</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>3</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="4">CL = 8</td><td>CWL = 5</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>3</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td rowspan="3">CL = 9</td><td>CWL = 5, 6</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>3</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="3">CL = 10</td><td>CWL = 5, 6</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>3</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 11</td><td>CWL = 5, 6, 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td>1.25</td><td>&lt;1.5</td><td>ns</td><td>3</td></tr><tr><td colspan="3">Supported CL settings</td><td colspan="2">5, 6, 7, 8, 9, 10, 11</td><td>CK</td><td></td></tr><tr><td colspan="3">Supported CWL settings</td><td colspan="2">5, 6, 7, 8</td><td>CK</td><td></td></tr></table>


Notes: 1. The -125 speed grade is backward compatible with 1333, $\mathbf { C L } = 9$ (-15E) and 1066, $\mathrm { { C L } } = 7$ (-187E). 



2. t REFI depends on TOPER. 



3. The CL and CWL settings result in $\mathsf { t } _ { \mathsf { C K } }$ requirements. When making a selection of ${ } ^ { \mathrm { t } } { \mathsf { C K } } ,$ , both CL and CWL requirement settings need to be fulfilled. 



4. Reserved settings are not allowed. 



Table 56: DDR3L-1866 Speed Bins


<table><tr><td colspan="3">DDR3L-1866 Speed Bin</td><td colspan="2">-1071</td><td rowspan="3">Unit</td><td rowspan="3">Notes</td></tr><tr><td colspan="3">CL-tRCD-tRP</td><td colspan="2">13-13-13</td></tr><tr><td colspan="2">Parameter</td><td>Symbol</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">Internal READ command to first data</td><td>tAA</td><td>13.91</td><td>20</td><td></td><td></td></tr><tr><td colspan="2">ACTIVATE to internal READ or WRITE delay time</td><td>tRCD</td><td>13.91</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">PRECHARGE command period</td><td>tRP</td><td>13.91</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-ACTIVATE or REFRESH command period</td><td>tRC</td><td>47.91</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-PRECHARGE command period</td><td>tRAS</td><td>34</td><td>9 x tREFI</td><td>ns</td><td>2</td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK (AVG)</td><td>3.0</td><td>3.3</td><td>ns</td><td>3</td></tr><tr><td>CWL = 6, 7, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 6</td><td>CWL = 5</td><td>tCK (AVG)</td><td>2.5</td><td>3.3</td><td>ns</td><td>3</td></tr><tr><td>CWL = 6, 7, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 7</td><td>CWL = 5, 7, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>3</td></tr><tr><td rowspan="3">CL = 8</td><td>CWL = 5, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>3</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 9</td><td>CWL = 5, 6, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>3</td></tr><tr><td rowspan="3">CL = 10</td><td>CWL = 5, 6, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>3</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="3">CL = 11</td><td>CWL = 5, 6, 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td>1.25</td><td>&lt;1.5</td><td>ns</td><td>3</td></tr><tr><td>CWL = 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 12</td><td>CWL = 5, 6, 7, 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 13</td><td>CWL = 5, 6, 7, 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 9</td><td>tCK (AVG)</td><td>1.07</td><td>&lt;1.25</td><td>ns</td><td>3</td></tr><tr><td colspan="3">Supported CL settings</td><td colspan="2">5, 6, 7, 8, 9, 10, 11, 13</td><td>CK</td><td></td></tr><tr><td colspan="3">Supported CWL settings</td><td colspan="2">5, 6, 7, 8, 9</td><td>CK</td><td></td></tr></table>


Notes: 1. The -107 speed grade is backward compatible with 1600, CL = 11 (-125) , 1333, $\mathbf { C L } = 9$ (-15E) and 1066, $\mathrm { { C L } } = 7$ (-187E). 



2. t REFI depends on TOPER. 



3. The CL and CWL settings result in $\mathsf { t } _ { \mathsf { C K } }$ requirements. When making a selection of ${ } ^ { \mathrm { t } } { \mathsf { C K } } ,$ , both CL and CWL requirement settings need to be fulfilled. 



4. Reserved settings are not allowed. 



Table 57: DDR3L-2133 Speed Bins


<table><tr><td colspan="3">DDR3L-2133 Speed Bin</td><td colspan="2">-0931</td><td rowspan="3">Unit</td><td rowspan="3">Notes</td></tr><tr><td colspan="3">CL-tRCD-tRP</td><td colspan="2">14-14-14</td></tr><tr><td colspan="2">Parameter</td><td>Symbol</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">Internal READ command to first data</td><td>tAA</td><td>13.09</td><td>20</td><td></td><td></td></tr><tr><td colspan="2">ACTIVATE to internal READ or WRITE delay time</td><td>tRCD</td><td>13.09</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">PRECHARGE command period</td><td>tRP</td><td>13.09</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-ACTIVATE or REFRESH command period</td><td>tRC</td><td>46.09</td><td>-</td><td>ns</td><td></td></tr><tr><td colspan="2">ACTIVATE-to-PRECHARGE command period</td><td>tRAS</td><td>33</td><td>9 x tREFI</td><td>ns</td><td>2</td></tr><tr><td rowspan="2">CL = 5</td><td>CWL = 5</td><td>tCK (AVG)</td><td>3.0</td><td>3.3</td><td>ns</td><td>3</td></tr><tr><td>CWL = 6, 7, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 6</td><td>CWL = 5</td><td>tCK (AVG)</td><td>2.5</td><td>3.3</td><td>ns</td><td>3</td></tr><tr><td>CWL = 6, 7, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 7</td><td>CWL = 5, 7, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>3</td></tr><tr><td rowspan="3">CL = 8</td><td>CWL = 5, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 6</td><td>tCK (AVG)</td><td>1.875</td><td>&lt;2.5</td><td>ns</td><td>3</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 9</td><td>CWL = 5, 6, 8, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>3</td></tr><tr><td rowspan="3">CL = 10</td><td>CWL = 5, 6, 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 7</td><td>tCK (AVG)</td><td>1.5</td><td>&lt;1.875</td><td>ns</td><td>3</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="3">CL = 11</td><td>CWL = 5, 6, 7</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 8</td><td>tCK (AVG)</td><td>1.25</td><td>&lt;1.5</td><td>ns</td><td>3</td></tr><tr><td>CWL = 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 12</td><td>CWL = 5, 6, 7, 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 9</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td rowspan="2">CL = 13</td><td>CWL = 5, 6, 7, 8</td><td>tCK (AVG)</td><td colspan="2">Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 9</td><td>tCK (AVG)</td><td>1.07</td><td>&lt;1.25</td><td>ns</td><td>3</td></tr><tr><td rowspan="2">CL = 14</td><td>CWL = 5, 6, 7, 8, 9</td><td>tCK (AVG)</td><td>Reserved</td><td>Reserved</td><td>ns</td><td>4</td></tr><tr><td>CWL = 10</td><td>tCK (AVG)</td><td>0.938</td><td>&lt;1.07</td><td>ns</td><td>3</td></tr><tr><td colspan="3">Supported CL settings</td><td colspan="2">5, 6, 7, 8, 9, 10, 11, 13, 14</td><td>CK</td><td></td></tr><tr><td colspan="3">Supported CWL settings</td><td colspan="2">5, 6, 7, 8, 9</td><td>CK</td><td></td></tr></table>

Notes: 1. The -093 speed grade is backward compatible with 1866, CL = 13 (-107) , 1600, CL = 11 (-125) , 1333, $\mathbf { C L } = 9$ (-15E) and 1066, $\mathrm { { C L } } = 7$ (-187E). 

2. t REFI depends on TOPER. 

3. The CL and CWL settings result in $\mathsf { t } _ { \mathsf { C K } }$ requirements. When making a selection of ${ } ^ { \mathrm { t } } { \mathsf { C K } } ,$ both CL and CWL requirement settings need to be fulfilled. 

4. Reserved settings are not allowed. 

# E lectrica l Characteristics and AC Operati ng Cond itions


Table 58: E lectrica l Characteristics and AC Operati ng Cond itions



N otes 1 –8 a p p l y to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-800</td><td colspan="2">DDR3L-1066</td><td colspan="2">DDR3L-1333</td><td colspan="2">DDR3L-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="13">Clock Timing</td></tr><tr><td rowspan="2">Clock period average: DLL disable mode</td><td>\(T_{C}\) ≤ 85°C</td><td rowspan="2">\({}^{t}\text{CK}\) (DLL_DIS)</td><td>8</td><td>7800</td><td>8</td><td>7800</td><td>8</td><td>7800</td><td>8</td><td>7800</td><td>ns</td><td>9,42</td></tr><tr><td>\(T_{C}\)=&gt;85°C to 95°C</td><td>8</td><td>3900</td><td>8</td><td>3900</td><td>8</td><td>3900</td><td>8</td><td>3900</td><td>ns</td><td>42</td></tr><tr><td colspan="2">Clock period average: DLL enable mode</td><td>\({}^{t}\text{CK}\)(AVG)</td><td colspan="8">See Speed Bin Tables for \({}^{t}\text{CK}\) range allowed</td><td>ns</td><td>10,11</td></tr><tr><td colspan="2">High pulse width average</td><td>\({}^{t}\text{CH}\)(AVG)</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>CK</td><td>12</td></tr><tr><td colspan="2">Low pulse width average</td><td>\({}^{t}\text{CL}\)(AVG)</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>CK</td><td>12</td></tr><tr><td rowspan="2">Clock period jitter</td><td>DLL locked</td><td>\({}^{t}\text{JITper}\)</td><td>-100</td><td>100</td><td>-90</td><td>90</td><td>-80</td><td>80</td><td>-70</td><td>70</td><td>ps</td><td>13</td></tr><tr><td>DLL locking</td><td>\({}^{t}\text{JITper,lck}\)</td><td>-90</td><td>90</td><td>-80</td><td>80</td><td>-70</td><td>70</td><td>-60</td><td>60</td><td>ps</td><td>13</td></tr><tr><td colspan="2">Clock absolute period</td><td>\({}^{t}\text{CK}\)(ABS)</td><td colspan="8">MIN = \({}^{t}\text{CK}\)(AVG) MIN + \({}^{t}\text{JITper MIN; MAX = }^{t}\text{CK(AVG) MAX + }^{t}\text{JITper MAX}}\)</td><td>ps</td><td></td></tr><tr><td colspan="2">Clock absolute high pulse width</td><td>\({}^{t}\text{CH}\)(ABS)</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>\({}^{t}\text{CK}\)(AVG)</td><td>14</td></tr><tr><td colspan="2">Clock absolute low pulse width</td><td>\({}^{t}\text{CL}\)(ABS)</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>\({}^{t}\text{CK}\)(AVG)</td><td>15</td></tr><tr><td rowspan="2">Cycle-to-cycle jitter</td><td>DLL locked</td><td>\({}^{t}\text{JITcc}\)</td><td colspan="2">200</td><td colspan="2">180</td><td colspan="2">160</td><td colspan="2">140</td><td>ps</td><td>16</td></tr><tr><td>DLL locking</td><td>\({}^{t}\text{JITcc,lck}\)</td><td colspan="2">180</td><td colspan="2">160</td><td colspan="2">140</td><td colspan="2">120</td><td>ps</td><td>16</td></tr><tr><td rowspan="12">Cumulative error across</td><td>2 cycles</td><td>\({}^{t}\text{ERR2per}\)</td><td>-147</td><td>147</td><td>-132</td><td>132</td><td>-118</td><td>118</td><td>-103</td><td>103</td><td>ps</td><td>17</td></tr><tr><td>3 cycles</td><td>\({}^{t}\text{ERR3per}\)</td><td>-175</td><td>175</td><td>-157</td><td>157</td><td>-140</td><td>140</td><td>-122</td><td>122</td><td>ps</td><td>17</td></tr><tr><td>4 cycles</td><td>\({}^{t}\text{ERR4per}\)</td><td>-194</td><td>194</td><td>-175</td><td>175</td><td>-155</td><td>155</td><td>-136</td><td>136</td><td>ps</td><td>17</td></tr><tr><td>5 cycles</td><td>\({}^{t}\text{ERR5per}\)</td><td>-209</td><td>209</td><td>-188</td><td>188</td><td>-168</td><td>168</td><td>-147</td><td>147</td><td>ps</td><td>17</td></tr><tr><td>6 cycles</td><td>\({}^{t}\text{ERR6per}\)</td><td>-222</td><td>222</td><td>-200</td><td>200</td><td>-177</td><td>177</td><td>-155</td><td>155</td><td>ps</td><td>17</td></tr><tr><td>7 cycles</td><td>\({}^{t}\text{ERR7per}\)</td><td>-232</td><td>232</td><td>-209</td><td>209</td><td>-186</td><td>186</td><td>-163</td><td>163</td><td>ps</td><td>17</td></tr><tr><td>8 cycles</td><td>\({}^{t}\text{ERR8per}\)</td><td>-241</td><td>241</td><td>-217</td><td>217</td><td>-193</td><td>193</td><td>-169</td><td>169</td><td>ps</td><td>17</td></tr><tr><td>9 cycles</td><td>\({}^{t}\text{ERR9per}\)</td><td>-249</td><td>249</td><td>-224</td><td>224</td><td>-200</td><td>200</td><td>-175</td><td>175</td><td>ps</td><td>17</td></tr><tr><td>10 cycles</td><td>\({}^{t}\text{ERR10per}\)</td><td>-257</td><td>257</td><td>-231</td><td>231</td><td>-205</td><td>205</td><td>-180</td><td>180</td><td>ps</td><td>17</td></tr><tr><td>11 cycles</td><td>\({}^{t}\text{ERR11per}\)</td><td>-263</td><td>263</td><td>-237</td><td>237</td><td>-210</td><td>210</td><td>-184</td><td>184</td><td>ps</td><td>17</td></tr><tr><td>12 cycles</td><td>\({}^{t}\text{ERR12per}\)</td><td>-269</td><td>269</td><td>-242</td><td>242</td><td>-215</td><td>215</td><td>-188</td><td>188</td><td>ps</td><td>17</td></tr><tr><td>n=13, 14...49, 50 cycles</td><td>\({}^{t}\text{ERRnper}\)</td><td colspan="8">\({}^{t}\text{ERRnper MIN = (1 + 0.68In[n]) × }^{t}\text{JITper MIN}\)\({}^{t}\text{ERRnper MAX = (1 + 0.68In[n]) × }^{t}\text{JITper MAX}}\)</td><td>ps</td><td>17</td></tr></table>


Table 58: E lectrica l Characteristics and AC Operati ng Cond itions (Conti nued)



N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-800</td><td colspan="2">DDR3L-1066</td><td colspan="2">DDR3L-1333</td><td colspan="2">DDR3L-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="13">DQ Input Timing</td></tr><tr><td rowspan="2">Data setup time to DQS, DQS#</td><td>Base (specification)</td><td rowspan="2">tDS (AC160)</td><td>90</td><td>-</td><td>40</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>ps</td><td>18, 19, 44</td></tr><tr><td>VREF @ 1 V/ns</td><td>250</td><td>-</td><td>200</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>ps</td><td>19, 20</td></tr><tr><td rowspan="2">Data setup time to DQS, DQS#</td><td>Base (specification)</td><td rowspan="2">tDS (AC135)</td><td>140</td><td>-</td><td>90</td><td>-</td><td>45</td><td>-</td><td>25</td><td>-</td><td>ps</td><td>18, 19, 44</td></tr><tr><td>VREF @ 1 V/ns</td><td>275</td><td>-</td><td>250</td><td>-</td><td>180</td><td>-</td><td>160</td><td>-</td><td>ps</td><td>19, 20</td></tr><tr><td rowspan="2">Data hold time from DQS, DQS#</td><td>Base (specification)</td><td rowspan="2">tDH (DC90)</td><td>160</td><td>-</td><td>110</td><td>-</td><td>75</td><td>-</td><td>55</td><td>-</td><td>ps</td><td>18, 19</td></tr><tr><td>VREF @ 1 V/ns</td><td>250</td><td>-</td><td>200</td><td>-</td><td>165</td><td>-</td><td>145</td><td>-</td><td>ps</td><td>19, 20</td></tr><tr><td colspan="2">Minimum data pulse width</td><td>tDIPW</td><td>600</td><td>-</td><td>490</td><td>-</td><td>400</td><td>-</td><td>360</td><td>-</td><td>ps</td><td>41</td></tr><tr><td colspan="13">DQ Output Timing</td></tr><tr><td colspan="2">DQS, DQS# to DQ skew, per access</td><td>tDQSQ</td><td>-</td><td>200</td><td>-</td><td>150</td><td>-</td><td>125</td><td>-</td><td>100</td><td>ps</td><td></td></tr><tr><td colspan="2">DQ output hold time from DQS, DQS#</td><td>tQH</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>tCK (AVG)</td><td>21</td></tr><tr><td colspan="2">DQ Low-Z time from CK, CK#</td><td>tLZDQ</td><td>-800</td><td>400</td><td>-600</td><td>300</td><td>-500</td><td>250</td><td>-450</td><td>225</td><td>ps</td><td>22, 23</td></tr><tr><td colspan="2">DQ High-Z time from CK, CK#</td><td>tHZDQ</td><td>-</td><td>400</td><td>-</td><td>300</td><td>-</td><td>250</td><td>-</td><td>225</td><td>ps</td><td>22, 23</td></tr><tr><td colspan="13">DQ Strobe Input Timing</td></tr><tr><td colspan="2">DQS, DQS# rising to CK, CK# rising</td><td>tDQSS</td><td>-0.25</td><td>0.25</td><td>-0.25</td><td>0.25</td><td>-0.25</td><td>0.25</td><td>-0.27</td><td>0.27</td><td>CK</td><td>25</td></tr><tr><td colspan="2">DQS, DQS# differential input low pulse width</td><td>tDQSL</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>CK</td><td></td></tr><tr><td colspan="2">DQS, DQS# differential input high pulse width</td><td>tDQSH</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>CK</td><td></td></tr><tr><td colspan="2">DQS, DQS# falling setup to CK, CK# rising</td><td>tDSS</td><td>0.2</td><td>-</td><td>0.2</td><td>-</td><td>0.2</td><td>-</td><td>0.18</td><td>-</td><td>CK</td><td>25</td></tr><tr><td colspan="2">DQS, DQS# falling hold from CK, CK# rising</td><td>tDSH</td><td>0.2</td><td>-</td><td>0.2</td><td>-</td><td>0.2</td><td>-</td><td>0.18</td><td>-</td><td>CK</td><td>25</td></tr><tr><td colspan="2">DQS, DQS# differential WRITE preamble</td><td>tWPRE</td><td>0.9</td><td>-</td><td>0.9</td><td>-</td><td>0.9</td><td>-</td><td>0.9</td><td>-</td><td>CK</td><td></td></tr><tr><td colspan="2">DQS, DQS# differential WRITE postamble</td><td>tWPST</td><td>0.3</td><td>-</td><td>0.3</td><td>-</td><td>0.3</td><td>-</td><td>0.3</td><td>-</td><td>CK</td><td></td></tr><tr><td colspan="13">DQ Strobe Output Timing</td></tr><tr><td colspan="2">DQS, DQS# rising to/from rising CK, CK#</td><td>tDQsCK</td><td>-400</td><td>400</td><td>-300</td><td>300</td><td>-255</td><td>255</td><td>-225</td><td>225</td><td>ps</td><td>23</td></tr><tr><td colspan="2">DQS, DQS# rising to/from rising CK, CK# when DLL is disabled</td><td>tDQsCK (DLL_DIS)</td><td>1</td><td>10</td><td>1</td><td>10</td><td>1</td><td>10</td><td>1</td><td>10</td><td>ns</td><td>26</td></tr><tr><td colspan="2">DQS, DQS# differential output high time</td><td>tQSH</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>0.40</td><td>-</td><td>0.40</td><td>-</td><td>CK</td><td>21</td></tr><tr><td colspan="2">DQS, DQS# differential output low time</td><td>tQSL</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>0.40</td><td>-</td><td>0.40</td><td>-</td><td>CK</td><td>21</td></tr></table>

# Table 58: E lectrica l Characteristics and AC Operati ng Cond itions (Conti nued)


N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-800</td><td colspan="2">DDR3L-1066</td><td colspan="2">DDR3L-1333</td><td colspan="2">DDR3L-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">DQS, DQS# Low-Z time (RL - 1)</td><td>tLZDQS</td><td>-800</td><td>400</td><td>-600</td><td>300</td><td>-500</td><td>250</td><td>-450</td><td>225</td><td>ps</td><td>22, 23</td></tr><tr><td colspan="2">DQS, DQS# High-Z time (RL + BL/2)</td><td>tHZDQS</td><td>-</td><td>400</td><td>-</td><td>300</td><td>-</td><td>250</td><td>-</td><td>225</td><td>ps</td><td>22, 23</td></tr><tr><td colspan="2">DQS, DQS# differential READ preamble</td><td>tRPRE</td><td>0.9</td><td>Note 24</td><td>0.9</td><td>Note 24</td><td>0.9</td><td>Note 24</td><td>0.9</td><td>Note 24</td><td>CK</td><td>23, 24</td></tr><tr><td colspan="2">DQS, DQS# differential READ postamble</td><td>tRPST</td><td>0.3</td><td>Note 27</td><td>0.3</td><td>Note 27</td><td>0.3</td><td>Note 27</td><td>0.3</td><td>Note 27</td><td>CK</td><td>23, 27</td></tr><tr><td colspan="13">Command and Address Timing</td></tr><tr><td colspan="2">DLL locking time</td><td>tDLLK</td><td>512</td><td>-</td><td>512</td><td>-</td><td>512</td><td>-</td><td>512</td><td>-</td><td>CK</td><td>28</td></tr><tr><td rowspan="2">CTRL, CMD, ADDR setup to CK,CK#</td><td>Base (specification)</td><td rowspan="2">tIS(AC160)</td><td>215</td><td>-</td><td>140</td><td>-</td><td>80</td><td>-</td><td>60</td><td>-</td><td>ps</td><td>29, 30, 44</td></tr><tr><td>VREF@ 1 V/ns</td><td>375</td><td>-</td><td>300</td><td>-</td><td>240</td><td>-</td><td>220</td><td>-</td><td>ps</td><td>20, 30</td></tr><tr><td rowspan="2">CTRL, CMD, ADDR setup to CK,CK#</td><td>Base (specification)</td><td rowspan="2">tIS(AC135)</td><td>365</td><td>-</td><td>290</td><td>-</td><td>205</td><td>-</td><td>185</td><td>-</td><td>ps</td><td>29, 30, 44</td></tr><tr><td>VREF@ 1 V/ns</td><td>500</td><td>-</td><td>425</td><td>-</td><td>340</td><td>-</td><td>320</td><td>-</td><td>ps</td><td>20, 30</td></tr><tr><td rowspan="2">CTRL, CMD, ADDR setup to CK,CK#</td><td>Base (specification)</td><td rowspan="2">tIH(DC90)</td><td>285</td><td>-</td><td>210</td><td>-</td><td>150</td><td>-</td><td>130</td><td>-</td><td>ps</td><td>29, 30, 44</td></tr><tr><td>VREF@ 1 V/ns</td><td>375</td><td>-</td><td>300</td><td>-</td><td>240</td><td>-</td><td>220</td><td>-</td><td>ps</td><td>20, 30</td></tr><tr><td colspan="2">Minimum CTRL, CMD, ADDR pulse width</td><td>tIPW</td><td>900</td><td>-</td><td>780</td><td>-</td><td>620</td><td>-</td><td>560</td><td>-</td><td>ps</td><td>41</td></tr><tr><td colspan="2">ACTIVATE to internal READ or WRITE delay</td><td>tRCD</td><td colspan="8">See Speed Bin Tables for tRCD</td><td>ns</td><td>31</td></tr><tr><td colspan="2">PRECHARGE command period</td><td>tRP</td><td colspan="8">See Speed Bin Tables for tRP</td><td>ns</td><td>31</td></tr><tr><td colspan="2">ACTIVATE-to-PRECHARGE command period</td><td>tRAS</td><td colspan="8">See Speed Bin Tables for tRAS</td><td>ns</td><td>31, 32</td></tr><tr><td colspan="2">ACTIVATE-to-ACTIVATE command period</td><td>tRC</td><td colspan="8">See Speed Bin Tables for tRC</td><td>ns</td><td>31, 43</td></tr><tr><td rowspan="2">ACTIVATE-to-ACTIVATE minimum command period</td><td>x4/x8 (1KB page size)</td><td rowspan="2">tRRD</td><td>MIN = greater of 4CK or 10ns</td><td colspan="2">MIN = greater of 4CK or 7.5ns</td><td colspan="2">MIN = greater of 4CK or 6ns</td><td colspan="3">MIN = greater of 4CK or 6ns</td><td>CK</td><td>31</td></tr><tr><td>x16 (2KB page size)</td><td colspan="3">MIN = greater of 4CK or 10ns</td><td colspan="5">MIN = greater of 4CK or 7.5ns</td><td>CK</td><td>31</td></tr><tr><td rowspan="2">Four ACTIVATE windows</td><td>x4/x8 (1KB page size)</td><td rowspan="2">tFAW</td><td>40</td><td>-</td><td>37.5</td><td>-</td><td>30</td><td>-</td><td>30</td><td>-</td><td>ns</td><td>31</td></tr><tr><td>x16 (2KB page size)</td><td>50</td><td>-</td><td>50</td><td>-</td><td>45</td><td>-</td><td>40</td><td>-</td><td>ns</td><td>31</td></tr><tr><td colspan="2">Write recovery time</td><td>tWR</td><td colspan="8">MIN = 15ns; MAX = N/A</td><td>ns</td><td>31, 32, 33,34</td></tr><tr><td colspan="2">Delay from start of internal WRITE transaction to internal READ command</td><td>tWTR</td><td colspan="8">MIN = greater of 4CK or 7.5ns; MAX = N/A</td><td>CK</td><td>31, 34</td></tr><tr><td colspan="2">READ-to-PRECHARGE time</td><td>tRTP</td><td colspan="8">MIN = greater of 4CK or 7.5ns; MAX = N/A</td><td>CK</td><td>31, 32</td></tr></table>

# Table 58: E lectrica l Characteristics and AC Operati ng Cond itions (Conti nued)


N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-800</td><td colspan="2">DDR3L-1066</td><td colspan="2">DDR3L-1333</td><td colspan="2">DDR3L-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">CAS#-to-CAS# command delay</td><td>tCCD</td><td colspan="8">MIN = 4CK; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Auto precharge write recovery + precharge time</td><td>tDAL</td><td colspan="8">MIN = WR + tRP/tCK (AVG); MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">MODE REGISTER SET command cycle time</td><td>tMRD</td><td colspan="8">MIN = 4CK; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">MODE REGISTER SET command update delay</td><td>tMOD</td><td colspan="8">MIN = greater of 12CK or 15ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">MULTIPURPOSE REGISTER READ burst end to mode register set for multipurpose register exit</td><td>tMPRR</td><td colspan="8">MIN = 1CK; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="13">Calibration Timing</td></tr><tr><td rowspan="2">ZQCL command: Long calibration time</td><td>POWER-UP and RE-SET operation</td><td>tZQinit</td><td>512</td><td>-</td><td>512</td><td>-</td><td>512</td><td>-</td><td>512</td><td>-</td><td>CK</td><td></td></tr><tr><td>Normal operation</td><td>tZQoper</td><td>256</td><td>-</td><td>256</td><td>-</td><td>256</td><td>-</td><td>256</td><td>-</td><td>CK</td><td></td></tr><tr><td colspan="2">ZQCS command: Short calibration time</td><td>tZQCS</td><td>64</td><td>-</td><td>64</td><td>-</td><td>64</td><td>-</td><td>64</td><td>-</td><td>CK</td><td></td></tr><tr><td colspan="13">Initialization and Reset Timing</td></tr><tr><td colspan="2">Exit reset from CKE HIGH to a valid command</td><td>tXPR</td><td colspan="8">MIN = greater of 5CK or tRFC + 10ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Begin power supply ramp to power supplies stable</td><td>tVDDPR</td><td colspan="8">MIN = N/A; MAX = 200</td><td>ms</td><td></td></tr><tr><td colspan="2">RESET# LOW to power supplies stable</td><td>tRPS</td><td colspan="8">MIN = 0; MAX = 200</td><td>ms</td><td></td></tr><tr><td colspan="2">RESET# LOW to I/O and RTT High-Z</td><td>tIOZ</td><td colspan="8">MIN = N/A; MAX = 20</td><td>ns</td><td>35</td></tr><tr><td colspan="13">Refresh Timing</td></tr><tr><td rowspan="4" colspan="2">REFRESH-to-ACTIVATE or REFRESH command period</td><td>tRFC - 1Gb</td><td colspan="8">MIN = 110; MAX = 70,200</td><td>ns</td><td></td></tr><tr><td>tRFC - 2Gb</td><td colspan="8">MIN = 160; MAX = 70,200</td><td>ns</td><td></td></tr><tr><td>tRFC - 4Gb</td><td colspan="8">MIN = 260; MAX = 70,200</td><td>ns</td><td></td></tr><tr><td>tRFC - 8Gb</td><td colspan="8">MIN = 350; MAX = 70,200</td><td>ns</td><td></td></tr><tr><td rowspan="2">Maximum refresh period</td><td>TC≤85°C</td><td rowspan="2">-</td><td colspan="8">64 (1X)</td><td>ms</td><td>36</td></tr><tr><td>TC&gt;85°C</td><td colspan="8">32 (2X)</td><td>ms</td><td>36</td></tr><tr><td rowspan="2">Maximum average periodic refresh</td><td>TC≤85°C</td><td rowspan="2">tREFI</td><td colspan="8">7.8 (64ms/8192)</td><td>μs</td><td>36</td></tr><tr><td>TC&gt;85°C</td><td colspan="8">3.9 (32ms/8192)</td><td>μs</td><td>36</td></tr><tr><td colspan="13">Self Refresh Timing</td></tr><tr><td colspan="2">Exit self refresh to commands not requiring a locked DLL</td><td>tXS</td><td colspan="8">MIN = greater of 5CK or tRFC + 10ns; MAX = N/A</td><td>CK</td><td></td></tr></table>

# Table 58: E lectrica l Characteristics and AC Operati ng Cond itions (Conti nued)


N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-800</td><td colspan="2">DDR3L-1066</td><td colspan="2">DDR3L-1333</td><td colspan="2">DDR3L-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">Exit self refresh to commands requiring a locked DLL</td><td>tXSDLL</td><td colspan="8">MIN = tDLLK (MIN); MAX = N/A</td><td>CK</td><td>28</td></tr><tr><td colspan="2">Minimum CKE low pulse width for self refresh entry to self refresh exit timing</td><td>tCKESR</td><td colspan="8">MIN = tCKE (MIN) + CK; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Valid clocks after self refresh entry or power-down entry</td><td>tCKSRE</td><td colspan="8">MIN = greater of 5CK or 10ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Valid clocks before self refresh exit, power-down exit, or reset exit</td><td>tCKSRX</td><td colspan="8">MIN = greater of 5CK or 10ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="13">Power-Down Timing</td></tr><tr><td colspan="2">CKE MIN pulse width</td><td>tCKE (MIN)</td><td colspan="2">Greater of 3CK or 7.5ns</td><td colspan="2">Greater of 3CK or 5.625ns</td><td colspan="2">Greater of 3CK or 5.625ns</td><td colspan="2">Greater of 3CK or 5ns</td><td>CK</td><td></td></tr><tr><td colspan="2">Command pass disable delay</td><td>tCPDED</td><td colspan="8">MIN = 1; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Power-down entry to power-down exit timing</td><td>tPD</td><td colspan="8">MIN = tCKE (MIN); MAX = 9 * tREFI</td><td>CK</td><td></td></tr><tr><td colspan="2">Begin power-down period prior to CKE registered HIGH</td><td>tANPD</td><td colspan="8">WL - 1CK</td><td>CK</td><td></td></tr><tr><td colspan="2">Power-down entry period: ODT either synchronous or asynchronous</td><td>PDE</td><td colspan="8">Greater of tANPD or tRFC - REFRESH command to CKE LOW time</td><td>CK</td><td></td></tr><tr><td colspan="2">Power-down exit period: ODT either synchronous or asynchronous</td><td>PDX</td><td colspan="8">tANPD + tXPDLL</td><td>CK</td><td></td></tr><tr><td colspan="13">Power-Down Entry Minimum Timing</td></tr><tr><td colspan="2">ACTIVATE command to power-down entry</td><td>tACTPDEN</td><td colspan="8">MIN = 1</td><td>CK</td><td></td></tr><tr><td colspan="2">PRECHARGE/PRECHARGE ALL command to power-down entry</td><td>tPRPDEN</td><td colspan="8">MIN = 1</td><td>CK</td><td></td></tr><tr><td colspan="2">REFRESH command to power-down entry</td><td>tREFPDEN</td><td colspan="8">MIN = 1</td><td>CK</td><td>37</td></tr><tr><td colspan="2">MRS command to power-down entry</td><td>tMRSPDEN</td><td colspan="8">MIN = tMOD (MIN)</td><td>CK</td><td></td></tr><tr><td colspan="2">READ/READ with auto precharge command to power-down entry</td><td>tRDPDEN</td><td colspan="8">MIN = RL + 4 + 1</td><td>CK</td><td></td></tr><tr><td rowspan="3">WRITE command to power-down entry</td><td>BL8 (OTF, MRS)</td><td rowspan="2">tWRPDEN</td><td rowspan="2" colspan="8">MIN = WL + 4 + tWR/tCK (AVG)</td><td rowspan="2">CK</td><td></td></tr><tr><td>BC4OTF</td><td></td></tr><tr><td>BC4MRS</td><td>tWRPDEN</td><td colspan="8">MIN = WL + 2 + tWR/tCK (AVG)</td><td>CK</td><td></td></tr></table>

# Table 58: E lectrica l Characteristics and AC Operati ng Cond itions (Conti nued)


N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-800</td><td colspan="2">DDR3L-1066</td><td colspan="2">DDR3L-1333</td><td colspan="2">DDR3L-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td rowspan="2">WRITE with auto precharge command to power-down entry</td><td>BL8 (OTF, MRS) BC4OTF</td><td>tWRAP-DEN</td><td colspan="8">MIN = WL + 4 + WR + 1</td><td>CK</td><td></td></tr><tr><td>BC4MRS</td><td>tWRAP-DEN</td><td colspan="8">MIN = WL + 2 + WR + 1</td><td>CK</td><td></td></tr><tr><td colspan="13">Power-Down Exit Timing</td></tr><tr><td>DLL on, any valid command, or DLL off to commands not requiring locked DLL</td><td>tXP</td><td colspan="5">MIN = greater of 3CK or 7.5ns; MAX = N/A</td><td colspan="4">MIN = greater of 3CK or 6ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td>Precharge power-down with DLL off to commands requiring a locked DLL</td><td>tXPDLL</td><td colspan="9">MIN = greater of 10CK or 24ns; MAX = N/A</td><td>CK</td><td>28</td></tr><tr><td colspan="13">ODT Timing</td></tr><tr><td>RTT synchronous turn-on delay</td><td>ODTLon</td><td colspan="9">CWL + AL - 2CK</td><td>CK</td><td>38</td></tr><tr><td>RTT synchronous turn-off delay</td><td>ODTLoff</td><td colspan="9">CWL + AL - 2CK</td><td>CK</td><td>40</td></tr><tr><td>RTT turn-on from ODTL on reference</td><td>tAON</td><td>-400</td><td>400</td><td>-300</td><td>300</td><td>-250</td><td>250</td><td>-225</td><td>225</td><td>ps</td><td>23, 38</td><td></td></tr><tr><td>RTT turn-off from ODTL off reference</td><td>tAOF</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>CK</td><td>39, 40</td><td></td></tr><tr><td>Asynchronous RTT turn-on delay (power-down with DLL off)</td><td>tAONPD</td><td colspan="9">MIN = 2; MAX = 8.5</td><td>ns</td><td>38</td></tr><tr><td>Asynchronous RTT turn-off delay (power-down with DLL off)</td><td>tAOFPD</td><td colspan="9">MIN = 2; MAX = 8.5</td><td>ns</td><td>40</td></tr><tr><td>ODT HIGH time with WRITE command and BL8</td><td>ODTH8</td><td colspan="9">MIN = 6; MAX = N/A</td><td>CK</td><td></td></tr><tr><td>ODT HIGH time without WRITE command or with WRITE command and BC4</td><td>ODTH4</td><td colspan="9">MIN = 4; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="13">Dynamic ODT Timing</td></tr><tr><td>RTT,nom-to-RTT(WR) change skew</td><td>ODTLcnw</td><td colspan="9">WL - 2CK</td><td>CK</td><td></td></tr><tr><td>RTT(WR)-to-RTT,nom change skew - BC4</td><td>ODTLcwn4</td><td colspan="9">4CK + ODTLoff</td><td>CK</td><td></td></tr><tr><td>RTT(WR)-to-RTT,nom change skew - BL8</td><td>ODTLcwn8</td><td colspan="9">6CK + ODTLoff</td><td>CK</td><td></td></tr><tr><td>RTT dynamic change skew</td><td>tADC</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>CK</td><td>39</td><td></td></tr><tr><td colspan="13">Write Leveling Timing</td></tr><tr><td>First DQS, DQS# rising edge</td><td>tWLMRD</td><td>40</td><td>-</td><td>40</td><td>-</td><td>40</td><td>-</td><td>40</td><td>-</td><td>CK</td><td></td><td></td></tr><tr><td>DQS, DQS# delay</td><td>tWLDQSEN</td><td>25</td><td>-</td><td>25</td><td>-</td><td>25</td><td>-</td><td>25</td><td>-</td><td>CK</td><td></td><td></td></tr><tr><td>Write leveling setup from rising CK, CK# crossing to rising DQS, DQS# crossing</td><td>tWLS</td><td>325</td><td>-</td><td>245</td><td>-</td><td>195</td><td>-</td><td>165</td><td>-</td><td>ps</td><td></td><td></td></tr></table>


Table 58: E lectrica l Characteristics and AC Operati ng Cond itions (Conti nued)



N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-800</td><td colspan="2">DDR3L-1066</td><td colspan="2">DDR3L-1333</td><td colspan="2">DDR3L-1600</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td>Write leveling hold from rising DQS, DQS# crossing to rising CK, CK# crossing</td><td>tWLH</td><td>325</td><td>-</td><td>245</td><td>-</td><td>195</td><td>-</td><td>165</td><td>-</td><td>ps</td><td></td></tr><tr><td>Write leveling output delay</td><td>tWLO</td><td>0</td><td>9</td><td>0</td><td>9</td><td>0</td><td>9</td><td>0</td><td>7.5</td><td>ns</td><td></td></tr><tr><td>Write leveling output error</td><td>tWLOE</td><td>0</td><td>2</td><td>0</td><td>2</td><td>0</td><td>2</td><td>0</td><td>2</td><td>ns</td><td></td></tr></table>

Notes: 1. AC timing parameters are valid from specified ${ { \sf T } _ { \mathsf { C } } }$ MIN to ${ { \sf T } _ { \mathsf { C } } }$ MAX values. 

2. All voltages are referenced to $\mathsf { V } _ { \mathsf { S } \mathsf { S } }$ 

3. Output timings are only valid for RON34 output buffer selection. 

4. The unit $^ \mathrm { t } \mathsf { C K }$ (AVG) represents the actual $^ \mathrm { t } \mathsf { C K }$ (AVG) of the input clock under operation. The unit CK represents one clock cycle of the input clock, counting the actual clock edges. 

5. AC timing and $1 _ { \mathsf { D D } }$ tests may use a ${ \mathsf { V } } _ { \parallel }$ -to- $\boldsymbol { \cdot } \mathsf { V } _ { \sf I H }$ swing of up to $9 0 0 \mathsf { m } \mathsf { V }$ in the test environment, but input timing is still referenced to $V _ { \mathsf { R E F } }$ (except t IS, t IH, $\mathrm { \Delta ^ { t } D S } ,$ , and $^ \mathrm { t } \mathsf { D H }$ use the AC/DC trip points and CK, CK# and DQS, DQS# use their crossing points). The minimum slew rate for the input signals used to test the device is 1 V/ns for single-ended inputs and 2 V/ns for differential inputs in the range between $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ and $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ . 

6. All timings that use time-based values (ns, μs, ms) should use $\mathsf { t } _ { \mathsf { C K } }$ (AVG) to determine the correct number of clocks (Table 58 (page 81) uses CK or $^ \mathrm { t } \mathsf { C K }$ [AVG] interchangeably). In the case of noninteger results, all minimum limits are to be rounded up to the nearest whole integer, and all maximum limits are to be rounded down to the nearest whole integer. 

7. Strobe or ${ \mathsf { D Q S } } _ { \mathsf { d i f f } }$ refers to the DQS and DQS# differential crossing point when DQS is the rising edge. Clock or CK refers to the CK and CK# differential crossing point when CK is the rising edge. 

8. This output load is used for all AC timing (except ODT reference timing) and slew rates. The actual test load may be different. The output signal voltage reference point is $\mathsf { V } _ { \mathsf { D D Q } } / 2$ for single-ended signals and the crossing point for differential signals (see Figure 31 (page 73)). 

9. When operating in DLL disable mode, Micron does not warrant compliance with normal mode timings or functionality. 

10. The clock’s $\mathsf { t } _ { \mathsf { C K } }$ (AVG) is the average clock over any 200 consecutive clocks and $^ \mathrm { t } \mathsf { C K }$ (AVG) MIN is the smallest clock rate allowed, with the exception of a deviation due to clock jitter. Input clock jitter is allowed provided it does not exceed values specified and must be of a random Gaussian distribution in nature. 

11. Spread spectrum is not included in the jitter specification values. However, the input clock can accommodate spread-spectrum at a sweep rate in the range of $2 0 – 6 0 \ \mathsf { k H z }$ with an additional $1 \%$ of $\mathsf { t } _ { \mathsf { C K } }$ (AVG) as a long-term jitter component; however, the spread spectrum may not use a clock rate below $^ \mathrm { t } \mathsf { C K }$ (AVG) MIN. 

12. The clock’s $^ \mathrm { t } C \mathsf { H }$ (AVG) and $^ \mathrm { t } \mathsf { C L }$ (AVG) are the average half clock period over any 200 consecutive clocks and is the smallest clock half period allowed, with the exception of a deviation due to clock jitter. Input clock jitter is allowed provided it does not exceed values specified and must be of a random Gaussian distribution in nature. 

13. The period jitter (t JITper) is the maximum deviation in the clock period from the average or nominal clock. It is allowed in either the positive or negative direction. 

14. t CH (ABS) is the absolute instantaneous clock high pulse width as measured from one rising edge to the following falling edge. 

15. t CL (ABS) is the absolute instantaneous clock low pulse width as measured from one falling edge to the following rising edge. 

16. The cycle-to-cycle jitter t JITcc is the amount the clock period can deviate from one cycle to the next. It is important to keep cycle-to-cycle jitter at a minimum during the DLL locking time. 

17. The cumulative jitter error t ERRnper, where n is the number of clocks between 2 and 50, is the amount of clock time allowed to accumulate consecutively away from the average clock over n number of clock cycles. 

18. t DS (base) and $^ \mathrm { t } \mathsf { D } \mathsf { H }$ (base) values are for a single-ended 1 V/ns slew rate DQs and 2 V/ns slew rate differential DQS, DQS#; when DQ single-ended slew rate is 2V/ns, the DQS differential slew rate is 4V/ns. 

19. These parameters are measured from a data signal (DM, DQ0, DQ1, and so forth) transition edge to its respective data strobe signal (DQS, DQS#) crossing. 

20. The setup and hold times are listed converting the base specification values (to which derating tables apply) to $V _ { R E F }$ when the slew rate is 1 V/ns. These values, with a slew rate of 1 V/ns, are for reference only. 

21. When the device is operated with input clock jitter, this parameter needs to be derated by the actual t JITper (larger of t JITper (MIN) or t JITper (MAX) of the input clock (output deratings are relative to the SDRAM input clock). 

22. Single-ended signal parameter. 

23. The DRAM output timing is aligned to the nominal or average clock. Most output parameters must be derated by the actual jitter error when input clock jitter is present, even when within specification. This results in each parameter becoming larger. The following parameters are required to be derated by subtracting t ERR10per (MAX): t DQSCK (MIN), t LZDQS (MIN), t LZDQ (MIN), and t AON (MIN). The following parameters are required to be derated by subtracting t ERR10per (MIN): t DQSCK (MAX), $\mathrm { t } _ { \mathsf { H } , \mathsf { Z } }$ (MAX), t LZDQS (MAX), t LZDQ MAX, and t AON (MAX). The parameter t RPRE (MIN) is derated by subtracting t JITper (MAX), while t RPRE (MAX) is derated by subtracting t JITper (MIN). 

24. The maximum preamble is bound by t LZDQS (MAX). 

25. These parameters are measured from a data strobe signal (DQS, DQS#) crossing to its respective clock signal (CK, CK#) crossing. The specification values are not affected by the amount of clock jitter applied, as these are relative to the clock signal crossing. These parameters should be met whether clock jitter is present. 

26. The t DQSCK (DLL_DIS) parameter begins $\mathsf { C L } + \mathsf { A L } - 1$ cycles after the READ command. 

27. The maximum postamble is bound by t HZDQS (MAX). 

28. Commands requiring a locked DLL are: READ (and RDAP) and synchronous ODT commands. In addition, after any change of latency t XPDLL, timing must be met. 

29. t IS (base) and t IH (base) values are for a single-ended 1 V/ns control/command/address slew rate and 2 V/ns CK, CK# differential slew rate. 

30. These parameters are measured from a command/address signal transition edge to its respective clock (CK, CK#) signal crossing. The specification values are not affected by the amount of clock jitter applied as the setup and hold times are relative to the clock signal crossing that latches the command/address. These parameters should be met whether clock jitter is present. 

31. For these parameters, the DDR3L SDRAM device supports t nPARAM $( n \mathsf { C K } ) = \mathsf { R U }$ (t PARAM [ns]/t CK[AVG] [ns]), assuming all input clock jitter specifications are satisfied. For example, the device will support ${ } ^ { \mathrm { t } } n \mathsf { R P } \left( n \mathsf { C K } \right) = \mathsf { R U } ( ^ { \mathrm { t } } \mathsf { R P } / ^ { \mathrm { t } } \mathsf { C K } [ \mathsf { A V G } ] )$ if all input clock jitter specifications are met. This means that for DDR3-800 6-6-6, of which $^ { \mathrm { t } } { \mathsf { R P } } = 5 { \mathsf { n s , } }$ the device will support $^ { \mathrm { t } } n \mathsf { R P } = \mathsf { R U } ( ^ { \mathrm { t } } \mathsf { R P } / ^ { \mathrm { t } } \mathsf { C K } [ \mathsf { A V G } ] ) = 6$ as long as the input clock jitter specifications are met. That is, the PRECHARGE command at T0 and the ACTIVATE command at $\mathsf { T } 0 + 6$ are valid even if six clocks are less than 15ns due to input clock jitter. 

32. During READs and WRITEs with auto precharge, the DDR3 SDRAM will hold off the internal PRECHARGE command until t RAS (MIN) has been satisfied. 

33. When operating in DLL disable mode, the greater of 4CK or 15ns is satisfied for t WR. 

34. The start of the write recovery time is defined as follows: 

• For BL8 (fixed by MRS or OTF): Rising clock edge four clock cycles after WL 

• For BC4 (OTF): Rising clock edge four clock cycles after WL 

• For BC4 (fixed by MRS): Rising clock edge two clock cycles after WL 

35. RESET# should be LOW as soon as power starts to ramp to ensure the outputs are in High-Z. Until RESET# is LOW, the outputs are at risk of driving and could result in excessive current, depending on bus activity. 

36. The refresh period is $6 4 \mathsf { m s }$ when ${ { \sf T } _ { \mathsf { C } } }$ is less than or equal to $8 5 ^ { \circ } \mathsf { C }$ . This equates to an average refresh rate of $7 . 8 1 2 5 \mu s$ . However, nine REFRESH commands should be asserted at least once every $7 0 . 3 \mu \ s$ . When ${ { \sf T } _ { \mathsf { C } } }$ is greater than ${ 8 5 ^ { \circ } } \mathsf C ,$ the refresh period is 32ms. 

37. Although CKE is allowed to be registered LOW after a REFRESH command when t REFPDEN (MIN) is satisfied, there are cases where additional time such as t XPDLL (MIN) is required. 

38. ODT turn-on time MIN is when the device leaves High-Z and ODT resistance begins to turn on. ODT turn-on time maximum is when the ODT resistance is fully on. The ODT reference load is shown in Figure 24 (page 61). This output load is used for ODT timings (see Figure 31 (page 73)).Designs that were created prior to JEDEC tightening the maximum limit from 9ns to 8.5ns will be allowed to have a 9ns maximum. 

39. Half-clock output parameters must be derated by the actual t ERR10per and t JITdty when input clock jitter is present. This results in each parameter becoming larger. The parameters t ADC (MIN) and tAOF (MIN) are each required to be derated by subtracting both t ERR10per (MAX) and t JITdty (MAX). The parameters t ADC (MAX) and t AOF (MAX) are required to be derated by subtracting both t ERR10per (MAX) and t JITdty (MAX). 

40. ODT turn-off time minimum is when the device starts to turn off ODT resistance. ODT turn-off time maximum is when the DRAM buffer is in High-Z. The ODT reference load is shown in Figure 24 (page 61). This output load is used for ODT timings (see Figure 31 (page 73)). 

41. Pulse width of a input signal is defined as the width between the first crossing of VREF(DC) and the consecutive crossing of VREF(DC). 

42. Should the clock rate be larger than t RFC (MIN), an AUTO REFRESH command should have at least one NOP command between it and another AUTO REFRESH command. Additionally, if the clock rate is slower than 40ns (25 MHz), all REFRESH commands should be followed by a PRECHARGE ALL command. 

43. DRAM devices should be evenly addressed when being accessed. Disproportionate accesses to a particular row address may result in a reduction of REFRESH characteristics or product lifetime. 

44. When two $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ values (and two corresponding $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ values) are listed for a specific speed bin, the user may choose either value for the input AC level. Whichever value is used, the associated setup time for that AC level must also be used. Additionally, one $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ value may be used for address/command inputs and the other $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ value may be used for data inputs. 

For example, for DDR3-800, two input AC levels are defined: $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } 1 7 5 ) , \mathsf { m i n } }$ and $\mathsf { V } _ { | \mathsf { H } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } }$ (corresponding $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C 1 7 5 } ) , \mathsf { m i n } }$ and $\mathsf { V } _ { 1 \mathsf { L } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } } )$ . For DDR3-800, the address/ command inputs must use either $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 7 5 ) , \mathsf { m i n } }$ with t IS(AC175) of 200ps or $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } }$ with t IS(AC150) of 350ps; independently, the data inputs must use either $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 7 5 ) , \mathsf { m i n } }$ with t DS(AC175) of 75ps or $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } }$ with t DS(AC150) of 125ps. 

# E lectrica l Characteristics and AC Operati ng Cond itions


Table 59: E lectrica l Characteristics and AC Operati ng Cond itions for Speed Extensions



N otes 1 –8 a p p l y to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-1866</td><td colspan="2">DDR3L-2133</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="9">Clock Timing</td></tr><tr><td rowspan="2">Clock period average: DLL disable mode</td><td>TC=0°C to 85°C</td><td rowspan="2">tCK (DLL_DIS)</td><td>8</td><td>7800</td><td>8</td><td>7800</td><td>ns</td><td>9,42</td></tr><tr><td>TC=&gt;85°C to 95°C</td><td>8</td><td>3900</td><td>8</td><td>3900</td><td>ns</td><td>42</td></tr><tr><td colspan="2">Clock period average: DLL enable mode</td><td>tCK (AVG)</td><td colspan="5">See Speed Bin Tables for tCK range allowed ns</td><td>10,11</td></tr><tr><td colspan="2">High pulse width average</td><td>tCH (AVG)</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>CK</td><td>12</td></tr><tr><td colspan="2">Low pulse width average</td><td>tCL (AVG)</td><td>0.47</td><td>0.53</td><td>0.47</td><td>0.53</td><td>CK</td><td>12</td></tr><tr><td rowspan="2">Clock period jitter</td><td>DLL locked</td><td>tJITper</td><td>-60</td><td>60</td><td>-50</td><td>50</td><td>ps</td><td>13</td></tr><tr><td>DLL locking</td><td>tJITper,lck</td><td>-50</td><td>50</td><td>-40</td><td>40</td><td>ps</td><td>13</td></tr><tr><td colspan="2">Clock absolute period</td><td>tCK (ABS)</td><td colspan="5">MIN = tCK (AVG) MIN + tJITper MIN; MAX = tCK (AVG) MAX + tJITper MAX ps</td><td></td></tr><tr><td colspan="2">Clock absolute high pulse width</td><td>tCH (ABS)</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>tCK (AVG)</td><td>14</td></tr><tr><td colspan="2">Clock absolute low pulse width</td><td>tCL (ABS)</td><td>0.43</td><td>-</td><td>0.43</td><td>-</td><td>tCK (AVG)</td><td>15</td></tr><tr><td rowspan="2">Cycle-to-cycle jitter</td><td>DLL locked</td><td>tJITcc</td><td colspan="2">120</td><td colspan="2">120</td><td>ps</td><td>16</td></tr><tr><td>DLL locking</td><td>tJITcc,lck</td><td colspan="2">100</td><td colspan="2">100</td><td>ps</td><td>16</td></tr></table>


Table 59: E lectrica l Characteristics and AC Operati ng Cond itions for Speed Extensions (Conti nued)



N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-1866</td><td colspan="2">DDR3L-2133</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td rowspan="12">Cumulative error across</td><td>2 cycles</td><td>tERR2per</td><td>-88</td><td>88</td><td>-74</td><td>74</td><td>ps</td><td>17</td></tr><tr><td>3 cycles</td><td>tERR3per</td><td>-105</td><td>105</td><td>-87</td><td>87</td><td>ps</td><td>17</td></tr><tr><td>4 cycles</td><td>tERR4per</td><td>-117</td><td>117</td><td>-97</td><td>97</td><td>ps</td><td>17</td></tr><tr><td>5 cycles</td><td>tERR5per</td><td>-126</td><td>126</td><td>-105</td><td>105</td><td>ps</td><td>17</td></tr><tr><td>6 cycles</td><td>tERR6per</td><td>-133</td><td>133</td><td>-111</td><td>111</td><td>ps</td><td>17</td></tr><tr><td>7 cycles</td><td>tERR7per</td><td>-139</td><td>139</td><td>-116</td><td>116</td><td>ps</td><td>17</td></tr><tr><td>8 cycles</td><td>tERR8per</td><td>-145</td><td>145</td><td>-121</td><td>121</td><td>ps</td><td>17</td></tr><tr><td>9 cycles</td><td>tERR9per</td><td>-150</td><td>150</td><td>-125</td><td>125</td><td>ps</td><td>17</td></tr><tr><td>10 cycles</td><td>tERR10per</td><td>-154</td><td>154</td><td>-128</td><td>128</td><td>ps</td><td>17</td></tr><tr><td>11 cycles</td><td>tERR11per</td><td>-158</td><td>158</td><td>-132</td><td>132</td><td>ps</td><td>17</td></tr><tr><td>12 cycles</td><td>tERR12per</td><td>-161</td><td>161</td><td>-134</td><td>134</td><td>ps</td><td>17</td></tr><tr><td>n = 13, 14 . . . 49, 50 cycles</td><td>tERRnper</td><td colspan="4">tERRnper MIN = (1 + 0.68ln[n]) × tJITper MINtERRnper MAX = (1 + 0.68ln[n]) × tJITper MAX</td><td>ps</td><td>17</td></tr><tr><td colspan="9">DQ Input Timing</td></tr><tr><td rowspan="2">Data setup time to DQS, DQS#</td><td>Base (specification) @ 2 V/ns</td><td rowspan="2">tDS(AC130)</td><td>70</td><td>-</td><td>55</td><td>-</td><td>ps</td><td>18, 19</td></tr><tr><td>VREF@ 2 V/ns</td><td>135</td><td>-</td><td>120.5</td><td>-</td><td>ps</td><td>19, 20</td></tr><tr><td rowspan="2">Data hold time from DQS, DQS#</td><td>Base (specification) @ 2 V/ns</td><td rowspan="2">tDH(DC90)</td><td>75</td><td>-</td><td>60</td><td>-</td><td>ps</td><td>18, 19</td></tr><tr><td>VREF@ 2 V/ns</td><td>110</td><td>-</td><td>105</td><td>-</td><td>ps</td><td>19, 20</td></tr><tr><td colspan="2">Minimum data pulse width</td><td>tDIPW</td><td>320</td><td>-</td><td>280</td><td>-</td><td>ps</td><td>41</td></tr><tr><td colspan="9">DQ Output Timing</td></tr><tr><td colspan="2">DQS, DQS# to DQ skew, per access</td><td>tDQSQ</td><td>-</td><td>85</td><td>-</td><td>75</td><td>ps</td><td></td></tr><tr><td colspan="2">DQ output hold time from DQS, DQS#</td><td>tQH</td><td>0.38</td><td>-</td><td>0.38</td><td>-</td><td>tCK(AVG)</td><td>21</td></tr><tr><td colspan="2">DQ Low-Z time from CK, CK#</td><td>tLZDQ</td><td>-390</td><td>195</td><td>-360</td><td>180</td><td>ps</td><td>22, 23</td></tr><tr><td colspan="2">DQ High-Z time from CK, CK#</td><td>tHZDQ</td><td>-</td><td>195</td><td>-</td><td>180</td><td>ps</td><td>22, 23</td></tr><tr><td colspan="9">DQ Strobe Input Timing</td></tr><tr><td colspan="2">DQS, DQS# rising to CK, CK# rising</td><td>tDQSS</td><td>-0.27</td><td>0.27</td><td>-0.27</td><td>0.27</td><td>CK</td><td>25</td></tr><tr><td colspan="2">DQS, DQS# differential input low pulse width</td><td>tDQSL</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>CK</td><td></td></tr></table>


Table 59: E lectrica l Characteristics and AC Operati ng Cond itions for Speed Extensions (Conti nued)



N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-1866</td><td colspan="2">DDR3L-2133</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">DQS, DQS# differential input high pulse width</td><td>tDQSH</td><td>0.45</td><td>0.55</td><td>0.45</td><td>0.55</td><td>CK</td><td></td></tr><tr><td colspan="2">DQS, DQS# falling setup to CK, CK# rising</td><td>tDSS</td><td>0.18</td><td>-</td><td>0.18</td><td>-</td><td>CK</td><td>25</td></tr><tr><td colspan="2">DQS, DQS# falling hold from CK, CK# rising</td><td>tDSH</td><td>0.18</td><td>-</td><td>0.18</td><td>-</td><td>CK</td><td>25</td></tr><tr><td colspan="2">DQS, DQS# differential WRITE preamble</td><td>tWPRE</td><td>0.9</td><td>-</td><td>0.9</td><td>-</td><td>CK</td><td></td></tr><tr><td colspan="2">DQS, DQS# differential WRITE postamble</td><td>tWPST</td><td>0.3</td><td>-</td><td>0.3</td><td>-</td><td>CK</td><td></td></tr><tr><td colspan="9">DQ Strobe Output Timing</td></tr><tr><td colspan="2">DQS, DQS# rising to/from rising CK, CK#</td><td>tDQSCK</td><td>-195</td><td>195</td><td>-180</td><td>180</td><td>ps</td><td>23</td></tr><tr><td colspan="2">DQS, DQS# rising to/from rising CK, CK# when DLL is disabled</td><td>tDQSCK (DLL_DIS)</td><td>1</td><td>10</td><td>1</td><td>10</td><td>ns</td><td>26</td></tr><tr><td colspan="2">DQS, DQS# differential output high time</td><td>tQSH</td><td>0.40</td><td>-</td><td>0.40</td><td>-</td><td>CK</td><td>21</td></tr><tr><td colspan="2">DQS, DQS# differential output low time</td><td>tQSL</td><td>0.40</td><td>-</td><td>0.40</td><td>-</td><td>CK</td><td>21</td></tr><tr><td colspan="2">DQS, DQS# Low-Z time (RL - 1)</td><td>tLZDQS</td><td>-390</td><td>195</td><td>-360</td><td>180</td><td>ps</td><td>22, 23</td></tr><tr><td colspan="2">DQS, DQS# High-Z time (RL + BL/2)</td><td>tHZDQS</td><td>-</td><td>195</td><td>-</td><td>180</td><td>ps</td><td>22, 23</td></tr><tr><td colspan="2">DQS, DQS# differential READ preamble</td><td>tRPRE</td><td>0.9</td><td>Note 24</td><td>0.9</td><td>Note 24</td><td>CK</td><td>23, 24</td></tr><tr><td colspan="2">DQS, DQS# differential READ postamble</td><td>tRPST</td><td>0.3</td><td>Note 27</td><td>0.3</td><td>Note 27</td><td>CK</td><td>23, 27</td></tr><tr><td colspan="9">Command and Address Timing</td></tr><tr><td colspan="2">DLL locking time</td><td>tDLLK</td><td>512</td><td>-</td><td>512</td><td>-</td><td>CK</td><td>28</td></tr><tr><td rowspan="2">CTRL, CMD, ADDR setup to CK,CK#</td><td>Base (specification)</td><td rowspan="2">tIS (AC135)</td><td>65</td><td>-</td><td>60</td><td>-</td><td>ps</td><td>29, 30, 44</td></tr><tr><td>VREF @ 1 V/ns</td><td>200</td><td>-</td><td>195</td><td>-</td><td>ps</td><td>20, 30</td></tr><tr><td rowspan="2">CTRL, CMD, ADDR setup to CK,CK#</td><td>Base (specification)</td><td rowspan="2">tIS (AC125)</td><td>150</td><td>-</td><td>135</td><td>-</td><td>ps</td><td>29, 30, 44</td></tr><tr><td>VREF @ 1 V/ns</td><td>275</td><td>-</td><td>260</td><td>-</td><td>ps</td><td>20, 30</td></tr><tr><td rowspan="2">CTRL, CMD, ADDR hold from CK,CK#</td><td>Base (specification)</td><td rowspan="2">tIH (DC90)</td><td>110</td><td>-</td><td>95</td><td>-</td><td>ps</td><td>29, 30</td></tr><tr><td>VREF @ 1 V/ns</td><td>200</td><td>-</td><td>195</td><td>-</td><td>ps</td><td>20, 30</td></tr><tr><td colspan="2">Minimum CTRL, CMD, ADDR pulse width</td><td>tIPW</td><td>535</td><td>-</td><td>470</td><td>-</td><td>ps</td><td>41</td></tr><tr><td colspan="2">ACTIVATE to internal READ or WRITE delay</td><td>tRCD</td><td colspan="4">See Speed Bin Tables for tRCD</td><td>ns</td><td>31</td></tr><tr><td colspan="2">PRECHARGE command period</td><td>tRP</td><td colspan="4">See Speed Bin Tables for tRP</td><td>ns</td><td>31</td></tr><tr><td colspan="2">ACTIVATE-to-PRECHARGE command period</td><td>tRAS</td><td colspan="4">See Speed Bin Tables for tRAS</td><td>ns</td><td>31, 32</td></tr><tr><td colspan="2">ACTIVATE-to-ACTIVATE command period</td><td>tRC</td><td colspan="4">See Speed Bin Tables for tRC</td><td>ns</td><td>31, 43</td></tr></table>


Table 59: E lectrica l Characteristics and AC Operati ng Cond itions for Speed Extensions (Conti nued)



N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-1866</td><td colspan="2">DDR3L-2133</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td rowspan="2">ACTIVATE-to-ACTIVATE minimum command period</td><td>1KB page size</td><td rowspan="2">tRRD</td><td colspan="4">MIN = greater of 4CK or 5ns</td><td>CK</td><td>31</td></tr><tr><td>2KB page size</td><td colspan="4">MIN = greater of 4CK or 6ns</td><td>CK</td><td>31</td></tr><tr><td rowspan="2">Four ACTIVATE windows</td><td>1KB page size</td><td rowspan="2">tFAW</td><td>27</td><td>-</td><td>25</td><td>-</td><td>ns</td><td>31</td></tr><tr><td>2KB page size</td><td>35</td><td>-</td><td>35</td><td>-</td><td>ns</td><td>31</td></tr><tr><td colspan="2">Write recovery time</td><td>tWR</td><td colspan="4">MIN = 15ns; MAX = N/A</td><td>ns</td><td>31, 32, 33</td></tr><tr><td colspan="2">Delay from start of internal WRITE transac-tion to internal READ command</td><td>tWTR</td><td colspan="4">MIN = greater of 4CK or 7.5ns; MAX = N/A</td><td>CK</td><td>31, 34</td></tr><tr><td colspan="2">READ-to-PRECHARGE time</td><td>tRTP</td><td colspan="4">MIN = greater of 4CK or 7.5ns; MAX = N/A</td><td>CK</td><td>31, 32</td></tr><tr><td colspan="2">CAS#-to-CAS# command delay</td><td>tCCD</td><td colspan="4">MIN = 4CK; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Auto precharge write recovery + precharge time</td><td>tDAL</td><td colspan="4">MIN = WR + tRP/tCK (AVG); MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">MODE REGISTER SET command cycle time</td><td>tMRD</td><td colspan="4">MIN = 4CK; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">MODE REGISTER SET command update delay</td><td>tMOD</td><td colspan="4">MIN = greater of 12CK or 15ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">MULTIPURPOSE REGISTER READ burst end to mode register set for multipurpose register exit</td><td>tMPRR</td><td colspan="4">MIN = 1CK; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="9">Calibration Timing</td></tr><tr><td rowspan="2">ZQCL command: Long calibration time</td><td>POWER-UP and RE-SET operation</td><td>tZQinit</td><td colspan="4">MIN = N/AMAX = MAX(512nCK, 640ns)</td><td>CK</td><td></td></tr><tr><td>Normal operation</td><td>tZQoper</td><td colspan="4">MIN = N/AMAX = max(256nCK, 320ns)</td><td>CK</td><td></td></tr><tr><td colspan="2">ZQCS command: Short calibration time</td><td colspan="5">MIN = N/AMAX = max(64nCK, 80ns) tZQCS</td><td>CK</td><td></td></tr><tr><td colspan="9">Initialization and Reset Timing</td></tr><tr><td colspan="2">Exit reset from CKE HIGH to a valid command</td><td>tXPR</td><td colspan="4">MIN = greater of 5CK or tRFC + 10ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Begin power supply ramp to power supplies stable</td><td>tVDDPR</td><td colspan="4">MIN = N/A; MAX = 200</td><td>ms</td><td></td></tr><tr><td colspan="2">RESET# LOW to power supplies stable</td><td>tRPS</td><td colspan="4">MIN = 0; MAX = 200</td><td>ms</td><td></td></tr><tr><td colspan="2">RESET# LOW to I/O and RTT High-Z</td><td>tIOZ</td><td colspan="4">MIN = N/A; MAX = 20</td><td>ns</td><td>35</td></tr><tr><td colspan="9">Refresh Timing</td></tr></table>


Table 59: E lectrica l Characteristics and AC Operati ng Cond itions for Speed Extensions (Conti nued)



N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-1866</td><td colspan="2">DDR3L-2133</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td rowspan="4" colspan="2">REFRESH-to-ACTIVATE or REFRESH command period</td><td>tRFC - 1Gb</td><td colspan="4">MIN = 110; MAX = 70,200</td><td>ns</td><td></td></tr><tr><td>tRFC - 2Gb</td><td colspan="4">MIN = 160; MAX = 70,200</td><td>ns</td><td></td></tr><tr><td>tRFC - 4Gb</td><td colspan="4">MIN = 260; MAX = 70,200</td><td>ns</td><td></td></tr><tr><td>tRFC - 8Gb</td><td colspan="4">MIN = 350; MAX = 70,200</td><td>ns</td><td></td></tr><tr><td rowspan="2">Maximum refresh period</td><td>TC ≤ 85°C</td><td rowspan="2">-</td><td colspan="4">64 (1X)</td><td>ms</td><td>36</td></tr><tr><td>TC &gt; 85°C</td><td colspan="4">32 (2X)</td><td>ms</td><td>36</td></tr><tr><td rowspan="2">Maximum average periodic refresh</td><td>TC ≤ 85°C</td><td rowspan="2">tREFI</td><td colspan="4">7.8 (64ms/8192)</td><td>μs</td><td>36</td></tr><tr><td>TC &gt; 85°C</td><td colspan="4">3.9 (32ms/8192)</td><td>μs</td><td>36</td></tr><tr><td colspan="9">Self Refresh Timing</td></tr><tr><td colspan="2">Exit self refresh to commands not requiring a locked DLL</td><td>tXS</td><td colspan="4">MIN = greater of 5CK or tRFC + 10ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Exit self refresh to commands requiring a locked DLL</td><td>tXSDLL</td><td colspan="4">MIN = tDLLK (MIN); MAX = N/A</td><td>CK</td><td>28</td></tr><tr><td colspan="2">Minimum CKE low pulse width for self refresh entry to self refresh exit timing</td><td>tCKESR</td><td colspan="4">MIN = tCKE (MIN) + CK; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Valid clocks after self refresh entry or power-down entry</td><td>tCKSRE</td><td colspan="4">MIN = greater of 5CK or 10ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Valid clocks before self refresh exit, power-down exit, or reset exit</td><td>tCKSRX</td><td colspan="4">MIN = greater of 5CK or 10ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="9">Power-Down Timing</td></tr><tr><td colspan="2">CKE MIN pulse width</td><td>tCKE (MIN)</td><td colspan="4">Greater of 3CK or 5ns</td><td>CK</td><td></td></tr><tr><td colspan="2">Command pass disable delay</td><td>tCPDED</td><td colspan="4">MIN = 2; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Power-down entry to power-down exit timing</td><td>tPD</td><td colspan="4">MIN = tCKE (MIN); MAX = 9 * tREFI</td><td>CK</td><td></td></tr><tr><td colspan="2">Begin power-down period prior to CKE registered HIGH</td><td>tANPD</td><td colspan="4">WL - 1CK</td><td>CK</td><td></td></tr><tr><td colspan="2">Power-down entry period: ODT either synchronous or asynchronous</td><td>PDE</td><td colspan="4">Greater of tANPD or tRFC - REFRESH command to CKE LOW time</td><td>CK</td><td></td></tr><tr><td colspan="2">Power-down exit period: ODT either synchronous or asynchronous</td><td>PDX</td><td colspan="4">tANPD + tXPDLL</td><td>CK</td><td></td></tr><tr><td colspan="9">Power-Down Entry Minimum Timing</td></tr></table>


Table 59: E lectrica l Characteristics and AC Operati ng Cond itions for Speed Extensions (Conti nued)



N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2" colspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-1866</td><td colspan="2">DDR3L-2133</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td colspan="2">ACTIVATE command to power-down entry</td><td>tACTPDEN</td><td colspan="4">MIN = 2</td><td>CK</td><td></td></tr><tr><td colspan="2">PRECHARGE/PRECHARGE ALL command to power-down entry</td><td>tPRPDEN</td><td colspan="4">MIN = 2</td><td>CK</td><td></td></tr><tr><td colspan="2">REFRESH command to power-down entry</td><td>tREFPDEN</td><td colspan="4">MIN = 2</td><td>CK</td><td>37</td></tr><tr><td colspan="2">MRS command to power-down entry</td><td>tMRSPDEN</td><td colspan="4">MIN = tMOD (MIN)</td><td>CK</td><td></td></tr><tr><td colspan="2">READ/READ with auto precharge command to power-down entry</td><td>tRDPDEN</td><td colspan="4">MIN = RL + 4 + 1</td><td>CK</td><td></td></tr><tr><td rowspan="3">WRITE command to power-down entry</td><td>BL8 (OTF, MRS)</td><td rowspan="2">tWRPDEN</td><td rowspan="2" colspan="4">MIN = WL + 4 + tWR/tCK (AVG)</td><td rowspan="2">CK</td><td rowspan="2"></td></tr><tr><td>BC4OTF</td></tr><tr><td>BC4MRS</td><td>tWRPDEN</td><td colspan="4">MIN = WL + 2 + tWR/tCK (AVG)</td><td>CK</td><td></td></tr><tr><td rowspan="3">WRITE with auto pre-charge command to power-down entry</td><td>BL8 (OTF, MRS)</td><td rowspan="2">tWRAP-DEN</td><td rowspan="2" colspan="4">MIN = WL + 4 + WR + 1</td><td rowspan="2">CK</td><td rowspan="2"></td></tr><tr><td>BC4OTF</td></tr><tr><td>BC4MRS</td><td>tWRAP-DEN</td><td colspan="4">MIN = WL + 2 + WR + 1</td><td>CK</td><td></td></tr><tr><td colspan="9">Power-Down Exit Timing</td></tr><tr><td colspan="2">DLL on, any valid command, or DLL off to commands not requiring locked DLL</td><td>tXP</td><td colspan="4">MIN = greater of 3CK or 6ns; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="2">Precharge power-down with DLL off to commands requiring a locked DLL</td><td>tXPDLL</td><td colspan="4">MIN = greater of 10CK or 24ns; MAX = N/A</td><td>CK</td><td>28</td></tr><tr><td colspan="9">ODT Timing</td></tr><tr><td colspan="2">RTT synchronous turn-on delay</td><td>ODTL on</td><td colspan="4">CWL + AL - 2CK</td><td>CK</td><td>38</td></tr><tr><td colspan="2">RTT synchronous turn-off delay</td><td>ODTL off</td><td colspan="4">CWL + AL - 2CK</td><td>CK</td><td>40</td></tr><tr><td colspan="2">RTT turn-on from ODTL on reference</td><td>tAON</td><td>-195</td><td>195</td><td>-180</td><td>180</td><td>ps</td><td>23, 38</td></tr><tr><td colspan="2">RTT turn-off from ODTL off reference</td><td>tAOF</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>CK</td><td>39, 40</td></tr><tr><td colspan="2">Asynchronous RTT turn-on delay (power-down with DLL off)</td><td>tAONPD</td><td colspan="4">MIN = 2; MAX = 8.5</td><td>ns</td><td>38</td></tr><tr><td colspan="2">Asynchronous RTT turn-off delay (power-down with DLL off)</td><td>tAOFPD</td><td colspan="4">MIN = 2; MAX = 8.5</td><td>ns</td><td>40</td></tr><tr><td colspan="2">ODT HIGH time with WRITE command and BL8</td><td>ODTH8</td><td colspan="4">MIN = 6; MAX = N/A</td><td>CK</td><td></td></tr></table>


Table 59: E lectrica l Characteristics and AC Operati ng Cond itions for Speed Extensions (Conti nued)



N otes 1 –8 a p p ly to t h e e nt i re ta b l e


<table><tr><td rowspan="2">Parameter</td><td rowspan="2">Symbol</td><td colspan="2">DDR3L-1866</td><td colspan="2">DDR3L-2133</td><td rowspan="2">Unit</td><td rowspan="2">Notes</td></tr><tr><td>Min</td><td>Max</td><td>Min</td><td>Max</td></tr><tr><td>ODT HIGH time without WRITE command or with WRITE command and BC4</td><td>ODTH4</td><td colspan="4">MIN = 4; MAX = N/A</td><td>CK</td><td></td></tr><tr><td colspan="8">Dynamic ODT Timing</td></tr><tr><td>RTT,nom-to-RTT(WR) change skew</td><td>ODTLcnw</td><td colspan="4">WL - 2CK</td><td>CK</td><td></td></tr><tr><td>RTT(WR)-to-RTT,nom change skew - BC4</td><td>ODTLcwn4</td><td colspan="4">4CK + ODTLoff</td><td>CK</td><td></td></tr><tr><td>RTT(WR)-to-RTT,nom change skew - BL8</td><td>ODTLcwn8</td><td colspan="4">6CK + ODTLoff</td><td>CK</td><td></td></tr><tr><td>RTT dynamic change skew</td><td>tADC</td><td>0.3</td><td>0.7</td><td>0.3</td><td>0.7</td><td>CK</td><td>39</td></tr><tr><td colspan="8">Write Leveling Timing</td></tr><tr><td>First DQS, DQS# rising edge</td><td>tWLMRD</td><td>40</td><td>-</td><td>40</td><td>-</td><td>CK</td><td></td></tr><tr><td>DQS, DQS# delay</td><td>tWLDQSEN</td><td>25</td><td>-</td><td>25</td><td>-</td><td>CK</td><td></td></tr><tr><td>Write leveling setup from rising CK, CK# crossing to rising DQS, DQS# crossing</td><td>tWLS</td><td>140</td><td>-</td><td>125</td><td>-</td><td>ps</td><td></td></tr><tr><td>Write leveling hold from rising DQS, DQS# crossing to rising CK, CK# crossing</td><td>tWLH</td><td>140</td><td>-</td><td>125</td><td>-</td><td>ps</td><td></td></tr><tr><td>Write leveling output delay</td><td>tWLO</td><td>0</td><td>7.5</td><td>0</td><td>7</td><td>ns</td><td></td></tr><tr><td>Write leveling output error</td><td>tWLOE</td><td>0</td><td>2</td><td>0</td><td>2</td><td>ns</td><td></td></tr></table>

Notes: 1. AC timing parameters are valid from specified ${ { \sf T } _ { \mathsf { C } } }$ MIN to ${ { \sf T } _ { \mathsf { C } } }$ MAX values. 

2. All voltages are referenced to $\mathsf { V } _ { \mathsf { S } \mathsf { S } }$ . 

3. Output timings are only valid for RON34 output buffer selection. 

4. The unit $^ \mathrm { t } \mathsf { C K }$ (AVG) represents the actual $^ \mathrm { t } \mathsf { C K }$ (AVG) of the input clock under operation. The unit CK represents one clock cycle of the input clock, counting the actual clock edges. 

5. AC timing and $1 _ { \mathsf { D D } }$ tests may use a ${ \mathsf { V } } _ { \parallel }$ -to- $ { \boldsymbol { \cdot } }  { \boldsymbol { \vee } } _ { \sf I H }$ swing of up to $9 0 0 \mathsf { m } \mathsf { V }$ in the test environment, but input timing is still referenced to $V _ { R E F }$ (except t IS, t IH, $\mathrm { \Delta ^ { t } D S } ,$ , and $^ \mathrm { t } \mathsf { D H }$ use the AC/DC trip points and CK, CK# and DQS, DQS# use their crossing points). The minimum slew rate for the input signals used to test the device is 1 V/ns for single-ended inputs (DQs are at 2V/ns for DDR3-1866 and DDR3-2133) and 2 V/ns for differential inputs in the range between $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ and $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ . 

6. All timings that use time-based values (ns, μs, ms) should use $\mathsf { t } _ { \mathsf { C K } }$ (AVG) to determine the correct number of clocks (Table 59 (page 91) uses CK or $^ \mathrm { t } \mathsf { C K }$ [AVG] interchangeably). In the case of noninteger results, all minimum limits are to be rounded up to the nearest whole integer, and all maximum limits are to be rounded down to the nearest whole integer. 

7. Strobe or DQSdiff refers to the DQS and DQS# differential crossing point when DQS is the rising edge. Clock or CK refers to the CK and CK# differential crossing point when CK is the rising edge. 

8. This output load is used for all AC timing (except ODT reference timing) and slew rates. The actual test load may be different. The output signal voltage reference point is $\mathsf { V } _ { \mathsf { D D Q } } / 2$ for single-ended signals and the crossing point for differential signals (see Figure 31 (page 73)). 

9. When operating in DLL disable mode, Micron does not warrant compliance with normal mode timings or functionality. 

10. The clock’s $\mathsf { t } _ { \mathsf { C K } }$ (AVG) is the average clock over any 200 consecutive clocks and $^ \mathrm { t } \mathsf { C K }$ (AVG) MIN is the smallest clock rate allowed, with the exception of a deviation due to clock jitter. Input clock jitter is allowed provided it does not exceed values specified and must be of a random Gaussian distribution in nature. 

11. Spread spectrum is not included in the jitter specification values. However, the input clock can accommodate spread-spectrum at a sweep rate in the range of $2 0 – 6 0 \ \mathsf { k H z }$ with an additional $1 \%$ of $\mathsf { t } _ { \mathsf { C K } }$ (AVG) as a long-term jitter component; however, the spread spectrum may not use a clock rate below $^ \mathrm { t } \mathsf { C K }$ (AVG) MIN. 

12. The clock’s $^ \mathrm { t } { \mathsf { C H } }$ (AVG) and $^ \mathrm { t } \mathsf { C L }$ (AVG) are the average half clock period over any 200 consecutive clocks and is the smallest clock half period allowed, with the exception of a deviation due to clock jitter. Input clock jitter is allowed provided it does not exceed values specified and must be of a random Gaussian distribution in nature. 

13. The period jitter (t JITper) is the maximum deviation in the clock period from the average or nominal clock. It is allowed in either the positive or negative direction. 

14. t CH (ABS) is the absolute instantaneous clock high pulse width as measured from one rising edge to the following falling edge. 

15. t CL (ABS) is the absolute instantaneous clock low pulse width as measured from one falling edge to the following rising edge. 

16. The cycle-to-cycle jitter t JITcc is the amount the clock period can deviate from one cycle to the next. It is important to keep cycle-to-cycle jitter at a minimum during the DLL locking time. 

17. The cumulative jitter error t ERRnper, where n is the number of clocks between 2 and 50, is the amount of clock time allowed to accumulate consecutively away from the average clock over n number of clock cycles. 

18. t DS (base) and t DH (base) values are for a single-ended 1 V/ns slew rate DQs (DQs are at 2V/ns for DDR3-1866 and DDR3-2133) and 2 V/ns slew rate differential DQS, DQS#; when DQ single-ended slew rate is 2V/ns, the DQS differential slew rate is 4V/ns. 

19. These parameters are measured from a data signal (DM, DQ0, DQ1, and so forth) transition edge to its respective data strobe signal (DQS, DQS#) crossing. 

20. The setup and hold times are listed converting the base specification values (to which derating tables apply) to $V _ { R E F }$ when the slew rate is 1 V/ns (DQs are at 2V/ns for DDR3-1866 and DDR3-2133). These values, with a slew rate of 1 V/ns (DQs are at 2V/ns for DDR3-1866 and DDR3-2133), are for reference only. 

21. When the device is operated with input clock jitter, this parameter needs to be derated by the actual t JITper (larger of t JITper (MIN) or t JITper (MAX) of the input clock (output deratings are relative to the SDRAM input clock). 

22. Single-ended signal parameter. 

23. The DRAM output timing is aligned to the nominal or average clock. Most output parameters must be derated by the actual jitter error when input clock jitter is present, even when within specification. This results in each parameter becoming larger. The following parameters are required to be derated by subtracting t ERR10per (MAX): t DQSCK (MIN), t LZDQS (MIN), t LZDQ (MIN), and t AON (MIN). The following parameters are required to be derated by subtracting t ERR10per (MIN): t DQSCK (MAX), $^ \mathrm { t } \mathsf { H } Z$ (MAX), t LZDQS (MAX), t LZDQ (MAX), and t AON (MAX). The parameter t RPRE (MIN) is derated by subtracting t JITper (MAX), while t RPRE (MAX) is derated by subtracting t JITper (MIN). 

24. The maximum preamble is bound by t LZDQS (MAX). 

25. These parameters are measured from a data strobe signal (DQS, DQS#) crossing to its respective clock signal (CK, CK#) crossing. The specification values are not affected by the amount of clock jitter applied, as these are relative to the clock signal crossing. These parameters should be met whether clock jitter is present. 

26. The t DQSCK (DLL_DIS) parameter begins $\mathsf { C L } + \mathsf { A L } - 1$ cycles after the READ command. 

27. The maximum postamble is bound by t HZDQS (MAX). 

28. Commands requiring a locked DLL are: READ (and RDAP) and synchronous ODT commands. In addition, after any change of latency t XPDLL, timing must be met. 

29. t IS (base) and t IH (base) values are for a single-ended 1 V/ns control/command/address slew rate and 2 V/ns CK, CK# differential slew rate. 

30. These parameters are measured from a command/address signal transition edge to its respective clock (CK, CK#) signal crossing. The specification values are not affected by the amount of clock jitter applied as the setup and hold times are relative to the clock signal crossing that latches the command/address. These parameters should be met whether clock jitter is present. 

31. For these parameters, the DDR3L SDRAM device supports t nPARAM $( n \mathsf { C K } ) = \mathsf { R U }$ (t PARAM [ns]/t CK[AVG] [ns]), assuming all input clock jitter specifications are satisfied. For example, the device will support ${ } ^ { \mathrm { t } } n \mathsf { R P } ( n \mathsf { C K } ) = \mathsf { R U ( } ^ { \mathrm { t } } \mathsf { R P / } \mathsf { C K } [ \mathsf { A V G } ] )$ if all input clock jitter specifications are met. This means that for DDR3-800 6-6-6, of which $^ { \mathrm { t } } { \mathsf { R P } } = 5 { \mathsf { n s , } }$ the device will support $^ { \mathrm { t } } n \mathsf { R P } = \mathsf { R U } ( ^ { \mathrm { t } } \mathsf { R P } / ^ { \mathrm { t } } \mathsf { C K } [ \mathsf { A V G } ] ) = 6$ as long as the input clock jitter specifications are met. That is, the PRECHARGE command at T0 and the ACTIVATE command at $\mathsf { T } 0 + 6$ are valid even if six clocks are less than 15ns due to input clock jitter. 

32. During READs and WRITEs with auto precharge, the DDR3 SDRAM will hold off the internal PRECHARGE command until t RAS (MIN) has been satisfied. 

33. When operating in DLL disable mode, the greater of 5CK or 15ns is satisfied for t WR. 

34. The start of the write recovery time is defined as follows: 

• For BL8 (fixed by MRS or OTF): Rising clock edge four clock cycles after WL 

• For BC4 (OTF): Rising clock edge four clock cycles after WL 

• For BC4 (fixed by MRS): Rising clock edge two clock cycles after WL 

35. RESET# should be LOW as soon as power starts to ramp to ensure the outputs are in High-Z. Until RESET# is LOW, the outputs are at risk of driving and could result in excessive current, depending on bus activity. 

36. The refresh period is $6 4 \mathsf { m s }$ when ${ { \sf T } _ { \mathsf { C } } }$ is less than or equal to $8 5 ^ { \circ } \mathsf { C }$ . This equates to an average refresh rate of $7 . 8 1 2 5 \mu s$ . However, nine REFRESH commands should be asserted at least once every $7 0 . 3 \mu \ s$ . When ${ { \sf T } _ { \mathsf { C } } }$ is greater than ${ 8 5 ^ { \circ } } \mathsf C ,$ the refresh period is 32ms. 

37. Although CKE is allowed to be registered LOW after a REFRESH command when t REFPDEN (MIN) is satisfied, there are cases where additional time such as t XPDLL (MIN) is required. 

38. ODT turn-on time MIN is when the device leaves High-Z and ODT resistance begins to turn on. ODT turn-on time maximum is when the ODT resistance is fully on. The ODT reference load is shown in Figure 24 (page 61). This output load is used for ODT timings (see Figure 31 (page 73)).Designs that were created prior to JEDEC tightening the maximum limit from 9ns to 8.5ns will be allowed to have a 9ns maximum. 

39. Half-clock output parameters must be derated by the actual t ERR10per and t JITdty when input clock jitter is present. This results in each parameter becoming larger. The parameters t ADC (MIN) and tAOF (MIN) are each required to be derated by subtracting both t ERR10per (MAX) and t JITdty (MAX). The parameters t ADC (MAX) and t AOF (MAX) are required to be derated by subtracting both t ERR10per (MAX) and t JITdty (MAX). 

40. ODT turn-off time minimum is when the device starts to turn off ODT resistance. ODT turn-off time maximum is when the DRAM buffer is in High-Z. The ODT reference load is shown in Figure 24 (page 61). This output load is used for ODT timings (see Figure 31 (page 73)). 

41. Pulse width of a input signal is defined as the width between the first crossing of VREF(DC) and the consecutive crossing of VREF(DC). 

42. Should the clock rate be larger than t RFC (MIN), an AUTO REFRESH command should have at least one NOP command between it and another AUTO REFRESH command. Additionally, if the clock rate is slower than 40ns (25 MHz), all REFRESH commands should be followed by a PRECHARGE ALL command. 

43. DRAM devices should be evenly addressed when being accessed. Disproportionate accesses to a particular row address may result in a reduction of REFRESH characteristics or product lifetime. 

44. When two $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ values (and two corresponding $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ values) are listed for a specific speed bin, the user may choose either value for the input AC level. Whichever value is used, the associated setup time for that AC level must also be used. Additionally, one $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ value may be used for address/command inputs and the other $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ value may be used for data inputs. 

For example, for DDR3-800, two input AC levels are defined: $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } 1 7 5 ) , \mathsf { m i n } }$ and $\mathsf { V } _ { | \mathsf { H } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } }$ (corresponding $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C 1 7 5 } ) , \mathsf { m i n } }$ and $\mathsf { V } _ { 1 \mathsf { L } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } } )$ . For DDR3-800, the address/ command inputs must use either $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 7 5 ) , \mathsf { m i n } }$ with t IS(AC175) of 200ps or $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } }$ with t IS(AC150) of 350ps; independently, the data inputs must use either $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 7 5 ) , \mathsf { m i n } }$ with t DS(AC175) of 75ps or $\mathsf { V } _ { { \mathsf { I H } } ( \mathsf { A C } 1 5 0 ) , \mathsf { m i n } }$ with t DS(AC150) of 125ps. 

# Command and Address Setup, Hold, and Derating

The total t IS (setup time) and t IH (hold time) required is calculated by adding the data sheet t IS (base) and $\mathrm { \Delta t H }$ (base) values (see Table 60; values come from the Electrical Characteristics and AC Operating Conditions table) to the $\Delta ^ { \mathrm { t J S } }$ and $\Delta ^ { \mathrm { t } } \mathrm { I H }$ derating values (see Table 61 (page 102), Table 62 (page 102) or Table 63 (page 102)) respectively. Example: t IS (total setup time) $= { } ^ { \mathrm { t } } \mathrm { I S }$ (base) $+ \Delta ^ { \mathrm { t } } \mathrm { I S }$ . For a valid transition, the input signal has to remain above/below $\mathrm { V _ { I H ( A C ) } / V _ { I L ( A C ) } }$ for some time t VAC (see Table 64 (page 103)). 

Although the total setup time for slow slew rates might be negative (for example, a valid input signal will not have reached $\mathrm { V _ { I H ( A C ) } / V _ { I L ( A C ) } }$ at the time of the rising clock transition), a valid input signal is still required to complete the transition and to reach $\mathrm { V _ { I H ( A C ) } / V _ { I L ( A C ) } }$ (see Figure 15 (page 51) for input signal requirements). For slew rates that fall between the values listed in Table 61 (page 102) and Table 63 (page 102), the derating values may be obtained by linear interpolation. 

Setup (t IS) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V _ { R E F ( D C ) } }$ and the first crossing of $ { \mathrm { V } } _ { \mathrm { I H ( A C ) m i n } }$ . Setup (t IS) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of $\mathrm { V _ { R E F ( D C ) } }$ and the first crossing of $\mathrm { V _ { I L ( A C ) m a x } }$ . If the actual signal is always earlier than the nominal slew rate line between the shaded $\mathrm { V _ { R E F ( D C ) } }$ -to-AC region, use the nominal slew rate for derating value (see Figure 34 (page 104)). If the actual signal is later than the nominal slew rate line anywhere between the shaded $\mathrm { V _ { R E F ( D C ) } }$ -to-AC region, the slew rate of a tangent line to the actual signal from the AC level to the DC level is used for derating value (see Figure 36 (page 106)). 

Hold (t IH) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V _ { I L ( D C ) m a x } }$ and the first crossing of VREF(DC). Hold (t IH) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of $ { \mathrm { V } _ { \mathrm { I H ( D C ) m i n } } }$ and the first crossing of $\mathrm { V _ { R E F ( D C ) } }$ . If the actual signal is always later than the nominal slew rate line between the shaded DC-to-VREF(DC) region, use the nominal slew rate for derating value (see Figure 35 (page 105)). If the actual signal is earlier than the nominal slew rate line anywhere between the shaded DC-to-VREF(DC) region, the slew rate of a tangent line to the actual signal from the DC level to the VREF(DC) level is used for derating value (see Figure 37 (page 107)). 


Table 60: DDR3L Command and Address Setup and Hold Values 1 V/ns Referenced – AC/DC-Based


<table><tr><td>Symbol</td><td>800</td><td>1066</td><td>1333</td><td>1600</td><td>1866</td><td>2133</td><td>Unit</td><td>Reference</td></tr><tr><td>tIS(base, AC160)</td><td>215</td><td>140</td><td>80</td><td>60</td><td>-</td><td>-</td><td>ps</td><td>VIH(AC)/VIL(AC)</td></tr><tr><td>tIS(base, AC135)</td><td>365</td><td>290</td><td>205</td><td>185</td><td>65</td><td>60</td><td>ps</td><td>VIH(AC)/VIL(AC)</td></tr><tr><td>tIS(base, AC125)</td><td>-</td><td>-</td><td>-</td><td>-</td><td>150</td><td>135</td><td>ps</td><td>VIH(AC)/VIL(AC)</td></tr><tr><td>tIH(base, DC90)</td><td>285</td><td>210</td><td>150</td><td>130</td><td>110</td><td>105</td><td>ps</td><td>VIH(DC)/VIL(DC)</td></tr></table>


Table 61: DDR3L-800/1066 Derating Values t IS/t IH – AC160/DC90-Based


<table><tr><td colspan="17">ΔtIS, ΔtIH Derating (ps) - AC/DC-Based</td></tr><tr><td rowspan="3">CMD/ADDR Slew Rate V/ns</td><td colspan="16">CK, CK# Differential Slew Rate</td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td colspan="2">1.0 V/ns</td></tr><tr><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td></tr><tr><td>2.0</td><td>80</td><td>45</td><td>80</td><td>45</td><td>80</td><td>45</td><td>88</td><td>53</td><td>96</td><td>61</td><td>104</td><td>69</td><td>112</td><td>79</td><td>120</td><td>95</td></tr><tr><td>1.5</td><td>53</td><td>30</td><td>53</td><td>30</td><td>53</td><td>30</td><td>61</td><td>38</td><td>69</td><td>46</td><td>77</td><td>54</td><td>85</td><td>64</td><td>93</td><td>80</td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td>24</td><td>24</td><td>32</td><td>34</td><td>40</td><td>50</td></tr><tr><td>0.9</td><td>-1</td><td>-3</td><td>-1</td><td>-3</td><td>-1</td><td>-3</td><td>7</td><td>5</td><td>15</td><td>13</td><td>23</td><td>21</td><td>31</td><td>31</td><td>39</td><td>47</td></tr><tr><td>0.8</td><td>-3</td><td>-8</td><td>-3</td><td>-8</td><td>-3</td><td>-8</td><td>5</td><td>1</td><td>13</td><td>9</td><td>21</td><td>17</td><td>29</td><td>27</td><td>37</td><td>43</td></tr><tr><td>0.7</td><td>-5</td><td>-13</td><td>-5</td><td>-13</td><td>-5</td><td>-13</td><td>3</td><td>-5</td><td>11</td><td>3</td><td>19</td><td>11</td><td>27</td><td>21</td><td>35</td><td>37</td></tr><tr><td>0.6</td><td>-8</td><td>-20</td><td>-8</td><td>-20</td><td>-8</td><td>-20</td><td>0</td><td>-12</td><td>8</td><td>-4</td><td>16</td><td>4</td><td>24</td><td>14</td><td>32</td><td>30</td></tr><tr><td>0.5</td><td>-20</td><td>-30</td><td>-20</td><td>-30</td><td>-20</td><td>-30</td><td>-12</td><td>-22</td><td>-4</td><td>-14</td><td>4</td><td>-6</td><td>12</td><td>4</td><td>20</td><td>20</td></tr><tr><td>0.4</td><td>-40</td><td>-45</td><td>-40</td><td>-45</td><td>-40</td><td>-45</td><td>-32</td><td>-37</td><td>-24</td><td>-29</td><td>-16</td><td>-21</td><td>-8</td><td>-11</td><td>0</td><td>5</td></tr></table>


Table 62: DDR3L-800/1066/1333/1600 Derating Values for t IS/t IH – AC135/DC90-Based


<table><tr><td colspan="16">ΔtIS, ΔtIH Derating (ps) - AC/DC-Based</td><td></td></tr><tr><td rowspan="3">CMD/ADDR Slew Rate V/ns</td><td colspan="15">CK, CK# Differential Slew Rate</td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td>1.0 V/ns</td><td></td></tr><tr><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td></tr><tr><td>2.0</td><td>68</td><td>45</td><td>68</td><td>45</td><td>68</td><td>45</td><td>76</td><td>53</td><td>84</td><td>61</td><td>92</td><td>69</td><td>100</td><td>79</td><td>108</td><td>95</td></tr><tr><td>1.5</td><td>45</td><td>30</td><td>45</td><td>30</td><td>45</td><td>30</td><td>53</td><td>38</td><td>61</td><td>46</td><td>69</td><td>54</td><td>77</td><td>64</td><td>85</td><td>80</td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td>24</td><td>24</td><td>32</td><td>34</td><td>40</td><td>50</td></tr><tr><td>0.9</td><td>2</td><td>-3</td><td>2</td><td>-3</td><td>2</td><td>-3</td><td>10</td><td>5</td><td>18</td><td>13</td><td>26</td><td>21</td><td>34</td><td>31</td><td>42</td><td>47</td></tr><tr><td>0.8</td><td>3</td><td>-8</td><td>3</td><td>-8</td><td>3</td><td>-8</td><td>11</td><td>1</td><td>19</td><td>9</td><td>27</td><td>17</td><td>35</td><td>27</td><td>43</td><td>43</td></tr><tr><td>0.7</td><td>6</td><td>-13</td><td>6</td><td>-13</td><td>6</td><td>-13</td><td>14</td><td>-5</td><td>22</td><td>3</td><td>30</td><td>11</td><td>38</td><td>21</td><td>46</td><td>37</td></tr><tr><td>0.6</td><td>9</td><td>-20</td><td>9</td><td>-20</td><td>9</td><td>-20</td><td>17</td><td>-12</td><td>25</td><td>-4</td><td>33</td><td>4</td><td>41</td><td>14</td><td>49</td><td>30</td></tr><tr><td>0.5</td><td>5</td><td>-30</td><td>5</td><td>-30</td><td>5</td><td>-30</td><td>13</td><td>-22</td><td>21</td><td>-14</td><td>29</td><td>-6</td><td>37</td><td>4</td><td>45</td><td>20</td></tr><tr><td>0.4</td><td>-3</td><td>-45</td><td>-3</td><td>-45</td><td>-3</td><td>-45</td><td>6</td><td>-37</td><td>14</td><td>-29</td><td>22</td><td>-21</td><td>30</td><td>-11</td><td>38</td><td>5</td></tr></table>


Table 63: DDR3L-1866/2133 Derating Values for t IS/t IH – AC125/DC90-Based


<table><tr><td colspan="16">ΔtIS, ΔtIH Derating (ps) – AC/DC-Based</td><td></td></tr><tr><td rowspan="3">CMD/ADDR Slew Rate V/ns</td><td colspan="15">CK, CK# Differential Slew Rate</td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td>1.0 V/ns</td><td></td></tr><tr><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td></tr><tr><td>2.0</td><td>63</td><td>45</td><td>63</td><td>45</td><td>63</td><td>45</td><td>71</td><td>53</td><td>79</td><td>61</td><td>87</td><td>69</td><td>95</td><td>79</td><td>103</td><td>95</td></tr><tr><td>1.5</td><td>42</td><td>30</td><td>42</td><td>30</td><td>42</td><td>30</td><td>50</td><td>38</td><td>58</td><td>46</td><td>66</td><td>54</td><td>74</td><td>64</td><td>82</td><td>80</td></tr><tr><td colspan="16">ΔtIS, ΔtIH Derating (ps) - AC/DC-Based</td><td></td></tr><tr><td rowspan="3">CMD/ADDR Slew Rate V/ns</td><td colspan="15">CK, CK# Differential Slew Rate</td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td colspan="2">1.0 V/ns</td></tr><tr><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td><td>ΔtIS</td><td>ΔtIH</td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td>24</td><td>24</td><td>32</td><td>34</td><td>40</td><td>50</td></tr><tr><td>0.9</td><td>3</td><td>-3</td><td>3</td><td>-3</td><td>3</td><td>-3</td><td>11</td><td>5</td><td>19</td><td>13</td><td>27</td><td>21</td><td>35</td><td>31</td><td>43</td><td>47</td></tr><tr><td>0.8</td><td>6</td><td>-8</td><td>6</td><td>-8</td><td>6</td><td>-8</td><td>14</td><td>1</td><td>22</td><td>9</td><td>30</td><td>17</td><td>38</td><td>27</td><td>46</td><td>43</td></tr><tr><td>0.7</td><td>10</td><td>-13</td><td>10</td><td>-13</td><td>10</td><td>-13</td><td>18</td><td>-5</td><td>26</td><td>3</td><td>34</td><td>11</td><td>42</td><td>21</td><td>50</td><td>37</td></tr><tr><td>0.6</td><td>16</td><td>-20</td><td>16</td><td>-20</td><td>16</td><td>-20</td><td>24</td><td>-12</td><td>32</td><td>-4</td><td>40</td><td>4</td><td>48</td><td>14</td><td>56</td><td>30</td></tr><tr><td>0.5</td><td>15</td><td>-30</td><td>15</td><td>-30</td><td>15</td><td>-30</td><td>23</td><td>-22</td><td>31</td><td>-14</td><td>39</td><td>-6</td><td>47</td><td>4</td><td>55</td><td>20</td></tr><tr><td>0.4</td><td>13</td><td>-45</td><td>13</td><td>-45</td><td>13</td><td>-45</td><td>21</td><td>-37</td><td>29</td><td>-29</td><td>37</td><td>-21</td><td>45</td><td>-11</td><td>53</td><td>5</td></tr></table>


Table 64: DDR3L Minimum Required Time t VAC Above $\pmb { \mathsf { v } } _ { \mathsf { I H } ( \pmb { \mathsf { A C } } ) }$ (Below $\mathsf { \mathbf { v } } _ { \mathsf { I L } [ \mathsf { A C } ] } )$ for Valid ADD/CMD Transition


<table><tr><td rowspan="2">Slew Rate (V/ns)</td><td colspan="2">DDR3L-800/1066/1333/1600</td><td colspan="2">DDR3L-1866/2133</td></tr><tr><td>tVAC at 160mV (ps)</td><td>tVAC at 135mV (ps)</td><td>tVAC at 135mV (ps)</td><td>tVAC at 125mV (ps)</td></tr><tr><td>&gt;2.0</td><td>200</td><td>213</td><td>200</td><td>205</td></tr><tr><td>2.0</td><td>200</td><td>213</td><td>200</td><td>205</td></tr><tr><td>1.5</td><td>173</td><td>190</td><td>178</td><td>184</td></tr><tr><td>1.0</td><td>120</td><td>145</td><td>133</td><td>143</td></tr><tr><td>0.9</td><td>102</td><td>130</td><td>118</td><td>129</td></tr><tr><td>0.8</td><td>80</td><td>111</td><td>99</td><td>111</td></tr><tr><td>0.7</td><td>51</td><td>87</td><td>75</td><td>89</td></tr><tr><td>0.6</td><td>13</td><td>55</td><td>43</td><td>59</td></tr><tr><td>0.5</td><td>Note 1</td><td>10</td><td>Note 1</td><td>18</td></tr><tr><td>&lt;0.5</td><td>Note 1</td><td>10</td><td>Note 1</td><td>18</td></tr></table>


Note: 1. Rising input signal shall become equal to or greater than $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ level and Falling input signal shall become equal to or less than $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ level. 



Figure 34: Nominal Slew Rate and t VAC for t IS (Command and Address – Clock)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/4c441325908e6a6d0e7d72b1313a371632e13f029d9cefb5dc0d748b73aebfd8.jpg)



Note: 1. The clock and the strobe are drawn on different time scales.



Figure 35: Nominal Slew Rate for t IH (Command and Address – Clock)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/56f10de8b0e0db0efa7071d6741d765b98bbc13fd3c26c332a4264c1ddee0d7e.jpg)



Note: 1. The clock and the strobe are drawn on different time scales.



Figure 36: Tangent Line for t IS (Command and Address – Clock)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/20688574040e996620034f8bef33d0d9f893023017e0f1d4c035e4e7d1602dff.jpg)



Note: 1. The clock and the strobe are drawn on different time scales.



Figure 37: Tangent Line for t IH (Command and Address – Clock)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/4000531138c8ddaa7b99add0683582fa1baa6a69a4d4cb4f5dbba0739740904e.jpg)


$$
\begin{array}{l} \text {H o l d s l e w r a t e} \\ \text {r i s i n g s i g n a l} \end{array} = \frac {\text {T a n g e n t l i n e} \left(\mathrm {V} _ {\mathrm {R E F} (\mathrm {D C})} - \mathrm {V} _ {\mathrm {I L} (\mathrm {D C}) \max }\right)}{\Delta \mathrm {T R}}
$$

$$
\frac {\text {H o l d s l e w r a t e}}{\text {f a l l i n g s i g n a l}} = \frac {\text {T a n g e n t l i n e} \left(\mathrm {V} _ {\mathrm {I H} (\mathrm {D C}) \min } - \mathrm {V} _ {\mathrm {R E F} (\mathrm {D C})}\right)}{\Delta \mathrm {T F}}
$$


Note: 1. The clock and the strobe are drawn on different time scales.


# Data Setup, Hold, and Derating

The total t DS (setup time) and t DH (hold time) required is calculated by adding the data sheet t DS (base) and t DH (base) values (see Table 65 (page 108); values come from the Electrical Characteristics and AC Operating Conditions table) to the $\Delta { } ^ { \mathrm { t } } \mathrm { D } \mathrm { S }$ and $\Delta _ { \mathrm { \Phi } } ^ { \mathrm { t p H } }$ derating values (see Table 66 (page 109), Table 67 (page 109), or Table 68 (page 110)) respectively. Example: t DS (total setup time) $= { } ^ { \mathrm { t } } \mathrm { D S }$ (base) $+ \Delta { ^ { \mathrm { t } } } \mathrm { D S }$ . For a valid transition, the input signal has to remain above/below $\mathrm { V _ { I H ( A C ) } / V _ { I L ( A C ) } }$ for some time t VAC (see Table 69 (page 111)). 

Although the total setup time for slow slew rates might be negative (for example, a valid input signal will not have reached $\mathrm { V _ { I H ( A C ) } / V _ { I L ( A C ) } } )$ at the time of the rising clock transition), a valid input signal is still required to complete the transition and to reach $\mathrm { V _ { I H } / V _ { I L ( A C ) } }$ . For slew rates that fall between the values listed in Table 66 (page 109), Table 67 (page 109), or Table 68 (page 110), the derating values may obtained by linear interpolation. 

Setup (t DS) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V _ { R E F ( D C ) } }$ and the first crossing of $\mathrm { V _ { I H ( A C ) m i n } }$ . Setup (t DS) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of VREF(DC) and the first crossing of $\mathrm { V _ { I L ( A C ) m a x } }$ . If the actual signal is always earlier than the nominal slew rate line between the shaded $\mathrm { V _ { R E F ( D C ) } }$ -to-AC region, use the nominal slew rate for derating value (see Figure 38 (page 112)). If the actual signal is later than the nominal slew rate line anywhere between the shaded VREF(DC)-to-AC region, the slew rate of a tangent line to the actual signal from the AC level to the DC level is used for derating value (see Figure 40 (page 114)). 

Hold (t DH) nominal slew rate for a rising signal is defined as the slew rate between the last crossing of $\mathrm { V _ { I L ( D C ) m a x } }$ and the first crossing of VREF(DC). Hold (t DH) nominal slew rate for a falling signal is defined as the slew rate between the last crossing of $ { \mathrm { V } _ { \mathrm { I H ( D C ) m i n } } }$ and the first crossing of VREF(DC). If the actual signal is always later than the nominal slew rate line between the shaded DC-to-VREF(DC) region, use the nominal slew rate for derating value (see Figure 39 (page 113)). If the actual signal is earlier than the nominal slew rate line anywhere between the shaded DC-to-VREF(DC) region, the slew rate of a tangent line to the actual signal from the DC-to-VREF(DC) region is used for derating value (see Figure 41 (page 115)). 


Table 65: DDR3L Data Setup and Hold Values at 1 V/ns (DQS, DQS# at 2 V/ns) – AC/DC-Based


<table><tr><td>Symbol</td><td>800</td><td>1066</td><td>1333</td><td>1600</td><td>1866</td><td>2133</td><td>Unit</td><td>Reference</td></tr><tr><td>tDS (base) AC160</td><td>90</td><td>40</td><td>-</td><td>-</td><td>-</td><td>-</td><td>ps</td><td rowspan="5">VIH(AC)/VIL(AC)</td></tr><tr><td>tDS (base) AC135</td><td>140</td><td>90</td><td>45</td><td>25</td><td>-</td><td>-</td><td>ps</td></tr><tr><td>tDS (base) AC130</td><td>-</td><td>-</td><td>-</td><td>-</td><td>70</td><td>55</td><td>ps</td></tr><tr><td>tDH (base) DC90</td><td>160</td><td>110</td><td>75</td><td>55</td><td>-</td><td>-</td><td>ps</td></tr><tr><td>tDH (base) DC90</td><td>-</td><td>-</td><td>-</td><td>-</td><td>75</td><td>60</td><td>ps</td></tr><tr><td>Slew Rate Referenced</td><td>1</td><td>1</td><td>1</td><td>1</td><td>2</td><td>2</td><td>V/ns</td><td></td></tr></table>


Table 66: DDR3L Derating Values for t DS/t DH – AC160/DC90-Based


<table><tr><td colspan="16">ΔtDS, ΔtdH Derating (ps) - AC/DC-Based</td><td></td></tr><tr><td rowspan="3">DQ Slew Rate V/ns</td><td colspan="15">DQS, DQS# Differential Slew Rate</td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td>1.0 V/ns</td><td></td></tr><tr><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td></tr><tr><td>2.0</td><td>80</td><td>45</td><td>80</td><td>45</td><td>80</td><td>45</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>1.5</td><td>53</td><td>30</td><td>53</td><td>30</td><td>53</td><td>30</td><td>61</td><td>38</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>0.9</td><td></td><td></td><td>-1</td><td>-3</td><td>-1</td><td>-3</td><td>7</td><td>5</td><td>15</td><td>13</td><td>23</td><td>21</td><td></td><td></td><td></td><td></td></tr><tr><td>0.8</td><td></td><td></td><td></td><td></td><td>-3</td><td>-8</td><td>5</td><td>1</td><td>13</td><td>9</td><td>21</td><td>17</td><td>29</td><td>27</td><td></td><td></td></tr><tr><td>0.7</td><td></td><td></td><td></td><td></td><td></td><td></td><td>-3</td><td>-5</td><td>11</td><td>3</td><td>19</td><td>11</td><td>27</td><td>21</td><td>35</td><td>37</td></tr><tr><td>0.6</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>8</td><td>-4</td><td>16</td><td>4</td><td>24</td><td>14</td><td>32</td><td>30</td></tr><tr><td>0.5</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>4</td><td>6</td><td>12</td><td>4</td><td>20</td><td>20</td></tr><tr><td>0.4</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>-8</td><td>-11</td><td>0</td><td>5</td></tr></table>


Table 67: DDR3L Derating Values for t DS/t DH – AC135/DC90-Based


<table><tr><td colspan="16">ΔtDS, ΔtDH Derating (ps) - AC/DC-Based</td><td></td></tr><tr><td rowspan="3">DQ Slew Rate V/ns</td><td colspan="15">DQS, DQS# Differential Slew Rate</td><td></td></tr><tr><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td>1.0 V/ns</td><td></td></tr><tr><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td><td>ΔtDS</td><td>ΔtDH</td></tr><tr><td>2.0</td><td>68</td><td>45</td><td>68</td><td>45</td><td>68</td><td>45</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>1.5</td><td>45</td><td>30</td><td>45</td><td>30</td><td>45</td><td>30</td><td>53</td><td>38</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>1.0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>8</td><td>8</td><td>16</td><td>16</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>0.9</td><td></td><td></td><td>2</td><td>-3</td><td>2</td><td>-3</td><td>10</td><td>5</td><td>18</td><td>13</td><td>26</td><td>21</td><td></td><td></td><td></td><td></td></tr><tr><td>0.8</td><td></td><td></td><td></td><td></td><td>3</td><td>-8</td><td>11</td><td>1</td><td>19</td><td>9</td><td>27</td><td>17</td><td>35</td><td>27</td><td></td><td></td></tr><tr><td>0.7</td><td></td><td></td><td></td><td></td><td></td><td></td><td>14</td><td>-5</td><td>22</td><td>3</td><td>30</td><td>11</td><td>38</td><td>21</td><td>46</td><td>37</td></tr><tr><td>0.6</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>25</td><td>-4</td><td>33</td><td>4</td><td>41</td><td>14</td><td>49</td><td>30</td></tr><tr><td>0.5</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>39</td><td>-6</td><td>37</td><td>4</td><td>45</td><td>20</td></tr><tr><td>0.4</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>30</td><td>-11</td><td>38</td><td>5</td></tr></table>


Table 68: DDR3L Derati ng Val ues for tDS/tDH – AC1 30/DC90-Based at 2V/ns


S h a d ed ce l l s i n d i cate s l ew rate co m b i n at i o n s n ot s u p po rted 

<table><tr><td colspan="25">\( \Delta^tDS, \Delta^tDH Derating (ps) - AC/DC-Based \)</td><td></td><td></td></tr><tr><td rowspan="3">DQ Slew Rate V/ns</td><td colspan="24">DQS, DQS# Differential Slew Rate</td><td></td><td></td></tr><tr><td colspan="2">8.0 V/ns</td><td colspan="2">7.0 V/ns</td><td colspan="2">6.0 V/ns</td><td colspan="2">5.0 V/ns</td><td colspan="2">4.0 V/ns</td><td colspan="2">3.0 V/ns</td><td colspan="2">2.0 V/ns</td><td colspan="2">1.8 V/ns</td><td colspan="2">1.6 V/ns</td><td colspan="2">1.4 V/ns</td><td colspan="2">1.2 V/ns</td><td colspan="2">1.0 V/ns</td><td></td><td></td></tr><tr><td>\( \Delta {}^{t}{}_{\text{DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{DH }} \)</td><td>\( \Delta {}^{t}{}_{\text{DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DH}} \)</td><td>\( \Delta {}^{t}{}_{DS} \)</td><td>\( \Delta {}^{t}{}_{\text{:DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DH}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DS}} \)</td><td>\( \Delta {}^{t}{}_{\text{:DH}} \)</td></tr><tr><td>4.0</td><td>33</td><td>23</td><td>33</td><td>23</td><td>33</td><td>23</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>3.5</td><td>28</td><td>19</td><td>28</td><td>19</td><td>28</td><td>19</td><td>28</td><td>19</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>3.0</td><td>22</td><td>15</td><td>22</td><td>15</td><td>22</td><td>15</td><td>22</td><td>15</td><td>22</td><td>15</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>2.5</td><td></td><td></td><td>13</td><td>9</td><td>13</td><td>9</td><td>13</td><td>9</td><td>13</td><td>9</td><td>13</td><td>9</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>2.0</td><td></td><td></td><td></td><td></td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>1.5</td><td></td><td></td><td></td><td></td><td></td><td></td><td>-22</td><td>-15</td><td>-22</td><td>-15</td><td>-22</td><td>-15</td><td>-22</td><td>-15</td><td>-14</td><td>-7</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>1.0</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>-65</td><td>-45</td><td>-65</td><td>-45</td><td>-65</td><td>-45</td><td>-57</td><td>-37</td><td>-49</td><td>-29</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>0.9</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>-62</td><td>-48</td><td>-62</td><td>-48</td><td>-54</td><td>-40</td><td>-46</td><td>-32</td><td>-38</td><td>-24</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>0.8</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>-61</td><td>-53</td><td>-53</td><td>-45</td><td>-45</td><td>-37</td><td>-37</td><td>-29</td><td>-29</td><td>-19</td><td></td><td></td><td></td><td></td></tr><tr><td>0.7</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>-49</td><td>-50</td><td>-41</td><td>-42</td><td>-33</td><td>-34</td><td>-25</td><td>-24</td><td>-17</td><td>-8</td><td></td><td></td></tr><tr><td>0.6</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>-37</td><td>-49</td><td>-29</td><td>-41</td><td>-21</td><td>-31</td><td>-13</td><td>-15</td><td></td><td></td></tr><tr><td>0.5</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>-31</td><td>-51</td><td>-23</td><td>-41</td><td>-15</td><td>-25</td><td></td><td></td></tr><tr><td>0.4</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>-28</td><td>-56</td><td>-20</td><td>-40</td><td></td><td></td></tr></table>


Table 69: DDR3L Minimum Required Time t VAC Above $\mathsf { \pmb { v } } _ { \mathsf { I H } ( \mathsf { A C } ) }$ (Below ${ \pmb v } _ { \mathrm { { I L ( A C ) } } }$ for Valid DQ Transition


<table><tr><td>Slew Rate (V/ns)</td><td>DDR3L-800/1066 160mV (ps) min</td><td>DDR3L-800/1066/1333 135mV (ps) min</td><td>DDR3L-1866/2133 130mV (ps) min</td></tr><tr><td>&gt;2.0</td><td>165</td><td>113</td><td>95</td></tr><tr><td>2.0</td><td>165</td><td>113</td><td>95</td></tr><tr><td>1.5</td><td>138</td><td>90</td><td>73</td></tr><tr><td>1.0</td><td>85</td><td>45</td><td>30</td></tr><tr><td>0.9</td><td>67</td><td>30</td><td>16</td></tr><tr><td>0.8</td><td>45</td><td>11</td><td>Note 1</td></tr><tr><td>0.7</td><td>16</td><td>Note 1</td><td>-</td></tr><tr><td>0.6</td><td>Note 1</td><td>Note 1</td><td>-</td></tr><tr><td>0.5</td><td>Note 1</td><td>Note 1</td><td>-</td></tr><tr><td>&lt;0.5</td><td>Note 1</td><td>Note 1</td><td>-</td></tr></table>


Note: 1. Rising input signal shall become equal to or greater than $\mathsf { V } _ { \mathsf { I H } ( \mathsf { A C } ) }$ level and Falling input signal shall become equal to or less than $\mathsf { V } _ { \mathsf { I L } ( \mathsf { A C } ) }$ level. 



Figure 38: Nominal Slew Rate and t VAC for t DS (DQ – Strobe)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/28da5db048e2a414776a6b5d6d3458aef0e323215bc210e1f4c05a55fd0c523e.jpg)



Note: 1. The clock and the strobe are drawn on different time scales.



Figure 39: Nominal Slew Rate for t DH (DQ – Strobe)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/70f44f5e066b1f3d9449bccf4a29f1a4313f31bd152d3ec0fa46069c63b4f603.jpg)



Note: 1. The clock and the strobe are drawn on different time scales.



Figure 40: Tangent Line for t DS (DQ – Strobe)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/ab4d4ee0de4e502f94431cc882188e0ff2f19f261ab7576755e364a420e88cc3.jpg)



Note: 1. The clock and the strobe are drawn on different time scales.



Figure 41: Tangent Line for t DH (DQ – Strobe)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/b9288a2b98d1e9d66f44a0691588c685bc595db32dd5c50e24b14429a84371f7.jpg)


$$
\begin{array}{l} \text {H o l d s l e w r a t e} \\ \text {r i s i n g s i g n a l} \end{array} = \frac {\text {T a n g e n t l i n e} \left(\mathrm {V} _ {\mathrm {R E F (D C)}} - \mathrm {V} _ {\mathrm {I L (D C) m a x}}\right)}{\Delta \mathrm {T R}}
$$

$$
\begin{array}{l} \text {H o l d s l e w r a t e} \\ \text {f a l l i n g s i g n a l} \end{array} = \frac {\text {T a n g e n t l i n e (V _ {I H (D C) m i n} - V _ {R E F (D C)})}}{\Delta T F}
$$


Note: 1. The clock and the strobe are drawn on different time scales.


# Commands – Truth Tables


Table 70: Truth Table – Command



Notes 1–5 apply to the entire table


<table><tr><td rowspan="2" colspan="2">Function</td><td rowspan="2">Symbol</td><td colspan="2">CKE</td><td rowspan="2">CS#</td><td rowspan="2">RAS#</td><td rowspan="2">CAS#</td><td rowspan="2">WE#</td><td rowspan="2">BA[2:0]</td><td rowspan="2">An</td><td rowspan="2">A12</td><td rowspan="2">A10</td><td rowspan="2">A[11,9:0]</td><td rowspan="2">Notes</td></tr><tr><td>Prev Cycle</td><td>Next Cycle</td></tr><tr><td colspan="2">MODE REGISTER SET</td><td>MRS</td><td>H</td><td>H</td><td>L</td><td>L</td><td>L</td><td>L</td><td>BA</td><td colspan="4">OP code</td><td></td></tr><tr><td colspan="2">REFRESH</td><td>REF</td><td>H</td><td>H</td><td>L</td><td>L</td><td>L</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td><td></td></tr><tr><td colspan="2">Self refresh entry</td><td>SRE</td><td>H</td><td>L</td><td>L</td><td>L</td><td>L</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td><td>6</td></tr><tr><td rowspan="2" colspan="2">Self refresh exit</td><td rowspan="2">SRX</td><td rowspan="2">L</td><td rowspan="2">H</td><td>H</td><td>V</td><td>V</td><td>V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">6,7</td></tr><tr><td>L</td><td>H</td><td>H</td><td>H</td></tr><tr><td colspan="2">Single-bank PRECHARGE</td><td>PRE</td><td>H</td><td>H</td><td>L</td><td>L</td><td>H</td><td>L</td><td>BA</td><td>V</td><td>V</td><td>L</td><td>V</td><td></td></tr><tr><td colspan="2">PRECHARGE all banks</td><td>PREA</td><td>H</td><td>H</td><td>L</td><td>L</td><td>H</td><td>L</td><td>V</td><td></td><td>V</td><td>H</td><td>V</td><td></td></tr><tr><td colspan="2">Bank ACTIVATE</td><td>ACT</td><td>H</td><td>H</td><td>L</td><td>L</td><td>H</td><td>H</td><td>BA</td><td colspan="4">Row address (RA)</td><td></td></tr><tr><td rowspan="3">WRITE</td><td>BL8MRS,BC4MRS</td><td>WR</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>V</td><td>L</td><td>CA</td><td>8</td></tr><tr><td>BC4OTF</td><td>WRS4</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>L</td><td>L</td><td>CA</td><td>8</td></tr><tr><td>BL8OTF</td><td>WRS8</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>H</td><td>L</td><td>CA</td><td>8</td></tr><tr><td rowspan="3">WRITEwith auto precharge</td><td>BL8MRS,BC4MRS</td><td>WRAP</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>V</td><td>H</td><td>CA</td><td>8</td></tr><tr><td>BC4OTF</td><td>WRAPS4</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>L</td><td>H</td><td>CA</td><td>8</td></tr><tr><td>BL8OTF</td><td>WRAPS8</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>H</td><td>H</td><td>CA</td><td>8</td></tr><tr><td rowspan="3">READ</td><td>BL8MRS,BC4MRS</td><td>RD</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>V</td><td>L</td><td>CA</td><td>8</td></tr><tr><td>BC4OTF</td><td>RDS4</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>L</td><td>L</td><td>CA</td><td>8</td></tr><tr><td>BL8OTF</td><td>RDS8</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>H</td><td>L</td><td>CA</td><td>8</td></tr><tr><td rowspan="3">READwith auto precharge</td><td>BL8MRS,BC4MRS</td><td>RDAP</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>V</td><td>H</td><td>CA</td><td>8</td></tr><tr><td>BC4OTF</td><td>RDAPS4</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>L</td><td>H</td><td>CA</td><td>8</td></tr><tr><td>BL8OTF</td><td>RDAPS8</td><td>H</td><td>H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>H</td><td>H</td><td>CA</td><td>8</td></tr><tr><td colspan="2">NO OPERATION</td><td>NOP</td><td>H</td><td>H</td><td>L</td><td>H</td><td>H</td><td>H</td><td>V</td><td>V</td><td>V</td><td>V</td><td>V</td><td>9</td></tr><tr><td colspan="2">Device DESELECTED</td><td>DES</td><td>H</td><td>H</td><td>H</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>10</td></tr><tr><td rowspan="2" colspan="2">Power-down entry</td><td rowspan="2">PDE</td><td rowspan="2">H</td><td rowspan="2">L</td><td>L</td><td>H</td><td>H</td><td>H</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">6</td></tr><tr><td>H</td><td>V</td><td>V</td><td>V</td></tr><tr><td rowspan="2" colspan="2">Power-down exit</td><td rowspan="2">PDX</td><td rowspan="2">L</td><td rowspan="2">H</td><td>L</td><td>H</td><td>H</td><td>H</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">V</td><td rowspan="2">6, 11</td></tr><tr><td>H</td><td>V</td><td>V</td><td>V</td></tr><tr><td colspan="2">ZQ CALIBRATION LONG</td><td>ZQCL</td><td>H</td><td>H</td><td>L</td><td>H</td><td>H</td><td>L</td><td>X</td><td>X</td><td>X</td><td>H</td><td>X</td><td>12</td></tr><tr><td colspan="2">ZQ CALIBRATION SHORT</td><td>ZQCS</td><td>H</td><td>H</td><td>L</td><td>H</td><td>H</td><td>L</td><td>X</td><td>X</td><td>X</td><td>L</td><td>X</td><td></td></tr></table>


Notes: 1. Commands are defined by the states of CS#, RAS#, CAS#, WE#, and CKE at the rising edge of the clock. The MSB of BA, RA, and CA are device-, density-, and configurationdependent. 


2. RESET# is enabled LOW and used only for asynchronous reset. Thus, RESET# must be held HIGH during any normal operation. 

3. The state of ODT does not affect the states described in this table. 

4. Operations apply to the bank defined by the bank address. For MRS, BA selects one of four mode registers. 

5. “V” means $" \mathsf { H } ^ { \prime \prime }$ or “L” (a defined logic level), and “X” means “Don’t Care.” 

6. See Table 71 (page 118) for additional information on CKE transition. 

7. Self refresh exit is asynchronous. 

8. Burst READs or WRITEs cannot be terminated or interrupted. MRS (fixed) and OTF BL/BC are defined in MR0. 

9. The purpose of the NOP command is to prevent the DRAM from registering any unwanted commands. A NOP will not terminate an operation that is executing. 

10. The DES and NOP commands perform similarly. 

11. The power-down mode does not perform any REFRESH operations. 

12. ZQ CALIBRATION LONG is used for either ZQinit (first ZQCL command during initialization) or ZQoper (ZQCL command after initialization). 


Table 71: Truth Table – CKE



Notes 1–2 apply to the entire table; see Table 70 (page 116) for additional command details


<table><tr><td rowspan="2">Current State3</td><td colspan="2">CKE</td><td rowspan="2">Command5(RAS#, CAS#, WE#, CS#)</td><td rowspan="2">Action5</td><td rowspan="2">Notes</td></tr><tr><td>Previous Cycle4(n - 1)</td><td>Present Cycle4(n)</td></tr><tr><td rowspan="2">Power-down</td><td>L</td><td>L</td><td>&quot;Don&#x27;t Care&quot;</td><td>Maintain power-down</td><td></td></tr><tr><td>L</td><td>H</td><td>DES or NOP</td><td>Power-down exit</td><td></td></tr><tr><td rowspan="2">Self refresh</td><td>L</td><td>L</td><td>&quot;Don&#x27;t Care&quot;</td><td>Maintain self refresh</td><td></td></tr><tr><td>L</td><td>H</td><td>DES or NOP</td><td>Self refresh exit</td><td></td></tr><tr><td>Bank(s) active</td><td>H</td><td>L</td><td>DES or NOP</td><td>Active power-down entry</td><td></td></tr><tr><td>Reading</td><td>H</td><td>L</td><td>DES or NOP</td><td>Power-down entry</td><td></td></tr><tr><td>Writing</td><td>H</td><td>L</td><td>DES or NOP</td><td>Power-down entry</td><td></td></tr><tr><td>Precharging</td><td>H</td><td>L</td><td>DES or NOP</td><td>Power-down entry</td><td></td></tr><tr><td>Refreshing</td><td>H</td><td>L</td><td>DES or NOP</td><td>Precharge power-down entry</td><td></td></tr><tr><td rowspan="2">All banks idle</td><td>H</td><td>L</td><td>DES or NOP</td><td>Precharge power-down entry</td><td rowspan="2">6</td></tr><tr><td>H</td><td>L</td><td>REFRESH</td><td>Self refresh</td></tr></table>

Notes: 1. All states and sequences not shown are illegal or reserved unless explicitly described elsewhere in this document. 

2. t CKE (MIN) means CKE must be registered at multiple consecutive positive clock edges. CKE must remain at the valid input level the entire time it takes to achieve the required number of registration clocks. Thus, after any CKE transition, CKE may not transition from its valid level during the time period of $^ { \mathrm { t } } | \mathsf { S } + ^ { \mathrm { t } } \mathsf { C K E } \left( \mathsf { M } | \mathsf { N } \right) + ^ { \mathrm { t } } | \mathsf { H }$ 

3. Current state $=$ The state of the DRAM immediately prior to clock edge n. 

4. CKE (n) is the logic state of CKE at clock edge $n _ { \iota }$ CKE $( n - 1 )$ was the state of CKE at the previous clock edge. 

5. COMMAND is the command registered at the clock edge (must be a legal command as defined in Table 70 (page 116)). Action is a result of COMMAND. ODT does not affect the states described in this table and is not listed. 

6. Idle state $=$ All banks are closed, no data bursts are in progress, CKE is HIGH, and all timings from previous operations are satisfied. All self refresh exit and power-down exit parameters are also satisfied. 

# Commands

# DESELECT

The DESELT (DES) command (CS# HIGH) prevents new commands from being executed by the DRAM. Operations already in progress are not affected. 

# NO OPERATION

The NO OPERATION (NOP) command (CS# LOW) prevents unwanted commands from being registered during idle or wait states. Operations already in progress are not affected. 

# ZQ CALIBRATION LONG

The ZQ CALIBRATION LONG (ZQCL) command is used to perform the initial calibration during a power-up initialization and reset sequence (see Figure 50 (page 135)). This command may be issued at any time by the controller, depending on the system environment. The ZQCL command triggers the calibration engine inside the DRAM. After calibration is achieved, the calibrated values are transferred from the calibration engine to the DRAM I/O, which are reflected as updated $\operatorname { R o n }$ and ODT values. 

The DRAM is allowed a timing window defined by either t ZQinit or t ZQoper to perform a full calibration and transfer of values. When ZQCL is issued during the initialization sequence, the timing parameter t ZQinit must be satisfied. When initialization is complete, subsequent ZQCL commands require the timing parameter t ZQoper to be satisfied. 

# ZQ CALIBRATION SHORT

The ZQ CALIBRATION SHORT (ZQCS) command is used to perform periodic calibrations to account for small voltage and temperature variations. A shorter timing window is provided to perform the reduced calibration and transfer of values as defined by timing parameter t ZQCS. A ZQCS command can effectively correct a minimum of $0 . 5 \%$ RON and $\mathrm { R } _ { \mathrm { T T } }$ impedance error within 64 clock cycles, assuming the maximum sensitivities specified in DDR3L 34 Ohm Output Driver Sensitivity (page 67). 

# ACTIVATE

The ACTIVATE command is used to open (or activate) a row in a particular bank for a subsequent access. The value on the BA[2:0] inputs selects the bank, and the address provided on inputs A[n:0] selects the row. This row remains open (or active) for accesses until a PRECHARGE command is issued to that bank. 

A PRECHARGE command must be issued before opening a different row in the same bank. 

# READ

The READ command is used to initiate a burst read access to an active row. The address provided on inputs A[2:0] selects the starting column address, depending on the burst length and burst type selected (see Burst Order table for additional information). The value on input A10 determines whether auto precharge is used. If auto precharge is selected, the row being accessed will be precharged at the end of the READ burst. If auto 

precharge is not selected, the row will remain open for subsequent accesses. The value on input A12 (if enabled in the mode register) when the READ command is issued determines whether BC4 (chop) or BL8 is used. After a READ command is issued, the READ burst may not be interrupted. 


Table 72: READ Command Summary


<table><tr><td rowspan="2" colspan="2">Function</td><td rowspan="2">Symbol</td><td colspan="2">CKE</td><td rowspan="2">CS#</td><td rowspan="2">RAS#</td><td rowspan="2">CAS#</td><td rowspan="2">WE#</td><td rowspan="2">BA[2:0]</td><td rowspan="2">An</td><td rowspan="2">A12</td><td rowspan="2">A10</td><td rowspan="2">A[11,9:0]</td></tr><tr><td>Prev Cycle</td><td>Next Cycle</td></tr><tr><td rowspan="3">READ</td><td>BL8MRS, BC4MRS</td><td>RD</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>V</td><td>L</td><td>CA</td></tr><tr><td>BC4OTF</td><td>RDS4</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>L</td><td>L</td><td>CA</td></tr><tr><td>BL8OTF</td><td>RDS8</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>H</td><td>L</td><td>CA</td></tr><tr><td rowspan="3">READ with auto precharge</td><td>BL8MRS, BC4MRS</td><td>RDAP</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>V</td><td>H</td><td>CA</td></tr><tr><td>BC4OTF</td><td>RDAPS4</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>L</td><td>H</td><td>CA</td></tr><tr><td>BL8OTF</td><td>RDAPS8</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>H</td><td>BA</td><td>RFU</td><td>H</td><td>H</td><td>CA</td></tr></table>

# WRITE

The WRITE command is used to initiate a burst write access to an active row. The value on the BA[2:0] inputs selects the bank. The value on input A10 determines whether auto precharge is used. The value on input A12 (if enabled in the MR) when the WRITE command is issued determines whether BC4 (chop) or BL8 is used. 

Input data appearing on the DQ is written to the memory array subject to the DM input logic level appearing coincident with the data. If a given DM signal is registered LOW, the corresponding data will be written to memory. If the DM signal is registered HIGH, the corresponding data inputs will be ignored and a WRITE will not be executed to that byte/column location. 


Table 73: WRITE Command Summary


<table><tr><td rowspan="2" colspan="2">Function</td><td rowspan="2">Symbol</td><td colspan="2">CKE</td><td rowspan="2">CS#</td><td rowspan="2">RAS#</td><td rowspan="2">CAS#</td><td rowspan="2">WE#</td><td rowspan="2">BA[2:0]</td><td rowspan="2">An</td><td rowspan="2">A12</td><td rowspan="2">A10</td><td rowspan="2">A[11,9:0]</td></tr><tr><td>Prev Cycle</td><td>Next Cycle</td></tr><tr><td rowspan="3">WRITE</td><td>BL8MRS, BC4MRS</td><td>WR</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>V</td><td>L</td><td>CA</td></tr><tr><td>BC4OTF</td><td>WRS4</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>L</td><td>L</td><td>CA</td></tr><tr><td>BL8OTF</td><td>WRS8</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>H</td><td>L</td><td>CA</td></tr><tr><td rowspan="3">WRITE with auto precharge</td><td>BL8MRS, BC4MRS</td><td>WRAP</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>V</td><td>H</td><td>CA</td></tr><tr><td>BC4OTF</td><td>WRAPS4</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>L</td><td>H</td><td>CA</td></tr><tr><td>BL8OTF</td><td>WRAPS8</td><td colspan="2">H</td><td>L</td><td>H</td><td>L</td><td>L</td><td>BA</td><td>RFU</td><td>H</td><td>H</td><td>CA</td></tr></table>

# PRECHARGE

The PRECHARGE command is used to de-activate the open row in a particular bank or in all banks. The bank(s) are available for a subsequent row access a specified time (t RP) after the PRECHARGE command is issued, except in the case of concurrent auto precharge. A READ or WRITE command to a different bank is allowed during a concurrent auto precharge as long as it does not interrupt the data transfer in the current bank and does not violate any other timing parameters. Input A10 determines whether one or all banks are precharged. In the case where only one bank is precharged, inputs BA[2:0] select the bank; otherwise, BA[2:0] are treated as “Don’t Care.” 

After a bank is precharged, it is in the idle state and must be activated prior to any READ or WRITE commands being issued to that bank. A PRECHARGE command is treated as a NOP if there is no open row in that bank (idle state) or if the previously open row is already in the process of precharging. However, the precharge period is determined by the last PRECHARGE command issued to the bank. 

# REFRESH

The REFRESH command is used during normal operation of the DRAM and is analogous to CAS#-before-RAS# (CBR) refresh or auto refresh. This command is nonpersistent, so it must be issued each time a refresh is required. The addressing is generated by the internal refresh controller. This makes the address bits a “Don’t Care” during a RE-FRESH command. The DRAM requires REFRESH cycles at an average interval of 7.8μs (maximum when $\mathrm { T _ { C } } { \le } 8 5 ^ { \circ } \mathrm { C }$ or 3.9μs maximum when $\mathrm { T } _ { \mathrm { C } } { \leq } 9 5 ^ { \circ } \mathrm { C } )$ . The REFRESH period begins when the REFRESH command is registered and ends t RFC (MIN) later. 

To allow for improved efficiency in scheduling and switching between tasks, some flexibility in the absolute refresh interval is provided. A maximum of eight REFRESH commands can be posted to any given DRAM, meaning that the maximum absolute interval between any REFRESH command and the next REFRESH command is nine times the maximum average interval refresh rate. Self refresh may be entered with up to eight RE-FRESH commands being posted. After exiting self refresh (when entered with posted REFRESH commands), additional posting of REFRESH commands is allowed to the extent that the maximum number of cumulative posted REFRESH commands (both preand post-self refresh) does not exceed eight REFRESH commands. 

At any given time, a maximum of 16 REFRESH commands can be issued within $2 \mathbf { x }$ t REFI. 


Figure 42: Refresh Mode


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/24fa33b2e84a1e183acc22fb5bde45a021180686a368d243c4bc73eb9ddf1926.jpg)


Notes: 1. NOP commands are shown for ease of illustration; other valid commands may be possible at these times. CKE must be active during the PRECHARGE, ACTIVATE, and REFRESH commands, but may be inactive at other times (see Power-Down Mode (page 185)). 

2. The second REFRESH is not required, but two back-to-back REFRESH commands are shown. 

3. “Don’t Care” if A10 is HIGH at this point; however, A10 must be HIGH if more than one bank is active (must precharge all active banks). 

4. For operations shown, DM, DQ, and DQS signals are all “Don’t Care”/High-Z. 

5. Only NOP and DES commands are allowed after a REFRESH command and until t RFC (MIN) is satisfied. 

# SELF REFRESH

The SELF REFRESH command is used to retain data in the DRAM, even if the rest of the system is powered down. When in self refresh mode, the DRAM retains data without external clocking. Self refresh mode is also a convenient method used to enable/disable the DLL as well as to change the clock frequency within the allowed synchronous operating range (see Input Clock Frequency Change (page 127)). All power supply inputs (including VREFCA and $\mathrm { V _ { R E F D Q } } )$ ) must be maintained at valid levels upon entry/exit and during self refresh mode operation. $\mathrm { V _ { R E F D Q } }$ may float or not drive $\mathrm { V _ { D D Q } } / 2$ while in self refresh mode under the following conditions: 

• $\mathrm { V _ { S S } { < V _ { R E F D Q } < V _ { D D } } }$ is maintained 

• VREFDQ is valid and stable prior to CKE going back HIGH 

• The first WRITE operation may not occur earlier than 512 clocks after V REFDQ is valid 

• All other self refresh mode exit timing requirements are met 

# DLL Disable Mode

If the DLL is disabled by the mode register (MR1[0] can be switched during initialization or later), the DRAM is targeted, but not guaranteed, to operate similarly to the normal mode, with a few notable exceptions: 

• The DRAM supports only one value of CAS latency $\mathrm { { ( C L = 6 } }$ ) and one value of CAS WRITE latency $( \mathrm { C W L } = 6 )$ ). 

• DLL disable mode affects the read data clock-to-data strobe relationship (t DQSCK), but not the read data-to-data strobe relationship (t DQSQ, t QH). Special attention is required to line up the read data with the controller time domain when the DLL is disabled. 

• In normal operation (DLL on), t DQSCK starts from the rising clock edge $\mathrm { A L + C L }$ cycles after the READ command. In DLL disable mode, t DQSCK starts $\mathrm { A L + C L - 1 }$ cycles after the READ command. Additionally, with the DLL disabled, the value of t DQSCK could be larger than t CK. 

The ODT feature (including dynamic ODT) is not supported during DLL disable mode. The ODT resistors must be disabled by continuously registering the ODT ball LOW by programming RTT,nom MR1[9, 6, 2] and RTT(WR) MR2[10, 9] to 0 while in the DLL disable mode. 

Specific steps must be followed to switch between the DLL enable and DLL disable modes due to a gap in the allowed clock rates between the two modes (t CK [AVG] MAX and $^ \mathrm { t } \mathrm { C K }$ [DLL_DIS] MIN, respectively). The only time the clock is allowed to cross this clock rate gap is during self refresh mode. Thus, the required procedure for switching from the DLL enable mode to the DLL disable mode is to change frequency during self refresh: 

1. Starting from the idle state (all banks are precharged, all timings are fulfilled, ODT is turned off, and $\mathrm { R _ { T T , n o m } }$ and $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ are High-Z), set MR1[0] to 1 to disable the DLL 

2. Enter self refresh mode after t MOD has been satisfied. 

3. After t CKSRE is satisfied, change the frequency to the desired clock rate. 

4. Self refresh may be exited when the clock is stable with the new frequency for t CKSRX. After t XS is satisfied, update the mode registers with appropriate values. 

5. The DRAM will be ready for its next command in the DLL disable mode after the greater of t MRD or t MOD has been satisfied. A ZQCL command should be issued with appropriate timings met. 


Figure 43: DLL Enable Mode to DLL Disable Mode


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/14c8bbada8372467fcb75ede9e8972ed846b557bb68bd072700f4426a838eb4f.jpg)


Notes: 1. Any valid command. 

2. Disable DLL by setting MR1[0] to 1. 

3. Enter SELF REFRESH. 

4. Exit SELF REFRESH. 

5. Update the mode registers with the DLL disable parameters setting. 

6. Starting with the idle state, $\mathsf { R } _ { \mathsf { T T } }$ is in the High-Z state. 

7. Change frequency. 

8. Clock must be stable t CKSRX. 

9. Static LOW in the case that $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ or $\mathsf { R } _ { \mathsf { T T } ( \mathsf { W R } ) }$ is enabled; otherwise, static LOW or HIGH. 

A similar procedure is required for switching from the DLL disable mode back to the DLL enable mode. This also requires changing the frequency during self refresh mode (see Figure 44 (page 125)). 

1. Starting from the idle state (all banks are precharged, all timings are fulfilled, ODT is turned off, and $\mathrm { R _ { T T , n o m } }$ and $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ are High-Z), enter self refresh mode. 

2. After t CKSRE is satisfied, change the frequency to the new clock rate. 

3. Self refresh may be exited when the clock is stable with the new frequency for t CKSRX. After t XS is satisfied, update the mode registers with the appropriate values. At a minimum, set MR1[0] to 0 to enable the DLL. Wait t MRD, then set MR0[8] to 1 to enable DLL RESET. 

4. After another t MRD delay is satisfied, update the remaining mode registers with the appropriate values. 

5. The DRAM will be ready for its next command in the DLL enable mode after the greater of t MRD or t MOD has been satisfied. However, before applying any command or function requiring a locked DLL, a delay of t DLLK after DLL RESET must be satisfied. A ZQCL command should be issued with the appropriate timings met. 


Figure 44: DLL Disable Mode to DLL Enable Mode


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/b8ed02682513a7e547532d172fa1aef8df17f63069ab8f8b59a91d72453a502a.jpg)


Notes: 1. Enter SELF REFRESH. 

2. Exit SELF REFRESH. 

3. Wait t XS, then set MR1[0] to 0 to enable DLL. 

4. Wait t MRD, then set MR0[8] to 1 to begin DLL RESET. 

5. Wait t MRD, update registers (CL, CWL, and write recovery may be necessary). 

6. Wait t MOD, any valid command. 

7. Starting with the idle state. 

8. Change frequency. 

9. Clock must be stable at least t CKSRX. 

10. Static LOW in the case that $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ or RTT(WR) is enabled; otherwise, static LOW or HIGH. 

The clock frequency range for the DLL disable mode is specified by the parameter t CK (DLL_DIS). Due to latency counter and timing restrictions, only $\mathrm { C L } = 6$ and $\mathrm { C W L } = 6$ are supported. 

DLL disable mode will affect the read data clock to data strobe relationship (t DQSCK) but not the data strobe to data relationship (t DQSQ, t QH). Special attention is needed to line up read data to the controller time domain. 

Compared to the DLL on mode where t DQSCK starts from the rising clock edge $\mathrm { A L + C L }$ cycles after the READ command, the DLL disable mode t DQSCK starts $\mathrm { A L + C L - 1 }$ cycles after the READ command. 

WRITE operations function similarly between the DLL enable and DLL disable modes; however, ODT functionality is not allowed with DLL disable mode. 


Figure 45: DLL Disable t DQSCK


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/772191bf00d076a91e6572d80d5f903f2c09be461c5644ce3fefe37480be456a.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/f0ee78c16beb29d2f85160db29e23feac47b55fda2b9679cea772edc64078984.jpg)


Transitioning Data 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/886a9b3054f1982a70b3eef95c70f4507e769d4dd3d3d7f55167a0f720277267.jpg)


Don’t Care 


Table 74: READ Electrical Characteristics, DLL Disable Mode


<table><tr><td>Parameter</td><td>Symbol</td><td>Min</td><td>Max</td><td>Unit</td></tr><tr><td>Access window of DQS from CK, CK#</td><td>tDQSK (DLL_DIS)</td><td>1</td><td>10</td><td>ns</td></tr></table>

# Input Clock Frequency Change

When the DDR3 SDRAM is initialized, the clock must be stable during most normal states of operation. This means that after the clock frequency has been set to the stable state, the clock period is not allowed to deviate, except for what is allowed by the clock jitter and spread spectrum clocking (SSC) specifications. 

The input clock frequency can be changed from one stable clock rate to another under two conditions: self refresh mode and precharge power-down mode. It is illegal to change the clock frequency outside of those two modes. For the self refresh mode condition, when the DDR3 SDRAM has been successfully placed into self refresh mode and t CKSRE has been satisfied, the state of the clock becomes a “Don’t Care.” When the clock becomes a “Don’t Care,” changing the clock frequency is permissible if the new clock frequency is stable prior to t CKSRX. When entering and exiting self refresh mode for the sole purpose of changing the clock frequency, the self refresh entry and exit specifications must still be met. 

The precharge power-down mode condition is when the DDR3 SDRAM is in precharge power-down mode (either fast exit mode or slow exit mode). Either ODT must be at a logic LOW or $\mathrm { R _ { T T , n o m } }$ and RTT(WR) must be disabled via MR1 and MR2. This ensures $\mathrm { R _ { T T , n o m } }$ and $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ are in an off state prior to entering precharge power-down mode, and CKE must be at a logic LOW. A minimum of t CKSRE must occur after CKE goes LOW before the clock frequency can change. The DDR3 SDRAM input clock frequency is allowed to change only within the minimum and maximum operating frequency specified for the particular speed grade (t CK [AVG] MIN to $\operatorname { \mathrm { { t } } C K }$ [AVG] MAX). During the input clock frequency change, CKE must be held at a stable LOW level. When the input clock frequency is changed, a stable clock must be provided to the DRAM t CKSRX before precharge power-down may be exited. After precharge power-down is exited and t XP has been satisfied, the DLL must be reset via the MRS. Depending on the new clock frequency, additional MRS commands may need to be issued. During the DLL lock time, $\mathrm { R _ { T T , n o m } }$ and RTT(WR) must remain in an off state. After the DLL lock time, the DRAM is ready to operate with a new clock frequency. 


Figure 46: Change Frequency During Precharge Power-Down


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/c17ae5b373c618c5f5880aed58355670d94791271bf8aba15df1b85e730fc12f.jpg)


Notes: 1. Applicable for both SLOW-EXIT and FAST-EXIT precharge power-down modes. 

2. t AOFPD and t AOF must be satisfied and outputs High-Z prior to T1 (see On-Die Termination (ODT) (page 195)for exact requirements). 

3. If the $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ feature was enabled in the mode register prior to entering precharge power-down mode, the ODT signal must be continuously registered LOW, ensuring $\mathsf { R } _ { \mathsf { T T } }$ is in an off state. If the $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ feature was disabled in the mode register prior to entering precharge power-down mode, $\mathsf { R } _ { \mathsf { T T } }$ will remain in the off state. The ODT signal can be registered LOW or HIGH in this case. 

# Write Leveling

For better signal integrity, DDR3 SDRAM memory modules have adopted fly-by topology for the commands, addresses, control signals, and clocks. Write leveling is a scheme for the memory controller to adjust or de-skew the DQS strobe (DQS, DQS#) to CK relationship at the DRAM with a simple feedback feature provided by the DRAM. Write leveling is generally used as part of the initialization process, if required. For normal DRAM operation, this feature must be disabled. This is the only DRAM operation where the DQS functions as an input (to capture the incoming clock) and the DQ function as outputs (to report the state of the clock). Note that nonstandard ODT schemes are required. 

The memory controller using the write leveling procedure must have adjustable delay settings on its DQS strobe to align the rising edge of DQS to the clock at the DRAM pins. This is accomplished when the DRAM asynchronously feeds back the CK status via the DQ bus and samples with the rising edge of DQS. The controller repeatedly delays the DQS strobe until a CK transition from 0 to 1 is detected. The DQS delay established by this procedure helps ensure t DQSS, t DSS, and t DSH specifications in systems that use fly-by topology by de-skewing the trace length mismatch. A conceptual timing of this procedure is shown in Figure 47. 


Figure 47: Write Leveling Concept


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/43ae441bfb12ab8c703b2ef741aeb4a23f89049a36ce7207750991ec91b6e00e.jpg)


When write leveling is enabled, the rising edge of DQS samples CK, and the prime DQ outputs the sampled CK’s status. The prime DQ for a x4 or x8 configuration is DQ0 with 

all other DQ (DQ[7:1]) driving LOW. The prime DQ for a x16 configuration is DQ0 for the lower byte and DQ8 for the upper byte. It outputs the status of CK sampled by LDQS and UDQS. All other DQ (DQ[7:1], DQ[15:9]) continue to drive LOW. Two prime DQ on a x16 enable each byte lane to be leveled independently. 

The write leveling mode register interacts with other mode registers to correctly configure the write leveling functionality. Besides using MR1[7] to disable/enable write leveling, MR1[12] must be used to enable/disable the output buffers. The ODT value, burst length, and so forth need to be selected as well. This interaction is shown in Table 75. It should also be noted that when the outputs are enabled during write leveling mode, the DQS buffers are set as inputs, and the DQ are set as outputs. Additionally, during write leveling mode, only the DQS strobe terminations are activated and deactivated via the ODT ball. The DQ remain disabled and are not affected by the ODT ball. 


Table 75: Write Leveling Matrix



Note 1 applies to the entire table


<table><tr><td>MR1[7]</td><td>MR1[12]</td><td>MR1[2, 6, 9]</td><td colspan="3">DRAMRTT,nom</td><td rowspan="2">DRAM State</td><td rowspan="2">Case</td><td rowspan="2">Notes</td></tr><tr><td>Write Leveling</td><td>OutputBuffers</td><td>RTT,nomValue</td><td>ODT Ball</td><td>DQS</td><td>DQ</td></tr><tr><td>Disabled</td><td colspan="5">See normal operations</td><td>Write leveling not enabled</td><td>0</td><td></td></tr><tr><td rowspan="4">Enabled(1)</td><td rowspan="2">Disabled(1)</td><td>n/a</td><td>Low</td><td>Off</td><td rowspan="4">Off</td><td>DQS not receiving: not terminatedPrime DQ High-Z: not terminatedOther DQ High-Z: not terminated</td><td>1</td><td rowspan="2">2</td></tr><tr><td>20Ω, 30Ω,40Ω, 60Ω, or120Ω</td><td>High</td><td>On</td><td>DQS not receiving: terminated by RTTPrime DQ High-Z: not terminatedOther DQ High-Z: not terminated</td><td>2</td></tr><tr><td rowspan="2">Enabled(0)</td><td>n/a</td><td>Low</td><td>Off</td><td>DQS receiving: not terminatedPrime DQ driving CK state: not terminatedOther DQ driving LOW: not terminated</td><td>3</td><td rowspan="2">3</td></tr><tr><td>40Ω, 60Ω, or120Ω</td><td>High</td><td>On</td><td>DQS receiving: terminated by RTTPrime DQ driving CK state: not terminatedOther DQ driving LOW: not terminated</td><td>4</td></tr></table>

Notes: 1. Expected usage if used during write leveling: Case 1 may be used when DRAM are on a dual-rank module and on the rank not being leveled or on any rank of a module not being leveled on a multislot system. Case 2 may be used when DRAM are on any rank of a module not being leveled on a multislot system. Case 3 is generally not used. Case 4 is generally used when DRAM are on the rank that is being leveled. 

2. Since the DRAM DQS is not being driven $\begin{array} { r } { ( \mathsf { M } \mathsf { R } 1 [ 1 2 ] = \mathbb { 1 } } \end{array}$ ), DQS ignores the input strobe, and all $\mathsf { R } _ { \mathsf { T } , \mathsf { n o m } }$ values are allowed. This simulates a normal standby state to DQS. 

3. Since the DRAM DQS is being driven $( \mathsf { M R 1 } [ 1 2 ] = 0 )$ ), DQS captures the input strobe, and only some $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ values are allowed. This simulates a normal write state to DQS. 

# Write Leveling Procedure

A memory controller initiates the DRAM write leveling mode by setting MR1[7] to 1, assuming the other programable features (MR0, MR1, MR2, and MR3) are first set and the DLL is fully reset and locked. The DQ balls enter the write leveling mode going from a High-Z state to an undefined driving state, so the DQ bus should not be driven. During write leveling mode, only the NOP or DES commands are allowed. The memory controller should attempt to level only one rank at a time; thus, the outputs of other ranks should be disabled by setting MR1[12] to 1 in the other ranks. The memory controller may assert ODT after a t MOD delay, as the DRAM will be ready to process the ODT transition. ODT should be turned on prior to DQS being driven LOW by at least ODTLon delay $( \mathrm { W L } - 2 ^ { \mathrm { t } } \mathrm { C K } )$ , provided it does not violate the aforementioned t MOD delay requirement. 

The memory controller may drive DQS LOW and DQS# HIGH after t WLDQSEN has been satisfied. The controller may begin to toggle DQS after t WLMRD (one DQS toggle is DQS transitioning from a LOW state to a HIGH state with DQS# transitioning from a HIGH state to a LOW state, then both transition back to their original states). At a minimum, ODTLon and t AON must be satisfied at least one clock prior to DQS toggling. 

After t WLMRD and a DQS LOW preamble (t WPRE) have been satisfied, the memory controller may provide either a single DQS toggle or multiple DQS toggles to sample CK for a given DQS-to-CK skew. Each DQS toggle must not violate t DQSL (MIN) and t DQSH (MIN) specifications. t DQSL (MAX) and t DQSH (MAX) specifications are not applicable during write leveling mode. The DQS must be able to distinguish the CK’s rising edge within t WLS and t WLH. The prime DQ will output the CK’s status asynchronously from the associated DQS rising edge CK capture within t WLO. The remaining DQ that always drive LOW when DQS is toggling must be LOW within t WLOE after the first t WLO is satisfied (the prime DQ going LOW). As previously noted, DQS is an input and not an output during this process. Figure 48 (page 132) depicts the basic timing parameters for the overall write leveling procedure. 

The memory controller will most likely sample each applicable prime DQ state and determine whether to increment or decrement its DQS delay setting. After the memory controller performs enough DQS toggles to detect the CK’s 0-to-1 transition, the memory controller should lock the DQS delay setting for that DRAM. After locking the DQS setting is locked, leveling for the rank will have been achieved, and the write leveling mode for the rank should be disabled or reprogrammed (if write leveling of another rank follows). 


Figure 48: Write Leveling Sequence


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/ab7fc7f5b05c9e9859118165c33c97220fec4e0b6b83d780665bf6e2f583ffd3.jpg)


Notes: 1. MRS: Load MR1 to enter write leveling mode. 

2. NOP: NOP or DES. 

3. DQS, DQS# needs to fulfill minimum pulse width requirements t DQSH (MIN) and t DQSL (MIN) as defined for regular writes. The maximum pulse width is system-dependent. 

4. Differential DQS is the differential data strobe (DQS, DQS#). Timing reference points are the zero crossings. The solid line represents DQS; the dotted line represents DQS#. 

5. DRAM drives leveling feedback on a prime DQ (DQ0 for x4 and x8). The remaining DQ are driven LOW and remain in this state throughout the leveling procedure. 

# Write Leveling Mode Exit Procedure

After the DRAM are leveled, they must exit from write leveling mode before the normal mode can be used. Figure 49 depicts a general procedure for exiting write leveling mode. After the last rising DQS (capturing a 1 at T0), the memory controller should stop driving the DQS signals after t WLO (MAX) delay plus enough delay to enable the memory controller to capture the applicable prime DQ state (at ~Tb0). The DQ balls become undefined when DQS no longer remains LOW, and they remain undefined until t MOD after the MRS command (at Te1). 

The ODT input should be de-asserted LOW such that ODTLoff (MIN) expires after the DQS is no longer driving LOW. When ODT LOW satisfies t IS, ODT must be kept LOW (at ~Tb0) until the DRAM is ready for either another rank to be leveled or until the normal mode can be used. After DQS termination is switched off, write level mode should be disabled via the MRS command (at Tc2). After t MOD is satisfied (at Te1), any valid command may be registered by the DRAM. Some MRS commands may be issued after t MRD (at Td1). 


Figure 49: Write Leveling Exit Procedure


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/6aaacd024bf84eacfe6103aa39b0374c5986f0c647c7c36c1a3a5258b8af05e5.jpg)



Note: 1. The DQ result, $= 1$ , between Ta0 and Tc0, is a result of the DQS, DQS# signals capturing CK HIGH just after the T0 state.


# Initialization

The following sequence is required for power-up and initialization, as shown in Figure 50 (page 135): 

1. Apply power. RESET# is recommended to be below $0 . 2 \times \mathrm { V _ { D D Q } }$ during power ramp to ensure the outputs remain disabled (High-Z) and ODT off $\mathrm { R } _ { \mathrm { T T } }$ is also High-Z). All other inputs, including ODT, may be undefined. 

During power-up, either of the following conditions may exist and must be met: 

• Condition A: 

– $\mathrm { V _ { D D } }$ and $\mathrm { V _ { D D Q } }$ are driven from a single-power converter output and are ramped with a maximum delta voltage between them of $\Delta \mathrm { V } \leq 3 0 0 \mathrm { m V } .$ Slope reversal of any power supply signal is allowed. The voltage levels on all balls other than $\mathrm { V _ { D D } , V _ { D D Q } , V _ { S S } , V _ { S S Q } }$ must be less than or equal to $\mathrm { V _ { D D Q } }$ and $\mathrm { V _ { D D } }$ on one side, and must be greater than or equal to $\mathrm { V } _ { \mathrm { S S Q } }$ and $\mathrm { V } _ { \mathrm { S S } }$ on the other side. 

– Both $\mathrm { V _ { D D } }$ and VDDQ power supplies ramp to $\mathrm { V _ { D D , m i n } }$ and $\mathrm { V _ { D D Q , m i n } }$ within $\mathrm { ^ t V _ { D D P R } } = 2 0 0 \mathrm { m s } .$ . 

– VREFDQ tracks VDD × 0.5, VREFCA tracks $\mathrm { V _ { D D } } \times 0 . 5$ . 

– $\mathrm { V _ { T T } }$ is limited to 0.95V when the power ramp is complete and is not applied directly to the device; however, t VTD should be greater than or equal to 0 to avoid device latchup. 

• Condition B: 

– VDD may be applied before or at the same time as VDDQ. 

– VDDQ may be applied before or at the same time as VTT, VREFDQ, and VREFCA. 

– No slope reversals are allowed in the power supply ramp for this condition. 

2. Until stable power, maintain RESET# LOW to ensure the outputs remain disabled (High-Z). After the power is stable, RESET# must be LOW for at least 200μs to begin the initialization process. ODT will remain in the High-Z state while RESET# is LOW and until CKE is registered HIGH. 

3. CKE must be LOW 10ns prior to RESET# transitioning HIGH. 

4. After RESET# transitions HIGH, wait 500μs (minus one clock) with CKE LOW. 

5. After the CKE LOW time, CKE may be brought HIGH (synchronously) and only NOP or DES commands may be issued. The clock must be present and valid for at least 10ns (and a minimum of five clocks) and ODT must be driven LOW at least t IS prior to CKE being registered HIGH. When CKE is registered HIGH, it must be continuously registered HIGH until the full initialization process is complete. 

6. After CKE is registered HIGH and after t XPR has been satisfied, MRS commands may be issued. Issue an MRS (LOAD MODE) command to MR2 with the applicable settings (provide LOW to BA2 and BA0 and HIGH to BA1). 

7. Issue an MRS command to MR3 with the applicable settings. 

8. Issue an MRS command to MR1 with the applicable settings, including enabling the DLL and configuring ODT. 

9. Issue an MRS command to MR0 with the applicable settings, including a DLL RE-SET command. t DLLK (512) cycles of clock input are required to lock the DLL. 

10. Issue a ZQCL command to calibrate $\mathrm { R } _ { \mathrm { T T } }$ and $\mathrm { R _ { O N } }$ values for the process voltage temperature (PVT). Prior to normal operation, t ZQinit must be satisfied. 

11. When t DLLK and t ZQinit have been satisfied, the DDR3 SDRAM will be ready for normal operation. 


Figure 50: Initialization Sequence


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/c1ed253c7304b49b6bbb0f805eb532abeb2d8b0a59fea3bfaf7eb0ffec08272f.jpg)


# Voltage Initialization / Change

If the SDRAM is powered up and initialized for the 1.35V operating voltage range, voltage can be increased to the 1.5V operating range provided the following conditions are met (See Figure 51 (page 137)): 

• Just prior to increasing the 1.35V operating voltages, no further commands are issued, other than NOPs or COMMAND INHIBITs, and all banks are in the precharge state. 

• The 1.5V operating voltages are stable prior to issuing new commands, other than NOPs or COMMAND INHIBITs. 

• The DLL is reset and relocked after the 1.5V operating voltages are stable and prior to any READ command. 

• The ZQ calibration is performed. t ZQinit must be satisfied after the 1.5V operating voltages are stable and prior to any READ command. 

If the SDRAM is powered up and initialized for the 1.5V operating voltage range, voltage can be reduced to the 1.35V operation range provided the following conditions are met (See Figure 51 (page 137)) : 

• Just prior to reducing the 1.5V operating voltages, no further commands are issued, other than NOPs or COMMAND INHIBITs, and all banks are in the precharge state. 

• The 1.35V operating voltages are stable prior to issuing new commands, other than NOPs or COMMAND INHIBITs. 

• The DLL is reset and relocked after the 1.35V operating voltages are stable and prior to any READ command. 

• The ZQ calibration is performed. t ZQinit must be satisfied after the 1.35V operating voltages are stable and prior to any READ command. 

# VDD Voltage Switching

After the DDR3L DRAM is powered up and initialized, the power supply can be altered between the DDR3L and DDR3 levels, provided the sequence in Figure 51 is maintained. 


Figure 51: $\pmb { \nu _ { \mathsf { D D } } }$ Voltage Switching


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/2d912f8c314ff98554c7d7b5f946ce85064663799b7608b25ff8c333076b9839.jpg)



Note: 1. From time point Td until Tk, NOP or DES commands must be applied between MRS and ZQCL commands.


# Mode Registers

Mode registers (MR0–MR3) are used to define various modes of programmable operations of the DDR3 SDRAM. A mode register is programmed via the mode register set (MRS) command during initialization, and it retains the stored information (except for MR0[8], which is self-clearing) until it is reprogrammed, RESET# goes LOW, the device loses power. 

Contents of a mode register can be altered by re-executing the MRS command. Even if the user wants to modify only a subset of the mode register’s variables, all variables must be programmed when the MRS command is issued. Reprogramming the mode register will not alter the contents of the memory array, provided it is performed correctly. 

The MRS command can only be issued (or re-issued) when all banks are idle and in the precharged state (t RP is satisfied and no data bursts are in progress). After an MRS command has been issued, two parameters must be satisfied: t MRD and t MOD. The controller must wait t MRD before initiating any subsequent MRS commands. 


Figure 52: MRS to MRS Command Timing (t MRD)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/7c25b27a0646d0b91216eeba1cf443d669f50e2b7a912e84492951ad703e47cc.jpg)


Notes: 1. Prior to issuing the MRS command, all banks must be idle and precharged, t RP (MIN) must be satisfied, and no data bursts can be in progress. 

2. t MRD specifies the MRS to MRS command minimum cycle time. 

3. CKE must be registered HIGH from the MRS command until t MRSPDEN (MIN) (see Power-Down Mode (page 185)). 

4. For a CAS latency change, t XPDLL timing must be met before any non-MRS command. 

The controller must also wait t MOD before initiating any non-MRS commands (excluding NOP and DES). The DRAM requires t MOD in order to update the requested features, with the exception of DLL RESET, which requires additional time. Until t MOD has been satisfied, the updated features are to be assumed unavailable. 


Figure 53: MRS to nonMRS Command Timing (t MOD)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/724b9d07e99db96ca88ea15daf179d7d84b57fe38845709637307137edfe0113.jpg)


Notes: 1. Prior to issuing the MRS command, all banks must be idle (they must be precharged, t RP must be satisfied, and no data bursts can be in progress). 

2. Prior to Ta2 when t MOD (MIN) is being satisfied, no commands (except NOP/DES) may be issued. 

3. If $\mathsf { R } _ { \mathsf { T T } }$ was previously enabled, ODT must be registered LOW at T0 so that ODTL is satisfied prior to Ta1. ODT must also be registered LOW at each rising CK edge from T0 until t MODmin is satisfied at Ta2. 

4. CKE must be registered HIGH from the MRS command until t MRSPDEN (MIN), at which time power-down may occur (see Power-Down Mode (page 185)). 

# Mode Register 0 (MR0)

The base register, mode register 0 (MR0), is used to define various DDR3 SDRAM modes of operation. These definitions include the selection of a burst length, burst type, CAS latency, operating mode, DLL RESET, write recovery, and precharge power-down mode (see Figure 54 (page 140)). 

# Burst Length

Burst length is defined by MR0[1:0]. Read and write accesses to the DDR3 SDRAM are burst-oriented, with the burst length being programmable to 4 (chop) mode, 8 (fixed) mode, or selectable using A12 during a READ/WRITE command (on-the-fly). The burst length determines the maximum number of column locations that can be accessed for a given READ or WRITE command. When MR0[1:0] is set to 01 during a READ/WRITE command, if $\mathrm { A } 1 2 = 0$ , then BC4 mode is selected. If $\mathrm { A } 1 2 = 1$ , then BL8 mode is selected. Specific timing diagrams, and turnaround between READ/WRITE, are shown in the READ/WRITE sections of this document. 

When a READ or WRITE command is issued, a block of columns equal to the burst length is effectively selected. All accesses for that burst take place within this block, meaning that the burst will wrap within the block if a boundary is reached. The block is uniquely selected by A[i:2] when the burst length is set to 4 and by A[i:3] when the burst length is set to 8, where $\mathrm { A } i$ is the most significant column address bit for a given configuration. The remaining (least significant) address bit(s) is (are) used to select the start-

ing location within the block. The programmed burst length applies to both READ and WRITE bursts. 


Figure 54: Mode Register 0 (MR0) Definitions


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/88d44fa1c16d0a5b8959ef367d320177a4e6e41f5b2f8c87747b56049b97da82.jpg)



Note: 1. MR0[18, 15:13, 7] are reserved for future use and must be programmed to 0.


# Burst Type

Accesses within a given burst can be programmed to either a sequential or an interleaved order. The burst type is selected via MR0[3] (see Figure 54 (page 140)). The ordering of accesses within a burst is determined by the burst length, the burst type, and the starting column address. DDR3 only supports 4-bit burst chop and 8-bit burst access modes. Full interleave address ordering is supported for READs, while WRITEs are restricted to nibble (BC4) or word (BL8) boundaries. 


Table 76: Burst Order


<table><tr><td>Burst Length</td><td>READ/WRITE</td><td>Starting Column Address (A[2, 1, 0])</td><td>Burst Type = Sequential (Decimal)</td><td>Burst Type = Interleaved (Decimal)</td><td>Notes</td></tr><tr><td rowspan="10">4 (chop)</td><td rowspan="8">READ</td><td>0 0 0</td><td>0, 1, 2, 3, Z, Z, Z, Z</td><td>0, 1, 2, 3, Z, Z, Z, Z</td><td>1, 2</td></tr><tr><td>0 0 1</td><td>1, 2, 3, 0, Z, Z, Z, Z</td><td>1, 0, 3, 2, Z, Z, Z, Z</td><td>1, 2</td></tr><tr><td>0 1 0</td><td>2, 3, 0, 1, Z, Z, Z, Z</td><td>2, 3, 0, 1, Z, Z, Z, Z</td><td>1, 2</td></tr><tr><td>0 1 1</td><td>3, 0, 1, 2, Z, Z, Z, Z</td><td>3, 2, 1, 0, Z, Z, Z, Z</td><td>1, 2</td></tr><tr><td>1 0 0</td><td>4, 5, 6, 7, Z, Z, Z, Z</td><td>4, 5, 6, 7, Z, Z, Z, Z</td><td>1, 2</td></tr><tr><td>1 0 1</td><td>5, 6, 7, 4, Z, Z, Z, Z</td><td>5, 4, 7, 6, Z, Z, Z, Z</td><td>1, 2</td></tr><tr><td>1 1 0</td><td>6, 7, 4, 5, Z, Z, Z, Z</td><td>6, 7, 4, 5, Z, Z, Z, Z</td><td>1, 2</td></tr><tr><td>1 1 1</td><td>7, 4, 5, 6, Z, Z, Z, Z</td><td>7, 6, 5, 4, Z, Z, Z, Z</td><td>1, 2</td></tr><tr><td rowspan="2">WRITE</td><td>0 V V</td><td>0, 1, 2, 3, X, X, X, X</td><td>0, 1, 2, 3, X, X, X, X</td><td>1, 3, 4</td></tr><tr><td>1 V V</td><td>4, 5, 6, 7, X, X, X, X</td><td>4, 5, 6, 7, X, X, X, X</td><td>1, 3, 4</td></tr><tr><td rowspan="9">8 (fixed)</td><td rowspan="8">READ</td><td>0 0 0</td><td>0, 1, 2, 3, 4, 5, 6, 7</td><td>0, 1, 2, 3, 4, 5, 6, 7</td><td>1</td></tr><tr><td>0 0 1</td><td>1, 2, 3, 0, 5, 6, 7, 4</td><td>1, 0, 3, 2, 5, 4, 7, 6</td><td>1</td></tr><tr><td>0 1 0</td><td>2, 3, 0, 1, 6, 7, 4, 5</td><td>2, 3, 0, 1, 6, 7, 4, 5</td><td>1</td></tr><tr><td>0 1 1</td><td>3, 0, 1, 2, 7, 4, 5, 6</td><td>3, 2, 1, 0, 7, 6, 5, 4</td><td>1</td></tr><tr><td>1 0 0</td><td>4, 5, 6, 7, 0, 1, 2, 3</td><td>4, 5, 6, 7, 0, 1, 2, 3</td><td>1</td></tr><tr><td>1 0 1</td><td>5, 6, 7, 4, 1, 2, 3, 0</td><td>5, 4, 7, 6, 1, 0, 3, 2</td><td>1</td></tr><tr><td>1 1 0</td><td>6, 7, 4, 5, 2, 3, 0, 1</td><td>6, 7, 4, 5, 2, 3, 0, 1</td><td>1</td></tr><tr><td>1 1 1</td><td>7, 4, 5, 6, 3, 0, 1, 2</td><td>7, 6, 5, 4, 3, 2, 1, 0</td><td>1</td></tr><tr><td>WRITE</td><td>V V V</td><td>0, 1, 2, 3, 4, 5, 6, 7</td><td>0, 1, 2, 3, 4, 5, 6, 7</td><td>1, 3</td></tr></table>


Notes: 1. Internal READ and WRITE operations start at the same point in time for BC4 as they do for BL8. 



2. $Z =$ Data and strobe output drivers are in tri-state. 



3. $\mathsf { V } = \mathsf { A }$ valid logic level (0 or 1), but the respective input buffer ignores level-on input pins. 



4. $\times = \prime$ “Don’t Care.” 


# DLL RESET

DLL RESET is defined by MR0[8] (see Figure 54 (page 140)). Programming MR0[8] to 1 activates the DLL RESET function. MR0[8] is self-clearing, meaning it returns to a value of 0 after the DLL RESET function has been initiated. 

Anytime the DLL RESET function is initiated, CKE must be HIGH and the clock held stable for 512 (t DLLK) clock cycles before a READ command can be issued. This is to allow time for the internal clock to be synchronized with the external clock. Failing to wait for synchronization can result in invalid output timing specifications, such as t DQSCK timings. 

# Write Recovery

WRITE recovery time is defined by MR0[11:9] (see Figure 54 (page 140)). Write recovery values of 5, 6, 7, 8, 10, or 12 can be used by programming MR0[11:9]. The user is required to program the correct value of write recovery, which is calculated by dividing t WR (ns) by $^ \mathrm { t } \mathrm { C K }$ (ns) and rounding up a noninteger value to the next integer: WR (cycles) $=$ roundup (t WR (ns) $/ ^ { \mathrm { t } } \mathrm { C K }$ (ns)). 

# Precharge Power-Down (Precharge PD)

The precharge power-down (precharge PD) bit applies only when precharge powerdown mode is being used. When MR0[12] is set to 0, the DLL is off during precharge power-down, providing a lower standby current mode; however, t XPDLL must be satisfied when exiting. When MR0[12] is set to 1, the DLL continues to run during precharge power-down mode to enable a faster exit of precharge power-down mode; however, t XP must be satisfied when exiting (see Power-Down Mode (page 185)). 

# CAS Latency (CL)

CAS latency (CL) is defined by MR0[6:4], as shown in Figure 54 (page 140). CAS latency is the delay, in clock cycles, between the internal READ command and the availability of the first bit of output data. CL can be set to 5 through 14. DDR3 SDRAM do not support half-clock latencies. 

Examples of $\mathrm { C L } = 6$ and $\mathrm { C L } = 8$ are shown below. If an internal READ command is registered at clock edge $n$ , and the CAS latency is m clocks, the data will be available nominally coincident with clock edge $n + m$ . See Speed Bin Tables for the CLs supported at various operating frequencies. 


Figure 55: READ Latency


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/93bd6063ae04ea2d0f0bff549075328722f0ee6cd83f4153c50c737ab1695932.jpg)



Notes: 1. For illustration purposes, only $\mathtt { C L } = 6$ and $\mathtt { C L } = 8$ are shown. Other CL values are possible. 2. Shown with nominal t DQSCK and nominal t DSDQ.


# Mode Register 1 (MR1)

The mode register 1 (MR1) controls additional functions and features not available in the other mode registers: Q OFF (OUTPUT DISABLE), TDQS (for the x8 configuration only), DLL ENABLE/DLL DISABLE, $\mathrm { R _ { T T , n o m } }$ value (ODT), WRITE LEVELING, POSTED CAS ADDITIVE latency, and OUTPUT DRIVE STRENGTH. These functions are controlled via the bits shown in Figure 56 (page 144). The MR1 register is programmed via the MRS command and retains the stored information until it is reprogrammed, until RE-SET# goes LOW, or until the device loses power. Reprogramming the MR1 register will not alter the contents of the memory array, provided it is performed correctly. 

The MR1 register must be loaded when all banks are idle and no bursts are in progress. The controller must satisfy the specified timing parameters t MRD and t MOD before initiating a subsequent operation. 


Figure 56: Mode Register 1 (MR1) Definition


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/b12327b82f45fcf698e962768eae61cbe30742bc61acaa30d8f741178cd45c8c.jpg)


Notes: 1. MR1[18, 15:13, 10, 8] are reserved for future use and must be programmed to 0. 

2. During write leveling, if MR1[7] and MR1[12] are 1, then all $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ values are available for use. 

3. During write leveling, if MR1[7] is a 1, but MR1[12] is a 0, then only $\mathsf { R } _ { \mathsf { T } , \mathsf { n o m } }$ write values are available for use. 

# DLL Enable/DLL Disable

The DLL may be enabled or disabled by programming MR1[0] during the LOAD MODE command, as shown in Figure 56 (page 144). The DLL must be enabled for normal operation. DLL enable is required during power-up initialization and upon returning to normal operation after having disabled the DLL for the purpose of debugging or evaluation. Enabling the DLL should always be followed by resetting the DLL using the appropriate LOAD MODE command. 

If the DLL is enabled prior to entering self refresh mode, the DLL is automatically disabled when entering SELF REFRESH operation and is automatically re-enabled and reset upon exit of SELF REFRESH operation. If the DLL is disabled prior to entering self re-

fresh mode, the DLL remains disabled even upon exit of SELF REFRESH operation until it is re-enabled and reset. 

The DRAM is not tested to check—nor does Micron warrant compliance with—normal mode timings or functionality when the DLL is disabled. An attempt has been made to have the DRAM operate in the normal mode where reasonably possible when the DLL has been disabled; however, by industry standard, a few known exceptions are defined: 

• ODT is not allowed to be used 

• The output data is no longer edge-aligned to the clock 

• CL and CWL can only be six clocks 

When the DLL is disabled, timing and functionality can vary from the normal operation specifications when the DLL is enabled (see DLL Disable Mode (page 123)). Disabling the DLL also implies the need to change the clock frequency (see Input Clock Frequency Change (page 127)). 

# Output Drive Strength

The DDR3 SDRAM uses a programmable impedance output buffer. The drive strength mode register setting is defined by MR1[5, 1]. RZQ/7 (34Ω [NOM]) is the primary output driver impedance setting for DDR3 SDRAM devices. To calibrate the output driver impedance, an external precision resistor (RZQ) is connected between the ZQ ball and VSSQ. The value of the resistor must be $2 4 0 \Omega \pm 1 \%$ . 

The output impedance is set during initialization. Additional impedance calibration updates do not affect device operation, and all data sheet timings and current specifications are met during an update. 

To meet the 34Ω specification, the output drive strength must be set to 34Ω during initialization. To obtain a calibrated output driver impedance after power-up, the DDR3 SDRAM needs a calibration command that is part of the initialization and reset procedure. 

# OUTPUT ENABLE/DISABLE

The OUTPUT ENABLE function is defined by MR1[12], as shown in Figure 56 (page 144). When enabled $( \mathbf { M } \mathbf { R } 1 [ 1 2 ] = 0$ ), all outputs (DQ, DQS, DQS#) function when in the normal mode of operation. When disabled $( \mathbf { M } \mathbf { R } 1 [ 1 2 ] = 1 )$ ), all DDR3 SDRAM outputs (DQ and DQS, DQS#) are tri-stated. The output disable feature is intended to be used during $\mathrm { I _ { D D } }$ characterization of the READ current and during t DQSS margining (write leveling) only. 

# TDQS Enable

Termination data strobe (TDQS) is a feature of the x8 DDR3 SDRAM configuration that provides termination resistance $\mathrm { ( R _ { T T } ) }$ and may be useful in some system configurations. TDQS is not supported in x4 or x16 configurations. When enabled via the mode register (MR1[11]), the $\mathrm { R } _ { \mathrm { T T } }$ that is applied to DQS and DQS# is also applied to TDQS and TDQS#. In contrast to the RDQS function of DDR2 SDRAM, DDR3’s TDQS provides the termination resistance $\mathrm { R } _ { \mathrm { T T } }$ only. The OUTPUT DATA STROBE function of RDQS is not provided by TDQS; thus, $\operatorname { R } _ { \mathrm { O N } }$ does not apply to TDQS and TDQS#. The TDQS and DM functions share the same ball. When the TDQS function is enabled via the mode register, the DM function is not supported. When the TDQS function is disabled, the DM function is provided, and the TDQS# ball is not used. The TDQS function is available in the x8 DDR3 

SDRAM configuration only and must be disabled via the mode register for the x4 and x16 configurations. 

# On-Die Termination

ODT resistance $\mathrm { R _ { T T , n o m } }$ is defined by MR1[9, 6, 2] (see Figure 56 (page 144)). The $\mathrm { R } _ { \mathrm { T T } }$ termination value applies to the DQ, DM, DQS, DQS#, and TDQS, TDQS# balls. DDR3 supports multiple $\mathrm { R } _ { \mathrm { T T } }$ termination values based on RZQ/n where n can be 2, 4, 6, 8, or 12 and RZQ is 240Ω. 

Unlike DDR2, DDR3 ODT must be turned off prior to reading data out and must remain off during a READ burst. $\mathrm { R _ { T T , n o m } }$ termination is allowed any time after the DRAM is initialized, calibrated, and not performing read access, or when it is not in self refresh mode. Additionally, write accesses with dynamic ODT $( \mathrm { R } _ { \mathrm { T T ( W R ) } } )$ enabled temporarily replaces $\mathrm { R _ { T T , n o m } }$ with RTT(WR). 

The actual effective termination, $\mathrm { R } _ { \mathrm { T T ( E F F ) } }$ , may be different from the $\mathrm { R } _ { \mathrm { T T } }$ targeted due to nonlinearity of the termination. For $\mathrm { R } _ { \mathrm { T T ( E F F ) } }$ values and calculations (see On-Die Termination (ODT) (page 195)). 

The ODT feature is designed to improve signal integrity of the memory channel by enabling the DDR3 SDRAM controller to independently turn on/off ODT for any or all devices. The ODT input control pin is used to determine when $\mathrm { R } _ { \mathrm { T T } }$ is turned on (ODTL on) and off (ODTL off), assuming ODT has been enabled via MR1[9, 6, 2]. 

Timings for ODT are detailed in On-Die Termination (ODT) (page 195). 

# WRITE LEVELING

The WRITE LEVELING function is enabled by MR1[7], as shown in Figure 56 (page 144). Write leveling is used (during initialization) to deskew the DQS strobe to clock offset as a result of fly-by topology designs. For better signal integrity, DDR3 SDRAM memory modules adopted fly-by topology for the commands, addresses, control signals, and clocks. 

The fly-by topology benefits from a reduced number of stubs and their lengths. However, fly-by topology induces flight time skews between the clock and DQS strobe (and DQ) at each DRAM on the DIMM. Controllers will have a difficult time maintaining t DQSS, t DSS, and t DSH specifications without supporting write leveling in systems which use fly-by topology-based modules. Write leveling timing and detailed operation information is provided in Write Leveling (page 129). 

# POSTED CAS ADDITIVE Latency

POSTED CAS ADDITIVE latency (AL) is supported to make the command and data bus efficient for sustainable bandwidths in DDR3 SDRAM. MR1[4, 3] define the value of AL, as shown in Figure 57 (page 147). MR1[4, 3] enable the user to program the DDR3 SDRAM with $\mathrm { { A L } } = 0$ , CL - 1, or CL - 2. 


Figure 57: READ Latency (AL = 5, CL = 6)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/232bb74f6d2697edfa64681d8521f4a1bcac8a56c7044070698fafe46697ad14.jpg)


# Mode Register 2 (MR2)

The mode register 2 (MR2) controls additional functions and features not available in the other mode registers. These additional functions are CAS WRITE latency (CWL), AU-TO SELF REFRESH (ASR), SELF REFRESH TEMPERATURE (SRT), and DYNAMIC ODT $( \mathrm { R } _ { \mathrm { T T ( W R ) } } )$ . These functions are controlled via the bits shown in Figure 58. The MR2 is programmed via the MRS command and will retain the stored information until it is programmed again or until the device loses power. Reprogramming the MR2 register will not alter the contents of the memory array, provided it is performed correctly. The MR2 register must be loaded when all banks are idle and no data bursts are in progress, and the controller must wait the specified time t MRD and t MOD before initiating a subsequent operation. 


Figure 58: Mode Register 2 (MR2) Definition


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/d059a959b83c511c5d9c724d02dfad912c225caba836e98b685c5e6a38012ee8.jpg)



Note: 1. MR2[18, 15:11, 8, and 2:0] are reserved for future use and must all be programmed to 0.


# CAS Write Latency (CWL)

CWL is defined by MR2[5:3] and is the delay, in clock cycles, from the releasing of the internal write to the latching of the first data in. CWL must be correctly set to the corresponding operating clock frequency (see Figure 58 (page 147)). The overall WRITE latency (WL) is equal to CWL + AL (See Figure below). 


Figure 59: CAS Write Latency


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/0c6c22160d0e20c0302da8af4835f702da05406d2e5002449505d2821eccf99c.jpg)


# AUTO SELF REFRESH (ASR)

Mode register MR2[6] is used to disable/enable the ASR function. When ASR is disabled, the self refresh mode’s refresh rate is assumed to be at the normal $8 5 ^ { \circ } \mathrm { C }$ limit (sometimes referred to as 1x refresh rate). In the disabled mode, ASR requires the user to ensure the DRAM never exceeds a $\mathrm { T _ { C } }$ of $8 5 ^ { \circ } \mathrm { C }$ while in self refresh unless the user enables the SRT feature listed below when the $\mathrm { T _ { C } }$ is between $8 5 ^ { \circ } \mathrm { C }$ and $9 5 ^ { \circ } \mathrm { C }$ . 

Enabling ASR assumes the DRAM self refresh rate is changed automatically from 1x to 2x when the case temperature exceeds $8 5 ^ { \circ } \mathrm { C }$ . This enables the user to operate the DRAM beyond the standard $8 5 ^ { \circ } \mathrm { C }$ limit up to the optional extended temperature range of $9 5 ^ { \circ } \mathrm { C }$ while in self refresh mode. 

The standard self refresh current test specifies test conditions to normal case temperature $( 8 5 ^ { \circ } \mathrm { C } )$ only, meaning if ASR is enabled, the standard self refresh current specifications do not apply (see Extended Temperature Usage (page 184)). 

# SELF REFRESH TEMPERATURE (SRT)

Mode register MR2[7] is used to disable/enable the SRT function. When SRT is disabled, the self refresh mode’s refresh rate is assumed to be at the normal $8 5 ^ { \circ } \mathrm { C }$ limit (sometimes referred to as 1x refresh rate). In the disabled mode, SRT requires the user to ensure the DRAM never exceeds a TC of $8 5 ^ { \circ } \mathrm { C }$ while in self refresh mode unless the user enables ASR. 

When SRT is enabled, the DRAM self refresh is changed internally from 1x to 2x, regardless of the case temperature. This enables the user to operate the DRAM beyond the standard $8 5 ^ { \circ } \mathrm { C }$ limit up to the optional extended temperature range of $9 5 \mathrm { { ^ \circ C } }$ while in self refresh mode. The standard self refresh current test specifies test conditions to normal 

case temperature $( 8 5 ^ { \circ } \mathrm { C } )$ only, meaning if SRT is enabled, the standard self refresh current specifications do not apply (see Extended Temperature Usage (page 184)). 

# SRT vs. ASR

If the normal case temperature limit of $8 5 ^ { \circ } \mathrm { C }$ is not exceeded, then neither SRT nor ASR is required, and both can be disabled throughout operation. However, if the extended temperature option of $9 5 ^ { \circ } \mathrm { C }$ is needed, the user is required to provide a 2x refresh rate during (manual) refresh and to enable either the SRT or the ASR to ensure self refresh is performed at the 2x rate. 

SRT forces the DRAM to switch the internal self refresh rate from 1x to 2x. Self refresh is performed at the 2x refresh rate regardless of the case temperature. 

ASR automatically switches the DRAM’s internal self refresh rate from 1x to 2x. However, while in self refresh mode, ASR enables the refresh rate to automatically adjust between 1x to 2x over the supported temperature range. One other disadvantage with ASR is the DRAM cannot always switch from a 1x to a 2x refresh rate at an exact case temperature of $8 5 ^ { \circ } \mathrm { C }$ . Although the DRAM will support data integrity when it switches from a 1x to a 2x refresh rate, it may switch at a lower temperature than $8 5 ^ { \circ } \mathrm { C }$ . 

Since only one mode is necessary, SRT and ASR cannot be enabled at the same time. 

# DYNAMIC ODT

The dynamic ODT $( \mathrm { R } _ { \mathrm { T T ( W R ) } } )$ feature is defined by MR2[10, 9]. Dynamic ODT is enabled when a value is selected. This new DDR3 SDRAM feature enables the ODT termination value to change without issuing an MRS command, essentially changing the ODT termination on-the-fly. 

With dynamic ODT $( \mathrm { R } _ { \mathrm { T T ( W R ) } } )$ enabled, the DRAM switches from normal ODT $\mathrm { ( R _ { T T \_ n o m } ) }$ to dynamic ODT $\mathrm { ( R _ { T T ( W R ) } ) }$ when beginning a WRITE burst and subsequently switches back to ODT $\left( \mathrm { R } _ { \mathrm { T T \_ n o m } } \right)$ at the completion of the WRITE burst. If $\mathrm { R } _ { \mathrm { T T \_ n o m } }$ is disabled, the $\mathrm { R } _ { \mathrm { T T \_ n o m } }$ value will be High-Z. Special timing parameters must be adhered to when dynamic ODT $( \mathrm { R } _ { \mathrm { T T ( W R ) } } )$ is enabled: ODTLcnw, ODTLcnw4, ODTLcnw8, ODTH4, ODTH8, and t ADC. 

Dynamic ODT is only applicable during WRITE cycles. If ODT $\left( \mathrm { R } _ { \mathrm { T T \_ n o m } } \right)$ is disabled, dynamic ODT $( \mathrm { R } _ { \mathrm { T T ( W R ) } } )$ is still permitted. $\mathrm { R } _ { \mathrm { T T \_ n o m } }$ and $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ can be used independent of one other. Dynamic ODT is not available during write leveling mode, regardless of the state of ODT $\left( \mathrm { R } _ { \mathrm { T T \_ n o m } } \right)$ . For details on dynamic ODT operation, refer to Dynamic ODT (page 197). 

# Mode Register 3 (MR3)

The mode register 3 (MR3) controls additional functions and features not available in the other mode registers. Currently defined is the MULTIPURPOSE REGISTER (MPR). This function is controlled via the bits shown in Figure 60 (page 150). The MR3 is programmed via the LOAD MODE command and retains the stored information until it is programmed again or until the device loses power. Reprogramming the MR3 register will not alter the contents of the memory array, provided it is performed correctly. The MR3 register must be loaded when all banks are idle and no data bursts are in progress, and the controller must wait the specified time t MRD and t MOD before initiating a subsequent operation. 


Figure 60: Mode Register 3 (MR3) Definition


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/513939c189835a4358eb42a9721aa6d6a332f39c550dac7c9a7557f2d34b11ea.jpg)



Notes: 1. MR3[18 and 15:3] are reserved for future use and must all be programmed to 0.



2. When MPR control is set for normal DRAM operation, MR3[1, 0] will be ignored.



3. Intended to be used for READ synchronization.


# MULTIPURPOSE REGISTER (MPR)

The MULTIPURPOSE REGISTER function is used to output a predefined system timing calibration bit sequence. Bit 2 is the master bit that enables or disables access to the MPR register, and bits 1 and 0 determine which mode the MPR is placed in. The basic concept of the multipurpose register is shown in Figure 61 (page 151). 

If MR3[2] is a 0, then the MPR access is disabled, and the DRAM operates in normal mode. However, if MR3[2] is a 1, then the DRAM no longer outputs normal read data but outputs MPR data as defined by MR3[0, 1]. If MR3[0, 1] is equal to 00, then a predefined read pattern for system calibration is selected. 

To enable the MPR, the MRS command is issued to MR3, and MR3[2] = 1. Prior to issuing the MRS command, all banks must be in the idle state (all banks are precharged, and t RP is met). When the MPR is enabled, any subsequent READ or RDAP commands are redirected to the multipurpose register. The resulting operation when either a READ or a RDAP command is issued, is defined by MR3[1:0] when the MPR is enabled (see Table 78 (page 152)). When the MPR is enabled, only READ or RDAP commands are allowed until a subsequent MRS command is issued with the MPR disabled $( \mathrm { M R } 3 [ 2 ] = 0 )$ ). Power-down mode, self refresh, and any other nonREAD/RDAP commands are not allowed during MPR enable mode. The RESET function is supported during MPR enable mode. 


Figure 61: Multipurpose Register (MPR) Block Diagram


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/b88628cea287f95d678e62de99d544794d21e022c571f3d2e24282fb13fcb355.jpg)


Notes: 1. A predefined data pattern can be read out of the MPR with an external READ command. 

2. MR3[2] defines whether the data flow comes from the memory core or the MPR. When the data flow is defined, the MPR contents can be read out continuously with a regular READ or RDAP command. 


Table 77: MPR Functional Description of MR3 Bits


<table><tr><td>MR3[2]</td><td>MR3[1:0]</td><td rowspan="2">Function</td></tr><tr><td>MPR</td><td>MPR READ Function</td></tr><tr><td>0</td><td>&quot;Don&#x27;t Care&quot;</td><td>Normal operation, no MPR transaction
All subsequent READs come from the DRAM memory array
All subsequent WRITEs go to the DRAM memory array</td></tr><tr><td>1</td><td>A[1:0]
(see Table 78 (page 152))</td><td>Enable MPR mode, subsequent READ/RDAP commands defined by bits 1 and 2</td></tr></table>

# MPR Functional Description

The MPR JEDEC definition enables either a prime DQ (DQ0 on a x4 and a x8; on a x16, $\mathrm { D Q 0 } =$ lower byte and ${ \mathrm { D Q } } 8 =$ upper byte) to output the MPR data with the remaining DQs driven LOW, or for all DQs to output the MPR data . The MPR readout supports fixed READ burst and READ burst chop (MRS and OTF via A12/BC#) with regular READ latencies and AC timings applicable, provided the DLL is locked as required. 

MPR addressing for a valid MPR read is as follows: 

• A[1:0] must be set to 00 as the burst order is fixed per nibble 

• A2 selects the burst order: 

– BL8, A2 is set to 0, and the burst order is fixed to 0, 1, 2, 3, 4, 5, 6, 7 

• For burst chop 4 cases, the burst order is switched on the nibble base along with the following: 

– $\mathbf { A } 2 = 0$ ; burst order $= 0$ , 1, 2, 3 

– $\mathrm { A } 2 = 1$ ; burst order $= 4$ , 5, 6, 7 

• Burst order bit 0 (the first bit) is assigned to LSB, and burst order bit 7 (the last bit) is assigned to MSB 

• A[9:3] are a “Don’t Care” 

• A10 is a “Don’t Care” 

• A11 is a “Don’t Care” 

• A12: Selects burst chop mode on-the-fly, if enabled within MR0 

• A13 is a “Don’t Care” 

• BA[2:0] are a “Don’t Care” 

# MPR Register Address Definitions and Bursting Order

The MPR currently supports a single data format. This data format is a predefined read pattern for system calibration. The predefined pattern is always a repeating 0–1 bit pattern. 

Examples of the different types of predefined READ pattern bursts are shown in the following figures. 


Table 78: MPR Readouts and Burst Order Bit Mapping


<table><tr><td>MR3[2]</td><td>MR3[1:0]</td><td>Function</td><td>Burst Length</td><td>Read A[2:0]</td><td>Burst Order and Data Pattern</td></tr><tr><td rowspan="3">1</td><td rowspan="3">00</td><td rowspan="3">READ predefined pattern for system calibration</td><td>BL8</td><td>000</td><td>Burst order: 0, 1, 2, 3, 4, 5, 6, 7 
Predefined pattern: 0, 1, 0, 1, 0, 1, 0, 1</td></tr><tr><td>BC4</td><td>000</td><td>Burst order: 0, 1, 2, 3 
Predefined pattern: 0, 1, 0, 1</td></tr><tr><td>BC4</td><td>100</td><td>Burst order: 4, 5, 6, 7 
Predefined pattern: 0, 1, 0, 1</td></tr><tr><td rowspan="3">1</td><td rowspan="3">01</td><td rowspan="3">RFU</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td rowspan="3">1</td><td rowspan="3">10</td><td rowspan="3">RFU</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td rowspan="3">1</td><td rowspan="3">11</td><td rowspan="3">RFU</td><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>N/A</td><td>N/A</td><td>N/A</td></tr><tr><td>N/A</td><td>N/A</td><td>N/A</td></tr></table>


Note: 1. Burst order bit 0 is assigned to LSB, and burst order bit 7 is assigned to MSB of the selected MPR agent. 



Figure 62 : MPR System Read Cal ibration with BL8: Fixed Burst Order Si ng le Readout


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/1511e213587a6a590dc31ec18c3744dab8f7e2f47ded5ef6dad02106440f42b5.jpg)



N otes : 1 . R EA D w i t h B L8 e i t h e r by M RS o r OT F.



2 . M e m o ry co nt ro l l e r m u st d r i ve 0 o n A [ 2 : 0 ] .



Figure 63: MPR System Read Cal ibration with BL8: Fixed Burst Order, Back-to-Back Readout


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/a26c6b24b16db33cadf406f573728cf4769146d512e7e026bd3a8710469f70e4.jpg)



N otes : 1 . R EA D w i t h B L8 e i t h e r by M RS o r OT F.



2 . M e m o ry co nt ro l l e r m u st d r i ve 0 o n A [ 2 : 0 ] .



Figure 64: MPR System Read Cal ibration with BC4: Lower N ibble, Then Upper N ibble


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/422e755a0997eaa37743444af6634c7b7b4992cb24b8a1208fd50556967b8f2c.jpg)


N otes : 1 . R EAD w it h B C4 e it h e r by M RS o r OTF. 

2 . M e m o ry co n t ro l l e r m u st d r i ve 0 o n A [ 1 : 0 ] . 

3 . $\mathsf { A } 2 = 0$ s e l e cts l owe r 4 n i b b l e b i ts 0 . . . 3 . 

4 . $\mathsf { A } 2 = 1$ s e l e cts u p p e r 4 n i b b l e b i ts 4 . . . 7 . 


Figure 65: MPR System Read Cal ibration with BC4: Upper N ibble, Then Lower N ibble


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/a22f24cd6906dd42d58bc35b921a4111a46da42ce6683c2807661eca0fe7f2db.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/e6f9cad92171e03cb5d6c404dbde9fa70d7b50fa3573c6c3881c3fa80922e658.jpg)


I n d i cates b rea k i n t i m e sca l e 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/c3b877cb2c495a49cd916e82f8a3d23986b55b6da20423adc069a616224df229.jpg)


Do n ’t Ca re 

N otes : 1 . R EA D w i t h B C4 e i t h e r by M RS o r OT F. 

2 . M e m o ry co n t ro l l e r m u st d r i ve 0 o n A [ 1 : 0 ] . 

3 . $\mathsf { A } 2 = 1$ se l e cts u p p e r 4 n i b b l e b i ts 4 . . . 7 . 

4 . $\mathsf { A } 2 = 0$ s e l e cts l owe r 4 n i b b l e b i ts 0 . . . 3 . 

# MPR Read Predefined Pattern

The predetermined read calibration pattern is a fixed pattern of 0, 1, 0, 1, 0, 1, 0, 1. The following is an example of using the read out predetermined read calibration pattern. The example is to perform multiple reads from the multipurpose register to do system level read timing calibration based on the predetermined and standardized pattern. 

The following protocol outlines the steps used to perform the read calibration: 

1. Precharge all banks 

2. After t RP is satisfied, set MRS, $\mathrm { M R } 3 [ 2 ] = 1$ and $\mathrm { M R } 3 [ 1 { : } 0 ] = 0 0$ . This redirects all subsequent reads and loads the predefined pattern into the MPR. As soon as t MRD and t MOD are satisfied, the MPR is available 

3. Data WRITE operations are not allowed until the MPR returns to the normal DRAM state 

4. Issue a read with burst order information (all other address pins are “Don’t Care”): 

• $\mathrm { A } [ 1 { : } 0 ] = 0 0$ (data burst order is fixed starting at nibble) 

• $\mathbf { A } \mathbf { 2 } = \mathbf { 0 }$ (for BL8, burst order is fixed as 0, 1, 2, 3, 4, 5, 6, 7) 

• $\mathrm { A } 1 2 = 1$ (use BL8) 

5. After $\mathrm { R L } = \mathrm { A L } + \mathrm { C L }$ , the DRAM bursts out the predefined read calibration pattern $( 0 , 1 , 0 , 1 , 0 , 1 , 0 , 1 )$ 

6. The memory controller repeats the calibration reads until read data capture at memory controller is optimized 

7. After the last MPR READ burst and after t MPRR has been satisfied, issue MRS, $\mathbf { M } \mathbf { R } 3 [ 2 ] = 0$ , and MR3[1:0] $=$ “Don’t Care” to the normal DRAM state. All subsequent read and write accesses will be regular reads and writes from/to the DRAM array 

8. When t MRD and t MOD are satisfied from the last MRS, the regular DRAM commands (such as activate a memory bank for regular read or write access) are permitted 

# MODE REGISTER SET (MRS) Command

The mode registers are loaded via inputs BA[2:0], A[13:0]. BA[2:0] determine which mode register is programmed: 

• $\mathrm { B A } 2 = 0$ , $\mathrm { B A } 1 = 0$ , $\mathrm { B A } 0 = 0$ for MR0 

• $\mathbf { B A } 2 = 0$ , $\mathrm { B A } 1 = 0$ , $\mathrm { B A } 0 = 1$ for MR1 

• $\mathbf { B A } 2 = 0$ , $\mathrm { B A } 1 = 1$ , $\mathrm { B A } 0 = 0$ for MR2 

• $\mathrm { B A } 2 = 0$ , $\mathrm { B A } 1 = 1$ , $\mathrm { B A } 0 = 1$ for MR3 

The MRS command can only be issued (or re-issued) when all banks are idle and in the precharged state (t RP is satisfied and no data bursts are in progress). The controller must wait the specified time t MRD before initiating a subsequent operation such as an ACTIVATE command (see Figure 52 (page 138)). There is also a restriction after issuing an MRS command with regard to when the updated functions become available. This parameter is specified by t MOD. Both t MRD and t MOD parameters are shown in Figure 52 (page 138) and Figure 53 (page 139). Violating either of these requirements will result in unspecified operation. 

# ZQ CALIBRATION Operation

The ZQ CALIBRATION command is used to calibrate the DRAM output drivers $( \mathrm { R } _ { \mathrm { O N } } )$ and ODT values $\left( \mathrm { R } _ { \mathrm { T T } } \right)$ over process, voltage, and temperature, provided a dedicated 240Ω $( \pm 1 \% )$ external resistor is connected from the DRAM’s ZQ ball to VSSQ. 

DDR3 SDRAM require a longer time to calibrate $\operatorname { R o n }$ and ODT at power-up initialization and self refresh exit, and a relatively shorter time to perform periodic calibrations. DDR3 SDRAM defines two ZQ CALIBRATION commands: ZQCL and ZQCS. An example of ZQ calibration timing is shown below. 

All banks must be precharged and t RP must be met before ZQCL or ZQCS commands can be issued to the DRAM. No other activities (other than issuing another ZQCL or ZQCS command) can be performed on the DRAM channel by the controller for the duration of t ZQinit or t ZQoper. The quiet time on the DRAM channel helps accurately calibrate $\mathrm { R _ { O N } }$ and ODT. After DRAM calibration is achieved, the DRAM should disable the ZQ ball’s current consumption path to reduce power. 

ZQ CALIBRATION commands can be issued in parallel to DLL RESET and locking time. Upon self refresh exit, an explicit ZQCL is required if ZQ calibration is desired. 

In dual-rank systems that share the ZQ resistor between devices, the controller must not enable overlap of t ZQinit, t ZQoper, or t ZQCS between ranks. 


Figure 66: ZQ CALIBRATION Timing (ZQCL and ZQCS)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/9a8a6caa5eeebabfd91e5515209535bf7f1fbcfd0c20ba4e760d23c4c51fa97d.jpg)


Notes: 1. CKE must be continuously registered HIGH during the calibration procedure. 

2. ODT must be disabled via the ODT signal or the MRS during the calibration procedure. 

3. All devices connected to the DQ bus should be High-Z during calibration. 

# ACTIVATE Operation

Before any READ or WRITE commands can be issued to a bank within the DRAM, a row in that bank must be opened (activated). This is accomplished via the ACTIVATE command, which selects both the bank and the row to be activated. 

After a row is opened with an ACTIVATE command, a READ or WRITE command may be issued to that row, subject to the t RCD specification. However, if the additive latency is programmed correctly, a READ or WRITE command may be issued prior to $\mathrm { { \ t R C D } }$ (MIN). In this operation, the DRAM enables a READ or WRITE command to be issued after the ACTIVATE command for that bank, but prior to t RCD (MIN) with the requirement that (ACTIVATE-to-READ/WRITE) $+ \mathrm { A L } \ge \mathrm { { ^ { t } R C D } }$ (MIN) (see Posted CAS Additive Latency). t RCD (MIN) should be divided by the clock period and rounded up to the next whole number to determine the earliest clock edge after the ACTIVATE command on which a READ or WRITE command can be entered. The same procedure is used to convert other specification limits from time units to clock cycles. 

When at least one bank is open, any READ-to-READ command delay or WRITE-to-WRITE command delay is restricted to t CCD (MIN). 

A subsequent ACTIVATE command to a different row in the same bank can only be issued after the previous active row has been closed (precharged). The minimum time interval between successive ACTIVATE commands to the same bank is defined by t RC. 

A subsequent ACTIVATE command to another bank can be issued while the first bank is being accessed, which results in a reduction of total row-access overhead. The minimum time interval between successive ACTIVATE commands to different banks is defined by t RRD. No more than four bank ACTIVATE commands may be issued in a given t FAW (MIN) period, and the t RRD (MIN) restriction still applies. The t FAW (MIN) parameter applies, regardless of the number of banks already opened or closed. 


Figure 67: Example: Meeting t RRD (MIN) and t RCD (MIN)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/e4d464069822978057ac2617e434e612afb602f1b006acaf1bd0f4c17c32f702.jpg)



Figure 68: Example: t FAW


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/45c5c87fe30519a13644ea0d58da655c25b849ae266d08e0a48bed1d3c8a5b51.jpg)


# READ Operation

READ bursts are initiated with a READ command. The starting column and bank addresses are provided with the READ command and auto precharge is either enabled or disabled for that burst access. If auto precharge is enabled, the row being accessed is automatically precharged at the completion of the burst. If auto precharge is disabled, the row will be left open after the completion of the burst. 

During READ bursts, the valid data-out element from the starting column address is available READ latency (RL) clocks later. RL is defined as the sum of posted CAS additive latency (AL) and CAS latency (CL) $( \mathrm { R L } = \mathrm { A L } + \mathrm { C L } )$ . The value of AL and CL is programmable in the mode register via the MRS command. Each subsequent data-out element is valid nominally at the next positive or negative clock edge (that is, at the next crossing of CK and CK#). Figure 69 shows an example of RL based on a CL setting of 8 and an AL setting of 0. 


Figure 69: READ Latency


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/df546a71bd4d1530c35da806f0a7b0d866ebbf29d2412d72470264d32cff1e5c.jpg)


Notes: 1. DO $n =$ data-out from column n. 

2. Subsequent elements of data-out appear in the programmed order following DO n. 

DQS, DQS# is driven by the DRAM along with the output data. The initial LOW state on DQS and HIGH state on DQS# is known as the READ preamble (t RPRE). The LOW state on DQS and the HIGH state on DQS#, coincident with the last data-out element, is known as the READ postamble (t RPST). Upon completion of a burst, assuming no other commands have been initiated, the DQ goes High-Z. A detailed explanation of t DQSQ (valid data-out skew), t QH (data-out window hold), and the valid data window are depicted in Figure 80 (page 169). A detailed explanation of t DQSCK (DQS transition skew to CK) is also depicted in Figure 80 (page 169). 

Data from any READ burst may be concatenated with data from a subsequent READ command to provide a continuous flow of data. The first data element from the new burst follows the last element of a completed burst. The new READ command should be issued $\mathrm { { } ^ { t } C C D }$ cycles after the first READ command. This is shown for BL8 in Figure 70 (page 163). If BC4 is enabled, t CCD must still be met, which will cause a gap in the data output, as shown in Figure 71 (page 163). Nonconsecutive READ data is reflected in Figure 72 (page 164). DDR3 SDRAM does not allow interrupting or truncating any READ burst. 

Data from any READ burst must be completed before a subsequent WRITE burst is allowed. An example of a READ burst followed by a WRITE burst for BL8 is shown in Figure 73 (page 164) (BC4 is shown in Figure 74 (page 165)). To ensure the READ data is completed before the WRITE data is on the bus, the minimum READ-to-WRITE timing is $\mathrm { R L } + \mathrm { ^ t C C D } \cdot \mathrm { W L } + 2 \mathrm { ^ t C K } .$ . 

A READ burst may be followed by a PRECHARGE command to the same bank, provided auto precharge is not activated. The minimum READ-to-PRECHARGE command spacing to the same bank is four clocks and must also satisfy a minimum analog time from the READ command. This time is called t RTP (READ-to-PRECHARGE). t RTP starts AL cycles later than the READ command. Examples for BL8 are shown in Figure 75 (page 165) and BC4 in Figure 76 (page 166). Following the PRECHARGE command, a subsequent command to the same bank cannot be issued until t RP is met. The PRECHARGE command followed by another PRECHARGE command to the same bank is allowed. However, the precharge period will be determined by the last PRECHARGE command issued to the bank. 

If A10 is HIGH when a READ command is issued, the READ with auto precharge function is engaged. The DRAM starts an auto precharge operation on the rising edge, which is $\mathrm { A L + ^ { t } R T P }$ cycles after the READ command. DRAM support a t RAS lockout feature (see Figure 78 (page 166)). If t RAS (MIN) is not satisfied at the edge, the starting point of the auto precharge operation will be delayed until t RAS (MIN) is satisfied. If t RTP (MIN) is not satisfied at the edge, the starting point of the auto precharge operation is delayed until t RTP (MIN) is satisfied. In case the internal precharge is pushed out by t RTP, t RP starts at the point at which the internal precharge happens (not at the next rising clock edge after this event). The time from READ with auto precharge to the next ACTIVATE command to the same bank is $\mathrm { A L } + ( \mathrm { ^ t R T P + ^ { t } R P } ) ^ { * }$ , where * means rounded up to the next integer. In any event, internal precharge does not start earlier than four clocks after the last $_ { 8 n }$ -bit prefetch. 


Figure 70: Consecutive READ Bursts (BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/534c9139ec7b125d06809c2618b55308b6ea35b620ec0a38bfc6a752648b61b1.jpg)


N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . Th e B L8 sett i n g i s a ct i vate d by e i t h e r M R0 [ 1 : 0] $= 0 0$ o r M R 0 [ 1 : 0 ] $= 0 1$ a n d $\mathsf { A } 1 2 = 1$ d u ri n g R EAD co m m a n d at T0 a n d T4. 

3 . D O n (o r b) $=$ d ata -o ut fro m co l u m n n (o r co l u m n b) . 

4 . B L8, ${ \mathsf { R L } } = 5$ ( $\mathtt { C L } = 5$ , ${ \mathsf { A L } } = 0$ ) . 


Fig ure 7 1 : Consecutive READ Bursts (BC4)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/37c965d21c1b8389f447fc50740c6c85c1be65db265c13a15cb13fa2f827dab8.jpg)


N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . Th e B C4 sett i n g i s a ct i vate d by e i t h e r M R0 [ 1 : 0] $= 1 0$ o r M R 0 [ 1 : 0 ] $= 0 1$ a n d $\mathsf { A } 1 2 = 0$ d u ri n g R EAD co m m a n d at T0 a n d T4. 

3 . D O n (o r b) $=$ d ata -o ut fro m co l u m n n (o r co l u m n b) . 

4. B C4, ${ \mathsf { R L } } = 5$ (C L = 5 , ${ \mathsf { A L } } = 0 $ ) . 


Figure 72 : Nonconsecutive READ Bursts


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/31a010c4badf1ee79415ebabddcadf95905ab4f75bc112b2891b4d8c0627f993.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/c26b51898ec5e082e636b65ef9fc5c32187dac18a87b9ebc24619c7cf76a33f0.jpg)


Tra n s it i o n i n g Data 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/b52ee3ed5df9e1a688cd4872727cb0bb3fc329f9ec567926356bb85489aa5701.jpg)


D o n ’t Ca re 

N otes : 1 . ${ \sf A L } = 0$ , $\mathtt { R L } = 8$ 

2 . D O n (o r b) = d ata -o ut f ro m co l u m n n (o r co l u m n b) . 

3 . Seve n s u bseq u e nt e l e m e nts of d ata -o ut a p pea r i n t h e p rog ra m m ed o rd e r fo l l owi n g D O n . 

4. Seve n s u bseq u e nt e l e m e nts of d ata -o ut a p pea r i n th e p rog ra m m ed o rd e r fo l l owi n g D O b . 


Figure 73 : READ (BL8) to WRITE (BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/e38702156c287f97a050c063e961ee9877f66ca1390ae73721ff782487b70b64.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/ab283abc8cb1b4bd52093c809970c154dfe7bb164b34c3fe1390d7cea6a1b788.jpg)


Tra n s it i o n i n g Data 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/91e96ad6a659fc1665346d17ca6d0bb4d6d7b91340afc0456e625e4ff2a2496c.jpg)


Do n ’t Ca re 

N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . Th e B L8 sett i n g i s a ct i vate d by e i t h e r M R0 [ 1 : 0] $= 0 0$ o r M R 0 [ 1 : 0 ] $= 0 1$ a n d $\mathsf { A } 1 2 = 1$ d u r i n g t h e R EAD co m m a n d at T0, a n d t h e WR ITE co m m a n d at T6 . 

3 . D O $n =$ d ata -o ut fro m co l u m n, D I $b =$ d ata - i n fo r co l u m n b . 

4 . B L8, R L = 5 $\mathrm { \sf ~ A L } = 0$ , ${ \mathsf { C L } } = 5$ ) , W L $= 5$ ${ \mathrm { { A L } } } = 0$ , CW L = 5 ) . 


Figure 74: READ (BC4) to WRITE (BC4) OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/9f283b76dafdd45bd907e7daafa063a7e1dc5d6ce081f1a3e33bc06439455303.jpg)


N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . Th e B C4 OTF sett i n g i s a ct ivated by M R0 [ 1 : 0] a n d $\mathsf { A } 1 2 = 0$ d u r i n g R EAD co m m a n d at T0 a n d WR ITE co m m a n d at T 4 . 

3 . D O $n =$ d ata -o ut fro m co l u m n $n ;$ D I $n =$ d ata - i n f ro m co l u m n b . 

4. B C4, ${ \mathsf { R L } } = 5$ (A L - 0, ${ \mathsf { C L } } = 5$ ) , W L = 5 ${ \mathrm { . A L } } = 0$ , ${ \mathsf { C W L } } = 5$ ) . 


Figure 7 5: READ to PRECHARG E (BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/e96fe34846db5bcbc03dc87d7a2980cf90279331f4f337f8d1150025ed06abf5.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/bbb8da67735ed8d327bdffc9ab93a59a8f110be8da3b816d8f1c73408e6e455e.jpg)



Tra n s it i o n i n g Data


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/ba911a26c10ec5434c89d7621e1f67dbb94e4d6c2bdd60647c0f79cacb977a5b.jpg)



Do n ’t Ca re



Figure 76: READ to PRECHARGE (BC4)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/ca84441a4d1a846d2759100646d47196e121409b775e7c5aae763df926f48844.jpg)



Figure 77 : READ to PRECHARG E (AL = 5, $\mathbf { C L } = { \mathfrak { G } } )$ )


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/c065d09ac37c1bd2a5afcb46e062c26706f21d0496f9a77a4880d39153cbe29b.jpg)



Figure 78: READ with Auto Precharge (AL = 4, CL = 6)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/aabc83fecbde81907c7d75492632b5d53d851c73d01fddb4bf2efcda76fb8e23.jpg)


DQS to DQ output timing is shown in Figure 79 (page 168). The DQ transitions between valid data outputs must be within t DQSQ of the crossing point of DQS, DQS#. DQS must also maintain a minimum HIGH and LOW time of t QSH and t QSL. Prior to the READ preamble, the DQ balls will either be floating or terminated, depending on the status of the ODT signal. 

Figure 80 (page 169) shows the strobe-to-clock timing during a READ. The crossing point DQS, DQS# must transition within $\pm ^ { \mathrm { t D Q S C K } }$ of the clock crossing point. The data out has no timing relationship to CK, only to DQS, as shown in Figure 80 (page 169). 

Figure 80 (page 169) also shows the READ preamble and postamble. Typically, both DQS and DQS# are High-Z to save power $\mathrm { ( V _ { D D Q } ) }$ . Prior to data output from the DRAM, DQS is driven LOW and DQS# is HIGH for t RPRE. This is known as the READ preamble. 

The READ postamble, t RPST, is one half clock from the last DQS, DQS# transition. During the READ postamble, DQS is driven LOW and DQS# is HIGH. When complete, the DQ is disabled or continues terminating, depending on the state of the ODT signal. Figure 83 (page 171) demonstrates how to measure t RPST. 


Figure 79: Data Output Ti m i ng – tDQSQ and Data Val id Wi ndow


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/94836ef5f89709245ceef08b7ceee1f55c9d07de55e567d1a501d43989d03892.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/7a162f41e6a778560ac3d3c3da43a8c50d6714a8997dffd09bcb332094042198.jpg)


D o n ’t Ca re 

N otes : 1 . N O P co m m a n d s a re s h own fo r ea se of i l l u st rat i o n ; ot h e r co m m a n d s m ay be va l i d at t h ese t i m es . 

2 . T h e B L8 sett i n g i s a ct i vate d by e i t h e r M R0 [ 1 , 0 ] = 0, 0 o r M R0 [ 0, 1 ] = 0, 1 a n d $\mathsf { A } 1 2 = 1$ d u r i n g R EAD co m m a n d at T 0 . 

3 . D O $n =$ d ata -o ut fro m co l u m n n . 

4 . B L8, ${ \mathsf { R L } } = 5$ ${ \mathrm { ( A L } } = 0$ , ${ \mathsf { C L } } = 5$ ) . 

5 . O ut p ut t i m i n g s a re refe re n ced to $\mathsf { V } _ { \mathsf { D D Q } } / 2$ a n d D LL o n a n d l ocked . 

6 . tD QSQ d efi n es th e s kew betwee n D QS, D QS# to d ata a n d d oes n ot d efi n e D QS, D QS# to C K. 

7 . E a r l y d ata t ra n s it i o n s m ay n ot a l ways h a p pe n at t h e sa m e D Q . D ata t ra n s it i o n s of a D Q ca n be ea r l y o r l ate w it h i n a b u rst . 

t HZ and t LZ transitions occur in the same access time as valid data transitions. These parameters are referenced to a specific voltage level that specifies when the device output is no longer driving t HZDQS and t HZDQ, or begins driving t LZDQS, t LZDQ. Figure 81 (page 170) shows a method of calculating the point when the device is no longer driving t HZDQS and t HZDQ, or begins driving t LZDQS, t LZDQ, by measuring the signal at two different voltages. The actual voltage measurement points are not critical as long as the calculation is consistent. The parameters t LZDQS, t LZDQ, t HZDQS, and t HZDQ are defined as single-ended. 


Figure 80: Data Strobe Timing – READs


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/696c2504c41833998fd15d9aebe81c9773180ccd32ce13860290bba0ca3bd80e.jpg)



Figure 81: Method for Calculating t LZ and t HZ


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/7b69d00665aa92ed78668783c56d452ea8294ceddf602faa6a7950ea1d3f3ebb.jpg)



t HZDQS, t HZDQ end point = 2 × T1 - T2


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/f19d74902d885bd2d288fcbe715205f801e9445a0fa917ed9938a22688f2b138.jpg)



t LZDQS, t LZDQ begin point = 2 × T1 - T2


Notes: 1. Within a burst, the rising strobe edge is not necessarily fixed at t DQSCK (MIN) or t DQSCK (MAX). Instead, the rising strobe edge can vary between t DQSCK (MIN) and t DQSCK (MAX). 

2. The DQS HIGH pulse width is defined by t QSH, and the DQS LOW pulse width is defined by $^ \mathrm { t } Q \mathsf { S L }$ . Likewise, t LZDQS (MIN) and t HZDQS (MIN) are not tied to t DQSCK (MIN) (early strobe case), and t LZDQS (MAX) and t HZDQS (MAX) are not tied to t DQSCK (MAX) (late strobe case); however, they tend to track one another. 

3. The minimum pulse width of the READ preamble is defined by t RPRE (MIN). The minimum pulse width of the READ postamble is defined by t RPST (MIN). 


Figure 82: t RPRE Timing


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/b6a84de831ed897e2a6c73d258aecd07f043d81e5dc46c0e21e16f06fde32828.jpg)



Figure 83: t RPST Timing


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/e1dc77a3cdc6fac9059b791165504d1cd23e1e4b6082fcacd5a1a4665b63b016.jpg)


# WRITE Operation

WRITE bursts are initiated with a WRITE command. The starting column and bank addresses are provided with the WRITE command, and auto precharge is either enabled or disabled for that access. If auto precharge is selected, the row being accessed is precharged at the end of the WRITE burst. If auto precharge is not selected, the row will remain open for subsequent accesses. After a WRITE command has been issued, the WRITE burst may not be interrupted. For the generic WRITE commands used in Figure 86 (page 174) through Figure 94 (page 179), auto precharge is disabled. 

During WRITE bursts, the first valid data-in element is registered on a rising edge of DQS following the WRITE latency (WL) clocks later and subsequent data elements will be registered on successive edges of DQS. WRITE latency (WL) is defined as the sum of posted CAS additive latency (AL) and CAS WRITE latency (CWL): $\mathrm { W L } = \mathrm { A L } + \mathrm { C W L }$ . The values of AL and CWL are programmed in the MR0 and MR2 registers, respectively. Prior to the first valid DQS edge, a full cycle is needed (including a dummy crossover of DQS, DQS#) and specified as the WRITE preamble shown in Figure 86 (page 174). The half cycle on DQS following the last data-in element is known as the WRITE postamble. 

The time between the WRITE command and the first valid edge of DQS is WL clocks $\pm \mathrm { { ^ { t } D Q S S } }$ . Figure 87 (page 175) through Figure 94 (page 179) show the nominal case where $\mathrm { { ^ t D Q S S } = 0 n s }$ ; however, Figure 86 (page 174) includes t DQSS (MIN) and t DQSS (MAX) cases. 

Data may be masked from completing a WRITE using data mask. The data mask occurs on the DM ball aligned to the WRITE data. If DM is LOW, the WRITE completes normally. If DM is HIGH, that bit of data is masked. 

Upon completion of a burst, assuming no other commands have been initiated, the DQ will remain High-Z, and any additional input data will be ignored. 

Data for any WRITE burst may be concatenated with a subsequent WRITE command to provide a continuous flow of input data. The new WRITE command can be t CCD clocks following the previous WRITE command. The first data element from the new burst is applied after the last element of a completed burst. Figure 87 (page 175) and Figure 88 (page 175) show concatenated bursts. An example of nonconsecutive WRITEs is shown in Figure 89 (page 176). 

Data for any WRITE burst may be followed by a subsequent READ command after t WTR has been met (see Figure 90 (page 176), Figure 91 (page 177), and Figure 92 (page 178)). 

Data for any WRITE burst may be followed by a subsequent PRECHARGE command, providing t WR has been met, as shown in Figure 93 (page 179) and Figure 94 (page 179). 

Both t WTR and t WR starting time may vary, depending on the mode register settings (fixed BC4, BL8 versus OTF). 


Figure 84: t WPRE Timing


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/d600b3602c4471f400f650116dc91401882df22d0fd545be2a755bb60c93bac6.jpg)



Figure 85: t WPST Timing


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/f666d2e03e451efc418fb9ea40556d478f44230f16b6e4e6d991ff13dd47dea4.jpg)



Figure 86: WRITE Burst


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/418505e32e55af15452c1993a65ce747e619366e630c26334940c8e64c6fb7d3.jpg)


Notes: 1. NOP commands are shown for ease of illustration; other commands may be valid at these times. 

2. The BL8 setting is activated by either $\mathsf { M R } 0 [ 1 : 0 ] = 0 0$ $= 0 0$ or $\mathsf { M R } 0 [ 1 : 0 ] = 0 1$ and $\mathsf { A } 1 2 = 1$ during the WRITE command at T0. 

3. DI $n =$ data-in for column n. 

4. BL8, WL $= 5$ ( ${ \mathrm { A L } } = 0$ , CWL = 5). 

5. t DQSS must be met at each rising clock edge. 

6. t WPST is usually depicted as ending at the crossing of DQS, DQS#; however, t WPST actually ends when DQS no longer drives LOW and DQS# no longer drives HIGH. 


Figure 87 : Consecutive WRITE (BL8) to WRITE (BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/063a7863955f15771d0ea95d35fa5ae5bd5552b80a37f01b16d510ecc8f4588e.jpg)


N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . Th e B L8 sett i n g i s a ct i vate d by e i t h e r M R0 [ 1 : 0] $= 0 0$ o r M R 0 [ 1 : 0 ] $= 0 1$ a n d $\mathsf { A } 1 2 = 1$ d u r i n g t h e WR ITE co m m a n d s at T0 a n d T4. 

3 . D I n (o r b) = d a t a - i n fo r c o l u m n n (o r c o l u m n b) . 

4 . B L8, WL $= 5$ $\mathrm { \sf ~ A L } = 0$ , ${ \mathsf { C W L } } = 5$ ) . 


Figure 88: Consecutive WRITE (BC4) to WRITE (BC4) via OTF


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/1eb8e1020e223f2b66b8b39f069aa1e40aca80657da389ba4f2a85c8a810632e.jpg)


N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . B C4, WL $= 5$ $\mathrm { \sf ~ A L } = 0$ , ${ \mathsf { C W L } } = 5$ 

3 . D I n (o r b) = d a t a - i n fo r c o l u m n n (o r c o l u m n b) . 

4 . Th e B C4 sett i n g i s a ct ivated by $\mathsf { M R } 0 [ 1 : 0 ] = 0 1$ a n d $\mathsf { A } 1 2 = 0$ d u r i n g t h e WR ITE co m m a n d at T0 a n d T4. 

5 . I f set v i a M RS (f i xe d ) tW R a n d tWT R wo u l d sta rt T 1 1 (2 cyc l es e a r l i e r) . 


Figure 89: Nonconsecutive WRITE to WRITE


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/84e64995cffd9bba51e2272504742be461baa80d54ee7f745d55efc65ad9e60f.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/fc7fd80a9753c7a0f531043f595285218349c94c12a31faa0aa3aa5db8ee78d8.jpg)


Tra n s it i o n i n g D ata 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/65b037d40cec9d143535ba9a65d60799eb01c7cf1be0d5c9dfd18f0087d52df5.jpg)


Do n 't Ca re 

N ot e s : 1 . D I n (o r b) $=$ d ata - i n fo r co l u m n n (o r co l u m n b) . 

2 . Seve n s u bseq u e nt e l e m e nts of d ata - i n a re a p p l i ed i n t h e p rog ra m m ed o rd e r fo l l owi n g D O n . 

3 . E a ch WR ITE co m m a n d m ay be to a ny ba n k. 

4 . S h own fo r WL $= 7$ (CW L = 7 , ${ \mathsf { A L } } = 0 ,$ ) . 


Figure 90: WRITE (BL8) to READ (BL8)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/2a6ff929c87f1b4d698faccf7fff146f29adfbbce4820057bbce6a72dd8ef3c4.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/263525127c3b76eca16e32c85c590d4a9ab94e038a2bd8a32c40899d363ac686.jpg)


I n d i cates b rea k i n t i m e sca l e 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/82ecb6c2ca5094ebf3dd29ca7d0b2f3e8ce7859ff20a952ab937691ec68222d2.jpg)


Tra n s it i o n i n g Data 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/82f70008aa41274b4d2dd56255e53c0fd5f96b5ec720f81bbdc0bbeb9b4ab85c.jpg)


D o n ’t Ca re 

N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . tWT R co nt ro l s t h e WR I T E -to- R EA D d e l ay to t h e sa m e d ev i ce a n d sta rts w i t h t h e f i rst r i s i n g c l oc k e d g e a fte r t h e l a st w r i te d ata s h ow n at T9 . 

3 . Th e B L8 sett i n g i s a ct i vate d by e i t h e r $\mathsf { M R } 0 [ 1 : 0 ] = 0 0$ o r $\mathsf { M R } 0 [ 1 : 0 ] = 0 1$ a n d $\mathsf { M R } 0 [ 1 2 ] = 1$ $= 1$ d u ri n g th e WR ITE co m m a n d at T0 . Th e R EAD co m m a n d at Ta 0 ca n be e it h e r B C4 o r B L8, d e pe n d i n g o n M R0 [ 1 : 0] a n d t h e A 1 2 stat u s at Ta 0 . 

4 . D I $n =$ d ata - i n fo r co l u m n n . 

5 . R L = 5 ${ \mathrm { A L } } = 0$ , ${ \mathsf { C L } } = 5 ,$ ) , W L = 5 ${ \mathrm { . A L } } = 0$ , CW L = 5 ) . 


Figure 91 : WRITE to READ (BC4 Mode Reg ister Setti ng)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/5ed3feedbc7f9648172250330037df4bee5f6e212b49585d5c10e1d01198dae0.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/fdddf12ee77ad6e3cd2cd7b1a3acdf8765a1749fe3f6f3629776afbaf8cc0e7b.jpg)


I n d i cates b rea k i n t i m e sca l e 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/19442927d4d5bf9c8aa16cbfaf3bfabfb80686a41c427c5e40416d8e5c09484a.jpg)


Tra n s it i o n i n g Data 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/8bb40525375742853795ba2b364f0645e1551d4fc8544d6b7bd1a7292a911580.jpg)


D o n ’t Ca re 

N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . tWT R co nt ro l s t h e WR I T E -to- R EA D d e l ay to t h e sa m e d ev i ce a n d sta rts w i t h t h e f i rst r i s i n g c l oc k e d g e a fte r t h e l a st w r i te d ata s h ow n at T7 . 

3 . Th e fixed B C4 sett i n g i s a ct ivated by $\mathsf { M R } 0 [ 1 : 0 ] = 1 0$ $= 1 0$ d u ri n g th e WR ITE co m m a n d at T0 a n d th e R EAD co m m a n d at Ta 0 . 

4 . D I $n =$ d ata - i n fo r co l u m n n . 

5 . B C4 (f i xe d ), ${ \mathsf { W L } } = 5$ ${ \mathrm { \ A L } } = 0$ , CW L = 5 ) , $\mathsf { R L } = 5$ (A L = 0, C L = 5 ) . 


Figure 92 : WRITE (BC4 OTF) to READ (BC4 OTF)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/1b5527c4344bbf0cd888e5ae788af01ee4824b90a02513cc8ce6409590ed9031.jpg)


N otes : 1 . N O P co m m a n d s a re s h ow n fo r e a se of i l l u st rat i o n ; ot h e r co m m a n d s m ay b e va l i d at t h ese t i m es . 

2 . tWTR co nt ro l s t h e WR I T E -to- R EAD d e l ay to t h e sa m e d ev i ce a n d sta rts afte r $^ \mathrm { t } { \tt B } { \tt L }$ 

3 . Th e B C4 OTF sett i n g i s a ct i vated by M R0 [ 1 : 0] $= 0 1$ a n d $\mathsf { A } 1 2 = 0$ d u ri n g th e WR ITE co m m a n d at T0 a n d th e R EAD co m m a n d at Tn . 

4 . D I $n =$ d ata - i n fo r co l u m n n . 

5 . B C4, ${ \mathsf { R L } } = 5$ $\mathrm { \sf ~ A L } = 0$ , ${ \mathsf { C L } } = 5$ ) , W L = 5 (A L = 0, CW L = 5 ) . 


Figure 93: WRITE (BL8) to PRECHARGE


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/40ac9d81680fe112f3754c257f265bef3faef55a3fdd49f83fb27ab93c055a62.jpg)


Notes: 1. DI $n =$ data-in from column n. 

2. Seven subsequent elements of data-in are applied in the programmed order following DO n. 

3. Shown for WL = 7 ( $\mathtt { A L } = 0$ , CWL = 7). 


Figure 94: WRITE (BC4 Mode Register Setting) to PRECHARGE


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/c4827583c1b0d6ea1b27c705ede50d732eb3fcb6a755c2d521e9a15477cd8efe.jpg)


Notes: 1. NOP commands are shown for ease of illustration; other commands may be valid at these times. 

2. The write recovery time (t WR) is referenced from the first rising clock edge after the last write data is shown at T7. t WR specifies the last burst WRITE cycle until the PRECHARGE command can be issued to the same bank. 

3. The fixed BC4 setting is activated by MR0[1:0] $= 1 0$ during the WRITE command at T0. 

4. DI $n =$ data-in for column n. 

5. BC4 (fixed), WL $= 5 ,$ , ${ \mathsf { R L } } = 5$ . 


Figure 95: WRITE (BC4 OTF) to PRECHARGE


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/9fdc3498b9f9464b7324b4c92e520dcb2dc052a426aadca4088c42a6e42c9a1f.jpg)


Notes: 1. NOP commands are shown for ease of illustration; other commands may be valid at these times. 

2. The write recovery time $( ^ { \mathrm { t } } \mathsf { W R } )$ is referenced from the rising clock edge at T9. t WR specifies the last burst WRITE cycle until the PRECHARGE command can be issued to the same bank. 

3. The BC4 setting is activated by $\mathsf { M R } 0 [ 1 : 0 ] = 0 1$ and $\mathsf { A } 1 2 = 0$ during the WRITE command at T0. 

4. DI $n =$ data-in for column n. 

5. BC4 (OTF), WL = 5, ${ \mathsf { R L } } = 5$ . 

# DQ Input Timing

Figure 86 (page 174) shows the strobe-to-clock timing during a WRITE burst. DQS, DQS# must transition within $0 . 2 5 ^ { \mathrm { t } } \mathrm { C K }$ of the clock transitions, as limited by t DQSS. All data and data mask setup and hold timings are measured relative to the DQS, DQS# crossing, not the clock crossing. 

The WRITE preamble and postamble are also shown in Figure 86 (page 174). One clock prior to data input to the DRAM, DQS must be HIGH and DQS# must be LOW. Then for a half clock, DQS is driven LOW (DQS# is driven HIGH) during the WRITE preamble, t WPRE. Likewise, DQS must be kept LOW by the controller after the last data is written to the DRAM during the WRITE postamble, t WPST. 

Data setup and hold times are also shown in Figure 86 (page 174). All setup and hold times are measured from the crossing points of DQS and DQS#. These setup and hold values pertain to data input and data mask input. 

Additionally, the half period of the data input strobe is specified by t DQSH and t DQSL. 


Figure 96: Data Input Timing


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/1a48ba440c7d0d3ff6421533d444c19527275c6138e4fbd408dfbb77fd4c7bbc.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/df54a1503708a9cff141bc30f0b0af4170091096dc118ed0fa0470aa1cd68617.jpg)


Transitioning Data 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/2457e1f0099523310494e346f026eb5358a9e4fe85139ad30912ffc9bece93b6.jpg)


Don’t Care 

# PRECHARGE Operation

Input A10 determines whether one bank or all banks are to be precharged and, in the case where only one bank is to be precharged, inputs BA[2:0] select the bank. 

When all banks are to be precharged, inputs BA[2:0] are treated as “Don’t Care.” After a bank is precharged, it is in the idle state and must be activated prior to any READ or WRITE commands being issued. 

# SELF REFRESH Operation

The SELF REFRESH operation is initiated like a REFRESH command except CKE is LOW. The DLL is automatically disabled upon entering SELF REFRESH and is automatically enabled and reset upon exiting SELF REFRESH. 

All power supply inputs (including VREFCA and VREFDQ) must be maintained at valid levels upon entry/exit and during self refresh mode operation. VREFDQ may float or not drive $\mathrm { V _ { D D Q } } / 2$ while in self refresh mode under certain conditions: 

• $\mathrm { V _ { S S } { < V _ { R E F D Q } < V _ { D D } } }$ is maintained. 

• VREFDQ is valid and stable prior to CKE going back HIGH. 

• The first WRITE operation may not occur earlier than 512 clocks after V REFDQ is valid. 

• All other self refresh mode exit timing requirements are met. 

The DRAM must be idle with all banks in the precharge state (t RP is satisfied and no bursts are in progress) before a self refresh entry command can be issued. ODT must also be turned off before self refresh entry by registering the ODT ball LOW prior to the self refresh entry command (see On-Die Termination (ODT) ( for timing requirements). If $\mathrm { R _ { T T , n o m } }$ and RTT(WR) are disabled in the mode registers, ODT can be a “Don’t Care.” After the self refresh entry command is registered, CKE must be held LOW to keep the DRAM in self refresh mode. 

After the DRAM has entered self refresh mode, all external control signals, except CKE and RESET#, are “Don’t Care.” The DRAM initiates a minimum of one REFRESH command internally within the t CKE period when it enters self refresh mode. 

The requirements for entering and exiting self refresh mode depend on the state of the clock during self refresh mode. First and foremost, the clock must be stable (meeting t CK specifications) when self refresh mode is entered. If the clock remains stable and the frequency is not altered while in self refresh mode, then the DRAM is allowed to exit self refresh mode after t CKESR is satisfied (CKE is allowed to transition HIGH t CKESR later than when CKE was registered LOW). Since the clock remains stable in self refresh mode (no frequency change), t CKSRE and t CKSRX are not required. However, if the clock is altered during self refresh mode (if it is turned-off or its frequency changes), then t CKSRE and t CKSRX must be satisfied. When entering self refresh mode, t CKSRE must be satisfied prior to altering the clock's frequency. Prior to exiting self refresh mode, t CKSRX must be satisfied prior to registering CKE HIGH. 

When CKE is HIGH during self refresh exit, NOP or DES must be issued for t XS time. t XS is required for the completion of any internal refresh already in progress and must be satisfied before a valid command not requiring a locked DLL can be issued to the device. t XS is also the earliest time self refresh re-entry may occur. Before a command requiring a locked DLL can be applied, a ZQCL command must be issued, t ZQOPER timing must be met, and t XSDLL must be satisfied. ODT must be off during t XSDLL. 


Figure 97: Self Refresh Entry/Exit Timing


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/7938ffb7e97a472157154ca3425f52c72f908aa5b30fb31d46e8a506192ea5e5.jpg)


Notes: 1. The clock must be valid and stable, meeting $\mathsf { t } _ { \mathsf { C K } }$ specifications at least t CKSRE after entering self refresh mode, and at least $^ { \mathrm { t } } { \mathsf { C K S R X } }$ prior to exiting self refresh mode, if the clock is stopped or altered between states Ta0 and Tb0. If the clock remains valid and unchanged from entry and during self refresh mode, then t CKSRE and t CKSRX do not apply; however, $^ { \mathrm { t } } C K E S R$ must be satisfied prior to exiting at SRX. 

2. ODT must be disabled and $\mathsf { R } _ { \mathsf { T T } }$ off prior to entering self refresh at state T1. If both $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ and RTT(WR) are disabled in the mode registers, ODT can be a “Don’t Care.” 

3. Self refresh entry (SRE) is synchronous via a REFRESH command with CKE LOW. 

4. A NOP or DES command is required at T2 after the SRE command is issued prior to the inputs becoming “Don’t Care.” 

5. NOP or DES commands are required prior to exiting self refresh mode until state Te0. 

6. t XS is required before any commands not requiring a locked DLL. 

7. t XSDLL is required before any commands requiring a locked DLL. 

8. The device must be in the all banks idle state prior to entering self refresh mode. For example, all banks must be precharged, t RP must be met, and no data bursts can be in progress. 

9. Self refresh exit is asynchronous; however, $^ \mathrm { t x }$ and t XSDLL timings start at the first rising clock edge where CKE HIGH satisfies t ISXR at Tc1. t CKSRX timing is also measured so that t ISXR is satisfied at Tc1. 

# Extended Temperature Usage

Micron’s DDR3 SDRAM support the optional extended case temperature $( \mathrm { T _ { C } } )$ range of $0 ^ { \circ } \mathrm { C }$ to $9 5 ^ { \circ } \mathrm { C }$ . Thus, the SRT and ASR options must be used at a minimum. 

The extended temperature range DRAM must be refreshed externally at 2x (double refresh) anytime the case temperature is above $8 5 ^ { \circ } \mathrm { C }$ (and does not exceed $9 5 \mathrm { ^ \circ C }$ ). The external refresh requirement is accomplished by reducing the refresh period from 64ms to 32ms. However, self refresh mode requires either ASR or SRT to support the extended temperature. Thus, either ASR or SRT must be enabled when $\mathrm { T _ { C } }$ is above $8 5 ^ { \circ } \mathrm { C }$ or self refresh cannot be used until $\mathrm { T _ { C } }$ is at or below $8 5 ^ { \circ } \mathrm { C }$ Table 79 summarizes the two extended temperature options and Table 80 summarizes how the two extended temperature options relate to one another. 


Table 79: Self Refresh Temperature and Auto Self Refresh Description


<table><tr><td>Field</td><td>MR2 Bits</td><td>Description</td></tr><tr><td colspan="3">Self Refresh Temperature (SRT)</td></tr><tr><td>SRT</td><td>7</td><td>If ASR is disabled (MR2[6] = 0), SRT must be programmed to indicate TOPER during self refresh:*MR2[7] = 0: Normal operating temperature range (0°C to 85°C)*MR2[7] = 1: Extended operating temperature range (0°C to 95°C)If ASR is enabled (MR2[7] = 1), SRT must be set to 0, even if the extended temperature range is supported*MR2[7] = 0: SRT is disabled</td></tr><tr><td colspan="3">Auto Self Refresh (ASR)</td></tr><tr><td>ASR</td><td>6</td><td>When ASR is enabled, the DRAM automatically provides SELF REFRESH power management functions, (refresh rate for all supported operating temperature values)* MR2[6] = 1: ASR is enabled (M7 must = 0)When ASR is not enabled, the SRT bit must be programmed to indicate TOPER during SELF REFRESH operation* MR2[6] = 0: ASR is disabled; must use manual self refresh temperature (SRT)</td></tr></table>


Table 80: Self Refresh Mode Summary


<table><tr><td>MR2[6] (ASR)</td><td>MR2[7] (SRT)</td><td>SELF REFRESH Operation</td><td>Permitted Operating Temperature Range for Self Refresh Mode</td></tr><tr><td>0</td><td>0</td><td>Self refresh mode is supported in the normal temperature range</td><td>Normal (0°C to 85°C)</td></tr><tr><td>0</td><td>1</td><td>Self refresh mode is supported in normal and extended temper- ature ranges; When SRT is enabled, it increases self refresh power consumption</td><td>Normal and extended (0°C to 95°C)</td></tr><tr><td>1</td><td>0</td><td>Self refresh mode is supported in normal and extended temper- ature ranges; Self refresh power consumption may be tempera- ture-dependent</td><td>Normal and extended (0°C to 95°C)</td></tr><tr><td>1</td><td>1</td><td>Illegal</td><td></td></tr></table>

# Power-Down Mode

Power-down is synchronously entered when CKE is registered LOW coincident with a NOP or DES command. CKE is not allowed to go LOW while an MRS, MPR, ZQCAL, READ, or WRITE operation is in progress. CKE is allowed to go LOW while any of the other legal operations (such as ROW ACTIVATION, PRECHARGE, auto precharge, or RE-FRESH) are in progress. However, the power-down IDD specifications are not applicable until such operations have completed. Depending on the previous DRAM state and the command issued prior to CKE going LOW, certain timing constraints must be satisfied (as noted in Table 81). Timing diagrams detailing the different power-down mode entry and exits are shown in Figure 98 (page 187) through Figure 107 (page 191). 


Table 81: Command to Power-Down Entry Parameters


<table><tr><td>DRAM Status</td><td>Last Command Prior to CKE LOW1</td><td>Parameter (Min)</td><td>Parameter Value</td><td>Figure</td></tr><tr><td>Idle or active</td><td>ACTIVATE</td><td>tACTPDEN</td><td>1tCK</td><td>Figure 105 (page 190)</td></tr><tr><td>Idle or active</td><td>PRECHARGE</td><td>tPRPDEN</td><td>1tCK</td><td>Figure 106 (page 191)</td></tr><tr><td>Active</td><td>READ or READAP</td><td>tRDPDEN</td><td>RL + 4tCK + 1tCK</td><td>Figure 101 (page 188)</td></tr><tr><td>Active</td><td>WRITE: BL8OTF, BL8MRS, BC4OTF</td><td rowspan="2">tWRPDEN</td><td>WL + 4tCK + tWR/tCK</td><td>Figure 102 (page 189)</td></tr><tr><td>Active</td><td>WRITE: BC4MRS</td><td>WL + 2tCK + tWR/tCK</td><td>Figure 102 (page 189)</td></tr><tr><td>Active</td><td>WRITEAP: BL8OTF, BL8MRS, BC4OTF</td><td rowspan="2">tWRAPDEN</td><td>WL + 4tCK + WR + 1tCK</td><td>Figure 103 (page 189)</td></tr><tr><td>Active</td><td>WRITEAP: BC4MRS</td><td>WL + 2tCK + WR + 1tCK</td><td>Figure 103 (page 189)</td></tr><tr><td>Idle</td><td>REFRESH</td><td>tREFPDEN</td><td>1tCK</td><td>Figure 104 (page 190)</td></tr><tr><td>Power-down</td><td>REFRESH</td><td>tXPDLL</td><td>Greater of 10tCK or 24ns</td><td>Figure 108 (page 192)</td></tr><tr><td>Idle</td><td>MODE REGISTER SET</td><td>tMRSPDEN</td><td>tMOD</td><td>Figure 107 (page 191)</td></tr></table>


Note: 1. If slow-exit mode precharge power-down is enabled and entered, ODT becomes asynchronous t ANPD prior to CKE going LOW and remains asynchronous until t ANPD $^ +$ t XPDLL after CKE goes HIGH. 


Entering power-down disables the input and output buffers, excluding CK, CK#, ODT, CKE, and RESET#. NOP or DES commands are required until t CPDED has been satisfied, at which time all specified input/output buffers are disabled. The DLL should be in a locked state when power-down is entered for the fastest power-down exit timing. If the DLL is not locked during power-down entry, the DLL must be reset after exiting power-down mode for proper READ operation as well as synchronous ODT operation. 

During power-down entry, if any bank remains open after all in-progress commands are complete, the DRAM will be in active power-down mode. If all banks are closed after all in-progress commands are complete, the DRAM will be in precharge power-down mode. Precharge power-down mode must be programmed to exit with either a slow exit mode or a fast exit mode. When entering precharge power-down mode, the DLL is turned off in slow exit mode or kept on in fast exit mode. 

The DLL also remains on when entering active power-down. ODT has special timing constraints when slow exit mode precharge power-down is enabled and entered. Refer to Asynchronous ODT Mode (page 208) for detailed ODT usage requirements in slow 

exit mode precharge power-down. A summary of the two power-down modes is listed in Table 82 (page 186). 

While in either power-down state, CKE is held LOW, RESET# is held HIGH, and a stable clock signal must be maintained. ODT must be in a valid state but all other input signals are “Don’t Care.” If RESET# goes LOW during power-down, the DRAM will switch out of power-down mode and go into the reset state. After CKE is registered LOW, CKE must remain LOW until t PD (MIN) has been satisfied. The maximum time allowed for powerdown duration is t PD (MAX) $( 9 \times { } ^ { \mathrm { t } } \mathrm { R E F I } )$ . 

The power-down states are synchronously exited when CKE is registered HIGH (with a required NOP or DES command). CKE must be maintained HIGH until t CKE has been satisfied. A valid, executable command may be applied after power-down exit latency, t XP, and t XPDLL have been satisfied. A summary of the power-down modes is listed below. 

For specific CKE-intensive operations, such as repeating a power-down-exit-to-refreshto-power-down-entry sequence, the number of clock cycles between power-down exit and power-down entry may not be sufficient to keep the DLL properly updated. In addition to meeting t PD when the REFRESH command is used between power-down exit and power-down entry, two other conditions must be met. First, t XP must be satisfied before issuing the REFRESH command. Second, t XPDLL must be satisfied before the next power-down may be entered. An example is shown in Figure 108 (page 192). 


Table 82: Power-Down Modes


<table><tr><td>DRAM State</td><td>MR0[12]</td><td>DLL State</td><td>Power-Down Exit</td><td>Relevant Parameters</td></tr><tr><td>Active (any bank open)</td><td>&quot;Don&#x27;t Care&quot;</td><td>On</td><td>Fast</td><td>\( ^{\dagger}\mathrm{{XP}} \) to any other valid command</td></tr><tr><td rowspan="2">Precharged(all banks precharged)</td><td>1</td><td>On</td><td>Fast</td><td>\( ^{\dagger}\mathrm{{XP}} \) to any other valid command</td></tr><tr><td>0</td><td>Off</td><td>Slow</td><td>\( ^{\dagger}\mathrm{{XPDLL}} \) to commands that require the DLL to be locked (READ, RDAP, or ODT on);\( ^{\dagger}\mathrm{{XP}} \) to any other valid command</td></tr></table>


Figure 98: Active Power-Down Entry and Exit


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/193eff8ce3bbefbf7721e619874f1509d8d9e117fd26f410a848c0a80ae90e49.jpg)



Figure 99: Precharge Power-Down (Fast-Exit Mode) Entry and Exit


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/a6ee2e9baee1e42b26842597a9d2d25059ad4cb5a3a2996d314ba91f3fe24c42.jpg)



Figure 100: Precharge Power-Down (Slow-Exit Mode) Entry and Exit


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/48bdcdcba7eb03cfd0f99f1187442d7c166552eb99ca97c7e188bedfeda594f9.jpg)



Notes: 1. Any valid command not requiring a locked DLL.



2. Any valid command requiring a locked DLL.



Figure 101: Power-Down Entry After READ or READ with Auto Precharge (RDAP)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/6351d6a954a47ec739b3f9b9771b92ff798f3289b873791d4a3d76257a1a0bbf.jpg)



Figure 102: Power-Down Entry After WRITE


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/abc8fbd11f40fc79c205a6dcccc21f65d83b2df313d0848c25b50d99edc78cf3.jpg)



Note: 1. CKE can go LOW 2t CK earlier if BC4MRS.



Figure 103: Power-Down Entry After WRITE with Auto Precharge (WRAP)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/36105d8095d83888b55fac90ed897ee0382354d1d696c041ed060417b2866a10.jpg)


Notes: 1. t WR is programmed through MR0[11:9] and represents t WRmin (ns)/t CK rounded up to the next integer $^ \mathrm { t } \mathsf { C K }$ . 

2. CKE can go LOW 2t CK earlier if BC4MRS. 


Figure 104: REFRESH to Power-Down Entry


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/b4102b1c4fc2f7eed0c4ca48ac89a10116dd8f49ad7c041aaa485df81b38aa32.jpg)



Note: 1. After CKE goes HIGH during t RFC, CKE must remain HIGH until t RFC is satisfied.



Figure 105: ACTIVATE to Power-Down Entry


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/7ca400c6b40b200de14101649b547be3a8ee57430a53bd34ebdaff75056df22e.jpg)



Figure 106: PRECHARGE to Power-Down Entry


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/d979c569419585bb74558eb462baacaed1b5821ecebeddf546235d1b82894804.jpg)



Figure 107: MRS Command to Power-Down Entry


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/a75da704b775718cb4fd63aa473bfc7e44cbcade0abd5a8a4e808568db3f5b8a.jpg)



Figure 108: Power-Down Exit to Refresh to Power-Down Entry


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/eb01fe29-e8bd-4a35-9778-6ff6d8c7f7dd/ab68a8291a32d3ecc9913da69c685467c42d272a7e12c714f441151213cd68a2.jpg)



Notes: 1. t XP must be satisfied before issuing the command.



2. t XPDLL must be satisfied (referenced to the registration of power-down exit) before the next power-down can be entered.


# RESET Operation

The RESET signal (RESET#) is an asynchronous reset signal that triggers any time it drops LOW, and there are no restrictions about when it can go LOW. After RESET# goes LOW, it must remain LOW for 100ns. During this time, the outputs are disabled, ODT $\mathrm { ( R _ { T T } ) }$ turns off (High-Z), and the DRAM resets itself. CKE should be driven LOW prior to RESET# being driven HIGH. After RESET# goes HIGH, the DRAM must be re-initialized as though a normal power-up was executed. All counters, except refresh counters, on the DRAM are reset, and data stored in the DRAM is assumed unknown after RESET# has gone LOW. 


Figure 109: RESET Sequence


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/927c16e5e4d311986d3665d1b809eae6d6c2f8b0c5227daa15921f858acea26d.jpg)



Note: 1. The minimum time required is the longer of 10ns or 5 clocks.


# On-Die Termination (ODT)

On-die termination (ODT) is a feature that enables the DRAM to enable/disable and turn on/off termination resistance for each DQ, DQS, DQS#, and DM for the x4 and x8 configurations (and TDQS, TDQS# for the x8 configuration, when enabled). ODT is applied to each DQ, UDQS, UDQS#, LDQS, LDQS#, UDM, and LDM signal for the x16 configuration. 

ODT is designed to improve signal integrity of the memory channel by enabling the DRAM controller to independently turn on/off the DRAM’s internal termination resistance for any grouping of DRAM devices. ODT is not supported during DLL disable mode (simple functional representation shown below). The switch is enabled by the internal ODT control logic, which uses the external ODT ball and other control information. 


Figure 110: On-Die Termination


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/e29c34cc80791e9a38f046f244b53fc1644182f6a9321ef2b6f0eb50987ec303.jpg)


# Functional Representation of ODT

The value of $\mathrm { R } _ { \mathrm { T T } }$ (ODT termination resistance value) is determined by the settings of several mode register bits (see Table 88 (page 199)). The ODT ball is ignored while in self refresh mode (must be turned off prior to self refresh entry) or if mode registers MR1 and MR2 are programmed to disable ODT. ODT is comprised of nominal ODT and dynamic ODT modes and either of these can function in synchronous or asynchronous mode (when the DLL is off during precharge power-down or when the DLL is synchronizing). Nominal ODT is the base termination and is used in any allowable ODT state. Dynamic ODT is applied only during writes and provides OTF switching from no $\mathrm { R } _ { \mathrm { T T } }$ or $\mathrm { R _ { T T , n o m } }$ to $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ . 

The actual effective termination, RTT(EFF), may be different from $\mathrm { R } _ { \mathrm { T T } }$ targeted due to nonlinearity of the termination. For $\mathrm { R } _ { \mathrm { T T ( E F F ) } }$ values and calculations, see Table 33 (page 59). 

# Nominal ODT

ODT (NOM) is the base termination resistance for each applicable ball; it is enabled or disabled via MR1[9, 6, 2] (see Mode Register 1 (MR1) Definition), and it is turned on or off via the ODT ball. 


Table 83: Truth Table – ODT (Nominal)



Note 1 applies to the entire table


<table><tr><td>MR1[9, 6, 2]</td><td>ODT Pin</td><td>DRAM Termination State</td><td>DRAM State</td><td>Notes</td></tr><tr><td>000</td><td>0</td><td>RTT,nom disabled, ODT off</td><td>Any valid</td><td>2</td></tr><tr><td>000</td><td>1</td><td>RTT,nom disabled, ODT on</td><td>Any valid except self refresh, read</td><td>3</td></tr><tr><td>000–101</td><td>0</td><td>RTT,nom enabled, ODT off</td><td>Any valid</td><td>2</td></tr><tr><td>000–101</td><td>1</td><td>RTT,nom enabled, ODT on</td><td>Any valid except self refresh, read</td><td>3</td></tr><tr><td>110 and 111</td><td>X</td><td>RTT,nom reserved, ODT on or off</td><td>Illegal</td><td></td></tr></table>

Notes: 1. Assumes dynamic ODT is disabled (see Dynamic ODT (page 197) when enabled). 

2. ODT is enabled and active during most writes for proper termination, but it is not illegal for it to be off during writes. 

3. ODT must be disabled during reads. The $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ value is restricted during writes. Dynamic ODT is applicable if enabled. 

Nominal ODT resistance $\mathrm { R _ { T T , n o m } }$ is defined by MR1[9, 6, 2], as shown in Mode Register 1 (MR1) Definition. The $\mathrm { R } _ { \mathrm { T T , n o m } }$ termination value applies to the output pins previously mentioned. DDR3 SDRAM supports multiple $\mathrm { R _ { T T , n o m } }$ values based on $\mathrm { R Z Q } / n$ where $n$ can be 2, 4, 6, 8, or 12 and RZQ is 240Ω. $\mathrm { R _ { T T , n o m } }$ termination is allowed any time after the DRAM is initialized, calibrated, and not performing read access, or when it is not in self refresh mode. 

Write accesses use $\mathrm { R _ { T T , n o m } }$ if dynamic ODT $( \mathrm { R } _ { \mathrm { T T ( W R ) } } )$ is disabled. If $\mathrm { R _ { T T , n o m } }$ is used during writes, only RZQ/2, RZQ/4, and RZQ/6 are allowed (see Table 87 (page 198)). ODT timings are summarized in Table 84 (page 196), as well as listed in the Electrical Characteristics and AC Operating Conditions table. 

Examples of nominal ODT timing are shown in conjunction with the synchronous mode of operation in Synchronous ODT Mode (page 203). 


Table 84: ODT Parameters


<table><tr><td>Symbol</td><td>Description</td><td>Begins at</td><td>Defined to</td><td>Definition for All DDR3L Speed Bins</td><td>Unit</td></tr><tr><td>ODTLon</td><td>ODT synchronous turn-on delay</td><td>ODT registered HIGH</td><td>RTT(ON) ±tAON</td><td>CWL + AL - 2</td><td>tCK</td></tr><tr><td>ODTLoff</td><td>ODT synchronous turn-off delay</td><td>ODT registered HIGH</td><td>RTT(OFF) ±tAOF</td><td>CWL + AL - 2</td><td>tCK</td></tr><tr><td>tAONPD</td><td>ODT asynchronous turn-on delay</td><td>ODT registered HIGH</td><td>RTT(ON)</td><td>2-8.5</td><td>ns</td></tr><tr><td>tAOFPD</td><td>ODT asynchronous turn-off delay</td><td>ODT registered HIGH</td><td>RTT(OFF)</td><td>2-8.5</td><td>ns</td></tr><tr><td>ODTH4</td><td>ODT minimum HIGH time after ODT assertion or write (BC4)</td><td>ODT registered HIGH or write registration with ODT HIGH</td><td>ODT registered LOW</td><td>4tCK</td><td>tCK</td></tr><tr><td>ODTH8</td><td>ODT minimum HIGH time after write (BL8)</td><td>Write registration with ODT HIGH</td><td>ODT registered LOW</td><td>6tCK</td><td>tCK</td></tr><tr><td>tAON</td><td>ODT turn-on relative to ODTLon completion</td><td>Completion of ODTLon</td><td>RTT(ON)</td><td>See Electrical Characteristics and AC Operating Conditions table</td><td>ps</td></tr><tr><td>tAOF</td><td>ODT turn-off relative to ODTOff completion</td><td>Completion of ODTOff</td><td>RTT(OFF)</td><td>0.5tCK ± 0.2tCK</td><td>tCK</td></tr></table>

# Dynamic ODT

In certain application cases, and to further enhance signal integrity on the data bus, it is desirable that the termination strength of the DDR3 SDRAM can be changed without issuing an MRS command, essentially changing the ODT termination on the fly. With dynamic ODT $\mathrm { R } _ { \mathrm { T T ( W R ) } } )$ enabled, the DRAM switches from nominal ODT $\mathrm { R } _ { \mathrm { T T , n o m } } )$ to dynamic ODT ${ \mathrm { R } } _ { { \mathrm { T T } } ( { \mathrm { W R } } ) } )$ when beginning a WRITE burst and subsequently switches back to nominal ODT $\operatorname { R } _ { \mathrm { T T , n o m } } )$ at the completion of the WRITE burst. This requirement is supported by the dynamic ODT feature, as described below. 

# Dynamic ODT Special Use Case

When DDR3 devices are architect as a single rank memory array, dynamic ODT offers a special use case: the ODT ball can be wired high (via a current limiting resistor preferred) by having $\mathrm { R _ { T T , n o m } }$ disabled via MR1 and RTT(WR) enabled via MR2. This will allow the ODT signal not to have to be routed yet the DRAM can provide ODT coverage during write accesses. 

When enabling this special use case, some standard ODT spec conditions may be violated: ODT is sometimes suppose to be held low. Such ODT spec violation (ODT not LOW) is allowed under this special use case. Most notably, if Write Leveling is used, this would appear to be a problem since $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ can not be used (should be disabled) and $\mathrm { R } _ { \mathrm { T T ( N O M ) } }$ should be used. For Write leveling during this special use case, with the DLL locked, then $\mathrm { R } _ { \mathrm { T T ( N O M ) } }$ maybe enabled when entering Write Leveling mode and disabled when exiting Write Leveling mode. More so, $\mathrm { R } _ { \mathrm { T T ( N O M ) } }$ must be enabled when enabling Write Leveling, via same MR1 load, and disabled when disabling Write Leveling, via same MR1 load if $\mathrm { R } _ { \mathrm { T T ( N O M ) } }$ is to be used. 

ODT will turn-on within a delay of ODTLon $+ \mathrm { ^ { t } A O N + ^ { t } M O D + 1 C K }$ (enabling via MR1) or turn-off within a delay of ODTLoff $+ ^ { \mathrm { t } } \mathrm { A O F } + ^ { \mathrm { t } } \mathrm { M O D } + 1 \mathrm { C K }$ . As seen in the table below, between the Load Mode of MR1 and the previously specified delay, the value of ODT is uncertain. this means the DQ ODT termination could turn-on and then turn-off again during the period of stated uncertainty. 


Table 85: Write Leveling with Dynamic ODT Special Case


<table><tr><td>Begin RTT,nom Uncertainty</td><td>End RTT,nom Uncertainty</td><td>I/Os</td><td>RTT,nom Final State</td></tr><tr><td>MR1 load mode command:</td><td rowspan="2">ODTLon + tAON + tMOD + 1CK</td><td>DQS, DQS#</td><td>Drive RTT,nom value</td></tr><tr><td>Enable Write Leveling and RTT(NOM)</td><td>DQs</td><td>No RTT,nom</td></tr><tr><td>MR1 load mode command:</td><td rowspan="2">ODTLoff + tAOFF + tMOD + 1CK</td><td>DQS, DQS#</td><td>No RTT,nom</td></tr><tr><td>Disable Write Leveling and RTT(NOM)</td><td>DQs</td><td>No RTT,nom</td></tr></table>

# Functional Description

The dynamic ODT mode is enabled if either MR2[9] or MR2[10] is set to 1. Dynamic ODT is not supported during DLL disable mode so $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ must be disabled. The dynamic ODT function is described below: 

• Two $\mathrm { R } _ { \mathrm { T T } }$ values are available— $\mathbf { \cdot R _ { \mathrm { T T , n o m } } }$ and RTT(WR). 

– The value for $\mathrm { R _ { T T , n o m } }$ is preselected via MR1[9, 6, 2]. 

– The value for $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ is preselected via MR2[10, 9]. 

• During DRAM operation without READ or WRITE commands, the termination is controlled. 

– Nominal termination strength $\mathrm { R _ { T T , n o m } }$ is used. 

– Termination on/off timing is controlled via the ODT ball and latencies ODTLon and ODTLoff. 

• When a WRITE command (WR, WRAP, WRS4, WRS8, WRAPS4, WRAPS8) is registered, and if dynamic ODT is enabled, the ODT termination is controlled. 

– A latency of ODTLcnw after the WRITE command: termination strength RTT,nom switches to RTT(WR) 

– A latency of ODTLcwn8 (for BL8, fixed or OTF) or ODTLcwn4 (for BC4, fixed or OTF) after the WRITE command: termination strength RTT(WR) switches back to $\mathrm { R _ { T T , n o m } }$ . 

– On/off termination timing is controlled via the ODT ball and determined by ODT-Lon, ODTLoff, ODTH4, and ODTH8. 

– During the t ADC transition window, the value of $\mathrm { R } _ { \mathrm { T T } }$ is undefined. 

ODT is constrained during writes and when dynamic ODT is enabled (see the table below, Dynamic ODT Specific Parameters). ODT timings listed in the ODT Parameters table in On-Die Termination (ODT) also apply to dynamic ODT mode. 


Table 86: Dynamic ODT Specific Parameters


<table><tr><td>Symbol</td><td>Description</td><td>Begins at</td><td>Defined to</td><td>Definition for All DDR3L Speed Bins</td><td>Unit</td></tr><tr><td>ODTLcnw</td><td>Change from RTT,nom to RTT(WR)</td><td>Write registration</td><td>RTT switched from RTT,nom to RTT(WR)</td><td>WL - 2</td><td>tCK</td></tr><tr><td>ODTLcwn4</td><td>Change from RTT(WR) to RTT,nom (BC4)</td><td>Write registration</td><td>RTT switched from RTT(WR) to RTT,nom</td><td>4tCK + ODTL off</td><td>tCK</td></tr><tr><td>ODTLcwn8</td><td>Change from RTT(WR) to RTT,nom (BL8)</td><td>Write registration</td><td>RTT switched from RTT(WR) to RTT,nom</td><td>6tCK + ODTL off</td><td>tCK</td></tr><tr><td>tADC</td><td>RTT change skew</td><td>ODTLcnw completed</td><td>RTT transition complete</td><td>0.5tCK ± 0.2tCK</td><td>tCK</td></tr></table>


Table 87: Mode Registers for $\scriptstyle \mathbf { R _ { T I , n o m } }$


<table><tr><td colspan="3">MR1 (RTT,nom)</td><td rowspan="2">RTT,nom (RZQ)</td><td rowspan="2">RTT,nom (Ohm)</td><td rowspan="2">RTT,nom Mode Restriction</td></tr><tr><td>M9</td><td>M6</td><td>M2</td></tr><tr><td>0</td><td>0</td><td>0</td><td>Off</td><td>Off</td><td>n/a</td></tr><tr><td>0</td><td>0</td><td>1</td><td>RZQ/4</td><td>60</td><td rowspan="3">Self refresh</td></tr><tr><td>0</td><td>1</td><td>0</td><td>RZQ/2</td><td>120</td></tr><tr><td>0</td><td>1</td><td>1</td><td>RZQ/6</td><td>40</td></tr><tr><td>1</td><td>0</td><td>0</td><td>RZQ/12</td><td>20</td><td rowspan="2">Self refresh, write</td></tr><tr><td>1</td><td>0</td><td>1</td><td>RZQ/8</td><td>30</td></tr><tr><td>1</td><td>1</td><td>0</td><td>Reserved</td><td>Reserved</td><td>n/a</td></tr><tr><td>1</td><td>1</td><td>1</td><td>Reserved</td><td>Reserved</td><td>n/a</td></tr></table>


Note: 1. ${ \mathsf { R Z Q } } = 2 4 0 { \Omega }$ . If $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ is used during WRITEs, only RZQ/2, RZQ/4, RZQ/6 are allowed. 



Table 88: Mode Registers for RTT(WR)


<table><tr><td colspan="2">MR2 (RTT(WR))</td><td rowspan="2">RTT(WR) (RZQ)</td><td rowspan="2">RTT(WR) (Ohm)</td></tr><tr><td>M10</td><td>M9</td></tr><tr><td>0</td><td>0</td><td colspan="2">Dynamic ODT off: WRITE does not affect RTT,nom</td></tr><tr><td>0</td><td>1</td><td>RZQ/4</td><td>60</td></tr><tr><td>1</td><td>0</td><td>RZQ/2</td><td>120</td></tr><tr><td>1</td><td>1</td><td>Reserved</td><td>Reserved</td></tr></table>


Table 89: Timing Diagrams for Dynamic ODT


<table><tr><td>Figure and Page</td><td>Title</td></tr><tr><td>Figure 111 (page 200)</td><td>Dynamic ODT: ODT Asserted Before and After the WRITE, BC4</td></tr><tr><td>Figure 112 (page 200)</td><td>Dynamic ODT: Without WRITE Command</td></tr><tr><td>Figure 113 (page 201)</td><td>Dynamic ODT: ODT Pin Asserted Together with WRITE Command for 6 Clock Cycles, BL8</td></tr><tr><td>Figure 114 (page 202)</td><td>Dynamic ODT: ODT Pin Asserted with WRITE Command for 6 Clock Cycles, BC4</td></tr><tr><td>Figure 115 (page 202)</td><td>Dynamic ODT: ODT Pin Asserted with WRITE Command for 4 Clock Cycles, BC4</td></tr></table>


Figure 1 1 1 : Dynam ic ODT: ODT Asserted Before and After the WRITE, BC4


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/419d8c6270382f9d3920a6a259f342e17463b6618589bf9466d6d6aa3b98f00b.jpg)


N otes : 1 . Vi a M RS o r OT F. ${ \mathsf { A L } } = 0$ , ${ \mathsf { C W L } } = 5$ . $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ a n d RTT(WR) a re e n a b l ed . 

2 . O DT H 4 a p p l i es to f i rst re g i ste r i n g O DT H I G H a n d t h e n to t h e re g i st rat i o n of t h e WR I T E co m m a n d . I n t h i s exa m p l e, O DT H 4 i s sat i sf i ed i f O DT g oes LOW at T8 (fo u r c l oc ks a fte r t h e WR I T E co m m a n d) . 


Figure 1 1 2 : Dynam ic ODT: Without WRITE Command


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/cbcd5343f97aec320469644b066f8fd161ee820e53c90ecc02d102259db985ef.jpg)


N otes : 1 . ${ \mathsf { A L } } = 0$ , CW L = 5 . $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ i s e n a b l ed a n d $\mathsf { R } _ { \mathsf { T } \mathsf { I } ( \mathsf { W } \mathsf { R } ) }$ i s e i t h e r e n a b l e d o r d i sa b l e d . 

2 . O DT H 4 i s d ef i n ed fro m O DT reg i ste red H I G H to O DT reg i ste red LOW; i n t h i s exa m p l e, O DT H 4 i s sat i sf i ed . O DT reg - i ste re d LOW a t T 5 i s a l so l e g a l . 


Figure 1 1 3: Dynam ic ODT: ODT Pi n Asserted Together with WRITE Command for 6 Clock Cycles, BL8


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/fd2fd97a8957dd474937beb5ecac01b9be84cde238b1d6efa1e7e18c51d3b98d.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/ce54be0be7242c112f8212266eaf8d591cb67072135a270cbe1e92edf46c0302.jpg)


Tra n s it i o n i n g 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/8d090fd6836e8bb04b80704beff8f94d9a7a7a91870d996faa56f0fb70d0c9db.jpg)


Do n ’t Ca re 

N otes : 1 . Vi a M RS o r OT F; ${ \sf A L } = 0$ , CW L = 5 . I f $\mathsf { R } _ { \mathsf { T } , \mathsf { n o m } }$ ca n be e it h e r e n a b l ed o r d i sa b l ed, O DT ca n be H I G H . RTT(WR) i s e n a b l ed . 

2 . I n th i s exa m p l e, O DTH 8 $= 6$ i s sa t i sf i e d exa ct l y. 


Figure 114: Dynamic ODT: ODT Pin Asserted with WRITE Command for 6 Clock Cycles, BC4


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/3fe86567d75ac424b5a87c24491bcd866bdb03ab316d3932d8453fcaf815e452.jpg)



Notes: 1. Via MRS or OTF. ${ \mathsf { A L } } = 0$ , CWL = 5. $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ and $\mathsf { R } _ { \mathsf { T } \mathsf { I } ( \mathsf { W } \mathsf { R } ) }$ are enabled.



2. ODTH4 is defined from ODT registered HIGH to ODT registered LOW, so in this example, ODTH4 is satisfied. ODT registered LOW at T5 is also legal.



Figure 115: Dynamic ODT: ODT Pin Asserted with WRITE Command for 4 Clock Cycles, BC4


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/374e18f393d34c8eec6adfc07f3b52c79c1042746a094c62562e31b794083096.jpg)



Notes: 1. Via MRS or OTF. ${ \mathsf { A L } } = 0$ , CWL = 5. $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ can be either enabled or disabled. If disabled, ODT can remain HIGH. $\mathsf { R } _ { \mathsf { T T } ( \mathsf { W R } ) }$ is enabled.



2. In this example ODTH4 $= 4$ is satisfied exactly.


# Synchronous ODT Mode

Synchronous ODT mode is selected whenever the DLL is turned on and locked and when either $\mathrm { R _ { T T , n o m } }$ or $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ is enabled. Based on the power-down definition, these modes are: 

• Any bank active with CKE HIGH 

• Refresh mode with CKE HIGH 

• Idle mode with CKE HIGH 

• Active power-down mode (regardless of MR0[12]) 

• Precharge power-down mode if DLL is enabled by MR0[12] during precharge powerdown 

# ODT Latency and Posted ODT

In synchronous ODT mode, $\mathrm { R } _ { \mathrm { T T } }$ turns on ODTLon clock cycles after ODT is sampled HIGH by a rising clock edge and turns off ODTLoff clock cycles after ODT is registered LOW by a rising clock edge. The actual on/off times varies by t AON and t AOF around each clock edge (see Table 90 (page 204)). The ODT latency is tied to the WRITE latency (WL) by ODTLon = WL - 2 and ODTLoff $= \mathrm { W L } - 2$ . 

Since write latency is made up of CAS WRITE latency (CWL) and additive latency (AL), the AL programmed into the mode register (MR1[4, 3]) also applies to the ODT signal. The device’s internal ODT signal is delayed a number of clock cycles defined by the AL relative to the external ODT signal. Thus, ODTLon $= { \mathrm { C W L } } + \mathrm { A L } - 2$ $=$ and ODTLoff $= { \mathrm { C W L } } +$ AL - 2. 

# Timing Parameters

Synchronous ODT mode uses the following timing parameters: ODTLon, ODTLoff, ODTH4, ODTH8, t AON, and t AOF. The minimum $\mathrm { R } _ { \mathrm { T T } }$ turn-on time (t AON [MIN]) is the point at which the device leaves High-Z and ODT resistance begins to turn on. Maximum $\mathrm { R } _ { \mathrm { T T } }$ turn-on time (t AON [MAX]) is the point at which ODT resistance is fully on. Both are measured relative to ODTLon. The minimum $\mathrm { R } _ { \mathrm { T T } }$ turn-off time (t AOF [MIN]) is the point at which the device starts to turn off ODT resistance. The maximum $\mathrm { R } _ { \mathrm { T T } }$ turn off time (t AOF [MAX]) is the point at which ODT has reached High-Z. Both are measured from ODTLoff. 

When ODT is asserted, it must remain HIGH until ODTH4 is satisfied. If a WRITE command is registered by the DRAM with ODT HIGH, then ODT must remain HIGH until ODTH4 (BC4) or ODTH8 (BL8) after the WRITE command (see Figure 117 (page 205)). ODTH4 and ODTH8 are measured from ODT registered HIGH to ODT registered LOW or from the registration of a WRITE command until ODT is registered LOW. 


Table 90: Synchronous ODT Parameters


<table><tr><td>Symbol</td><td>Description</td><td>Begins at</td><td>Defined to</td><td>Definition for All DDR3L Speed Bins</td><td>Unit</td></tr><tr><td>ODTLon</td><td>ODT synchronous turn-on delay</td><td>ODT registered HIGH</td><td>RTT(ON) ±tAON</td><td>CWL + AL - 2</td><td>tCK</td></tr><tr><td>ODTLoff</td><td>ODT synchronous turn-off delay</td><td>ODT registered HIGH</td><td>RTT(OFF) ±tAOF</td><td>CWL + AL - 2</td><td>tCK</td></tr><tr><td>ODTH4</td><td>ODT minimum HIGH time after ODT assertion or WRITE (BC4)</td><td>ODT registered HIGH or write registration with ODT HIGH</td><td>ODT registered LOW</td><td>4tCK</td><td>tCK</td></tr><tr><td>ODTH8</td><td>ODT minimum HIGH time after WRITE (BL8)</td><td>Write registration with ODT HIGH</td><td>ODT registered LOW</td><td>6tCK</td><td>tCK</td></tr><tr><td>tAON</td><td>ODT turn-on relative to ODTLon completion</td><td>Completion of ODTLon</td><td>RTT(ON)</td><td>See Electrical Characteristics and AC Operating Conditions table</td><td>ps</td></tr><tr><td>tAOF</td><td>ODT turn-off relative to ODTOff completion</td><td>Completion of ODTOff</td><td>RTT(OFF)</td><td>0.5tCK ± 0.2tCK</td><td>tCK</td></tr></table>


Figure 1 1 6: Synchronous ODT


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/f8102f23819a97975e5408ceb31279563482ec8540b0f11d2df4502b06f7617d.jpg)



N ote : 1 . A L = 3; CWL $= 5$ ; O DTLo n $= \mathsf { W L } = 6 . 0$ ; O DT Loff $=$ W L - 2 = 6 . $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ i s e n a b l e d .



Figure 1 1 7 : Synchronous ODT (BC4)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/ba40362e14e6b03f2a0dac7fc135d779d6adb26a8fc698c92aac84668a8198a7.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/fa7a73f758b9d3f700fac780d768977a47d104aea2feb1d212f8b8d48576abfe.jpg)


Tra n s it i o n i n g 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/1d0439a9e5f12e765ce95ed15f30f69780568fe577d00540a25cdcacdec35517.jpg)


Do n ’t Ca re 

N otes : 1 . W L $= 7$ . $\mathsf { R } _ { \mathsf { T T } , \mathsf { n o m } }$ i s e n a b l e d . RTT(WR) i s d i sa b l e d . 

2 . O DT m u st b e h e l d H I G H fo r at l e a st O DT H 4 a fte r a sse rt i o n (T 1 ) . 

3 . O DT m u st be ke pt H I G H O DTH 4 (B C4) o r O DTH 8 (B L8) afte r th e WR ITE co m m a n d (T7) . 

4 . O DT H i s m e a s u re d f ro m O DT f i rst re g i ste re d H I G H to O DT f i rst re g i ste re d LOW o r f ro m t h e re g i st rat i o n of t h e WR ITE co m m a n d with O DT H I G H to O DT reg i ste red LOW. 

5 . Alt h o u g h O DT H 4 i s sat i sfi ed fro m O DT reg i ste red H I G H at T6, O DT m u st n ot g o LOW befo re T 1 1 a s O DT H 4 m u st a l so b e sat i sf i e d f ro m t h e re g i st rat i o n of t h e WR I T E co m m a n d at T7 . 

# ODT Off During READs

Because the device cannot terminate and drive at the same time, $\mathrm { R } _ { \mathrm { T T } }$ must be disabled at least one-half clock cycle before the READ preamble by driving the ODT ball LOW (if either $\mathrm { R _ { T T , n o m } }$ or $\mathrm { R } _ { \mathrm { T T ( W R ) } }$ is enabled). $\mathrm { R } _ { \mathrm { T T } }$ may not be enabled until the end of the postamble, as shown in the following example. 

Note: ODT may be disabled earlier and enabled later than shown in Figure 118 (page 207). 


Figure 1 1 8: ODT Duri ng READs


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/5b51015e5d1d479437f3c963513944f381356329ff192a9c16c32cc69e301c8a.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/0c89c66138c11b2a551c5b8d3571183797a718276b3243bed67896933182f64c.jpg)


Tra n s it i o n i n g 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/b73375ae77b6d55c66ae153d3e6d2ba6c7064b68702d57792ea790d8ca64ce56.jpg)


D o n ’t Ca re 


N ote : 1 . O DT m u st be d i sa b l ed exte rn a l ly d u ri n g R EADs by d rivi n g O DT LOW. Fo r exa m p l e, ${ \mathsf { C L } } = 6 ;$ ${ \mathsf { A L } } = { \mathsf { C L } } - 1 = 5 ;$ ${ \sf R L } = { \sf A L }$ $+ \mathsf { C L } = 1 1$ ; CWL $= 5$ ; O DTLo n $= C W L + A L - 2 = 8 ;$ $=$ O DTLoff $= C W L + A L - 2 = 8$ $=$ . $\mathsf { R } _ { \mathsf { T } , \mathsf { n o m } }$ i s e n a b l ed . $\mathsf { R } _ { \mathsf { T } \mathsf { I } ( \mathsf { W } \mathsf { R } ) }$ i s a “ D o n ’t Ca re . ”


# Asynchronous ODT Mode

Asynchronous ODT mode is available when the DRAM runs in DLL on mode and when either $\mathrm { R _ { T T , n o m } }$ or RTT(WR) is enabled; however, the DLL is temporarily turned off in precharged power-down standby (via MR0[12]). Additionally, ODT operates asynchronously when the DLL is synchronizing after being reset. See Power-Down Mode (page 185) for definition and guidance over power-down details. 

In asynchronous ODT timing mode, the internal ODT command is not delayed by AL relative to the external ODT command. In asynchronous ODT mode, ODT controls $\mathrm { R } _ { \mathrm { T T } }$ by analog time. The timing parameters t AONPD and t AOFPD replace ODTLon/t AON and ODTLoff/t AOF, respectively, when ODT operates asynchronously. 

The minimum $\mathrm { R } _ { \mathrm { T T } }$ turn-on time (t AONPD [MIN]) is the point at which the device termination circuit leaves High-Z and ODT resistance begins to turn on. Maximum $\mathrm { R } _ { \mathrm { T T } }$ turnon time (t AONPD [MAX]) is the point at which ODT resistance is fully on. t AONPD (MIN) and t AONPD (MAX) are measured from ODT being sampled HIGH. 

The minimum $\mathrm { R } _ { \mathrm { T T } }$ turn-off time (t AOFPD [MIN]) is the point at which the device termination circuit starts to turn off ODT resistance. Maximum $\mathrm { R } _ { \mathrm { T T } }$ turn-off time (t AOFPD [MAX]) is the point at which ODT has reached High-Z. t AOFPD (MIN) and t AOFPD (MAX) are measured from ODT being sampled LOW. 


Figure 1 1 9: Asynchronous ODT Ti m i ng with Fast ODT Transition


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/81fe88b4cb0c48adaf0d3d091c40a88aa4c83688720191761fbc3a8cc0c366a0.jpg)



N ot e : 1 . A L i s i g n o re d .



Table 91 : Asynchronous ODT Ti m i ng Parameters for Al l Speed Bi ns


<table><tr><td>Symbol</td><td>Description</td><td>Min</td><td>Max</td><td>Unit</td></tr><tr><td>tAONPD</td><td>Asynchronous RT turn-on delay (power-down with DLL off)</td><td>2</td><td>8.5</td><td>ns</td></tr><tr><td>tAOFPD</td><td>Asynchronous RT turn-off delay (power-down with DLL off)</td><td>2</td><td>8.5</td><td>ns</td></tr></table>

# Synchronous to Asynchronous ODT Mode Transition (Power-Down Entry)

There is a transition period around power-down entry (PDE) where the DRAM’s ODT may exhibit either synchronous or asynchronous behavior. This transition period occurs if the DLL is selected to be off when in precharge power-down mode by the setting $\mathrm { M R } 0 [ 1 2 ] = 0$ . Power-down entry begins t ANPD prior to CKE first being registered LOW, and ends when CKE is first registered LOW. t ANPD is equal to the greater of ODTLoff $^ +$ $1 ^ { \mathrm { t C K } }$ or ODTLon $+ 1 ^ { \mathrm { t } } \mathrm { C K }$ If a REFRESH command has been issued, and it is in progress when CKE goes LOW, power-down entry ends t RFC after the REFRESH command, rather than when CKE is first registered LOW. Power-down entry then becomes the greater of t ANPD and t RFC - REFRESH command to CKE registered LOW. 

ODT assertion during power-down entry results in an $\mathrm { R } _ { \mathrm { T T } }$ change as early as the lesser of t AONPD (MIN) and ODTLon $\times { } ^ { \mathrm { t } } \mathrm { C K } + { } ^ { \mathrm { t } } \mathrm { A O N }$ (MIN), or as late as the greater of t AONPD (MAX) and ODTLon $\times { } ^ { \mathrm { t C K } } + { } ^ { \mathrm { t } } \mathrm { A O N }$ (MAX). ODT de-assertion during power-down entry can result in an $\mathrm { R } _ { \mathrm { T T } }$ change as early as the lesser of t AOFPD (MIN) and ODTLoff $\times \operatorname { \mathrm { ~ } t C K + }$ t AOF (MIN), or as late as the greater of t AOFPD (MAX) and ODTLoff $\mathrm { \Omega \times { ^ { t } C K } + { ^ { t } A O F } }$ (MAX). Table 92 (page 211) summarizes these parameters. 

If AL has a large value, the uncertainty of the state of $\mathrm { R } _ { \mathrm { T T } }$ becomes quite large. This is because ODTLon and ODTLoff are derived from the WL; and WL is equal to $\mathrm { C W L + A L }$ . Figure 120 (page 211) shows three different cases: 

• ODT_A: Synchronous behavior before t ANPD. 

• ODT_B: ODT state changes during the transition period with t AONPD (MIN) < ODTLon $\times { } ^ { \mathrm { t C K } } + { } ^ { \mathrm { t } } \mathrm { A O N }$ (MIN) and t AONPD $\mathrm { ( M A X ) > O D T L o n \times ^ { t } C K + ^ { t } A O N }$ (MAX). 

• ODT_C: ODT state changes after the transition period with asynchronous behavior. 


Table 92 : ODT Parameters for Power-Down (DLL Off) Entry and Exit Transition Period


<table><tr><td>Description</td><td>Min</td><td>Max</td></tr><tr><td>Power-down entry transition period (power-down entry)</td><td colspan="2">Greater of: tANPD or tRFC - refresh to CKE LOW</td></tr><tr><td>Power-down exit transition period (power-down exit)</td><td colspan="2">tANPD + tXPDLL</td></tr><tr><td>ODT to RT turn-on delay (ODTLon = WL - 2)</td><td>Lesser of: tAONPD (MIN) (2ns) or ODTLon × tCK + tAON (MIN)</td><td>Greater of: tAONPD (MAX) (8.5ns) or ODTLon × tCK + tAON (MAX)</td></tr><tr><td>ODT to RT turn-off delay (ODTLoff = WL - 2)</td><td>Lesser of: tAOFPD (MIN) (2ns) or ODTOff × tCK + tAOF (MIN)</td><td>Greater of: tAOFPD (MAX) (8.5ns) or ODTOff × tCK + tAOF (MAX)</td></tr><tr><td>tANPD</td><td colspan="2">WL - 1 (greater of ODTOff + 1 or ODTLon + 1)</td></tr></table>


Figure 1 20: Synchronous to Asynchronous Transition Duri ng Precharge Power-Down (DLL Off) Entry


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/d1dc0db84db28da8f6b35a1fdb5ae8ef128b387f5e44e372ba3e464a7631e3b9.jpg)



N ote : 1 . A L = 0; CWL $= 5$ ; O DT L(off) $=$ W L - 2 = 3 .


# Asynchronous to Synchronous ODT Mode Transition (Power-Down Exit)

The DRAM’s ODT can exhibit either asynchronous or synchronous behavior during power-down exit (PDX). This transition period occurs if the DLL is selected to be off when in precharge power-down mode by setting MR0[12] to 0. Power-down exit begins t ANPD prior to CKE first being registered HIGH, and ends t XPDLL after CKE is first registered HIGH. t ANPD is equal to the greater of ODTLoff $+ 1 ^ { \mathrm { t } } \mathrm { C K }$ or ODTLon $+ 1 ^ { \mathrm { t } } \mathrm { C K } .$ . The transition period is t ANPD $^ +$ t XPDLL. 

ODT assertion during power-down exit results in an $\mathrm { R } _ { \mathrm { T T } }$ change as early as the lesser of t AONPD (MIN) and $\mathrm { O D T L o n } \times \mathrm { ^ t C K } + \mathrm { ^ t A O N }$ (MIN), or as late as the greater of t AONPD (MAX) and ODTLon $\times { } ^ { \mathrm { t } } \mathrm { C K } + { } ^ { \mathrm { t } } \mathrm { A O N }$ (MAX). ODT de-assertion during power-down exit may result in an $\mathrm { R } _ { \mathrm { T T } }$ change as early as the lesser of t AOFPD (MIN) and ODTLoff $\times \operatorname { t C K } +$ t AOF (MIN), or as late as the greater of t AOFPD (MAX) and ODTLoff $\times ^ { \mathrm { t } } \mathrm { C K } + ^ { \mathrm { t } } \mathrm { A O F }$ (MAX). Table 92 (page 211) summarizes these parameters. 

If AL has a large value, the uncertainty of the $\mathrm { R } _ { \mathrm { T T } }$ state becomes quite large. This is because ODTLon and ODTLoff are derived from WL, and WL is equal to $\mathrm { C W L + A L }$ . Figure 121 (page 213) shows three different cases: 

• ODT C: Asynchronous behavior before t ANPD. 

• ODT B: ODT state changes during the transition period, with t AOFPD (MIN) $<$ ODTLof $\mathrm { \Phi _ { \times } \ t C K + \mathrm { \Lambda _ { A O F } } }$ (MIN), and ODTLoff × t CK + t AOF (MAX) > t AOFPD (MAX). 

• ODT A: ODT state changes after the transition period with synchronous response. 


Figure 1 2 1 : Asynchronous to Synchronous Transition Duri ng Precharge Power-Down (DLL Off) Exit


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/f8a69dd3288d558f58d540c5c13e0fa6b54347a5748f54d9ce8dd0d48f3c9fe2.jpg)


N ote : 1 . ${ \mathsf { C L } } = 6 ;$ A L = C L - 1 ; CW L $= 5$ ; O DT Loff $= W L - 2 = 8$ $=$ . 

# Asynchronous to Synchronous ODT Mode Transition (Short CKE Pulse)

If the time in the precharge power-down or idle states is very short (short CKE LOW pulse), the power-down entry and power-down exit transition periods overlap. When overlap occurs, the response of the DRAM’s $\mathrm { R } _ { \mathrm { T T } }$ to a change in the ODT state can be synchronous or asynchronous from the start of the power-down entry transition period to the end of the power-down exit transition period, even if the entry period ends later than the exit period. 

If the time in the idle state is very short (short CKE HIGH pulse), the power-down exit and power-down entry transition periods overlap. When this overlap occurs, the response of the DRAM’s $\mathrm { R } _ { \mathrm { T T } }$ to a change in the ODT state may be synchronous or asynchronous from the start of power-down exit transition period to the end of the powerdown entry transition period. 


Figure 1 22 : Transition Period for Short CKE LOW Cycles with Entry and Exit Period Overlappi ng


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/2644b636d848d41d82a5c782d077f48f0a9aa5db665329ffb05a5cf7e3c081b8.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/cbe38a2954f9628e5712b0b8da5a9526b2e05e6e0e5f245d439911abb41a40a5.jpg)


I n d i cates b rea k i n t i m e sca l e 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/91d7f7ffb06e99d23d7b4791e9c339e840b2eb0b19617824ab3669f02bba5e61.jpg)


Tra n s it i o n i n g 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/e6a15cdaabc0b88b579be2d53b0da0cfcee7679373d136087a08e818214116d5.jpg)


D o n ’t Ca re 


N ote : 1 . A L = 0, W L = 5, tA N P D = 4 .



Figure 1 23 : Transition Period for Short CKE H IG H Cycles with Entry and Exit Period Overlappi ng


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/bc867d34d2f2442431740f8fe119c023d31bef8821b5a2f62858b0c60753d96e.jpg)


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/c8aeeb0c27c6ef451af506660b1e94e99821a3f0a3b597904ae6ba703141331e.jpg)


I n d i cates b rea k i n t i m e sca l e 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/6002510a48c5ae848583bcd70dc61fad5ae770f85807826e87285437199b6509.jpg)


Tra n s it i o n i n g 

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-26/c55ad03e-da01-4026-9fb6-ac781800cfe8/8f3f3d9844dfcd750c1064b20d95a1512af1fc8f4fe74e4256cd80ee82a4e77d.jpg)


Do n ’t Ca re 


N ote : 1 . A L = 0, W L $= 5$ , tA N P D = 4 .


8000 S. Federal Way, P.O. Box 6, Boise, ID 83707-0006, Tel: 208-368-4000 

www.micron.com/products/support Sales inquiries: 800-932-4992 

Micron and the Micron logo are trademarks of Micron Technology, Inc. 

All other trademarks are the property of their respective owners. 

This data sheet contains minimum and maximum limits specified over the power supply and temperature range set forth herein. 

Although considered final, these specifications are subject to change, as further product development and data characterization some-

times occur. 