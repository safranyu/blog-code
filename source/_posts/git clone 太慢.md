---
title: git clone 太慢
comments: true
categories:
  - Git
tags:
  - Git
abbrlink: ads7e5ef
date: 2020-03-09 19:02:06
---

socks5 代替方法

1.首先查看自己socks5的端口号

![](https://pic4.zhimg.com/50/v2-602f596434a3e19e708c225f457e9283_hd.jpg)

2.我这里记下来是127.0.0.1:1086

![](https://pic1.zhimg.com/50/v2-8b2c6525c1ec8de284062da5cf85d01a_hd.jpg)

3.然后输入命令

```
git config--global http.https://github.com.proxysocks5://127.0.0.1:1086
git config --global https.https://github.com.proxysocks5://127.0.0.1:1086
```