# 第二十三章 DDR3 实验

I.MX6U-ALPHA 开发板上带有一个 256MB/512MB 的 DDR3 内存芯片，一般 Cortex-A 芯片自带的 RAM 很小，比如 I.MX6U 只有 128KB 的 OCRAM。如果要运行 Linux 的话完全不够用的，所以必须要外接一片 RAM 芯片，I.MX6U 支持 LPDDR2、LPDDR3/DDR3，I.MX6U-ALPHA开发板上选择的是DDR3，本章就来学习如何驱动 I.MX6U-ALPHA开发板上的这片DDR3。

# 23.1 DDR3 内存简介

在正式学习 DDR3 内存之前，我们要先了解一下 DDR 内存的发展历史，通过对比 SRAM、SDRAM、DDR、DDDR2和DDR3的区别，有助于我们更加深入的理解什么是 DDR。在看DDR 之前我们先来了解一个概念，那就是什么叫做RAM?

# 23.1.1 何为 RAM 和 ROM?

相信大家在购买手机、电脑等电子设备的时候，通常都会听到 RAM、ROM、硬盘等概念，很多人都是一头雾水的。普通用户区分不清楚 RAM、ROM到可以理解，但是作为一个嵌入式Linux开发者，要是不清楚什么是 RAM、什么是 ROM就绝对不行！RAM和ROM专业的解释如下：

RAM：随机存储器，可以随时进行读写操作，速度很快，掉电以后数据会丢失。比如内存条、SRAM、SDRAM、DDR 等都是 RAM。RAM 一般用来保存程序数据、中间结果，比如我们在程序中定义了一个变量 a，然后对这个a进行读写操作，示例代码如下：

```txt
示例代码23.1.1.1 RAM中的变量  
1 int a;  
2 a = 10;
```

a是一个变量，我们需要很方便的对这个变量进行读写操作，方法就是直接“a”进行读写操作，不需要在乎具体的读写过程。我们可以随意的对 RAM中任何地址的数据进行读写操作，非常方便。

ROM：只读存储器，笔者认为目前“只读存储器”这个定义不准确。比如我们买手机，通常会告诉你这个手机是 $4 { + } 6 4$ 或 $6 { + } 1 2 8$ 配置，说的就是 RAM 为 4GB 或 6GB，ROM 为 64G 或128GB。但是这个ROM 是 Flash，比如EMMC 或 UFS 存储器，因为历史原因，很多人还是将Flash 叫做 ROM。但是 EMMC 和 UFS，甚至是 NAND Flash，这些都是可以进行写操作的！只是写起来比较麻烦，要先进行擦除，然后再发送要写的地址或扇区，最后才是要写入的数据，学习过STM32，使用过WM25QXX系列的SPI Flash 的同学应该深有体会。可以看出，相比于RAM，向 ROM 或者 Flash 写入数据要复杂很多，因此意味着速度就会变慢(相比 RAM)，但是ROM和Flash可以将容量做的很大，而且掉电以后数据不会丢失，适合用来存储资料，比如音乐、图片、视频等信息。

综上所述，RAM 速度快，可以直接和 CPU 进行通信，但是掉电以后数据会丢失，容量不容易做大(和同价格的 Flash 相比)。ROM(目前来说，更适合叫做 Flash)速度虽然慢，但是容量大、适合存储数据。对于正点原子的 I.MX6U-ALPHA 开发板而言，256MB/512MB 的 DDR3 就是 RAM，而 512MB NANF Flash 或 8GB EMMC 就是 ROM。

# 23.1.2 SRAM 简介

为什么要讲 SRAM 呢？因为大多数的朋友最先接触 RAM 芯片都是从 SRAM 开始的，因为大量的STM32 单片机开发板都使用到了 SRAM，比如F103、F407等，基本都会外扩一个 512KB 或 1MB 的 SRAM 的，因为 STM32F103/F407 内部 RAM 比较小，在一些比较耗费内存的应用中会出现内存捉紧的情况，比如emWin做 UI界面。我们简单回顾一下SRAM，如果想要详细的了解SRAM请阅读正点原子 STM32F103 战舰开发板的开发指南。

SRAM 的全称叫做 Static Random-Access Memory，也就是静态随机存储器，这里的“静态”说的就是只要SRAM上电，那么SRAM里面的数据就会一直保存着，直到 SRAM掉电。对于 RAM 而言需要可以随机的读取任意一个地址空间内的数据，因此采用了地址线和数据线

分离的方式，这里就以 STM32F103/F407 开发板常用的 IS62WV51216 这颗 SRAM 芯片为例简单的讲解一下 SRAM，这是一颗 16 位宽(数据位为 16 位)、1MB 大小的 SRAM，芯片框图如图23.1.2.1 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/c6c8026fd9f3d6f7edd097cb757f5225dd08a866e6d530335d7d616db9adf391.jpg)



图 23.1.2.1 IS62WV51216 框图



图 23.1.2.1 主要分为三部分，我们依次来看一下这三部分：


# $\textcircled{1}$ 、地址线

这部分是地址线，一共A0~A18，也就是 19根地址线，因此可访问的地址大小就是 $2 ^ { \sim } 1 9 \mathrm { = }$ $5 2 4 2 8 8 { = } 5 1 2 \mathrm { K B }$ 。不是说 IS62WV51216 是个 1MB 的 SRAM 吗？为什么地址空间只有 512KB？前面我们说了IS62WV51216 是16位宽的，也就是一次访问 2个字节，因此需要对 512KB进行乘 2 处理，得到 $5 1 2 \mathrm { K B } ^ { \ast } 2 { = } 1 \mathrm { M B }$ 。位宽的话一般有 8 位/16 位/32 位，根据实际需求选择即可，一般都是根据处理器的 SRAM控制器位宽来选择SRAM位宽。

# $\textcircled{2}$ 、数据线

这部分是SRAM的数据线，根据SRAM位宽的不同，数据线的数量要不同，8位宽就有8根数据线，16位宽就有 16根数据线，32位宽就有 32根数据线。IS62WV51216是一个16位宽的 SRAM，因此就有 16根数据线，一次访问可以访问16bit的数据，也就是 2个字节。因此就有高字节和低字节数据之分，其中 IO0~IO7 是低字节数据，IO8~IO15 是高字节数据。

# $\textcircled{3}$ 、控制线

SRAM要工作还需要一堆的控制线，CS2和 CS1是片选信号，低电平有效，在一个系统中可能会有多片 SRAM(目的是为了扩展 SRAM 大小或位宽)，这个时候就需要 CS 信号来选择当前使用哪片 SRAM。另外，有的 SRAM 内部其实是由两片 SRAM 拼接起来的，因此就会提供两个片选信号。

OE是输出使能信号，低电平有效，也就是主控从 SRAM读取数据。

WE是写使能信号，低电平有效，也就是主控向 SRAM写数据。

UB 和LB信号，前面我们已经说了，IS62WV51216是个16位宽的SRAM，分为高字节和低字节，那么如何来控制读取高字节数据还是低字节数据呢？这个就是 UB 和 LB 这两个控制线的作用，这两根控制线都是低电平有效。UB为低电平的话表示访问高字节，LB 为低电平的话表示访问低字节。关于 IS62WV51216的简单原理就讲解到这里。

那么 SRAM有什么缺点没有？那必须有的啊，要不然就不可能有本章教程了，SRAM最大

的缺点就是成本高！价格高，大家可以在淘宝上搜索一下 IS62WV51216 这个仅仅只有 1 M B大小的SRAM售价为多少，大概为 5,6块钱。大家再搜索一下32MB 的 SDRAM多钱，以华邦的 W9825G6KH 为例，大概 4,5 块钱，可以看出 SDRAM 比 SRAM 容量大，但是价格更低。SRAM突出的特点就是无需刷新(SDRAM需要刷新，后面会讲解)，读写速度快！所以SRAM通常作为 SOC 的内部 RAM 使用或 Cache 使用，比如 STM32 内存的 RAM 或 I.MX6U 内部的 OCRAM 都是 SRAM。

# 23.1.3 SDRAM 简介

前面给大家简单讲解了 SRAM，可以看出 SRAM最大的缺点就是价格高、容量小！但是应用对于内存的需求越来越高，必须提供大内存解决方案。为此半导体厂商想了很多办法，提出了很多解决方法，最终 SDRAM 应运而生，得到推广。SDRAM 全称是 Synchronous DynamicRandom Access Memory，翻译过来就是同步动态随机存储器，“同步”的意思是 SDRAM工作需要时钟线，“动态”的意思是 SDRAM中的数据需要不断的刷新来保证数据不会丢失，“随机”的意思就是可以读写任意地址的数据。

