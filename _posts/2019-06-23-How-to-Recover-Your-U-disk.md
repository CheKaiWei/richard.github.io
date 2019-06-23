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

## How to recover your U disk? 1
1. 在桌面空白处单击鼠标右键，新建一个文本文档.   
2. 然后将下列一段代码拷贝到文档中：  
## command line

```bash
    for /f "delims=?" %%a in ('dir /a /b') do attrib -a -s -h -r "%%a"
　　@echo off
　　pause>nul
　　exit
```
3. 接着点击“文件--另存为”，将其保存在u盘中。并将文件命名为“显示隐藏文件.cmd”，保存类型为“所有文件”，随后点击“保存”。  
[git 常用命令(含删除文件)](https://www.cnblogs.com/springbarley/archive/2012/11/03/2752984.html)  


## How to recover your U disk? 2

```bash
    attrib -H -S **.** /S /D

    attrib -H -S Work /S /D
    attrib -H -S mydocument.doc /S /D
```