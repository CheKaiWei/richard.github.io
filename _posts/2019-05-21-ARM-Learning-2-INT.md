---
layout: post
title: ARM Learning 1 INT
category: ARM
tags: [Education, Opioions]
---
Press keys to Control the LEDs in S3C2440 by INT.

<p align="right">
Author：Richard 
</p>

<p align="right">
Github:
<a href="https://github.com/CheKaiWei/ARM-Programming/tree/master/int"> INT</a>
</p>


## head.s
<details>
<summary>head.s</summary>

```C    
.extern     main
.text 
.global _start 
_start:
@******************************************************************************       
@ 中断向量，本程序中，除Reset和HandleIRQ外，其它异常都没有使用
@******************************************************************************       
    b   Reset

@ 0x04: 未定义指令中止模式的向量地址

@@ 数据不长久，因此使用变量来代替

HandleUndef:
    b   HandleUndef 
 
@ 0x08: 管理模式的向量地址，通过SWI指令进入此模式
HandleSWI:
    b   HandleSWI

@ 0x0c: 指令预取终止导致的异常的向量地址
HandlePrefetchAbort:
    b   HandlePrefetchAbort

@ 0x10: 数据访问终止导致的异常的向量地址
HandleDataAbort:
    b   HandleDataAbort

@ 0x14: 保留
HandleNotUsed:
    b   HandleNotUsed

@ 0x18: 中断模式的向量地址
    b   HandleIRQ

@ 0x1c: 快中断模式的向量地址
HandleFIQ:
    b   HandleFIQ

Reset:                  
    ldr sp, =4096           @ 设置栈指针，以下都是C函数，调用前需要设好栈
    bl  disable_watch_dog   @ 关闭WATCHDOG，否则CPU会不断重启

	@@ 什么是看门狗？为什么要设置？
	@@ C要设置堆栈
    
    msr cpsr_c, #0xd2       @ 进入中断模式
    ldr sp, =3072           @ 设置中断模式栈指针

    msr cpsr_c, #0xd3       @ 进入管理模式
    ldr sp, =4096           @ 设置管理模式栈指针，
                            @ 其实复位之后，CPU就处于管理模式，
                            @ 前面的“ldr sp, =4096”完成同样的功能，此句可省略

    bl  init_led            @ 初始化LED的GPIO管脚
    bl  init_irq            @ 调用中断初始化函数，在init.c中
    msr cpsr_c, #0x5f       @ 设置I-bit=0，开IRQ中断
    
    ldr lr, =halt_loop      @ 设置返回地址
    ldr pc, =main           @ 调用main函数
	@@ 跳
halt_loop:
    b   halt_loop

HandleIRQ:
    sub lr, lr, #4                  @ 计算返回地址
    stmdb   sp!,    { r0-r12,lr }   @ 保存使用到的寄存器
                                    @ 注意，此时的sp是中断模式的sp
                                    @ 初始值是上面设置的3072
    
    ldr lr, =int_return             @ 设置调用ISR即EINT_Handle函数后的返回地址  
    ldr pc, =EINT_Handle            @ 调用中断服务函数，在interrupt.c中
int_return:
    ldmia   sp!,    { r0-r12,pc }^  @ 中断返回, ^表示将spsr的值复制到cpsr
    
```

</details>

功能：初始化，设置中断模式、管理模式的栈，设置好中断处理函数。

其中：
```C
    bl  init_led
    bl  init_irq 
```
为执行此两个函数。

---

## s3c24xx.h
<details>
<summary>s3c24xx.h</summary>