与 SRAM相比，SDRAM集成度高、功耗低、成本低、适合做大容量存储，但是需要定时刷新来保证数据不会丢失。因此 SDRAM 适合用来做内存条，SRAM 适合做高速缓存或 MCU内部的 RAM。SDRAM 目前已经发展到了第四代，分别为：SDRAM、DDR SDRAM、DDR2SDRAM、DDR3 SDRAM、DDR4 SDRAM。STM32F429/F767/H743 等芯片支持 SDRAM，学过 STM32F429/F767/H743 的朋友应该知道 SDRAM，这里我们就以 STM32 开发板最常用的华邦 W9825G6KH 为例，W9825G6KH 是一款 16 位宽(数据位为 16 位)、32MB 的 SDRAM、速度一般为 133MHz、166MHz 或 200MHz。W9825G6KH 框图如图 23.1.3.1 所示：


原子哥在线教学:www.yuanzige.com



论坛:www.openedv.com


![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/21c4f1f414d6ba305ff3baa6f8182335f083be4c227aac04e03bf4dfda9dc40d.jpg)



图 23.1.3.1 W9825G6KH 框图


# $\textcircled{1}$ 、控制线

SDRAM 也需要很多控制线，我们依次来看一下：

CLK：时钟线，SDRAM是同步动态随机存储器，“同步”的意思就是时钟，因此需要一根额外的时钟线，这是和 SRAM最大的不同，SRAM没有时钟线。

CKE：时钟使能信号线，SRAM没有CKE信号。

CS：片选信号，这个和SRAM一样，都有片选信号。

RAS：行选通信号，低电平有效，SDRAM 和 SRAM 的寻址方式不同，SDRAM 按照行、列来确定某个具体的存储区域。因此就有行地址和列地址之分，行地址和列地址共同复用同一组地址线，要访问某一个地址区域，必须要发送行地址和列地址，指定要访问哪一行？哪一列？RAS 是行选通信号，表示要发送行地址，行地址和列地址访问方式如图 23.1.3.2所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/6e83257880d9d274491b62ea0936febf77a0037e159e3e798462cae4d6ff3f4c.jpg)



图 23.1.3.2 SDRAM 行列寻址方式


CAS：列选通信号，和 RAS 类似，低电平有效，选中以后就可以发送列地址了。

WE：写使能信号，低电平有效。

# $\textcircled{2}$ 、A10 地址线

A10是地址线，那么这里为什么要单独将A10 地址线给提出来呢？因为A10地址线还有另外一个作用，A10还控制着 Auto-precharge，也就是预充电。这里又提到了预充电的概念，SDRAM芯片内部会分为多个BANK，关于BANK我们稍后会讲解。SDRAM在读写完成以后，如果要对同一个 BANK 中的另一行进行寻址操作就必须将原来有效的行关闭，然后发送新的行/列地址，关闭现在工作的行，准备打开新行的操作就叫做预充电。一般SDSRAM都支持自动预充电的功能。

# $\textcircled{3}$ 、地址线

对于W9825G6KH来说一共有A0~A12，共13根地址线，但是我们前面说了 SDRAM寻址是按照行地址和列地址来访问的，因此这A0~A12包含了行地址和列地址。不同的 SDRAM芯片，根据其位宽、容量等的不同，行列地址数是不同的，这个在SDRAM的数据手册里面会也清楚的。比如W9825G6KH的A0~A8是列地址，一共 9位列地址，A0~A12是行地址，一共13 位，因此可寻址范围为： $2 { \cdot } 9 { } ^ { * } 2 { \cdot } 1 3 { = } 4 1 9 4 3 0 4 \mathrm { B } { = } 4 \mathrm { M B }$ ，W9825G6KH 为 16 位宽(2 个字节)，因此还需要对4MB 进行乘 2处理，得到 $4 ^ { * } 2 { = } 8 \mathrm { M B }$ ，但是 W9825G6KH 是一个 32MB 的 SDRAM啊，为什么算出来只有 8MB，仅仅为实际容量的 1/4。不要急，这个就是我们接下来要讲的BANK，8MB 只是一个 BANK 的容量，W9825G6KH 一共有 4 个 BANK。

# $\textcircled{4}$ 、BANK 选择线

BS0 和 BS1 是 BANK 选择信号线，在一片 SDRAM 中因为技术、成本等原因，不可能做一个全容量的 BANK。而且，因为 SDRAM 的工作原理，单一的 BANK 会带来严重的寻址冲突，减低内存访问效率。为此，人们在一片SDRAM 中分割出多块BANK，一般都是2的n次方，比如 2，4，8 等。图 23.1.1.2 中的 $\textcircled{5}$ 就是 W9825G6KH 的 4 个 BANK 示意图，每个 SDRAM数据手册里面都会写清楚自己是几BANK。前面我们已经计算出来了一个BANK的大小为8MB，那么四个BANK 的总容量就是 $8 \mathrm { M B } ^ { * } 4 { = } 3 2 \mathrm { M B }$ 。

既然有4个BANK，那么在访问的时候就需要告诉SDRAM，我们现在需要访问哪个 BANK，BS0和BS1就是为此而生的，4个BANK 刚好2 根线，如果是8个BANK 的话就需要三根线，也就是BS0~BS2。BS0、BS1这两个线也是 SRAM所没有的。

# ⑤、BANK 区域

关于 BANK 的概念前面已经讲过了，这部分就是 W9825G6KH 的 4 个 BANK 区域。这个概念也是SRAM所没有的。

# $\textcircled{6}$ 、数据线

W9825G6KH 是 16 位宽的 SDRAM，因此有 16 根数据线，DQ0~DQ15，不同的位宽其数据线数量不同，这个和 SRAM是一样的。

# $\textcircled{7}$ 、高低字节选择

W9825G6KH是一个 16位的SDRAM，因此就分为低字节数据和高字节数据，LDQM和 UDQM就是低字节和高字节选择信号，这个也和 SRAM一样。

# 23.1.4 DDR 简介

终于到了 DDR 内存了，DDR 内存是 SDRAM 的升级版本，SDRAM 分为 SDR SDRAM、DDR SDRAM、DDR2 SDRAM、DDR3 SDRAM、DDR4 SDRAM。可以看出 DDR 本质上还是 SDRAM，只是随着技术的不断发展，DDR也在不断的更新换代。先来看一下 DDR，也就是DDR1，人们对于速度的追求是永无止境的，当发现 SDRAM 的速度不够快的时候人们就在思考如何提高 SDRAM 的速度，DDR SDRAM 由此诞生。

DDR 全称是 Double Data Rate SDRAM，也就是双倍速率 SDRAM，看名字就知道 DDR的速率(数据传输速率)比 SDRAM 高 1 倍！这 1 倍的速度不是简简单单的将 CLK 提高 1 倍，SDRAM 在一个 CLK 周期传输一次数据，DDR 在一个 CLK 周期传输两次数据，也就是在上升沿和下降沿各传输一次数据，这个概念叫做预取(prefetch)，相当于DDR的预取为2bit，因此DDR 的速度直接加倍！比如 SDRAM 速度一般是 133~200MHz，对应的传输速度就是 133~200MT/s，在描述DDR速度的时候一般都使用 MT/s，也就是每秒多少兆次数据传输。133MT/S就是每秒 133M 次数据传输，MT/s 描述的是单位时间内传输速率。同样 133~200MHz 的频率，DDR 的传输速度就变为了266~400MT/S，所以大家常说的 DDR266、DDR400就是这么来的。

DDR2 在 DDR 基础上进一步增加预取(prefetch)，增加到了 4bit，相当于比 DDR 多读取一倍的数据，因此DDR2的数据传输速率就是533~800MT/s，这个也就是大家常说的 DDR2 533、DDR2 800。当然了，DDR2 还有其他速度，这里只是说最常见的几种。

DDR3 在 DDR2 的基础上将预取(prefetch)提高到 8bit，因此又获得了比 DDR2 高一倍的传输速率，因此在总线时钟同样为 266~400MHz的情况下，DDR3 的传输速率就是 1066~1600MT/S。

