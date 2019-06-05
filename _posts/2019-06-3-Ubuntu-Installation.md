---
layout: post
title: Ubuntu Installation
category: ROS
tags: [Education, Opioions]
---
安装Ubuntu心得

<p align="right">
Author：Richard 
</p>

<p align="right">
Github:
<a href="https://github.com/CheKaiWei/ARM-Programming/tree/master/int"> INT</a>
</p>

## Environment
Ubuntu18  

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