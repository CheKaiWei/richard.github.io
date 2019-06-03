---
layout: post
title: ROS Learning
category: ROS
tags: [Education, Opioions]
---
回顾在DJI学习的ROS知识。

<p align="right">
Author：Richard 
</p>

<p align="right">
Github:
<a href="https://github.com/CheKaiWei/ARM-Programming/tree/master/int"> INT</a>
</p>

## Environment
Ubuntu18  
ROS Mikic

## Ubuntu安装
1. 在官网安装Ubuntu18版本  
2. 安装UltraISO
3. 把iso刻录进去
4. 重启进入BIOS，选择安全启动、UEIF启动  
[Win10+Ubuntu18.04 亲测UEFI启动模式双硬盘+双系统成功安装经验](https://blog.csdn.net/xrinosvip/article/details/80428133)  

### 优化
1. 安装搜狗输入法
安装fcitx:
```bash
sudo apt install fcitx
```
安装deb包：
```bash
sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb
```
修复缺少依赖：
```bash
sudo apt --fix-broken install
```
[ubuntu18.04 安装后快速初始化常用环境指南](https://blog.szfszf.top/tech/ubuntu18-04-%E5%AE%89%E8%A3%85%E5%90%8E%E5%BF%AB%E9%80%9F%E5%88%9D%E5%A7%8B%E5%8C%96%E5%B8%B8%E7%94%A8%E7%8E%AF%E5%A2%83%E6%8C%87%E5%8D%97/)  
[Ubuntu18.04安装之后的配置+优化](https://blog.csdn.net/ywk_hax/article/details/83790207)
### 问题
Q：ubuntu 解决“无法获得锁 /var/lib/dpkg/lock -open （11：资源暂时不可用）”的方法  
A：
在ubuntu系统的termial下，用apt-get install 安装软件的时候，如果在未完成下载的情况下将terminal close。此时 apt-get进程可能没有结束。结果，如果再次运行apt-get install 命令安装如今，可能会发生下面的提示  
   无法获得锁 /var/lib/dpkg/lock - open (11: 资源暂时不可用)  
   无法锁定管理目录(/var/lib/dpkg/)，是否有其他进程正占用它？  
解决办法如下：  
1。终端输入 ps  aux ，列出进程。找到含有apt-get的进程，直接sudo kill PID。  
2。强制解锁,命令  
```bash
sudo rm /var/cache/apt/archives/lock  
sudo rm /var/lib/dpkg/lock
```

Q：ubuntu命令行修改系统语言为英文
```bash
gedit /etc/default/locale
```
将原来的配置内容修改为
```
LANG="en_US.UTF-8"
LANGUAGE="en_US:en"
```
再在终端下运行：
```
locale-gen -en_US:en
```
注销或重启后，即可恢复为英文的语言环境。
## ROS安装

## ROS学习
### 






[ProcessOn](https://www.processon.com/diagraming/5b5e80c8e4b08d36229510a8)用于绘制流程图

## 技巧
- Multisim  
multisim中控制开关：DIPSW1  
[NE555 制作呼吸灯 ](http://dxx.qcuwh.cn/wcs/Upload/201611/583d3fd01ed2f.pdf)  


- AD  
[PCB专业术语翻译](https://wenku.baidu.com/view/87ec5d916f1aff00bfd51e4d)  
[Altium Designer——AD画PCB图步骤总结](https://blog.csdn.net/Tang_Chuanlin/article/details/79803575)  
[Altium Designer中如何进行覆铜和网状覆铜？](https://blog.csdn.net/ldcung/article/details/77388291)  
[如何使用Altium Designer 18铺铜？](http://www.icxbk.com/ask/detail/11544.html)   
AD如何统计pin数量：打开原理图→Tools→Parameter  
[Altium Designer覆铜后变为绿色是怎么回事？](https://blog.csdn.net/weixin_42164589/article/details/88853912)  
[如何用Altium Designer画PCB图](https://jingyan.baidu.com/article/363872ec357a206e4ba16f00.html)  
[AD 中设定PCB板尺寸大小的方法](https://blog.csdn.net/mzy202/article/details/54880947)  
[Altium designer如何镜像翻转元件？](https://zhidao.baidu.com/question/365170674728128452.html)  
[Altium Designer——原理图导出元件清单](https://blog.csdn.net/Tang_Chuanlin/article/details/79488115)

- Markdown换行  
两段文字之间敲两个空格符然后换行  


- 清华Latex  
[清华大学学位论文 LATEX 模板](http://mirrors.concertpass.com/tex-archive/macros/latex/contrib/thuthesis/main.pdf)  
[ThuThesis：清华大学学位论文模板](http://mirror.las.iastate.edu/tex-archive/macros/latex/contrib/thuthesis/thuthesis.pdf)  
[Github LaTeX Thesis Template for Tsinghua University](https://github.com/xueruini/thuthesis)

- Latex  
[LaTeX 有哪些「新手须知」的内容？](https://www.zhihu.com/question/30090572)  
[latex分文件编写技巧](https://blog.csdn.net/yanxiangtianji/article/details/13169699)  
Latex插入空白行：~\\\：一行空白
[TeX Live安装指南](https://blog.csdn.net/wr339988/article/details/66611166)

- Latex无法插入目录  
[latex不能生成目录，怎么解决？？](https://zhidao.baidu.com/question/1541025230634017307.html)  
[LaTeX简要教程7:生成目录](http://topspeedsnail.com/g-latex-content-table/)  
[LaTeX 插入pdf文档](https://blog.csdn.net/bendanban/article/details/51850659)  
[latex文字加粗、斜体](https://blog.csdn.net/jminer/article/details/14146939)  
[【LaTeX入门】05、换行、换段、换页、首行缩进等命令](https://blog.csdn.net/xiazdong/article/details/8892105)  
latex中怎么打出百分号： \\%   
[Latex中的cls文件使用](https://blog.csdn.net/owldestiny/article/details/5560347)  
[Latex 编译错误排查的一些经验](https://blog.csdn.net/u012675539/article/details/46272387)  
[Installing TeX fonts](https://www.tug.org/fonts/fontinstall.html)   
[使用VSCode编写LaTeX](https://zhuanlan.zhihu.com/p/38178015)  
[LaTeX技巧932：如何配置Visual Studio Code作为LaTeX编辑器](http://www.latexstudio.net/archives/12260.html)  
[论文写作的又一利器：VSCode + Latex Workshop + MikTex + Git](https://blog.csdn.net/yinqingwang/article/details/79684419)  

- Latex errors  
recipe teriminate with error source: latex workshop(Extension)