---
title: Github搭建Hexo博客
comments: true
categories:
  - Blog
tags:
  - Blog
  - Github
abbrlink: 9a98d601
date: 2018-10-02 18:02:25
---

# Github 搭建Hexo博客

利用Github page搭建一个人博客，在没有特殊需求，又想快速拥有一个个人博客，hexo是个不错的选择，搭建简单，无需另外购买服务器空间和域名，只需要有个Github账号即可。搭建简单，能够坚持维护和写文章难。。。

----

## 环境准备

1.安装Node.js

Hexo是基于nodeJS环境的静态博客

前往[Node官网](https://nodejs.org/)下载最新版本,一路安装即可。

查看是否安装好了，打开cdm 运行` node -V`查看版本号 

2.安装Git

[官网下载](https://git-scm.com/downloads/)

右键打Git Bash查看版本 `git version`

3.Sublime

随便一款文本编辑器，这里我用[Sublime](http://www.sublimetext.com/3)。支持各种编程语言和文件格式，当然也支持Markdown语法 。

## 安装步骤

1.安装Hexo

+ 先创建一个文件夹（用来存放所有blog的东西）然后`cd`到该文件夹下

+ 安装hexo命令：`npm i +g hexo`

+ 安装完后查看版本

  ![](http://pan.vmccc.cn/images/2018/10/02/8jDSlPigzd/githexo.jpg)

+ 初始化命令：`hexo init` ，初始化完成之后打开所在的文件夹可以看到以下文件：

![](http://pan.vmccc.cn/images/2018/10/03/FWonyhHnxo/git-dir.jpg)

+ 解释一下：

  + node_modules：是依赖包
  + public：存放的是生成的页面
  + scaffolds：命令生成文章等的模板
  + source：用命令创建的各种文章
  + themes：主题
  + _config.yml：整个博客的配置
  + db.json：source解析所得到的
  + package.json：项目所需模块项目的配置信息

+ 做好这些前置工作之后接下来的就是各种配配配置了。

### Github注册与配置

1.注册
访问：[GitHub](https://luuman.github.io/2015/12/27/Hexo/GitHubHexo/0)，注册你的username和邮箱，邮箱十分重要，GitHub上很多通知都是通过邮箱的。注册过程比较简单。

2.配置和使用Github

+ 创建一个repo，名称为`safranyu.github.io`, 其中safranyu是你的github名称，按照这个规则创建才有用哦，如下：(由于我已经提前创建好了，所以提示这个库已经存在)

![](http://pan.vmccc.cn/images/2018/10/03/59D6ETwVgq/git-user.jpg)

+ 回到gitbash中，配置github账户信息（YourName和YourEail都替换成你自己的）：

![](http://pan.vmccc.cn/images/2018/10/03/FYeGRdAdw7/githubUser.jpg)

+ 创建SSH
  在gitbash中输入：`ssh-keygen -t rsa -C "youremail@example.com`，生成ssh。然后按下图的方式找到`id_rsa.pub`文件的内容。

![](http://pan.vmccc.cn/images/2018/10/03/hy3IQ1Z73j/gitssh.jpg)

+ 将上面获取的ssh放到github中：

  ![](http://pan.vmccc.cn/images/2018/10/03/FueQEPx6Lf/settings.jpg)

  ![](http://pan.vmccc.cn/images/2018/10/03/FcbkdhRQul/gitsshkey.jpg)


添加一个 `New SSH key` ，title随便取，key就填刚刚那一段。

* 在gitbash中验证是否添加成功：`ssh +T git@github.com`

* 完成下一步你就成功啦！

3.配置

* 用编辑器打开你的blog项目，修改`_config.yml`文件的一些配置(冒号之后都是有一个半角空格的)：

  ```javascript
  deploy:
    type: git
    repo: https://github.com/YourgithubName/YourgithubName.github.io.git
    branch: master
  ```

* 回到gitbash中，进入你的blog目录，分别执行以下命令：

  ```javascript
  hexo clean
  hexo generate
  hexo server
  ```

* 打开浏览器输入：`http://localhost:4000`

+ 命令解释：

	+ 清除public，当 source 文件夹中的部分资源更改过之后，特别是对文件进行了删除或者路径的改变之后，需要执行这个命令，然后重新编译。
	+ 编译，一般部署上去的时候都需要编译一下，编译后，会出现一个 public 文件夹，将所有的md文件编译成html文件
	+ 开启本地服务

4.上传到github

+ 执行命令(建议每次都按照如下步骤部署,可简写)：

```javascript
hexo clean
hexo generate
hexo deploy
//简写
//hexo c
//hexo g
//hexo d
```

* 在浏览器中输入`http://safranyu.github.io`就可以看到你的个人博客啦，是不是很兴奋！
+ 感觉GitBash中东西太多的时候输入`clear`命令清空

5.绑定个人域名

- 不想绑定的自行忽略

- 第一步购买域名：随便在哪个网站买一个就好了。

- 第二步添加CNAME：添加记录，添加你的域名或者二级域名，比如我添加的是二级域名`blog`，记录值里填你Github里的域名,比如`safranyu.github.io`，
   ![](http://pan.vmccc.cn/images/2018/10/05/MVFBcdDSgc/blog-cname.jpg)

- 填写完后回到Github进入里的Blog库，设置里添加你的域名保存即可

   ![](http://pan.vmccc.cn/images/2018/10/05/jfma6xvxOz/blog-yuming.jpg)

## Hexo博客配置

### 新建博文

在Git Bash输入：

```
hexo new "新博文的名字"
```

即可在 Hexo\source_posts 目录中找到”新博文的名字.md”这个文件。你就可以使用maekdown编辑器打开进行编写博客内容了。

> hexo new [layout] “postName” #新建文章

其中layout是可选参数，默认值为post。有哪些layout呢，请到scaffolds目录下查看，这些文件名称就是layout名称。当然你可以添加自己的layout，方法就是添加一个文件即可，同时你也可以编辑现有的layout，比如post的layout默认是hexo\scaffolds\post.md

### 预览和发表

```
hexo clean
hexo g
hexo s
hexo d
```

### 安装主题

你可以在[Themes·Hexo](https://github.com/hexojs/hexo/wiki/Themes)或者[hexo主题](https://hexo.io/themes/)上选择你喜欢的主题，我使用的SPFK主题

#### 安装SPFK主题

- 安装
```shell
git clone https://github.com/luuman/hexo-theme-spfk.git themes/spfk
```

- 更新
```
cd themes/spfk
git pull
```

- 配置

  主题配置文件在主目录下的`_config.yml`：[_config.yml](http://luuman.github.io/2015/12/21/GitHub+Hexo/)

  相关插件的安装：请参照[Hexo插件安装](http://localhost:4000/2015/12/27/Hexo-plug/)

```
### Header
D:\blog\themes\spfk\_config.yml
menu:
  主页: /
  所有文章: /archives
  # 随笔: /tags/随笔
    #是否开启多说评论，填写你在多说申请的项目名称 duoshuo: duoshuo-key（http://duoshuo-key.duoshuo.com/）
    #若使用disqus，请在博客config文件中填写disqus_shortname，并关闭多说评论
    duoshuo: true
网页侧边栏背景:
# Background | 背景
## "background_sum": show images form /source/background/的图片数目background_sum: 24
## "on: true": 自动随机显示这5张图片
## "on: false": 自定义显示图片设置，background_image: 109
background:
  on: true
  #on: false
  background_sum: 24
  background_image: 109
```

- 多说评论

```
duoshuo: 
  on: true
  domain: luuman
  # 是否开启多说评论，http://duoshuo.com/create-site/
  # 使用上面网址登陆你的多说，然后创建站点，在 domain 中填入你设定的域名前半部分
  # http://<要填的部分>.duoshuo.com (domain只填上<>里的内容，不要填整个网址)
J:\Hexo\Hexo\themes\spfk\source\css\多说.css
```

添加方法：打开「后台」 > 「多说评论」 > 「设置」 > 「基本设置」 > 然后把样式粘贴到「自定义CSS」文本框 > 「保存」

具体样式请参照：[多说.css](https://github.com/luuman/luuman.github.io/blob/master/resoures/%E5%A4%9A%E8%AF%B4.css)

- 头像

```shell
# 头像尺寸大概200*200px
D:\blog\themes\spfk\source\img\head.jpg

```

- icon 图标

```shell
替换路径: /spfk/source/apple-touch-icon.png
D:\blog\themes\spfk\source\img\favicon.png

```

- 背景

```shell
# Background | 背景
# "background_sum": show images form /source/background/的图片数目
# "on: true": 自动随机显示这5张图片
# "on: false": 自定义显示图片设置 background_image: 5
background:
  on: true
  #on: false
  background_sum: 24
  background_image: 109
```

- 文章摘要

```shell
title: 前端知识体系
date: 2018-10-07 22:08:02
description: 
categories:
- HTML 书籍
- HTML 书籍
tags:
- HTML 标签 
- HTML 标签
toc: true 文章目录
author:
comments:
original:
permalink: 
---
　　** 前端知识体系：**<Excerpt in index | 首页摘要> 
+ <!-- more -->
<The rest of contents | 余下全文>
```

- 404 Page:
```shell
hexo new page 404
#And then set permalink: /404 in /source/404/index.md front matter.
#在 Hexo 中创建匹配主题的404页面
```

### 主题结构

```
.
├── languages            #多语言
|   ├── default.yml      #默认语言
|   └── zh-CN.yml        #中文语言
├── layout               #布局，根目录下的*.ejs文件是对主页，分页，存档等的控制
|   ├── _partial         #局部的布局，此目录下的*.ejs是对头尾等局部的控制
|   └── _widget          #小挂件的布局，页面下方小挂件的控制
├── source               #源码
|   ├── css              #css源码 
|   |   ├── _base        #*.styl基础css
|   |   ├── _partial     #*.styl局部css
|   |   ├── fonts        #字体
|   |   ├── images       #图片
|   |   └── style.styl   #*.styl引入需要的css源码
|   ├── fancybox         #fancybox效果源码
|   └── js               #javascript源代码
├── _config.yml          #主题配置文件
└── README.md            #用GitHub的都知道
```

### 参考资料

[hexo官方文档](https://hexo.io/zh-cn/docs/)

[luuman](https://github.com/luuman)

[hexo从零开始到搭建完整](https://www.cnblogs.com/visugar/p/6821777.html)

[Cherryblog](https://cherryblog.site/Use-Gitpagehexo-to-develop-their-own-blog.html)



