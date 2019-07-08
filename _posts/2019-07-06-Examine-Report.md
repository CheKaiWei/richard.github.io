---
layout: post
title: How to recover your U disk?
category: Computer
tags: [Education, Opioions]
---
中断点亮小灯

<p align="right">
Author：Richard 
</p>

<p align="right">
Github:
<a href="https://github.com/CheKaiWei/ARM-Programming"> 中断点亮小灯</a>
</p>


## Environment
Windows 10
Windows Surface
Andriod

## Summary
When the 5g coming, everything will be changed, including the way we use the computer.
I have an idea that, is it possible we use our "bad" computer like my surface 
(it doesn't mean surface is bad, but not that excellent compared to my PC) to control the 
"good" computer? As we know, the main source of computer is CPU and installed memory (RAM), 
whose source can't update through software but only hardware, which means if we want a 
good CPU and RAM, we must buy a new computer (or buy new RAM). 

With the purpose of using the best source and without spending so much money, I figure out a
fantastic idea --- remote desktop.

I know I know, maybe you would say "remote desktop" has been mentioned for a long period of time
and there are many products around the world, what is the special point of your idea?

Exactly, there is much software around the world can help us to control remote computer like TeamViewer.
How there are some vital problems that they didn't solve and this makes my points valuable. 

1. Remote computer software can only transfer the screen and somehow some specific files 
to my local computer, they can't transfer **USB device**, which is the most important thing 
when you are using a remote desktop because you need to use USB to **debug, transfer files, connect to important devices (like a camera)**.
Only when you can communicate with the outside world as the same as we did on the local computer,
can we say this remote computer is "acceptable".


Therefore, we need several steps to complete this remote desktop project, after that, you can
1. Control remote computer like the local computer.
2. Use USB as the same as the local computer.

Let's get start!

## Connect to Remote Computer
Solution: TeamViewer

there are many software:
Windows remote computer
[Connect to another computer using Remote Desktop Connection](https://support.microsoft.com/en-us/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection)  
You must in the same local network. IPV4

[花生壳](https://hsk.oray.com/download/) 
use to “内网穿透”, which means you can use public network to connect local network. 
[Teamviewer](http://www.teamviewer.com/en/index.aspx)  
[Splashtop](http://www.splashtop.com/)  
Splashtop是一款简单易用且性能优秀的远程桌面工具，它的用户已经超过1600万，被公认为是高效率和高性能的工具。甚至可以远程流畅看电影、玩游戏，并且跨平台支持Win、Mac、Linux等系统，甚至是诸如iOS、Android等移动系统。它包含服务端Streamer和客户端Remote Desktop两部分。  
[Chrome Remote Desktop app](https://support.google.com/chrome/answer/1649523?hl=en)  
[Logmein](https://secure.logmein.com/)  
Base on Web.  
[PC Anywhere](http://in.norton.com/symantec-pcanywhere/)  
PC Anywhere是一款老牌的远程控制软件，号称世界领先。  
[GoToMyPC](http://www.gotomypc.com/remote-access/)  
[Radmin](http://www.radmin.com/)  
Radmin是一款屡获殊荣的远程控制软件，它将远程控制、外包服务组件、以及网络监控结合到一个系统里，提供目前为止最快速、强健而安全的工具包。  
[UltraVNC](http://pcsupport.about.com/od/remote-access/fl/ultravnc-review.htm)  
[Show My PC](https://showmypc.com/)  
[Ammyy Admin](http://www.ammyy.com/en/downloads.html)  
Ammyy Admin 是个可靠的、用户体验友好的远程计算机访问工具。其无需然和安装或者配置，数秒即可连接远程计算机。我们可以浏览或者控制运行在远程计算机上的任何应用。并且该工具绝对免费。  
[Mikogo](https://www.mikogo.com/)  
[Any place control](http://www.anyplace-control.com/)  
[Ultra VNC](http://www.uvnc.com/downloads/ultravnc.html)  
UltraVNC 是一个优秀的远程管理软件，支持C/S和B/S访问，速度快捷，内置文件传输工具和对话工具。并且支持从客户端向服务端发送快捷键功能。  
[Yuuguu](https://yuuguu.en.softonic.com/)  
Yuuguu是一款web-conferencing软件，支持Mac, Windows和Linux。似乎其远程控制是个附属产品，不过其速度不错，使用很方便，值得一试。  
[Sky Fex](https://skyfex.com/tour/downloads.php)  
无需安装任何软件，SkyFex 远程桌面对于远程屏幕浏览和控制均很顺手、好用。  

[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  
[]()  

Remote Desktop Software Management Software:  
[RemoteDesktopManager](https://remotedesktopmanager.com/home)  
支持主流的windows和linux远程连接工具，对于windows的连接还是调用mstsc.exe,对于Linux我们可以使用ssh支持的putty，但如果使用vnc的话，可以连接windows，mac，linux：
* Microsoft Remote Desktop (RDP)
* VNC (UltraVNC, TightVNC and RealVNC)
* LogMeIn
* Team Viewer
* FTP (Explorer, Filezilla and WinSCP)
* X Window
* Putty (SSH, Telnet, RAW and rLogin)
* Dameware Mini Remote Control
* Radmin Viewer
* Citrix XenApp (ICA)
* Symantec PC Anywhere
* Microsoft Hyper-V
* Microsoft Virtual PC
* VMware Player

[远程桌面管理工具比较](https://blog.csdn.net/cainiao2013/article/details/87691587)  

## USB Redirector

## Next Stop