---
title: AutoJs学习
comments: true
categories:
  - JavaScript
tags:
  - AutoJs
abbrlink: adc7e5ef
date: 2019-03-24 16:02:06
---

### AutoJs学习

> **不需要Root权限**的JavaScript自动化软件

[官方文档](<https://hyb1996.github.io/AutoJs-Docs/#/>)
[视频教学](<https://search.bilibili.com/all?keyword=autojs>)

#### 常见单个控件

```javascript
TextView //文本控件
ImageView //图片控件
CheckBox //勾选控件
EditText //输入控件
View //视图控件
```

- 有图片的不一定是图片控件

#### 常见容器控件

```javascript
LinearLayout //线性布局容器
RelativeLayout //相对布局容器
FrameLayout //帧布局
ListView //列表容器
RecyclerView //列表容器
ScrollView //滚动容器
```

- 容器与容器之间可以相互嵌套

#### 单个控件的操作

```javascript
click	//点击
longClick //长按
scroll... //滚动
setText	//设置文本
children //遍历
find	//子控件查找
parent	// 父控件查找
```

#### 获取控件

```javascript
id("xxxx").findOne(1000)
className("xxxx").findOne(1000).find(id("xxxx"))
text("xxx")
desc("xxx")

//完全匹配
Contains //包含
StartWith //开头
EndWith //结尾
Matches //正则

```

#### 打印

```javascript
log("xxxx") //控制面板输出
toast("xxxx") //手机屏幕上输出
```

#### 基础

```javascript
auto.waitFor()
auto();// 自动打开无障碍服务
launchApp("app名字")
```



#### 问题

1. 有时候手机重新连接vs code总是连接不上，应该是没有正常退出占用端口，最简单的是重启电脑