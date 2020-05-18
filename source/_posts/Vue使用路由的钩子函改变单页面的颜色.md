---
title: Vue使用路由的钩子函改变单页面的颜色
comments: true
categories:
  - Vue
tags:
  - vue
abbrlink: 276258a
date: 2019-03-31 21:47:25
---

[导航守卫](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <link href="http://cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet" />
</head>
<body>
    <div id="app"></div>

    <template id="main">
        <div id="app">
            <ul>
                <li><router-link to="/">Home</router-link></li>
                <li><router-link to="/1">Page1</router-link></li>
                <li><router-link to="/2">Page2</router-link></li>
            </ul>
            <router-view></router-view>
        </div>
    </template>

    <script src="http://cdn.bootcss.com/vue/2.3.2/vue.min.js"></script>
    <script src="http://cdn.bootcss.com/vue-router/2.5.3/vue-router.min.js"></script>

    <script>
        const Home = { template: '<div>Home</div>' }

        const Page1 = {
            template: '<div>Page1</div>',
            beforeRouteEnter(to, from, next) {
                window.document.body.style.backgroundColor = 'red';
                next();
            },
            beforeRouteLeave(to, from, next) {
                window.document.body.style.backgroundColor = '';
                next();
            }
        }

        const Page2 = {
            template: '<div>Page2</div>',
            beforeRouteEnter(to, from, next) {
                window.document.body.style.backgroundColor = 'blue';
                next();
            },
            beforeRouteLeave(to, from, next) {
                window.document.body.style.backgroundColor = '';
                next();
            }
        }

        const router = new VueRouter({
            routes: [
              { path: '/', component: Home },
              { path: '/1', component: Page1 },
              { path: '/2', component: Page2 }
            ]
        })

        new Vue({
            router,
            template: '#main'
        }).$mount('#app')
    </script>
</body>
</html>
```

在`main.js`添加

```javascript
router.beforeEach((to, form, next) => {
  // 这里使用全局守卫
  if (to.matched[0].name == "login") {
    window.document.body.style.backgroundColor = 'white'
    next();
  } else {
    window.document.body.style.backgroundColor = ''
    next();
  }
})
```

使用组件内的守卫

```javascript
export default {
  beforeCreate: function() { // 单独更改页面的背景
    document.body.style.backgroundColor = '#fff'
  },
  beforeDestroy: function() { // 删除添加的背景
    document.body.removeAttribute("style","backgroundColor")
  },
}
```

