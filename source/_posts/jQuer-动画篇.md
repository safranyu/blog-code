---
title: jQuer--动画篇
comments: true
categories:
  - jQuer
tags:
  - jQuer
  - jQuer动画
abbrlink: 81a571d4
date: 2018-10-05 22:45:52
---

# jQuery——动画篇（隐藏显示、上卷下拉、淡入淡出、animate、stop、each）

## 隐藏显示

### hide方法

```javascript
$elem.hide()
.hide( options )hide()//就会匹配元素的宽度，高度，以及不透明度，同时进行动画操作
.hide("fast / slow")//代表200和600毫秒的延时动画
<script type="text/javascript">
 //点击buttom2 执行动画隐藏
 $("button:last").click(function() {
     $("#a2").hide({
         duration: 3000,
         complete: function() {
             alert('执行3000ms动画完毕')
         }
     })
 });
</script>
<script type="text/javascript">
//点击buttom1 直接隐藏
$("button:first").click(function() {
    $("#a1").hide()
});
</script>
```

### show方法

```javascript
<script type="text/javascript">
//点击buttom
//执行3秒隐藏
//执行3秒显示
$("button").click(function() {
    $("#a1").hide(3000).show(3000)
});
</script>
```

### 显示与隐藏切换toggle方法

```javascript
<script type="text/javascript">
$("button:first").click(function() {
    $(".left").toggle(3000)
});
 //如果元素是最初显示，它会被隐藏;如果隐藏的，它会显示出来
</script>
```

## 上卷下拉

### 下拉动画slideDown

```javascript
<script type="text/javascript">
//点击buttom
$("button:first").click(function() {
   $("#a1").slideDown(3000)
});
//slideDown([duration],[complete])
//$("ele").slideDown(1000, function() {等待动画执行1秒后,执行别的动作....});
</script>
```

### 上卷动画slideUp

```javascript
$("elem").slideUp();
slideUp([duration],[easing],[complete])
<script type="text/javascript">
$("button:first").click(function() {
   $("#a1").slideUp(3000)
});

$("button:last").click(function() {
   $("#a2").slideUp(3000,function(){
       alert('动画执行结束')
   })
});
</script>
```

### 上卷下拉切换slideToggle

```javascript
<script type="text/javascript">
$("button").click(function() {
    $("#a1").slideToggle(3000)
});
//slideToggle([duration],[complete])
</script>
```

## 淡入淡出动画

### 淡出动画fadeOut

```javascript
<script type="text/javascript">
.fadeOut([duration],[complete])
    $("p").fadeOut({
        duration: 1000
    });
</script>
```

### 淡入动画fadeIn

```javascript
.fadeIn( [duration ], [ complete ] )
<script type="text/javascript">
    $("p").fadeIn({
        duration: 1000
    });
</script>
```

### 淡入淡出切换fadeToggle

```javascript
<script type="text/javascript">
//fadeToggle切换fadeOut与fadeIn效果，所谓"切换"，即如果元素当前是可见的，则将其隐藏(淡出)；如果元素当前是隐藏的，则使其显示(淡入)。
.fadeToggle(([duration],[complete])
    $("p").fadeIn({
        duration: 1000
    });
</script>
```

### 淡入淡出fadeTo

```javascript
<script type="text/javascript">
//fadeToggle切换fadeOut与fadeIn效果，所谓"切换"，即如果元素当前是可见的，则将其隐藏(淡出)；如果元素当前是隐藏的，则使其显示(淡入)。
.fadeTo( duration, opacity ,callback)
     $("p").fadeTo(1000, 0.9, function() {
         alert('完成')
           });
</script>
```

## toggle与slideToggle以及fadeToggle的比较

```javascript
toggle、sildeToggle以及fadeToggle的区别：
toggle：切换显示与隐藏效果，改变样式display为none
sildeToggle：切换上下拉卷滚效果，设置位置高度为0
fadeToggle：切换淡入淡出效果，设置透明度为0

细节上还是有更多的不同点:
toggle：动态效果为从右至左。横向动作
slideToggle：动态效果从下至上。竖向动作
fadeToggle() 方法在 fadeIn() 和 fadeOut() 方法之间切换。
注释：隐藏的元素不会被完全显示（不再影响页面的布局）12345678910
```

------

## 动画animate

```javascript
$(elem).fadeOut(3000)  
$(elem).animate({   
    opacity:0
},3000)
.animate(properties,[duration],[easing],[complete])
.animate(properties,options)

properties：一个或多个css属性的键值对所构成的Object对象。border、margin、padding、width、height、font、left、top、right、bottom、wordSpacing。background-color很明显不可以，否则正常情况下是不能只用动画效果的。CSS 样式使用 DOM 名称（比如 "fontSize"）来设置。

属性值的单位像素（px）,除非另有说明。em和%需指定使用
.animate({
    left: 50,  
    fontSize: "10em",
}, 500);
.animate({
    width: "toggle"
});
如果提供一个以+= 或 -=开始的值，那么目标值就是以这个属性的当前值加上或者减去给定的数字来计算的
.animate({ 
    left: '+=50px'
}, "slow");

duration时间
动画以毫秒为单位的；'fast'和'slow'字符串，分别表示持续时间为200 和 600毫秒。

easing动画运动的算法
jQuery库中默认调用 swing。如果需要其他的动画算法，请查找相关的插件

complete回调
动画完成时执行的函数，这个可以保证当前动画确定完成后发会触发
```