I.MX6U 的 MMDC 外设用于连接 DDR，支持 LPDDR2、DDR3、DDR3L，最高支持 16 位数据位宽。总线速度为400MHz(实际是396MHz)，数据传输速率最大为 800MT/S。这里我们讲一下LPDDR3、DDR3 和 DDR3L 的区别，这三个都是 DDR3，但是区别主要在于工作电压，LPDDR3叫做低功耗DDR3，工作电压为1.2V。DDR3 叫做标压DDR3，工作电压为 1.5V，一般台式内存条都是 DDR3。DDR3L 是低压 DDR3，工作电压为 1.35V，一般手机、嵌入式、笔记本等都使用 DDR3L。

正点原子的 I.MX6U-ALPHA 开发板上接了一个 256MB/512MB 的 DDR3L，16 位宽，型号为 NT5CC128M16JR/MT5CC256M16EP，nanya 公司出品的，分为对应 256MB 和 512MB 容量。EMMC 核心板上用的 512MB 容量的 DDR3L，NAND 核心板上用的 256MB 容量的 DDR3L。本讲解我们就以 EMMC 核心板上使用的 NT5CC256M16EP-EK 为例讲解一下 DDR3。可以到 nanya官网去查找一下此型号，信息如图 23.1.4.1所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/1ad77a32889bf00a77df97fda1dcc1301ed74b2182ffc3f249561c27995eb7cb.jpg)



图 23.1.4.1 NT5CC256M16EP-EK 信息


从图 23.1.4.1 可以看出，NT5CC256M16EP-EK 是一款容量为 4Gb，也就是 512MB 大小、16 位宽、1.35V、传输速率为 1866MT/S 的 DDR3L 芯片。NT5CC256M16EP-EK 的数据手册没有在 nanya 官网找到，但是找到了 NT5CC256M16ER-EK 数据手册，在官网上没有看出这两个有什么区别，因此我们就直接用 NT5CC256M16ER-EK 的数据手册。数据手册已经放到了开发板光盘中，路径为：6、硬件资料-》1、芯片资料-》NT5CC256M16EP-EK.pdf。但是数据手册并没有给出 DDR3L 对的结构框图，这里我就直接用镁光 MT41K256M16 数据手册里面的结构框图了，都是一样的，DDR3L 结构框图如图23.1.4.2所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/ba9313facba9130299f941a68ebda1d9ebff8238d08736e26345c87b96ed64f4.jpg)



图 23.1.4.2 DDR3L 结构框图


从图 23.1.4.2可以看出，DDR3L和 SDRAM 对的结构框图很类似，但是还是有点区别。

# $\textcircled{1}$ 、控制线

ODT：片上终端使能，ODT 使能和禁止片内终端电阻。

ZQ：输出驱动校准的外部参考引脚，此引脚应该外接一个 240欧的电阻到VSSQ上，一般就是直接接地了。

RESET：复位引脚，低电平有效。

CKE：时钟使能引脚。

A12：A12 是地址引脚，但是有也有另外一个功能，因此也叫做 BC 引脚，A12 会在 REA

D 和 WRITE 命令期间被采样，以决定 burst chop 是否会被执行。

CK 和 CK#：时钟信号，DDR3 的时钟线是差分时钟线，所有的控制和地址信号都会在 CK 对的上升沿和CK#的下降沿交叉处被采集。

CS#：片选信号，低电平有效。

RAS#、CAS#和 WE#：行选通信号、列选通信号和写使能信号。

# $\textcircled{2}$ 、地址线

A[14:0]为地址线，A0~A14，一共 15 根地址线，根据 NT5CC256M16ER-EK 的数据手册可知，列地址为A0~A9，共10根，行地址为A0~A14，共15根，因此一个 BANK 的大小就是2$\wedge 1 0 ^ { * } 2 ^ { \wedge } 1 5 ^ { * } 2 { = } 3 2 \mathrm { M B } ^ { * } 2 { = } 6 4 \mathrm { M B }$ ，根据图 23.1.4.2 可知一共有 8 个 BANK，因此 DDR3L 的容量就是 $6 4 ^ { * } 8 { = } 5 1 2 \mathrm { M B }$ 。

# $\textcircled{3}$ 、BANK 选择线

一片 DDR3 有 8 个 BANK，因此需要 3 个线才能实现 8 个 BANK 的选择，BA0~BA2 就是用于完成BANK选择的。

# $\textcircled{4}$ 、BANK 区域

DDR3 一般都是 8 个 BANK 区域。

# $\textcircled{5}$ 、数据线

因为是 16 位宽的，因此有 16 根数据线，分别为 DQ0~DQ15。

# $\textcircled{6}$ 、数据选通引脚

DQS 和 DQS#是数据选通引脚，为差分信号，读的时候是输出，写的时候是输入。LDQS(有的叫做 DQSL)和 LDQS#(有的叫做 DQSL#)对应低字节，也就是 DQ0~7，UDQS(有的叫做 DQSU)和 UDQS#(有的叫做 DQSU#)，对应高字节，也就是 DQ8~15。

# $\textcircled{7}$ 、数据输入屏蔽引脚

DM是写数据输入屏蔽引脚。

关于 DDR3L 的框图就讲解到这里，想要详细的了解 DDR3 的组成，请阅读相应对的数据手册。

# 23.2 DDR3 关键时间参数

大家在购买DDR3内存的时候通常会重点观察几个常用的时间参数：

# 1、传输速率

比如 1066MT/S、1600MT/S、1866MT/S 等，这个是首要考虑的，因为这个决定了 DDR3 内存的最高传输速率。

# 2、tRCD 参数

tRCD 全称是RAS-to-CAS Delay，也就是行寻址到列寻址之间的延迟。DDR的寻址流程是先指定BANK 地址，然后再指定行地址，最后指定列地址确定最终要寻址的单元。BANK 地址和行地址是同时发出的，这个命令叫做“行激活”(Row Active)。行激活以后就发送列地址和具体的操作命令(读还是写)，这两个是同时发出的，因此一般也用“读/写命令”表示列寻址。在行有效(行激活)到读写命令发出的这段时间间隔叫做 tRCD，如图23.2.1所示：

原子哥在线教学:www.yuanzige.com

论坛:www.openedv.com

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/a6790a203349b2776ec4289d1726dac21270fe8562f1a81c86f7b9af40df0f22.jpg)


图 23.2.1 tRCD

一般 DDR3 数据手册中都会给出 tRCD 的时间值，比如正点原子所使用的 NT5CC256M16EP-EK 这个 DDR3，tRCD 参数如图 23.2.2 所示：

<table><tr><td>Speed Bins</td><td colspan="2">DDR3(L)-1866 13-13-13</td><td rowspan="2">Unit</td><td rowspan="2">Note</td></tr><tr><td>Parameter</td><td>Min</td><td>Max</td></tr><tr><td>tAA</td><td>13.91</td><td>20.0</td><td>ns</td><td></td></tr><tr><td>tRCD</td><td>13.91</td><td>-</td><td>ns</td><td></td></tr><tr><td>tRP</td><td>13.91</td><td>-</td><td>ns</td><td></td></tr><tr><td>tRAS</td><td>34.0</td><td>9xtREFI</td><td>ns</td><td></td></tr><tr><td>tRC</td><td>47.91</td><td>-</td><td>ns</td><td></td></tr></table>

图 23.2.2 tRCD 时间参数

从图 23.2.2可以看出，tRCD为13.91ns，这个我们在初始化 DDR3的时候需要配置。有时候大家也会看到“13-13-13”之类的参数，这个是用来描述CL-tRCD-TRP的，如图23.2.3所示：

<table><tr><td rowspan="2">Organization</td><td rowspan="2">Part Number</td><td rowspan="2">Package</td><td colspan="3">Speed</td></tr><tr><td>Clock (MHz)</td><td>Data Rate (Mb/s)</td><td>CL-TRCD-TRP</td></tr><tr><td colspan="6">DDR3(L) Commercial Grade</td></tr><tr><td rowspan="6">512M x 8</td><td>NT5CC512M8EQ-DIB</td><td rowspan="6">78-Ball</td><td>800</td><td>DDR3L-16001</td><td>11-11-11</td></tr><tr><td>NT5CC512M8EQ-DI</td><td>800</td><td>DDR3L-16001</td><td>11-11-11</td></tr><tr><td>NT5CB512M8EQ-DI</td><td>800</td><td>DDR3-1600</td><td>11-11-11</td></tr><tr><td>NT5CC512M8EQ-EK</td><td>933</td><td>DDR3L-18661</td><td>13-13-13</td></tr><tr><td>NT5CB512M8EQ-EK</td><td>933</td><td>DDR3-1866</td><td>13-13-13</td></tr><tr><td>NT5CB512M8EQ-FL</td><td>1066</td><td>DDR3-2133</td><td>14-14-14</td></tr><tr><td rowspan="6">256M x 16</td><td>NT5CC256M16ER-DIB</td><td rowspan="4">30-Ball</td><td>800</td><td>DDR3L-16001</td><td>11-11-11</td></tr><tr><td>NT5CC256M16ER-DI</td><td>800</td><td>DDR3L-16001</td><td>11-11-11</td></tr><tr><td>NT5CB256M16ER-DI</td><td>800</td><td>DDR3-1600</td><td>11-11-11</td></tr><tr><td>NT5CC256M16ER-EK</td><td>933</td><td>DDR3L-18661</td><td>13-13-13</td></tr><tr><td>NT5CB256M16ER-EK</td><td rowspan="2"></td><td>933</td><td>DDR3-1866</td><td>13-13-13</td></tr><tr><td>NT5CB256M16ER-FL</td><td>1066</td><td>DDR3-2133</td><td>14-14-14</td></tr></table>


