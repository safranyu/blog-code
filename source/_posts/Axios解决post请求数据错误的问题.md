---
title: Axios解决post请求数据错误的问题
comments: true
categories:
  - Vue
tags:
  - Vue
  - Axios
abbrlink: e4ed1a3d
date: 2019-03-24 21:05:15
---

在请求的过程中使用的json数据提交给后台，导致一直请求不到数据，最后请求设置为fromdata请求成功。

先在文档引入`import qs from 'qs'`在axios.js配置文件里加上

```javascript
// 添加请求拦截器

service.interceptors.request.use(

  (config) => {

    if (config.method === 'post' || config.method === 'put') {

      config.data = qs.stringify(config.data) //转换为表单模式

      config.headers['Content-Type'] = 'application/x-www-form-urlencoded'

    }

    // 请求发送前进行处理

    return config

  },

  (error) => {

   // 请求错误处理

   return Promise.reject(error)

  }

)

```

