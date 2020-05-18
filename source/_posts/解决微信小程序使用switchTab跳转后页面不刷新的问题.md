---
title: 解决微信小程序使用switchTab跳转后页面不刷新的问题
comments: true
categories:
  - 小程序
tags:
  - 小程序
abbrlink: adg7e5ef
date: 2020-04-01 19:02:06
---

```
wx.switchTab({
    url: '/pages/cart/index',
    success:function () {
        var page = getCurrentPages().pop();
        if (page == undefined || page == null) return;
        page.onLoad();   //重新刷新页面
    }
})
```
