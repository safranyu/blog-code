---
title: vue-cli3下的Axios封装
categories:
  - Vue
tags:
  - Vue
  - Axios
  - vue-cli3
abbrlink: 9bbb323
date: 2019-03-23 23:25:07
---
## axios 简介

首先要明白的是axios是什么：axios是基于promise（诺言）用于浏览器和node.js是http客户端。

axios的作用是什么：axios主要是用于向后台发起请求的，还有在请求中做更多是可控功能。

- 从浏览器中创建 XMLHttpRequest
- 从 node.js 发出 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防止 CSRF/XSRF

### 项目配置

##### 首先当然还是要安装啦：

```shell
npm install axios
```

之后我们新建一个api文件夹用来放接口和axios的配置。
先给大家看看我配置好之后的文件夹目录结构：

![](http://pan.vmccc.cn/?/images/2019/03/23/YbxfrFGHXM/hexoVue.png)

可以说这次配置是我划分的比较详细的配置方法了，具体每个文件都分别做什么用，我们现在来看看吧。

##### axios.js

这个文件主要创建axios实例并对拦截器进行配置，不理解拦截器的同学可以看看下图：

```javascript
import axios from 'axios'

// 创建 axios 实例
let service = axios.create({
  // headers: {'Content-Type': 'application/json'},
  timeout: 60000
})

// 设置 post、put 默认 Content-Type
service.defaults.headers.post['Content-Type'] = 'application/json'
service.defaults.headers.put['Content-Type'] = 'application/json'

// 添加请求拦截器
service.interceptors.request.use(
  (config) => {
    if (config.method === 'post' || config.method === 'put') {
      // post、put 提交时，将对象转换为string, 为处理Java后台解析问题
      config.data = JSON.stringify(config.data)
    }
    // 请求发送前进行处理
    return config
  },
  (error) => {
    // 请求错误处理
    return Promise.reject(error)
  }
)

// 添加响应拦截器
service.interceptors.response.use(
  (response) => {
    let { data } = response
    return data
  },
  (error) => {
    let info = {},
      { status, statusText, data } = error.response

    if (!error.response) {
      info = {
        code: 5000,
        msg: 'Network Error'
      }
    } else {
      // 此处整理错误信息格式
      info = {
        code: status,
        data: data,
        msg: statusText
      }
    }
  }
)

/**
 * 创建统一封装过的 axios 实例
 * @return {AxiosInstance}
 */
export default function() {
  return service
}
```

##### index.js

index.js文件主要封装我们几个常用的方法，get、post、put、delete

```javascript
import axios from './axios'

let instance = axios()

export default {
  get(url, params, headers) {
    let options = {}

    if (params) {
      options.params = params
    }
    if (headers) {
      options.headers = headers
    }
    return instance.get(url, options)
  },
  post(url, params, headers, data) {
    let options = {}

    if (params) {
      options.params = params
    }
    if (headers) {
      options.headers = headers
    }
    return instance.post(url, data, options)
  },
  put(url, params, headers) {
    let options = {}

    if (headers) {
      options.headers = headers
    }
    return instance.put(url, params, options)
  },
  delete(url, params, headers) {
    let options = {}

    if (params) {
      options.params = params
    }
    if (headers) {
      options.headers = headers
    }
    return instance.delete(url, options)
  }
}
```

##### install.js

install.js文件可以把我们所有的api接口安装到全局，之后我们在main.js文件中导入就可以了。

```javascript
import apiList from './apiList'

const install = function(Vue) {
  if (install.installed) {
    return

  install.installed = true
  Object.defineProperties(Vue.prototype, {
    $api: {
      get() {
        return apiList
      }
    }
  })
}

export default {
  install
}
```

**main.js中添加：**

```javascript
import api from './api/install'
Vue.use(api)
```

##### apiList.js

把我们所有的api文件夹导入到这一个文件中来。

```javascript
import matches from './matches'
import user from './user'

export default {
  matches,
  user
}
```

##### baseUrl.js

根据不同的环境设定不同的baseUrl，在配置这个文件前，我们先需要做如下几件事：
1.根目录新建`.env.dev`文件并在文件内写入`NODE_ENV = 'dev'`
2.在`package.json`文件内添加：

```javascript
 "build:dev": "vue-cli-service build --mode dev",
 "build:pre": "vue-cli-service build --mode pre",
```

以下是baseUrl.js的代码：

```javascript
let baseUrl = '/api' // 本地代理

switch (process.env.NODE_ENV) {
  case 'dev':
    baseUrl = 'http://testserver.feleti.cn/' // 测试环境url
    break
  case 'pre':
    baseUrl = 'https://pre-server.feleti.cn' // 预上线环境url
    break
  case 'production':
    baseUrl = 'https://api.feleti.cn' // 生产环境url
    break
}

export default baseUrl
```

##### matches、user

这两个文件夹都是根据api类型进行区分的，在项目以后也建议大家根据api类型划分出不同的文件存放，在小项目中这样做可能显得很麻烦，但如果项目比较大，这样做的优势就体现出来了。

我们就只看看matches文件夹下的内容：

###### urls.js

把一个类型下的所有url接口放入这一个文件，我只放了一个暂时，可以继续添加。

```javascript
import baseUrl from '../baseUrl'
export default {
  matches: baseUrl + '/matches'
}
```

###### index.js

有些接口需要在header中添加token或是其他，可以按如下配置。

```javascript
import api from '../index'
import urls from './urls'

const header = {}

export default {
  matches(params) {
    // return出去了一个promise
    return api.get(urls.matches, params, header)
  }
}
```

配置完上述全部文件就算是大功告成了，下面我们看看如何使用吧。

### 组件中调用

```javascript
created() {
    this.matches()
  },
  methods: {
    async matches() {
      // 这里用try catch包裹，请求失败的时候就执行catch里的
      try {
        //定义参数对象
        let params = {
          type: 'zc'
        }
        let res = await this.$api.matches.matches(params)

        console.log('getMatches -> res', res)
      } catch (e) {
        console.log('catch -> e', e)
      }
    }
  }
```

之后我们就可以在控制台看到我们调用成功的输出日志啦：



### 小结

在实际工作中，我们尽量要把项目做的细致一些，尤其是项目开始之前的配置，今天所涉及到的很多文件在之后的配置中还会有进步的更改，比如配置用户相关的接口、配置全局loading等，大家只要能把今天的内容完全理解，之后再配置这里就很容易啦。

