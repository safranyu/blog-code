---
title: 小程序wxml页面进行数据替换
comments: true
categories:
  - 小程序
tags:
  - 小程序
abbrlink: fc17f2c8
date: 2019-04-01 23:39:12
---

参考1.[微信小程序WXML页面上直接进行字符串截取实现方式](https://blog.csdn.net/cangahi09025566/article/details/82589831)

参考2.[wxs replace 正则用法该怎么用？？？？](https://www.aiyingli.com/51529.html)

### 代码

```html
//顶部引用
<!-- 引入wxs脚本 -->
<wxs src="./subutil.wxs" module="tools" />
<view class='nameSite'>{{tools.subs(addressModel.address_city)}} </view>
```

wxs脚本文件

```js
var sub = function (val) {
  if (val.length == 0 || val == undefined) {
    return;
  } else {
    var reg = getRegExp("(\|)", "g");
    console.log(reg);
    return val.replace(reg, ' ');
  }
 
}

module.exports.sub = sub;
```

