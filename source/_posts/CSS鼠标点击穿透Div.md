---
title: CSS鼠标点击穿透Div
comments: true
categories:
  - CSS
tags:
  - CSS技巧
abbrlink: cd5ef747
date: 2018-10-05 22:31:54
---

有些时候网页中用到了一些绝对定位的Div，因为需要事先这个Div是隐藏的，但是它所在的位置会遮挡住鼠标点击事件。这个时候可以用CCS3中的pointer-events属性来解决。

---

### 穿透该层

`pointer-events:none;`



### 恢复点击处理

`pointer-events:auto;`

根据情况来动态修改Div的pointer-events属性即可。



### 例如用JQuery可以这样写：

穿透该层

`$('#dvTest').css('pointer-events', 'none'); `

或者

恢复点击处理

`$('#dvTest').css('pointer-events', 'auto'); `