图 23.2.3 CL-TRCD-TRP 时间参数


从图 23.2.3 可以看出，NT5CC256M16ER-EK 这个 DDR3 的 CL-TRCD-TRP 时间参数为“13-13-13”。因此 $\mathrm { t R C D } { = } 1 3$ ，这里的13不是 ns数，而是CLK时间数，表示13个CLK周期。

# 3、CL 参数

当列地址发出以后就会触发数据传输，但是数据从存储单元到内存芯片 IO 接口上还需要一段时间，这段时间就是非常著名的 CL(CAS Latency)，也就是列地址选通潜伏期，如图 23.2.4 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/f5ca320a2494b3c0de89f80e8ed7dfaff079a126a1f1f7d6c4d12bf5a5b27f82.jpg)



图 23.2.4 CL


CL 参数一般在 DDR3 的数据手册中可以找到，比如 NT5CC256M16EP-EK 的 CL 值就是 13个时钟周期，一般 tRCD和CL 大小一样。

# 4、AL 参数

在 DDR 的发展中，提出了一个前置 CAS 的概念，目的是为了解决 DDR 中的指令冲突，它允许CAS信号紧随着RAS发送，相当于将DDR中的CAS 前置了。但是读/写操作并没有因此提前，依旧要保证足够的延迟/潜伏期，为此引入了 AL(Additive Latency)，单位也是时钟周期数。 $\mathrm { { A L + C L } }$ 组成了 RL(Read Latency)，从 DDR2 开始还引入了写潜伏期 WL(Write Latency)，WL表示写命令发出以后到第一笔数据写入的潜伏期。引入AL以后的读时序如图23.2.5所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/0e986d71a7a96be839dc6da3d2b22dbfb9c94c8d1cea9d33efea7dc798575389.jpg)



图 23.2.5 加入 AL 后的读时序图



图 32.2.5就是镁光DDR3L 的读时序图，我们依次来看一下图中这四部分都是什么内容：



$\textcircled{1}$ 、tRCD，前面已经说过了。



$\textcircled{2}$ 、AL。



$\textcircled{3}$ 、CL。



$\textcircled{4}$ 、RL 为读潜伏期， $\scriptstyle \mathrm { R L = A L + C L }$


# 5、tRC 参数

tRC 是两个 ACTIVE 命令，或者 ACTIVE 命令到 REFRESH 命令之间的周期，DDR3L 数据手册会给出这个值，比如 NT5CC256M16EP-EK 的 tRC 值为 47.91ns，参考图 23.2.2。

# 6、tRAS 参数

tRAS 是 ACTIVE 命令到 PRECHARGE 命令之间的最小时间，DDR3L 的数据手册同样也会给出此参数，NT5CC256M16EP-EK 的 tRAS 值为 34ns，参考图 23.2.2。

# 23.3 I.MX6U MMDC 控制器简介

# 23.3.1 MMDC 控制器

学过STM32的同学应该记得，STM32 的FMC或 FSMC 外设用于连接SRAM 或SDRAM，对于I.MX6U来说也有DDR 内存控制器，否则的话它怎么连接 DDR 呢？MMDC 就是I.MX6U的内存控制器，MMDC 是一个多模的 DDR 控制器，可以连接 16 位宽的 DDR3/DDR3L、16 位宽的 LPDDR2，MMDC 是一个可配置、高性能的 DDR 控制器。MMDC 外设包含一个内核(MMDC_CORE)和 PHY(MMDC_PHY)，内核和 PHY 的功能如下：

MMDC 内核：内核负责通过 AXI 接口与系统进行通信、DDR 命令生成、DDR 命令优化、读/写数据路径。

MMDC PHY：PHY 负责时序调整和校准，使用特殊的校准机制以保障数据能够在 400MHz被准确捕获。

MMDC 的主要特性如下：

$\textcircled{1}$ 、支持 DDR3/DDR3Lx16、支持 LPDDR2x16，不支持 LPDDR1MDDR 和 DDR2。

$\textcircled{2}$ 、支持单片 256Mbit~8Gbit 容量的 DDR，列地址范围：8-12 位，行地址范围 11-16bit。2个片选信号。

$\textcircled{3}$ 、对于 DDR3，最大支持 8bit 的突发访问。

$\textcircled{4}$ 、对于LPDDR2 最大支持4bit的突发访问。

$\textcircled{5}$ 、MMDC 最大频率为 $4 0 0 \mathrm { M H z }$ ，因此对应的数据速率为 800MT/S。

$\textcircled{6}$ 、支持各种校准程序，可以自动或手动运行。支持 ZQ校准外部DDR 设备，ZQ校准DDR I/O引脚、校准DDR驱动能力。

# 23.3.2 MMDC 控制器信号引脚

我们在使用STM32 的时候FMC/FSMC的 IO引脚是带有复用功能的，如果不接 SRAM或SDRAM的话 FMC/FSMC是可以用作其他外设 IO的。但是，对于DDR 接口就不一样了，因为DDR对于硬件要求非常严格，因此DDR的引脚都是独立的，一般没有复用功能，只做为DDR引脚使用。I.MX6U 也有专用的DDR引脚，如图 23.3.2.1所示：

