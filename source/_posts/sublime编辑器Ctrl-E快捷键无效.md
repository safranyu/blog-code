---
title: sublime编辑器Ctrl+E快捷键无效
comments: true
categories:
  - Sublime
tags:
  - Sublime
abbrlink: 8280745d
date: 2018-10-06 18:25:40
---
出现此情况有两种原因，一种没有安装Emmet，另一种就是安装出现了问题
安装Emmet
首先下载package control
过程如下：
```
(1) 打开sublime，
(2) 按Ctrl+`，调出命令框
(3) 在框中根据sublime版本输入代码
打开sublime，通过Ctrl+Shift+P快捷键调出命令面板，在命令面板中输入install package（sublime有模糊搜索功能），并按回车打开
在出来的命令框中输入emmet并按回车进行下载
结束（完美）。
```
安装Emmet出现错误
去gihub下载[pyV8](https://link.jianshu.com/?t=https://github.com/emmetio/pyv8-binaries#readme)
然后找到你的Sublime的packages的安装包路径
解压文件至Packages\PyV8文件夹内(Preferences – Browser Packages)
结束（完美）。
