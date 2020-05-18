---
title: pulltorefresh.js插件滚动重复刷新
comments: true
categories:
  - JavaScript
tags:
  - JavaScript
  - js插件
abbrlink: d9939f07
date: 2019-03-21 22:49:58
---

触发下拉事件

采用这个属性解决

- **shouldPullToRefresh**（函数）pullToRefresh要触发哪个条件？ 
  \- 默认为`!window.scrollY`

```javascript
PullToRefresh.init({
    mainElement: '.atmosphere',
    // triggerElement:'.atmosphere', //哪个元素应该触发刷新
    shouldPullToRefresh: function(){
    return !(document.documentElement.scrollTop||document.body.scrollTop)
    },
    onRefresh: function() {  //get请求
    // console.log('加载中。。。')
    alert('加载中。。。')

    }
});
```