<table><tr><td>Signal</td><td>Description</td><td>Pad</td><td>Mode</td><td>Direction</td></tr><tr><td>DRAM_ADDR[15:0]</td><td>Address Bus Signals</td><td>DRAM_A[15:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_CAS</td><td>Column Address Strobe Signal</td><td>DRAM_CAS</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_CS[1:0]</td><td>Chip Selects</td><td>DRAM_CS[1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_DATA[31:0]</td><td>Data Bus Signals</td><td>DRAM_D[31:0]</td><td>No Muxing</td><td>I/O</td></tr><tr><td>DRAM_DQM[1:0]</td><td>Data Mask Signals</td><td>DRAM_DQM[1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_ODT[1:0]</td><td>On-Die Termination Signals</td><td>DRAM_SDODT[1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_RAS</td><td>Row Address Strobe Signal</td><td>DRAM_RAS</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_RESET</td><td>Reset Signal</td><td>DRAM_RESET</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDBA[2:0]</td><td>Bank Select Signals</td><td>DRAM_SDBA[2:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDCKE[1:0]</td><td>Clock Enable Signals</td><td>DRAM_SDCKE[1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDCLK0_N</td><td>Negative Clock Signals</td><td>DRAM_SDCLK_1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDCLK0_P</td><td>Positive Clock Signals</td><td>DRAM_SDCLK_1:0]</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_SDQS[1:0]_N</td><td>Negative DQS Signals</td><td>DRAM_SDQS[1:0]_N</td><td>No Muxing</td><td>I/O</td></tr><tr><td>DRAM_SDQS[1:0]_P</td><td>Positive DQS Signals</td><td>DRAM_SDQS[1:0]_P</td><td>No Muxing</td><td>I/O</td></tr><tr><td>DRAM_SDWE</td><td>WE signal</td><td>DRAM_SDWE</td><td>No Muxing</td><td>O</td></tr><tr><td>DRAM_ZQPAD</td><td>ZQ signal</td><td>DRAM_ZQPAD</td><td>No Muxing</td><td>O</td></tr></table>

图 23.3.2.1 DDR 信号引脚

由于图 23.3.2.1 中的引脚是DDR 专属的，因此就不存在所谓的 DDR 引脚复用配置，只需要设置 DDR 引脚的电气属性即可，注意，DDR 引脚的电气属性寄存器和普通的外设引脚电气属性寄存器不同！

# 23.3.3 MMDC 控制器时钟源

前面说了很多次，I.MX6U 的 DDR 或者 MDDC 的时钟频率为 400MHz，那么这 400MHz时钟源怎么来的呢？这个就要查阅 I.MX6ULL 参考手册的《Chapter 18 Clock Controller Module(CCM)》章节。MMDC 时钟源如图 23.3.3.1 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/1b5f2e0ebce4b210c9713a48210c9a7b6d11be7ad71d2faafa82954e7af1f07c.jpg)



图 23.3.3.1 MMDC 时钟源


图 23.3.3.1就是MMDC的时钟源路径图，主要分为4 部分，我们依次来看一下每部分所组的工作：

$\textcircled{1}$ 、pre_periph2 时钟选择器，也就是 periph2_clkd 的前级选择器，由 CBCMR 寄存器的 PRE_PERIPH2_CLK_SEL 位(bit22:21)来控制，一共有四种可选方案，如表 23.3.3.1 所示：

<table><tr><td>PRE_PERIPH2_CLK_SEL(bit22: 21)</td><td>时钟源</td></tr><tr><td>00</td><td>PLL2</td></tr><tr><td>01</td><td>PLL2_PFD2</td></tr><tr><td>10</td><td>PLL2_PFD0</td></tr><tr><td>11</td><td>PLL4</td></tr></table>


表 23.3.3.1 pre_periph2 时钟源


从表 23.3.3.1 可以看出，当 PRE_PERIPH2_CLK_SEL 为 0x1 的时候选中 PLL2_PFD2 为 pre_periph2时钟源。在前面的《第十六章 主频和时钟配置》中我们已经将 PLL2_PFD2设置为396MHz(约等于 400MHz)，I.MX6U 内部 boot rom 就是设置 PLL2_PFD2 作为 MMDC 的最终时钟源，这就是 I.MX6U 的 DDR 频率为 400MHz 的原因。

$\textcircled{2}$ 、periph2_clk 时钟选择器，由 CBCDR 寄存器的 PERIPH2_CLK_SEL 位(bit26)来控制，当为 0 的时候选择 pll2_main_clk 作为 periph2_clk 的时钟源，当为 1 的时候选择 periph2_clk2_clk 作为 periph2_clk 的时钟源。这里肯定要将 PERIPH2_CLK_SEL 设置为 0，也就是选择 pll2_main_clk 作为 periph2_clk 的时钟源，因此 periph2_clk=PLL2_PFD0=396MHz。

$\textcircled{3}$ 、最后就是分频器，由 CBCDR 寄存器的 FABRIC_MMDC_PODF 位(bit5:3)设置分频值，可设置0~7，分别对应 1~8分频，要配置MMDC的时钟源为396MHz，那么此处就要设置为 1分频，因此 FABRIC_MMDC_PODF ${ \bf \omega } = 0$ 。

以上就是 MMDC 的时钟源设置，I.MX6U 参考手册一直说 DDR 的频率为 $4 0 0 \mathrm { M H z }$ ，但是实际只有 396MHz，就和 NXP 宣传自己的 I.MX6ULL 有 800MHz 一样，实际只有 792MHz。

# 23.4 ALPHA 开发板 DDR3L 原理图

ALPHA 开发板有 EMMC 和 NAND 两种核心板，EMMC 核心板使用的 DDR3L 的型号为NT5CC256M16EP-EK，容量为 512MB。NAND 核心板使用的 DDR3L 型号为 NT5CC128M16J

R-EK，容量为 256MB，这两种型号的DDR3L 封装一摸一样，有人可能就有疑问了，容量不同的话地址线是不同的，比如行地址和列地址线数就不同，没错！但是 DDR3L 厂商为了方便选择将不同容量的 DDR3 封装做成一样，没有用到的地址线 DDR3L 芯片会屏蔽掉。而且，根据规定，所有厂商的DDR芯片IO一摸一样，不管是引脚定义还是引脚间距，但是芯片外形大小可能不同。因此只要做好硬件，可以在不需要修改硬件 PCB 的前提下，随意的更换不同容量、不同品牌的DDR3L 芯片，极大的方便了我们的芯片选型。

正点原子 ALPHA 开发板 EMMC 和 NAND 核心板的 DDR3L 原理图一样，如图 23.4.1 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/7b8ffddcf09443eca24993fdc7bc22ef016bce4790b4d84c2b74c07c8d472e2f.jpg)



图 23.4.1 DDR3L 原理图


图 23.4.1 中左侧是 DDR3L 原理图，可以看出图中 DDR3L 的型号为 MT41K256M16TW，这个是镁光的 512MB DDR3L。但是我们实际使用的 512MB DDR3L 型号为 NT5CC256M16EP-EK，不排除以后可能会更换 DDR3L 型号，更换 DDR3L 芯片是不需要修改 PCB。图 23.4.1中右边的是 I.MX6U 的 MMDC 控制器 IO。

# 23.5 DDR3L 初始化与测试

# 23.5.1 ddr_stress_tester 简介

NXP 提供了一个非常好用的 DDR 初始化工具，叫做 ddr_stress_tester。此工具已经放到了开发板光盘中，路径为：5、开发工具 $\cdot$ 、NXP官方 DDR 初始化与测试工具 $\cdot$ ddr_stress_tester_v2.90_setup.exe.zip，我们简单介绍一下 ddr_stress_tester 工具，此工具特点如下：

$\textcircled{1}$ 、此工具通过 USB OTG 接口与开发板相连接，也就是通过 USB OTG 口进行 DDR 的初始化与测试。

$\textcircled{2}$ 、此工具有一个默认的配置文件，为 excel表，通过此表可以设置板子的DDR 信息，最

后生成一个.inc 结尾的 DDR 初始化脚本文件。这个.inc 文件就包含了 DDR 的初始化信息，一般都是寄存器地址和对应的寄存器值。

$\textcircled{3}$ 、此工具会加载.inc表里面的DDR初始化信息，然后通过 USB OTG 接口向板子下载DDR 相关的测试代码，包括初始化代码。

$\textcircled{4}$ 、对此工具进行简单的设置，即可开始 DDR 测试，一般要先做校准，因为不同的 PCB其结构肯定不同，必须要做一次校准，校准完成以后会得到两个寄存器对应的校准值，我们需要用这个新的校准值来重新初始化DDR。

$\textcircled{5}$ 、此工具可以测试板子的 DDR 超频性能，一般认为 DDR 能够以超过标准工作频率 $1 0 \%$ ${ \sim } 2 0 \%$ 稳定工作的话就认定此硬件 DDR 走线正常。

$\textcircled{6}$ 、此工具也可以对 DDR进行12小时的压力测试。

我们来看一下正点原子开发板光盘里面 5、开发工具 ${ } _ { - > 6 }$ 、NXP官方DDR 初始化与测试工具目录下的文件，如图 23.5.1.1所示：

<table><tr><td>ALIENTEK_256MB.inc</td><td>2019-06-06 20:16</td><td>INC文件</td><td>8 KB</td></tr><tr><td>ALIENTEK_512MB.inc</td><td>2019-06-06 18:06</td><td>INC文件</td><td>8 KB</td></tr><tr><td>ddr_stressTester_v2.90_setup.exe.zip</td><td>2018-07-31 11:47</td><td>360压缩ZIP文件</td><td>2,207 KB</td></tr><tr><td>I.MX6UL_DDR3_Script_Aid_V0.02.xlsx</td><td>2018-07-31 12:08</td><td>Microsoft Excel工...</td><td>84 KB</td></tr><tr><td>MX6X_DDR3_调校_应用手册_V4_20150730...</td><td>2018-08-11 9:38</td><td>Foxit Reader PDF D...</td><td>1,326 KB</td></tr><tr><td>飞思卡尔.i.MX6平台DRAM接口高阶应用指导...</td><td>2018-07-31 11:54</td><td>Foxit Reader PDF D...</td><td>3,164 KB</td></tr></table>

图 23.5.1.1 NXP 官方DDR 初始化与测试工具目录下的文件

我们依次来看一下图 23.5.1.1中的这些文件的作用：

$\textcircled{1}$ 、ALIENTEK_256MB.inc 和 ALIENTEK_512MB.inc，这两个就是通过 excel 表配置生成的，针对正点原子开发板的 DDR 配置脚本文件。

$\textcircled{2}$ 、ddr_stress_tester_v2.90_setup.exe.zip 就是我们要用的 ddr_stress_tester 软件，大家自行安装即可，一定要记得安装路径。

$\textcircled{3}$ 、I.MX6UL_DDR3_Script_Aid_V0.02.xlsx 就是 NXP 编写的针对 I.MX6UL 的 DDR 初始化 execl文件，可以在此文件里面填写 DDR 的相关参数，然后就会生成对应的.inc初始化脚本。

$\textcircled{4}$ 、最后两个PDF 文档就是关于I.MX6 系列的 DDR 调试文档，这两个是NXP 编写的。

# 23.5.2 DDR3L 驱动配置

# 1、安装 ddr_stress_tester

首先要安装 ddr_stress_testr 软件，安装方法很简单，这里就不做详细的讲解了。但是一定要记得安装路径！因为我们要到安装路径里面找到测试软件。比如我安装到了 D:\Program Files (x86)里面，安装完成以后就会在此目录下生成一个名为 ddr_stress_tester_v2.90 的文件夹，此文件夹就是DDR 测试软件，进入到此文件夹中，里面的文件如图 23.5.2.1 所示：

<table><tr><td>bin</td><td>2019-06-06 18:39</td><td>文件夹</td><td></td></tr><tr><td>log</td><td>2019-06-06 18:39</td><td>文件夹</td><td></td></tr><tr><td>script</td><td>2019-06-06 18:39</td><td>文件夹</td><td></td></tr><tr><td>DDRTester.exe</td><td>2017-08-02 10:44</td><td>应用程序</td><td>3,451 KB</td></tr><tr><td>LA_OPT_Base_License.html</td><td>2018-07-06 13:37</td><td>360 se HTML Docu...</td><td>195 KB</td></tr><tr><td>SCR-ddr_stressTester_v2.9.0.txt</td><td>2018-07-06 15:10</td><td>文本文档</td><td>4 KB</td></tr></table>

图 23.5.2.1 ddr_stress_tester 安装文件

图 23.5.2.1 中的 DDR_Tester.exe 就是我们稍后要使用的 DDR 测试软件。

# 2、配置 DDR3L，生成初始化脚本

将开发板光盘中的：5、开发工具 $- > 5$ 、NXP 官方 DDR 初始化与测试工具->I.MX6UL_DDR3_Script_Aid_V0.02.xlsx 文件拷贝到 ddr_stress_testr 软件安装目录中，完成以后如图 23.5.2.2 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/7cfee47695b4bbca509bbc4846a2c2212ea006cac2b92bc5fabcea4eadc12b69.jpg)



图 23.5.2.2 拷贝完成以后的测试软件目录


I.MX6UL_DDR3_Script_Aid_V0.02.xlsx 就是 NXP 为 I.MX6UL 编写的 DDR3 配置 excel 表，虽然看名字是为I.MX6UL编写的，但是I.MX6ULL也是可以使用的。

打开 I.MX6UL_DDR3_Script_Aid_V0.02.xlsx，打开以后如图 23.5.2.3 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/497f8cdc8bc2d866f3d8b6867bbc870e054eb6a19e423e48af879d0010f7cf83.jpg)



图 23.5.2.3 配置 excel 表


图 23.5.2.3中最下方有三个选项卡，这三个选项卡的功能如下：

$\textcircled{1}$ 、Readme 选项卡，此选项卡是帮助信息，告诉用户此文件如何使用。

$\textcircled{2}$ 、Register Configuration选项卡，顾名思义，此选项卡用于完成寄存器配置，也就是配置

DDR3，此选项卡是我们重点要讲解的。

$\textcircled{3}$ 、RealView.inc 选项卡，当我们配置好 Register Configuration 选项卡以后，RealView.inc选项卡里面就保存着寄存器地址和对应的寄存器值。我们需要另外新建一个后缀为.inc 的文件来保存 RealView.inc 中的初始化脚本内容，ddr_stress_testr 软件就是要使用此.inc 结尾的初始化脚本文件来初始化DDR3。

选中“Register Configuration”选项卡，如图 23.5.2.4 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/8f0da0723495c63793c70d35a02e1419ed6858556130ecc50ae14e1eb54d147e.jpg)



