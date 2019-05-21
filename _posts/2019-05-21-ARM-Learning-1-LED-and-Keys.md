---
layout: post
title: ARM Learning 1 LED and Keys
category: ARM
tags: [Education, Opioions]
---
Press keys to Control the LEDs in S3C2440

<p align="right">
Author：Richard 
</p>

<p align="right">
Github:
<a href="https://github.com/CheKaiWei/ARM-Programming/tree/master/key_led"> Key Led</a>
</p>

## key_led.s

```C    
.text
.global _start
_start:
            ldr     r0, =0x53000000     @ WATCHDOG寄存器地址
            mov     r1, #0x0                     
            str   r1, [r0]              @ 写入0，禁止WATCHDOG，否则CPU会不断重启
            
            ldr     sp, =1024*4         @ 设置堆栈，注意：不能大于4k, 因为现在可用的内存只有4K
                                        @ nand flash中的代码在复位后会移到内部ram中，此ram只有4K
            bl      main                @ 调用C程序中的main函数
halt_loop:
            b       halt_loop

```

### 为何要设置WATCHDOG
![WATCHDOG]({{"image/ARM Learning 1 LED and Keys/1-WATCHDOG.png" | absolute_url}})

WATCHDOG是用来重启的，程序启动则会不断返回1给WATCHDOG，如果程序卡死则返回0给WATCHDOG。此时程序仍未执行，因此会不断返回0，导致系统不断重启。我们不希望系统重启，因此此时我们选择将WATCHDOG置0，即屏蔽。

### 为什么设置堆栈

为了后续main程序可以使用堆栈。

## key_led.c
```C
#define GPFCON      (*(volatile unsigned long *)0x56000050)
#define GPFDAT      (*(volatile unsigned long *)0x56000054)

#define GPGCON      (*(volatile unsigned long *)0x56000060)
#define GPGDAT      (*(volatile unsigned long *)0x56000064)

/*
 * LED1,LED2,LED4对应GPF4、GPF5、GPF6
 */
#define	GPF4_out	(1<<(4*2))
#define	GPF5_out	(1<<(5*2))
#define	GPF6_out	(1<<(6*2))


// 为什么是2 
/*
 * S2,S3,S4对应GPF0、GPF2、GPG3
 */
#define GPF0_in     (0<<(0*2))
#define GPF2_in     (0<<(2*2))
#define GPG3_in     (0<<(3*2))



int main()
{
        
        // LED1,LED2,LED4对应的3根引脚设为输出
        GPFCON |= GPF4_out | GPF5_out | GPF6_out;
        
        // S2,S3对应的2根引脚设为输入
        GPFCON |= GPF0_in | GPF2_in;

        // S4对应的引脚设为输入
        GPGCON |= GPG3_in;

        unsigned long keyData;

        while(1){
            //若Kn为0(表示按下)，则令LEDn为0(表示点亮)
            keyData = GPFDAT;             // 读取GPF管脚电平状态
        
            if (keyData & (1<<0))        // S2没有按下
                GPFDAT |= (1<<4);       // LED1熄灭
            else    
                GPFDAT &= ~(1<<4);      // LED1点亮
                
            if (keyData & (1<<2))         // S3没有按下
                GPFDAT |= (1<<5);       // LED2熄灭
            else    
                GPFDAT &= ~(1<<5);      // LED2点亮
    
            keyData = GPGDAT;             // 读取GPG管脚电平状态
            
            if (keyData & (1<<3))         // S4没有按下
                GPFDAT |= (1<<6);       // LED3熄灭
            else    
                GPFDAT &= ~(1<<6);      // LED3点亮
    }

    return 0;
}


```

### 为什么要用到GPFCON和GPFDAT?


![GPFCON]({{"image/ARM Learning 1 LED and Keys/2-GPFCON.png" | absolute_url}})

![INT]({{"image/ARM Learning 1 LED and Keys/3-INT01.png" | absolute_url}})

![INT]({{"image/ARM Learning 1 LED and Keys/3-INT02.png" | absolute_url}})

![INT]({{"image/ARM Learning 1 LED and Keys/3-INT03.png" | absolute_url}})

由上面可知，其中需要用到的key和led对应的管脚需要F和G寄存器，CON是指config，用于指明寄存器的四种工作模式，DAT指data，用于指明寄存器现在的状态，其中CON是32位，DAT是8位。

### (0<<(0*2))什么意思？
是指把0向左移动0*2位，因为这里的GPFCON是两位控制一位的。

### GPFCON |= GPF4_out | GPF5_out | GPF6_out;什么意思？
是指把这三个数都“或”上，然后和GPFCON“或”，也就是把这三个数写入GPFCON内。也可以用其他方式写入。

### if (keyData & (1<<0))什么意思？
是指把keyData的第0位和1“与”之后，得出的逻辑输出