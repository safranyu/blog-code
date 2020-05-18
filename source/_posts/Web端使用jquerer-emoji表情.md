---
title: Web端使用jquerer_emoji表情
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

[参考emoji_jquery](https://github.com/eshengsky/jQuery-emoji)

在使用这个插件的时候解析过程比较困扰，在`<textarea>`文本框的情况下无法解析他的值，因此找到手动解析的方法。

### 安装install

```shell
$ npm install --save jQuery-emoji
```

### 页面引用

- 首先在页面上引用css文件和js文件，css文件一般在`<head>`中添加，js文件一般在`</body>`之前添加。注意要先引用jquery和jquery.mCustomScrollbar，再引用该js。

```html
<head>
    <!--the css for jquery.mCustomScrollbar-->
    <link rel="stylesheet" href="lib/css/jquery.mCustomScrollbar.min.css"/>
    <!--the css for this plugin-->
    <link rel="stylesheet" href="css/jquery.emoji.css"/>
</head>

<body>   
    <script src="http://cdn.bootcss.com/jquery/1.11.3/jquery.js"></script>
	<!--(Optional) the js for jquery.mCustomScrollbar's addon-->
	<script src="lib/script/jquery.mousewheel-3.0.6.min.js"></script>
	<!--the js for jquery.mCustomScrollbar-->
	<script src="lib/script/jquery.mCustomScrollbar.min.js"></script>
	<!--the js for this plugin-->
	<script src="js/jquery.emoji.js"></script>
</body>
```

### 调用

- 在文本框或可编辑div上初始化emoji

```javascript
$("#content").emoji(options);
```

[options参数和方法](http://eshengsky.github.io/jQuery-emoji/)

### 使用

##### Html部分

```html
<div ic="content"></div>
<textarea id="message" placeholder="请在此输入文本或上传图片"></textarea>
<input type="button" id="btn">
```

##### Js部分

```javascript
//给元素绑定表情 option里参数参照上面官方
$("#message").emoji({
        button:"#face",
        showTab: true,
        animation: 'fade',
        icons: [{
            name: "贴吧表情",
            path: "lib/eshengsky-jQuery-emoji/dist/img/tieba/",
            maxNum: 50,
            file: ".jpg",
            placeholder: "[emoji_{alias}]",

        }, {
            name: "QQ高清",
            path: "lib/eshengsky-jQuery-emoji/dist/img/qq/",
            maxNum: 91,
            excludeNums: [41, 45, 54],
            file: ".gif",
            placeholder: "[qq_{alias}]"
        }, {
            name: "emoji高清",
            path: "lib/eshengsky-jQuery-emoji/dist/img/emoji/",
            maxNum: 84,
            file: ".png",
            placeholder: "[em_{alias}]"
        }]
    });
// 解析方法
$('#btn').click(funtion(){
	var contents = $('#message').val();
	contents = replace_em(contents);
	onsole.log(contents)；
    $('#content').html(contents);
})

// 手动解析规则
function replace_em(str){
        str = str.replace(/\</g,'&lt;');
        str = str.replace(/\>/g,'&gt;');
        str = str.replace(/\n/g,'<br/>');
        str = str.replace(/\[qq_([0-9]*)\]/g,"<img src='lib/eshengsky-jQuery-emoji/dist/img/qq/$1.gif' />");
        str = str.replace(/\[em_([0-9]*)\]/g,"<img src='lib/eshengsky-jQuery-emoji/dist/img/emoji/$1.png'  />");
        str = str.replace(/\[emoji_([0-9]*)\]/g,"<img src='lib/eshengsky-jQuery-emoji/dist/img/tieba/$1.jpg' />");
        return str;
    }
```

官方转换方法有点复杂，转换不了`<textarea>`输入的值，可能要修改官方的解析方法。

[延伸插件](https://github.com/li914/emoji_jQuery)