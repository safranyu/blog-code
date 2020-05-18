---
title: Mac 下配置Flutter
comments: true
categories:
  - Flutter
tags:
  - Flutter
abbrlink: adh7e5ef
date: 2020-04-16 19:02:06
---


> https://segmentfault.com/a/1190000014845833

flutter中文网https://flutterchina.club

## 系统环境要求
macOS (64-bit)
硬盘空间: 700 MB (不包含android studio等编辑器工具).
命令行工具:bash, mkdir, rm, git, curl, unzip, which,brew需要保证上述命令在命令行下能使用，

如果没有安装brew，那么需要先安装：参考：https://segmentfault.com/a/1190000013317511
## 下载flutter
推荐去官网下载，速度并不慢，网址：
https://flutter.io/setup-macos/
## 设置flutter镜像
运行:
```
vim ~/.bash_profile
```
增加
```
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```
然后运行
```
source ~/.bash_profile
```
## 配置环境变量
先把刚才下载的解压缩，笔者选择使用的目录是Desktop下的flutter文件夹
![image](http://note.youdao.com/yws/res/255/WEBRESOURCE1e5a3a8733ba0ec9901abd6ee1eef564)
配置环境变量,这里笔者使用命令行：
```
vim ~/.bash_profile
```
将flutter工具添加到您的路径：
```
export PATH="$PATH:/Users/safran/Desktop/flutter/bin"
```
这个时候应该能运行flutter命令了，我们运行命令行：
```
flutter -h
```
## 检查环境
运行以下命令以查看是否需要安装任何依赖项来完成设置（对于详细输出，添加-v标志）：
```
flutter doctor
```
![image](http://note.youdao.com/yws/res/270/WEBRESOURCEf2f8e0838e159a29d02fc0af172c23b1)
按照检测结果的说明，如果有[!] ✗ 标志，表示本行检测不通过，需要做一些设置或者安装一些软件。
![image](http://note.youdao.com/yws/res/274/WEBRESOURCE0b98956a584dcc9460cce0097a821131)
如果android studio没有安装，那么可以先装下，并使用android studio下载最新的android sdk。android studio下载地址:http://www.android-studio.org/
下载完打开
如果有安装，那么很有可能看到：
```
[!]Android toolchain - develop for Android devices (Android SDK version 29.0.0)
```
```
! Some Android licenses not accepted.  To resolve this, run: flutter doctor --android-licens

```
需要运行
```
flutter doctor --android-licenses
```
一路输入y就行
