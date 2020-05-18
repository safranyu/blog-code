---
title: axios+mockjs在vue中使用
comments: true
categories:
  - Vue
tags:
  - mockjs
  - vue
  - axios
abbrlink: 2df016a3
date: 2019-03-30 23:29:15
---

[mockjs官网](<http://mockjs.com/>)

[参考文档](https://juejin.im/post/5b17ffcc51882513eb62e985)

#### 1、npm安装mockjs

```shell
npm intsall mockjs --save-dev
```

#### ２、在src目录下建立文件夹mock，mock文件夹下建立mock.js文件，js文件代码如下：

```javascript
import Mock from 'mockjs';//es6语法引入mock模块

export default Mock.mock('http://test.cn/buyRecord', {//输出数据
  'name': '@name',//随机生成姓名
  'age|1-10': 10
  //还可以自定义其他数据
});
```

#### 3、在vue组件中使用

```
import data from '../../assets/js/api/mock/mock.js'
```

#### 4、演示请求接口

```javascript
created() {
    this.$http.get('http://test.cn/buyRecord')
    .then(res => {
        console.log(res.data);
        this.msg = res.data.name;
        console.log(this.msg)
    })
}
```

### 二.安装和使用axios 

这里我把mockjs封装到一起，可以前往[axios封装](<https://safranyu.github.io/post/9bbb323.html>)。目录结构：

#### 1、在api目录下建立文件夹mock，mock文件夹下建立mock.js

```javascript
import Mock from 'mockjs'

export default Mock.mock('http://test.cn/buyRecord', {
  'name': '@name',
  'age|1-10': 10
})
```

#### 2、在mock文件在新建mockUrl.js用来存放请求的url

```javascript
/**
 * mock 模拟数据
 */
let baseUrl = 'http://test.cn'
export default {
  // 首页轮播图
  getBuyRecord: baseUrl + '/buyRecord',
}
```

#### 3、在当前文件新建index.js配置请求方法

```javascript
import api from '../index'
import urls from './mockUrl'

const header = {}

export default {
  getBuyRecord(params) {
    return api.get(urls.getBuyRecord, params, header)
  }
}
```

#### 4、在api目录下apiList.js引入刚配置的请求方法

```javascript
import matches from './matches'
import Mock from './mock'

export default {
  matches,
  Mock
}
```

#### 5、页面引用

```javascript
import '../../assets/js/api/mock/mock.js'
export default {
	methods: {
        async getBuyRecord() {
          try {
            let params = {}
            let res = await this.$api.Mock.getBuyRecord(params)
            console.log(res)
          } catch(err) {
            console.log(err)
          }
        }
	}
    created() {
       this.getBuyRecord()   
    }
}
```