图 23.5.2.4 配置界面



图 23.5.2.4就是具体的配置界面，主要分为三部分：


# $\textcircled{1}$ 、Device Information

DDR3 芯片设备信息设置，此部分需要根据所使用的 DDR3 芯片来设置，具体的设置项如下：

Manufacturer：DDR3 芯片厂商，默认为镁光(Micron)，这个没有意义，比如我们用的 nanya的DDR3，但是此配置文件也是可以使用的。

Memory part number：DDR3 芯片型号，可以不用设置，没有实际意义。

Memory type:DDR3 类型，有 DDR3-800、DDR3-1066、DDR3-1333 和 DDR3-1600，在此选项右侧有个下拉箭头，点击下拉箭头即可查看所有的可选选项，如图 23.5.2.5所示：

原子哥在线教学:www.yuanzige.com

论坛:www.openedv.com

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/516040bb59e0281f5da29ba6521dc14ead71d58eefe4ff82b18c17120bd7ed2a.jpg)



图 23.5.2.5 Memory type 可选选项


从图 23.5.2.5 可以看出，最大只能选择 DDR3-1600，没有 DDR3-1866 选项，因此我们就只能选择 DDR3-1600。

DRAM density(Gb)：DDR3 容量，根据实际情况选择，同样右边有个下拉箭头，打开下拉箭头即可看到所有可选的容量，如图23.5.2.6所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/eed6d91b924b8c4900f853c13380a1a56e678760206ca789693575a9079dc763.jpg)



图 23.5.2.6 容量选择


从图 23.5.2.6可以看出，可选的容量为 1、2、4和8Gb，如果使用的 512MB 的DDR3 就应该选择4，如果使用的 256MB的DDR3就应该选择 2。

DRAM Bus width：DDR3 位宽，可选的选项如图 23.5.2.7 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/afffcbadbf8c4fcecae41b72d1aac7898eda6b13bb84b18e7ac6b881f0bdc3d6.jpg)



图 23.5.2.7 DDR3 位宽


正点原子 ALPHA 开发板所有的 DDR3 都是 16 位宽，因此选择 16。

Number of Banks：DDR3 内部 BANK 数量，对于 DDR3 来说内部都是 8 个 BANK，因此固定为8。

Number of ROW Addresses：行地址宽度，可选 11~16 位，这个要具体所使用的 DDR3芯片来定，如果是 EMMC 核心板(DDR3 型号为 NT5CC256M16EP-EK)，那么行地址为 15 位。如果是 NAND 核心板(DDR3 型号为 NT5CC128M16JR-EK)，行地址就为 14 位。

Number COLUMN Addresses：列地址宽度，可选 9~12 位,EMMC 核心板和 NAND 核心板的DDR3 列地址都为10位。

Page Size(K)：DDR3 页大小，可选 1 和 2，NT5CC256M16EP-EK 和 NT5CC128M16JR-EK 的页大小都为2KB，因此选择2。

Self-Refresh Temperature(SRT)：固定为 Extended，不需要修改。

tRCD=tRP=CL(ns)：DDR3 的 tRCD-tRP-CL 时间参数，要查阅所使用的 DDR3 芯片手册，NT5CC256M16EP-EK 和 NT5CC128M16JR-EK 都为 13.91ns，因此在后面填写 13.91。

tRC Min(ns)：DDR3 的 tRC 时间参数，NT5CC256M16EP-EK 和 NT5CC128M16JR-EK 都为 47.91ns，因此在后面填写 47.91。

tRAS Min(ns)：DDR3 的 tRAS 时间参数，NT5CC256M16EP-EK 和 NT5CC128M16JR-EK都为34ns，因此在后面填写 34。

$\textcircled{2}$ 、System Information 

此部分设置I.MX6UL/6ULL 相关属性，具体的设置项如下：

i.Mx Part：固定为 i.MX6UL。

Bus Width：总线宽度，16 位宽。

Density per Chip select(Gb)：每个片选对应的 DDR3 容量，可选 1~16，根据实际所使用的 DDR3芯片来填写，512MB 的话就选择4，256MB 的话就选择2。

Number of Chip Select used：使用几个片选信号？可选择 1 或 2，正点原子所有的核心板都只使用了一个片选信号，因此选择1。

Total DRAM Density(Gb)：整个 DDR3 的容量，单位为 Gb，如果是 512MB 的话就是 4，如果是256MB的话就是2。

DRAM Clock Freq(MHz)：DDR3 工作频率，设置为 $4 0 0 \mathrm { M H z }$ 。

