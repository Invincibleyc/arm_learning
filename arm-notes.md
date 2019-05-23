参考资料：

https://blog.csdn.net/zerokkqq/article/details/79621739

https://www.anquanke.com/post/id/86393

#### 简介：

与x86一样，ARM也是一种CPU架构。x86广泛应用于PC机，而ARM广泛应用于工业控制、无线通讯、打印机数码相机等等，现在智能手机的处理器一般都是ARM架构。研究ARM编程是挖掘漏洞，保证手机的通讯、使用安全的基础。

与x86的异同：

1. 指令集

> 它们最主要的不同是指令集，x86属于复杂指令集（CISC），而ARM属于精简指令集（RISC），指令更少，单条指令的功能相对简单，仅通过LOAD/STORE指令来访存。

2. 指令长度

>ARM的指令长度固定，在arm模式下为32 bits，在Thumb模式下为16 bits
>
>而x86的指令不等长

3. 大端小端

> x86采用小端。ARM在版本3之前是小端，在那之后默认是大端。

**嵌入式系统**

根据IEEE定义，嵌入式系统是“控制、监视或者辅助操作机器和设备的装置。



---

#### ARM汇编

**一、编译运行**

1. 编译环境配置

   > sudo add-apt-repository ppa:terry.guo/gcc-arm-embedded 
   >
   > sudo apt-get update
   >
   > sudo apt-get install gcc-arm-none-eabi

   使用ln链接，对命令重新命名：

   > cd /usr/bin 
   >
   > sudo ln arm-none-eabi-gcc arm-linux-gcc 
   >
   > sudo ln arm-none-eabi-ar  arm-linux-ar 
   >
   > sudo ln arm-none-eabi-as arm-linux-as
   >
   > sudo ln arm-none-eabi-objdump arm-linux-objdump

2. 编译命令

   将C程序编译为.o

   > arm-none-eabi-gcc --specs=rdimon.specs main.c

   将arm程序编译为.o

   > arm-linux-as test.s -o test.o

   将.o文件反汇编

   > arm-linux-objdump -d test.o

**二、基础知识**

1. 数据类型

2. 寄存器

   在ARMv6-M和ARMv7-M处理器中，有30个通用寄存器，其中前16个是用户层可访问，其余寄存器在内核等高特权级下访问。

   对用户层可访问的寄存器介绍如下：

   > R0-R6、R8-R10      通用寄存器（R0常用于保存返回值）
   >
   > R7                             一般存放系统调用号
   >
   > R11    别名：FP       栈帧指针
   >
   > R12    别名：IP        内部程序调用
   >
   > R13    别名：SP       栈指针
   >
   > R14    别名：LR       链接寄存器（一般存放函数返回地址）
   >
   > R15    别名：PC       程序计数寄存器
   >
   > CPSR                         当前程序状态寄存器

   ![](https://p2.ssl.qhimg.com/t01a8e5d24fa91f9f0f.jpg)

   （图片来自网络）

   