```C
/* WOTCH DOG register */
#define     WTCON           (*(volatile unsigned long *)0x53000000)

/* SDRAM regisers */
#define     MEM_CTL_BASE    0x48000000
#define     SDRAM_BASE      0x30000000

/* NAND Flash registers */
#define NFCONF              (*(volatile unsigned int  *)0x4e000000)
#define NFCMD               (*(volatile unsigned char *)0x4e000004)
#define NFADDR              (*(volatile unsigned char *)0x4e000008)
#define NFDATA              (*(volatile unsigned char *)0x4e00000c)
#define NFSTAT              (*(volatile unsigned char *)0x4e000010)

/*GPIO registers*/
#define GPBCON              (*(volatile unsigned long *)0x56000010)
#define GPBDAT              (*(volatile unsigned long *)0x56000014)

#define GPFCON              (*(volatile unsigned long *)0x56000050)
#define GPFDAT              (*(volatile unsigned long *)0x56000054)
#define GPFUP               (*(volatile unsigned long *)0x56000058)

#define GPGCON              (*(volatile unsigned long *)0x56000060)
#define GPGDAT              (*(volatile unsigned long *)0x56000064)
#define GPGUP               (*(volatile unsigned long *)0x56000068)

#define GPHCON              (*(volatile unsigned long *)0x56000070)
#define GPHDAT              (*(volatile unsigned long *)0x56000074)
#define GPHUP               (*(volatile unsigned long *)0x56000078)



/*UART registers*/
#define ULCON0              (*(volatile unsigned long *)0x50000000)
#define UCON0               (*(volatile unsigned long *)0x50000004)
#define UFCON0              (*(volatile unsigned long *)0x50000008)
#define UMCON0              (*(volatile unsigned long *)0x5000000c)
#define UTRSTAT0            (*(volatile unsigned long *)0x50000010)
#define UTXH0               (*(volatile unsigned char *)0x50000020)
#define URXH0               (*(volatile unsigned char *)0x50000024)
#define UBRDIV0             (*(volatile unsigned long *)0x50000028)


/*interrupt registes*/
#define SRCPND              (*(volatile unsigned long *)0x4A000000)
#define INTMOD              (*(volatile unsigned long *)0x4A000004)
#define INTMSK              (*(volatile unsigned long *)0x4A000008)
#define PRIORITY            (*(volatile unsigned long *)0x4A00000c)
#define INTPND              (*(volatile unsigned long *)0x4A000010)
#define INTOFFSET           (*(volatile unsigned long *)0x4A000014)
#define SUBSRCPND           (*(volatile unsigned long *)0x4A000018)
#define INTSUBMSK           (*(volatile unsigned long *)0x4A00001c)

/*external interrupt registers*/
#define EINTMASK            (*(volatile unsigned long *)0x560000a4)
#define EINTPEND            (*(volatile unsigned long *)0x560000a8)
```
</details>

这里使用到的interrupt registes，我们可以看到：
```C
#define SRCPND              (*(volatile unsigned long *)0x4A000000)
#define INTMOD              (*(volatile unsigned long *)0x4A000004)
#define INTMSK              (*(volatile unsigned long *)0x4A000008)
#define PRIORITY            (*(volatile unsigned long *)0x4A00000c)
#define INTPND              (*(volatile unsigned long *)0x4A000010)
#define INTOFFSET           (*(volatile unsigned long *)0x4A000014)
#define SUBSRCPND           (*(volatile unsigned long *)0x4A000018)
#define INTSUBMSK           (*(volatile unsigned long *)0x4A00001c)
```
S3C2440A 中的中断控制器接受来自 60 个中断源的请求。提供这些中断源的是内部外设，如 DMA 控制器、UART、IIC 等等。在这些中断源中，UARTn、AC97 和 EINTn 中断对于中断控制器而言是“或”关系。当从内部外设和外部中断请求引脚收到多个中断请求时，中断控制器在仲裁步骤后请求 ARM920T 内核的 FIQ或 IRQ。仲裁步骤由硬件优先级逻辑决定并且写入结果到帮助用户通告是各种中断源中的哪个中断发生了的中断挂起寄存器中。

控制流程图如下：

![INT]({{"image/ARM Learning 1 LED and Keys/4-INT.png" | absolute_url}})

- 先收集到SRCPND
- 用INTMOD判断是否为FIQ
- 判断完后进入屏蔽环节INTMSK进行筛选
- PRIORITY进行优先级划分
- 划分结果存储在INTOFFSET

优先级如下：

![INT]({{"image/ARM Learning 1 LED and Keys/4-INT02.png" | absolute_url}})

---

## init.c
<details>
<summary>init.c</summary>

