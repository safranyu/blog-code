---
title: 正则表达式获取URL参数
comments: true
categories:
  - JavaScript
tags:
  - JavaScript
  - 正则表达式
abbrlink: a2dbbd02
date: 2019-03-29 23:11:13
---

```javascript
/**
 * 获取所有参数转化为数组
 */
function parseQuery(url) {
  let queryObj={};
  let reg=/[?&]([^=&#]+)=([^&#]*)/g;
  let querys=url.match(reg);
  if(querys){
    for(var i in querys){
      let query=querys[i].split('=');
      let key=query[0].substr(1),
      value=query[1];
      queryObj[key]?queryObj[key]=[].concat(queryObj[key],value):queryObj[key]=value;
    }
  }
  return queryObj;
}

/**
 * 获取某个字符串
 */
function getQueryByName(url,name){
  var reg=new RegExp('[?&]'+name+'=([^&#]+)');
  var query=url.match(reg);
  return query?query[1]:null;
}
```