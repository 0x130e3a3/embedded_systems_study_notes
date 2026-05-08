



在公司遇到问题的时候,总是以解决问题为目的,有的时候来不及对所涉及的知识做系统的整理.此文档一是对debug做记录,方便回顾总结,以后遇到相同相似的问题可以快速解决.二是整理debug过程中来不及梳理的知识,达到以点及面的作用.




1标题: boot启动kernel的时候卡死

问题描述:   
1   boot从flash的指定位置拿到了kernel+dtb的brn文件,通过解析brn文件头,得到了kernel(image)和dtb在flash中的具体位置和size位置,将kernel和dtb加载到ddr的指定位置.然后通过函数指针指向kernel的位置,在调用函数指针调准到kernel代码中.这个时候就是从boot阶段跳到kernel阶段了.
log到此为止了,按理说下一个log应该就是kernel的log了(kernel version啥的),但是没打印出来.
2 相同的固件试制了十几个机器,只有一个板子有这个问题

debug1 : 尝试通过拉io的方法定位具体的死机位置.确定了大概的死机位置在板级的c函数start和标准的kerenl启动的函数start的串口初始化之前死机的,但是拉io想要定位到集体的位置太麻烦了,暂时搁置进一步定位
debug2 : 在boot中爆ddr测试代码,先写在读,注意boot也在ddr上跑,避开boot的运行位置.发现异常的这块板子存在写读数据对不上的问题.基本确实是这个板子的soc的ddr的这块有问题
debug3 : 后续可以尝试交叉测试,将异常板子上的soc和正常板子的soc做交换,看看问题跟着谁走
debug4 : 通常情况下,ddr问题是可以找硬件量ddr时序看ddr是否稳定的,但是这款soc的ddr是集成在soc中的


涉及到的知识点: 
boot加载kernel   kernel启动流程   kernel反汇编  uimage和zimage和image和vmlinux  debug方式-拉io   ddr测试  ddr适配



2标题: 休眠唤醒后面板上的时间落后
问题描述: 
1 ddr自刷新级别的休眠唤醒后, 面板上的时间落后了一段时间,长度基本等于休眠时间
2 板子无rtc
3 需要考虑无网络情况
4 休眠时,会保留一个小核继续运行

debug1 : 发现面板上的时间使用的接口是硬件时间接口(错误,应该用系统时间)
debug2 : 休眠时的时间保证同步方案,休眠前保存系统时间,休眠中继续计时,唤醒后将休眠时间加到系统时间上(在无rtc的情况下保证系统时间的正确)

涉及到的知识点:
系统时间(linux的时间子系统,REALTIME,MONOTONIC,BOOTTIME,MONOTONIC_RAW)    硬件时间   时区配置      timedatectl     NTP(chrony,ntpd)   时间命令(uptime,date,hwclock)


3标题；lds脚本出错导致堆栈位置错位

问题描述：
1 csky架构
2 lds脚本中分了两个段，一个方text，rodata，data，bss等。另一个放heap和stack。通过 > MEM0 和 >MEM1实现。但是发现heap没有按照预想的那样在MEM1中而是在MEM0中紧跟着。bss的末尾

```c
//错误代码示例
/* MEM0 中的段 */
.bss : {
    *(.bss)
    /* 这里不要加 ALIGN(8)，让它自然结束 */
} > MEM0

/* MEM1 中的段 */
.heap ALIGN(8) : {
    *(.heap)
} > MEM1
```


```c
//可保证正确的代码示例
/* MEM1 中的段 */
.heap : {
    . = ALIGN(8);  /* ✅ 正确写法：进入 MEM1 后，再对内部的起始位置进行对齐 */
    *(.heap)
} > MEM1
```


debug1 ： 实测确认是 ALIGN(8) 这个条件导致的，去掉后heap就正常的分配到MEM1了

涉及到的知识点：
链接脚本及语法  编译流程 