```C
/*
 * init.c: 进行一些初始化
 */ 

#include "s3c24xx.h"
/*
 * LED1,LED2,LED4对应GPF4、GPF5、GPF6
 */
#define	GPF4_out	(1<<(4*2))
#define	GPF5_out	(1<<(5*2))
#define	GPF6_out	(1<<(6*2))

#define	GPF4_msk	(3<<(4*2))
#define	GPF5_msk	(3<<(5*2))
#define	GPF6_msk	(3<<(6*2))

/*
 * S2,S3,S4对应GPF0、GPF2、GPG3
 */
#define GPF0_eint     (0x2<<(0*2))
#define GPF2_eint     (0x2<<(2*2))
#define GPG3_eint     (0x2<<(3*2))

#define GPF0_msk    (3<<(0*2))
#define GPF2_msk    (3<<(2*2))
#define GPG3_msk    (3<<(3*2))

/*
 * 关闭WATCHDOG，否则CPU会不断重启
 */
void disable_watch_dog(void)
{
    WTCON = 0;  // 关闭WATCHDOG很简单，往这个寄存器写0即可
}

void init_led(void)
{
    // LED1,LED2,LED4对应的3根引脚设为输出
    GPFCON &= ~(GPF4_msk | GPF5_msk | GPF6_msk);
    GPFCON |= GPF4_out | GPF5_out | GPF6_out;
}

/*
 * 初始化GPIO引脚为外部中断
 * GPIO引脚用作外部中断时，默认为低电平触发、IRQ方式(不用设置INTMOD)
 */ 
void init_irq( )
{
    // S2,S3对应的2根引脚设为中断引脚 EINT0,ENT2
    GPFCON &= ~(GPF0_msk | GPF2_msk);
    GPFCON |= GPF0_eint | GPF2_eint;

    // S4对应的引脚设为中断引脚EINT11
    GPGCON &= ~GPG3_msk;
    GPGCON |= GPG3_eint;
    
    // 对于EINT11，需要在EINTMASK寄存器中使能它
    EINTMASK &= ~(1<<11);
        
    /*
     * 设定优先级：
     * ARB_SEL0 = 00b, ARB_MODE0 = 0: REQ1 > REQ3，即EINT0 > EINT2
     * 仲裁器1、6无需设置
     * 最终：
     * EINT0 > EINT2 > EINT11即K2 > K3 > K4
     */
    PRIORITY = (PRIORITY & ((~0x01) | (0x3<<7))) | (0x0 << 7) ;

    // EINT0、EINT2、EINT8_23使能
    INTMSK   &= (~(1<<0)) & (~(1<<2)) & (~(1<<5));
}
```
</details>
进行一些初始化，对优先级等寄存器进行赋值

---

## interrupt.c
<details>
<summary>interrupt.c</summary>

interrupt.c
```C
#include "s3c24xx.h"

void EINT_Handle()
{
    unsigned long oft = INTOFFSET;
    unsigned long val;
    
    switch( oft )
    {
        // S2被按下
        case 0: 
        {   
            GPFDAT |= (0x7<<4);   // 所有LED熄灭
            GPFDAT &= ~(1<<4);      // LED1点亮
            break;
        }
        
        // S3被按下
        case 2:
        {   
            GPFDAT |= (0x7<<4);   // 所有LED熄灭
            GPFDAT &= ~(1<<5);      // LED2点亮
            break;
        }

        // K4被按下
        case 5:
        {   
            GPFDAT |= (0x7<<4);   // 所有LED熄灭
            GPFDAT &= ~(1<<6);      // LED4点亮                
            break;
        }

        default:
            break;
    }

    //清中断
    if( oft == 5 ) 
        EINTPEND = (1<<11);   // EINT8_23合用IRQ5
    SRCPND = 1<<oft;
    INTPND = 1<<oft;
	//SRCPND = SRCPND;
}

// 中断过程：
//
```
</details>

这里用到INTOFFSET寄存器：
```C
    unsigned long oft = INTOFFSET;
```
可以看到，通过读取此寄存器，获得最优先级的中断请求。

![INT]({{"image/ARM Learning 1 LED and Keys/4-INT03.png" | absolute_url}})

同时，这里使用清理中断的方法如下：
```C
    //清中断
    if( oft == 5 ) 
        EINTPEND = (1<<11);   // EINT8_23合用IRQ5
    SRCPND = 1<<oft;
    INTPND = 1<<oft;
	//SRCPND = SRCPND;
```
可以看到，**是将此位置为1，即可清除此位的数值**！

有两种方法，如果是单次清理，使用
```C
    SRCPND = SRCPND;
```
如果是循环清理，就是未完成的中断还需要继续完成的话，则需要使用：
```C
    SRCPND = 1<<oft;
    INTPND = 1<<oft;
```
---
## main.c
<details>
<summary>main.c</summary>
main.c
```C
int main()
{
    while(1);
    return 0;
}
```
</details>
此处使用main循环，等待中断