------

```javascript
.animate( properties, options )

options参数
duration - 设置动画执行的时间
easing - 规定 easing 函数，过渡使用的缓动函数
step：规定每个动画的每一步完成之后要执行的函数
progress：每一次动画调用的时候会执行这个回调，就是一个进度的概念

complete：动画完成回调

$('#elem').animate({
    width: 'toggle',  
    height: 'toggle'
  }, {
    duration: 5000,
    specialEasing: {
      width: 'linear',
      height: 'easeOutBounce'
    },
    complete: function() {
      $(this).after('<div>Animation complete.</div>');
    }
  });
```

------

## 动画stop

```javascript
.stop( [clearQueue ], [ jumpToEnd ] )
.stop( [queue ], [ clearQueue ] ,[ jumpToEnd ] )
.stop(); 停止当前动画，点击在暂停处继续开始
.stop(true); 如果同一元素调用多个动画方法，尚未被执行的动画被放置在元素的效果队列中。这些动画不会开始，直到第一个完成。当调用.stop()的时候，队列中的下一个动画立即开始。
.stop(true,true); 当前动画将停止，但该元素上的 CSS 属性会被立刻修改成动画的目标值
$("#aaron").animate({
    height: 300
}, 5000)
$("#aaron").animate({
    width: 300
}, 5000)
$("#aaron").animate({
    opacity: 0.6
}, 2000)
stop()：只会停止第一个动画，第二个第三个继续
stop(true)：停止第一个、第二个和第三个动画
stop(true ture)：停止动画，直接跳到第一个动画的最终状态 
```

------

## each

```javascript
jQuery.each(array, callback )
jQuery.each( object, callback )
//第一个参数传递的就是一个对象或者数组，第二个是回调函数
<script type="text/javascript">
$("#exec").click(function() {
  var v = $("#animation").val();
  var $aaron = $("#aaron");
  $aaron.empty();
  if (v == "1") {
      // 遍历数组元素
      $.each(['Aaron', '慕课网'], function(i, item) {
          $aaron.append("索引=" + i + "; 元素=" + item);
      });
  } else if (v == "2") {
      // 遍历对象属性
      $.each({
          name: "张三",
          age: 18
      }, function(property, value) {
          $aaron.append("属性名=" + property + "; 属性值=" + value);
      });
  } 
});
</script>
```

------

## 索引inArray

```javascript
jQuery.inArray( value, array ,[ fromIndex ] )
$.inArray(5,[1,2,3,4,5,6,7]) //返回对应的索引：4
<script type="text/javascript">
$("#exec").click(function() {
    var v = $("#animation").val();
    var $aaron = $("#aaron");
       $aaron.empty();
    if (v == "1") {
        var index = $.inArray('Aaron',['test','Aaron', 'array','慕课网']);
        $aaron.text('Aaron的索引是: '+ index)//1
    } 
    else if (v == "2") {
        //指定索引开始的位置
        var index = $.inArray('a',['a','b','c','d','a','c']);
        $aaron.text('a的索引是: '+ index)//0
    } 
});
</script>
```

------

## 去空格神器trim方法

```javascript
//jQuery.trim()函数用于去除字符串两端的空白字符
//trim处理
<input type="text" name="" id="results2" value=" 前后留空 " />
<input id="exec2" type="button" value="点击执行">

$("#exec2").click(function() {
     alert("值的长度：" + $.trim($("#results2").val()).length)
});//412345678
```

------

## DOM元素的获取get方法

```javascript
.get( [index ] )
 $(a).get(1)
<script type="text/javascript">
$("#exec").click(function() 
{
   //get找到第二个a元素，并修改蓝色字体
   $aaron.get(1).style.color = "blue"
   //get找到最后一个a元素，并修改字体颜色
   $aaron.get(-1).style.color = "#8A2BE2"
});
</script>
```

##  

```javascript
.index()
.index( selector )
.index( element )
<ul>
   <a></a>
   <a></a>
   <li id="test1">1</li>
   <li id="test2">2</li>
   <li id="test3">3</li>
</ul>
<ul>
   <li id="test4">4</li>
   <li id="test5">5</li>
   <li id="test6">6</li>
</ul>
<script type="text/javascript">
$("#exec").click(function() 
{
    var v = $("#animation").val();
    var $span = $("span");
    $span.empty();
    if (v == "1") {
        //找到第一个li的同辈节点中的索引位置
        $span.text($("li").index())//2
        //通过传递dom查找      $span.text($("li").index(d$("#test5")))//4
    } else if (v == "3") {
        //通过传递jQuery对象查找
                 $span.text($("li").index($("#test6")))//5
    }
});
</script>
```