DRAM Clock Cycle Time(ns)：DDR3 工作频率对应的周期，单位为 ns，如果工作在 400MHz，那么周期就是 $2 . 5 \mathrm { n s }$ 。

Address Mirror(for CS1)：地址镜像，仅 CS1 有效，此处选择关闭，也就是“Disable”，此选项我们不需要修改。

# $\textcircled{3}$ 、SI Configuratin

此部分是信号完整性方面的配置，主要是一些信号线的阻抗设置，这个要咨询硬件工程师，这里我们直接使用NXP的默认设置即可。

关于 DDR3 的配置我们就讲解到这里，如果是 EMMC 核心板(DDR3 型号为 NT5CC256M16EP-EK)，那么配置如图 23.5.2.8 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/ff30a98b69b45f0117a1d7167c1655cc56d30b6d5a585df960673e0050ff7f80.jpg)



图 23.5.2.8 EMMC 核心板配置。


NAND 核心板配置(DDR3 型号为 NT5CC128M16JR-EK)配置如图 23.5.2.9 所示：

原子哥在线教学:www.yuanzige.com

论坛:www.openedv.com

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/aa5982ad5ecdf444cdd89d70219cef2f6eb932239e7cd77038a918d507496d4e.jpg)



图 23.5.2.9 NAND 核心板配置


后面我就以 EMMC 核心板为例讲解了，配置完成以后点击 RealView.inc 选项卡，如图 23.

# 5.2.10 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/5973f03791f978b2bfe46ad70fdd8afd8f35ff24d980a968da070b3d8897a1d3.jpg)



图 23.5.2.10 生成的配置脚本。


图 23.5.2.10 中的 RealView.inc 就是生成的配置脚本，全部是“寄存器地址 $: =$ 寄存器值”这

原子哥在线教学:www.yuanzige.com

论坛:www.openedv.com

种形式。RealView.inc 不能直接用，我们需要新建一个以.inc 结尾的文件，名字自定义，比如我名为“ALIENTEK_512MB”的.inc 文件，如图 23.5.2.11 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/7e771add46f42a6d14cfe811a46dca33de6f747c263e81e47eb5ed840b1ce485.jpg)



图 23.5.2.11 新建.inc 文件


用 notepad $^ { + + }$ 打开 ALIENTEK_512MB.inc 文件，然后将图 23.5.2.10 中 RealView.inc 里面的所有内容全部拷贝到 ALIENTEK_512MB.inc 文件中，完成以后如图 23.5.2.12 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/ac26a5aa39f68d727659cc4074a5ae3694c9ddb7c2c9bf2b71b4630d7492c275.jpg)



图 23.5.2.12 完成后的 ALIENTEK_512MB.inc 文件内容


至此，DDR3 配置就全部完成，DDR3 的配置文件 ALIENTEK_512MB.inc 已经得到了，接下来就是使用此配置文件对正点原子ALPHA开发板的DDR3 进行校准并进行超频测试。

# 23.5.3 DDR3L 校准

首先要用 DDR_Tester.exe 软件对正点原子 ALPAH 开发板的 DDR3L 进行校准，因为不同的 PCB其走线不同，必须要进行校准，经过校准一会 DDR3L 就会工作到最佳状态。

# 1、将开发板通过 USB OTG线连接到电脑上

DDR_Tester软件通过 USB OTG 线将测试程序下载到开发板中，因此首先需要使用 USBOTG 线将开发板和电脑连接起来，对于 V2.4 版本以前的底板，使用 Mini USB 线连接到电脑

上，如图 23.5.3.1 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/2cfe54fe7a50bf12b5d8e984d7ba54f3bafea4a6b3582291696c030529c21e8d.jpg)



图 23.5.3.1 V2.4 版本以前底板 USB OTG 连接示意图


V2.4 及以后版本的底板，使用 Type-C 线连接到电脑上，如图 23.5.3.2 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/6bb7c27bb8013c2b597e4c351a840dbb324ab7c94a83b0675818258bde8b3bdd.jpg)



图 23.5.3.2 V2.4 及以后版本底板 USB OTG 连接示意图


USB OTG线连接成功以后还需要如下两步：

$\textcircled{1}$ 、弹出TF卡，如果插入了 TF 卡，那么一定要弹出来！！

$\textcircled{2}$ 、设置拨码开关从 USB启动，如图23.5.3.3所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/fbe713cfb8a10f6cdbbda6cd9d59e7dc3257b35e76f7cb512c5172ca8afe19d9.jpg)



图 23.5.3.3 USB 启动


# 2、DDR_Tester 软件

双击“DDR_Tester.exe”，打开测试软件，如图 23.5.3.4 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/0998534504bcec621ba23e2c632fbf29590d0247e426a3193927b81b26a97af1.jpg)



图 23.5.3.4 NXP DDR Test Tool


点击图 23.5.3.4 中的“Load init Script”加载前面已经生成的初始化脚本文件 ALIENTEK_512MB.inc，注意，不能有中文路径，否则加载可能会失败！完成以后如图 23.5.3.5所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/8ddfc5bb4fdeb5e08d82d38cea39e9383ba5f642d11010444c0a71b5897f0c93.jpg)



图 23.5.3.5 .inc 文件加载成功后的界面


ALIENTEK_512MB.inc 文件加载成功以后还不能直接用，还需要对 DDR Test Tool 软件进行设置，设置完成以后如图 23.5.3.6所示：

原子哥在线教学:www.yuanzige.com

论坛:www.openedv.com

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/7a1101a79a10f051464d7039db537c11850f931a625ec2a26b67b8723e3b009d.jpg)



图 23.5.3.6 DDR Test Tool 配置


一切设置好以后点击图 23.5.3.6 中右上方大大的“Download”按钮，将测试代码下载到开发板中(具体下载到哪里笔者也不清楚，估计是 I.MX6ULL 内部的 OCRAM)，下载完成以后 DDR Test Tool下方的信息窗口就会输出一些内容，如图 23.5.3.7所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/9030b48b9f5cbcf1132e14bab98f5659b5f8738234a7ec5911c9efab89173a4e.jpg)



图 23.5.3.7 信息输出


图 23.5.3.7输出了一些关于板子的信息，比如 SOC型号、工作频率、DDR 配置信息等等。DDR Test Tool 工具有三个测试项：DDR Calibration、DDR Stess Test 和 32bit Memory Read/Write，我们首先要做校准测试，因为不同的PCB、不同的DDR3L 芯片对信号的影响不同，必须要进行校准，然后用新的校准值重新初始化 DDR。点击“Calibraton”按钮，如图 23.5.3.8 所示：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/c9a9360a7a83bfa5bfca16ac276962eca0c4489a79c1384880452bad3a14b8a4.jpg)



图 23.5.3.8 开始校准


点击图 23.5.3.8 中的“Calibration”按钮以后就会自动开始校准，最终会得到 Write leveling calibtarion、Read DQS Gating Calibration、Read calibration 和 Write calibration，一共四种校准结果，校准结果如下：

```txt
示例代码23.5.3.1 DDR3L校准结果  
1 Write leveling calibration  
2 MMDC_MPWLDECTRL0 ch0 (0x021b080c) = 0x00000000  
3 MMDC_MPWLDECTRL1 ch0 (0x021b0810) = 0x000B000B  
4  
5 Read DQS Gating calibration  
6 MPDGCTRL0 PHY0 (0x021b083c) = 0x0138013C  
7 MPDGCTRL1 PHY0 (0x021b0840) = 0x00000000  
8  
9 Read calibration  
10 MPRDDLCTL PHY0 (0x021b0848) = 0x40402E34  
11  
12 Write calibration  
13 MPWRDLCTL PHY0 (0x021b0850) = 0x40403A34
```

所谓的校准结果其实就是得到了一些寄存器对应的值，比如 MMDC_MPWLDECTRL0 寄存器地址为0X021B080C，此寄存器是PHY写平衡延时寄存器 0，经过校准以后此寄存器的值应该为 0X00000000，以此类推。我们需要修改 ALIENTEK_512MB.inc 文件，找到 MMDC_MPWLDECTRL0、MMDC_MPWLDECTRL1、MPDGCTRL0 PHY0、MPDGCTRL1 PHY0、MPRDDLCTL PHY0 和 MPWRDLCTL PHY0 这 6 个寄存器，然后将其值改为示例代码 23.5.3.1中的校准后的值。注意，在 ALIENTEK_512MB.inc 中可能找不到 MMDC_MPWLDECTRL1(0x021b0810)和 MPDGCTRL1 PHY0(0x021b0840)这两个寄存器，找不到就不用修改了。

