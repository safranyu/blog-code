---
title: hexo添加Gitalik评论
comments: true
categories:
  - jQuer
  - JS插件
tags:
  - JS插件
  - JavaScript
abbrlink: 59c352fb
date: 2018-10-08 21:21:57
---

我使用的是hexo模板是Yilia的，会有些不同。

[参考文档](https://knightcai.github.io/2017/12/19/%E4%B8%BA%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0-Gitalk-%E8%AF%84%E8%AE%BA%E6%8F%92%E4%BB%B6/)

1、在模板文件里创建一个`gitalk.ejs`文件，把下面的代码复制进去

```javascript
<link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
<div id="gitalk-container"></div>
<script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
<script type="text/javascript">
    var gitalk = new Gitalk({
        clientID: '<%= theme.gitalk.clientID %>',
        clientSecret: '<%= theme.gitalk.clientSecret %>',
        id: window.location.pathname,
        repo: '<%= theme.gitalk.repo %>',
        owner: '<%= theme.gitalk.owner %>',
        admin: '<%= theme.gitalk.admin %>',
        distractionFreeMode: '<%= theme.gitalk.shade %>',
        enableHotKey: '<%= theme.gitalk.enableHotKey %>',
       
    })
    gitalk.render('gitalk-container')
</script>
```

2、在文章页面添加这个模板，一般是在这个路径下`layout\_partial\article.ejs`

```javascript
<% if (theme.gitalk.enable){ %>
    <%- partial('_partial/post/gitalk') %>
  <% } %>
```

3、在模板的配置文件里添加

```javascript
#gitalk settings
gitalk:
  enable: true #用来做启用判断可以不用
  owner: 'Github 用户名'
  repo: 'Github 仓库名' #例：safranyu.github.io
  admin: 'Github 用户名'
  clientID: 'Github Application clientID'
  clientSecret: 'Github Application clientSecret'
  shade: true # 遮罩
  enableHotKey: true #启用热键（cmd | ctrl + enter）提交评论
```

4、Gitalk 需要一个 **Github Application**

[申请页面](https://github.com/settings/applications/new)

填写下面参数：

![](https://ws1.sinaimg.cn/large/006tKfTcgy1fmm7jaib6fj30jo0gaacs.jpg)

会得到`Client ID`和`Client Secret`在配置文件里填好就行。

我遇到报`Error: Bad credentials`错误，通过加单引号解决了