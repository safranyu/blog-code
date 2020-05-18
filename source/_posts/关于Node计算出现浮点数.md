---
title: 关于Node计算出现浮点数
comments: true
categories:
  - Node
tags:
  - Node
abbrlink: adu7e5ef
date: 2020-02-16 19:02:06
---

在金额展示的时候出这个问题

原因：
```
1.09*100 = 109.00000000000001
```

解决办法
```javascript
handleToFixed(origin, n = 0) {
  const scale = Math.pow(10, n);
  const r = origin * scale * 10;
  return Number((Math.round(Math.round(r) / 10) / scale).toFixed(n));
}
```