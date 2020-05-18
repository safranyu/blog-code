---
title: Mac 管理Node版本工-n
comments: true
categories:
  - Mac
tags:
  - Mac
  - Node
abbrlink: b72i3fe5
date: 2019-09-21 22:55:37
---

### 安装

`npm install -g n`

### 安装/激活版本

```
只需执行n <version>即可安装node。如果<version>已经安装（通过n），n将激活该版本。
例如：
    $ n 8.16.2
    $ n 12.12.0
```
### 选择

> n单独执行是查看当前安装的版本，使用向上和向下箭头键导航并按enter或右箭头键进行选择，使用command+ C（控制+ C）退出选择屏幕。

```
$n
    node/8.16.2
  ο node/12.12.0
    node/14.2.0
```

### 使用或安装最新的官方发布：

```shell
$n latest
```

### 使用或安装稳定的官方发布：

```
$n stable
```

### 使用或安装最新的LTS官方版本：

```
$n lts
```

### 删除版本，删除一些版本：

```
$n rm 8.16.2 v12.12.0
```

### 或者，您可以使用以下 - 代替rm：

```
$n - 0.9.4
```

### 相关用法也可以

```
$n --help
```

[官方文档](https://www.npmjs.com/package/n)

[Node历史版本](https://nodejs.org/en/blog/release/)

![image](http://nimit.io/images/n/n.gif)
