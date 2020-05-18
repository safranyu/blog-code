---
title: IOS端微信页面下拉刷新会触发滚动事件
comments: true
categories:
  - JavaScript
tags:
  - JavaScript
abbrlink: 9b47786
date: 2019-03-21 23:02:08
---
在开发的过程中如果设置了滚动加载数据，在ios微信端下拉触发了滚动事件因此重复加载了一次数据。

解决：判断当前文档的高度有没有大于浏览器视口高度

```javascript
var token = true;
    $(window).scroll(function(){
        let AllHeight = $(document).height(); //整个文档高度
        let  visual = $(window).height() // 浏览器的高度
        let heightNow = $(window).scrollTop(); // 滚动卷去的高度
        if((AllHeight - heightNow) < visual+150 && token && AllHeight > visual){
            token = false;
            getList();
        }
        return false;
    });
```

