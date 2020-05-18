---
title: bootstrap导航缩小折叠问题
comments: true
categories:
  - CSS
tags:
  - Bootstrap
  - CSS
abbrlink: 2665f262
date: 2019-03-19 22:57:27
---

## 示例代码
```javascript
 <nav class="navbar navbar-inverse navbar-fixed-top mr-nav ">
        <div class="container">
            <div id="navbar" class="collapse navbar-collapse">
                <ul class="nav navbar-nav">
                    <li class="active"><a href="#">首页</a></li>
                    <li><a href="#about">关于我们</a></li>
                    <li><a href="product.html">产品介绍</a></li>
                    <li><a href="joinus.html">加入我们</a></li>
                    <li><a href="series.html">联系我们</a></li>
                </ul>
            </div>
        </div>
    </nav>
```

## css解决办法
```javascript
/*解决bootstarp导航缩小折叠问题*/
@media (max-width: 768px){
    .navbar-nav {
        visibility: visible;
        width: 1000px;
        margin: 0;
    }
}
.navbar-collapse{
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
    visibility: visible !important;
}
.nav>li{
    float: left;
}
#navbar{
    border: none;
}
```