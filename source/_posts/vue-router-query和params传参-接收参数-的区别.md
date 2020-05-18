---
title: vue-router query和params传参(接收参数) 的区别
comments: true
categories:
  - JavaScript
  - Vue
tags:
  - vue
  - vue-router
abbrlink: '36597039'
date: 2019-03-30 23:18:16
---

#### **1、query方式传参和接收参数**

```javascript
传参: 
this.$router.push({
        path:'/xxx',
        query:{
          id:id
        }
      })
  
接收参数:
this.$route.query.id
```

注意:传参是this.$router,接收参数是this.$route,这里千万要看清了！！！

**this.$router 和this.$route有何区别？**

在控制台打印两者可以很明显的看出两者的一些区别：

![](https://segmentfault.com/img/bVbbI7f?w=652&h=425)

- 1.$router为VueRouter实例，想要导航到不同URL，则使用$router.push方法
- 2.$route为当前router跳转对象，里面可以获取name、path、query、params等

#### **2、params方式传参和接收参数**

```javascript
传参: 
this.$router.push({
        name:'xxx',
        params:{
          id:id
        }
      })
  
接收参数:
this.$route.params.id
```

注意:params传参，push里面只能是 name:'xxxx',不能是path:'/xxx',因为params只能用name来引入路由，如果这里写成了path，接收参数页面会是undefined！！！

转载 https://segmentfault.com/a/1190000012735168