ALIENTEK_512MB.inc 修改完成以后重新加载并下载到开发板中，至此 DDR校准完成，校准的目的就是得到示例代码 23.5.3.1中这6个寄存器的值！

# 23.5.4 DDR3L 超频测试

校准完成以后就可以进行DDR3 超频测试，超频测试的目的就是为了检验DDR3 硬件设计合不合理，一般DDR3能够超频到比标准频率高 $1 0 \% { \sim } 1 5 \%$ 的话就认为硬件没有问题，因此对于正点原子的ALPHA开发板而言，如果DDR3能够超频到 $4 4 0 \mathrm { M H z } { \sim } 4 6 0 \mathrm { M H z }$ 那么就认为DDR3 硬件工作良好。

DDR Test Tool支持DDR3超频测试，只要指定起始频率和终止频率，那么工具就会自动开始一点点的增加频率，直到达到终止频率或者测试失败。设置如图23.5.4.1 所示：

原子哥在线教学:www.yuanzige.com

论坛:www.openedv.com

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/6d1141189efe90b95f341f6c2396c72e4d2771c4a363220748b151e35565c2fb.jpg)



图 23.5.4.1 超频测试配置


图 23.5.4.1中设置好起始频率为400MHz，终止频率为 $6 0 0 \mathrm { M H z }$ ，设置好以后点击“StressTest”开启超频测试，超频测试时间比较久，大家耐心等待测试结果即可。超频测试完成以后结果如图23.5.4.2所示(因为硬件不同，测试结果可能有些许区别)：

![image](https://cdn-mineru.openxlab.org.cn/result/2026-04-29/6c854385-4c08-4aea-9a79-d5d707bdfb5b/618216dec9070647987b767c097c3b7791a22b9ae2ebd583157bb17cfb12ff08.jpg)



图 23.5.4.2 超频测试结果


从图 23.5.4.2可以看出，正点原子的ALPAH 开发板EMMC核心板DDR3最高可以超频到556MHz，当超频到 561MHz 的时候就失败了。556MHz 超过了 $4 6 0 \mathrm { M H z }$ ，说明正点原子的 ALPHA开发板DDR3硬件是没有任何问题的。

# 23.5.5 DDR3L 驱动总结

ALIENTEK_512MB.inc 就是我们最终得到的 DDR3L 初始化脚本，其中包括了时钟、IO 等初始化。I.MX6U 的 DDR3 接口关于 IO 有一些特殊的寄存器需要初始化，如表 23.5.5.1 所示：

<table><tr><td>寄存器地址</td><td>寄存器名</td><td>寄存器值</td></tr><tr><td>0X020E04B4</td><td>IOMUXC_SW_PAD_CTL_GRP_DDR_TYPE</td><td>0X000C0000</td></tr><tr><td>0X020E04AC</td><td>IOMUXC_SW_PAD_CTL_GRP_DDR_TYPE</td><td>0X00000000</td></tr><tr><td>0X020E027C</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_SDCLK_0</td><td>0X00000028</td></tr><tr><td>0X020E0250</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_CAS</td><td>0X00000028</td></tr><tr><td>0X020E024C</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_RAS</td><td>0X00000028</td></tr><tr><td>0X020E0490</td><td>IOMUXC_SW_PAD_CTL_GRP_ADDDS</td><td>0X00000028</td></tr><tr><td>0X020E0288</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_RESET</td><td>0X00000028</td></tr><tr><td>0X020E0270</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_SDBA2</td><td>0X00000000</td></tr></table>


原子哥在线教学:www.yuanzige.com



论坛:www.openedv.com


<table><tr><td>0X020E0260</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_SDODT0</td><td>0X00000028</td></tr><tr><td>0X020E0264</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_SDODT1</td><td>0X00000028</td></tr><tr><td>0X020E04A0</td><td>IOMUXC_SW_PAD_CTL_GRP_CTLDS</td><td>0X00000028</td></tr><tr><td>0X020E0494</td><td>IOMUXC_SW_PAD_CTL_GRP_DDRMODE_CTL</td><td>0X00020000</td></tr><tr><td>0X020e0280</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_SDQS0</td><td>0X00000028</td></tr><tr><td>0X020E0284</td><td>IOMUXC_SW_PAD_CTL_PAD_DRAM_SDQS1</td><td>0X00000028</td></tr><tr><td>0X020E04B0</td><td>IOMUXC_SW_PAD_CTL_GRP_DDRMODE</td><td>0X00020000</td></tr><tr><td>0X020e0498</td><td>IOMUXC_SW_PAD_CTL_GRP_B0DS</td><td>0X00000028</td></tr><tr><td>0X020E04A4</td><td>IOMUXC_SW_PAD_CTL_GRP_B1DS</td><td>0X00000028</td></tr><tr><td>0X020E0244</td><td>IOMUXC_SW_PAD_CTLPAD_DRAM_DQM0</td><td>0X00000028</td></tr><tr><td>0X020E0248</td><td>IOMUXC_SW_PAD_CTLPAD_DRAM_DQM1</td><td>0X00000028</td></tr></table>


表 23.5.5.1 DDR3 IO 相关初始化



接下来看一下 MMDC 外设寄存器初始化，如表 23.5.5.2 所示：


<table><tr><td>寄存器地址</td><td>寄存器名</td><td>寄存器值</td></tr><tr><td>0X021B0800</td><td>DDR_PHY_P0_MPZQHWCTRL</td><td>0XA1390003</td></tr><tr><td>0X021B080C</td><td>MMDC_MPWLDECTRL0</td><td>0X00000000</td></tr><tr><td>0X021B083C</td><td>MPDGCTRL0</td><td>0X0138013C</td></tr><tr><td>0X021B0848</td><td>MPRDDLCTL</td><td>0X40402E34</td></tr><tr><td>0X021B0850</td><td>MPWRDLCTL</td><td>0X40403A34</td></tr><tr><td>0X021B081C</td><td>MMDC_MPRDDQBY0DL</td><td>0X33333333</td></tr><tr><td>0X021B0820</td><td>MMDC_MPRDDQBY1DL</td><td>0X33333333</td></tr><tr><td>0X021B082C</td><td>MMDC_MPWRDQBY0DL</td><td>0XF3333333</td></tr><tr><td>0X021B0830</td><td>MMDC_MPWRDQBY1DL</td><td>0XF3333333</td></tr><tr><td>0X021B08C0</td><td>MMDC_MPDCCR</td><td>0X00921012</td></tr><tr><td>0X021B08B8</td><td>DDR_PHY_P0_MPMUR0</td><td>0X00000800</td></tr><tr><td>0X021B0004</td><td>MMDC0_MDPDC</td><td>0X0002002D</td></tr><tr><td>0X021B0008</td><td>MMDC0_MDOTC</td><td>0X1B333030</td></tr><tr><td>0X021B000C</td><td>MMDC0_MDCFG0</td><td>0X676B52F3</td></tr><tr><td>0X021B0010</td><td>MMDC0_MDCFG1</td><td>0XB66D0B63</td></tr><tr><td>0X021B0014</td><td>MMDC0_MDCFG2</td><td>0X01FF00DB</td></tr><tr><td>0X021b002c</td><td>MMDC0_MDRWD</td><td>0X000026D2</td></tr><tr><td>0X021b0030</td><td>MMDC0_MDOR</td><td>0X006B1023</td></tr><tr><td>0X021b0040</td><td>MMDC_MDASP</td><td>0X0000004F</td></tr><tr><td>0X021b0000</td><td>MMDC0_MDCTL</td><td>0X84180000</td></tr><tr><td>0X021b0890</td><td>MPPDCMPR2</td><td>0X00400a38</td></tr><tr><td>0X021b0020</td><td>MMDC0_MDREF</td><td>0X00007800</td></tr><tr><td>0X021b0818</td><td>DDR_PHY_P0_MPDTCTRL</td><td>0X00000227</td></tr><tr><td>0X021b0004</td><td>MMDC0_MDPDC</td><td>0X0002556D</td></tr><tr><td>0X021b0404</td><td>MMDC0_MAPSR</td><td>0X00011006</td></tr></table>


表23.5.5.2 MMDC外设寄存器初始化及初始化序列


关于 I.MX6U的 DDR3就讲解到这里，因为牵扯到的寄存器太多了，因此没有详细的去分析这些寄存器，大家感兴趣的可以对照着参考手册去分析各个寄存器的含义以及配置值。