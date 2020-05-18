---
title: 关于PC端缩小浏览器窗口，右边背景空白并出现滚动条
comments: true
categories:
  - CSS
tags:
  - CSS
abbrlink: 488e492e
date: 2018-11-15 22:23:30
---

出现原因

因为出现空白的元素设置了宽度100%，缩小窗口相当于减小了宽度值，那么为什么出现滚动条呢？是因为页面中至少有一个元素a的width大于窗口的width，导致把页面撑开，出现了滚动条，而此时那个width：100%的元素宽度等于窗口宽度且小于元素a的宽度，所以右侧的空白长度=a的宽度-窗口宽度。  



### 解决这个问题其实很简单

- 给body设置最小宽度`min-width`,在ie6下不兼容

  ```css
  body{
       min-width: 1000px;
       overflow-x: hidden;
  }
  ```

- 还可以给div元素设置最小宽度，如果页面元素复杂，要一个个设置

- 给CSS样式设置`width:expression(document.body.clientWidth <= 960? "960px": "auto");`

  ```css
  #wrap {
      width:100%;
      background:#ddd;
      width:expression(document.body.clientWidth <= 960? "960px": "auto");
      min-width:960px;
  }
  ```

  推荐第一种