title: "移动H5页面开发系列——part3:移动H5页面换场动画的实现原理"
date: 2015-10-23 09:09:09
tags: "html5"
---
在之前的文章中，我们了解了H5移动页面的主要特点，适用场景和设计技巧，也欣赏、学习了一些经典的H5移动页面案例，本文将重点分析下H5移动页面的换场动画的实现原理和技巧。
![genie.github.io](/assets/57.png)
<!--more--> 

## 换场动画的原理
在分析页面换场动画之前，我们先来讨论下HTML5移动页面的基本结构：
```html
<section class="container">
    <article class="page page-A"></article>
    <article class="page page-B"></article>
    <article class="page page-C"></article>
    <article class="page page-D"></article>
    <article class="page page-E"></article>
</section>
```

每个page是一个页面，这些页面由一个父元素container进行包裹。现在我们要设计page是上下滑动，首先得保证各个page在同一垂直线上吧。按照HTML的流式布局规则，默认即可。我们默认每个page都是占满整个屏幕的，因此有以下基础样式。
```css
html, body{margin:0;padding:0;width:100%;height:100%;position:releative;}
.page{width:100%;height:100%;}
```

## 换场动画的几种常见方式

### 容器整体滑动

首先，我们可以将滚动放在container上，每次向上滑动屏幕或者向下滑动屏幕是，将 container 滚动一个屏幕的高度。即改变container的`translateY` 的值。当然也可以改变 container 的 margin 值实现同样的效果，出于性能问题，这里不采用这种方式。

![genie.github.io](/assets/70.png)

```js
var index=0;
$('body').on('click', function(){
    index++;
    if(index==5) index=0;
    $('.container').css({
        transform: 'translateY(-'+ index*20 +'%)'
    })
})
```

实际效果，请查看案例演示（鼠标点击进行翻页操作）
<iframe src="http://sandbox.runjs.cn/show/fvsfab47" width="320" height="480" ></iframe>

### 单个页面滑动
之前我们把滚动放在container上，现在将会移动关注点放到page上。现在page采用绝对定位，而将container采用相对定位，作为page页面进行偏移的参考。
主要是将要呈现的页面的一半先覆盖在目前页面上并设置opacity为0，然后使用transition动画，改变opacity及translateX为0。
![genie.github.io](/assets/71.png)

```js
var index=1;
$('body').on('click', function(){
    index++;
    if(index==6) index=1;
    $('.page-'+index)
        .removeClass('hide')
        .css({
            opacity: 0,
            transform: 'translateY(50%)'
        }).animate({
            opacity: 1,
            transform: 'translateY(0%)' 
        }, 700, 'linear', function(){
            $('.page-'+(index-1)).addClass('hide')
        })    
})
```
实际效果，请查看案例演示（鼠标点击进行翻页操作）
<iframe src="http://sandbox.runjs.cn/show/gzeykuhr" width="320" height="480" ></iframe>

### 双页联动滑动
这种将会涉及两个page页面的动画，当前页面和即将呈现的页面同时向上或向下偏移100%，两者的运动频率一样，跟第一种容器整体滑动的效果看起来是没什么区别的。
![genie.github.io](/assets/72.png)


```js
var index=1;
var isAnimating = false;
$('body').on('click', function(){
    if(isAnimating) return;
    isAnimating = true;
    index++;
    if(index==6) index=1;
    var from = $('.page-'+(index-1));
    var to = $('.page-'+index);
    
    from
      .css({
            transform: 'translateY(0%)'
        })
      .animate({
            transform: 'translateY(-100%)'
      }, 700, 'linear', function(){
          from.addClass('hide')
            isAnimating = false;
      })
            
    to
      .removeClass('hide')
      .css({
            transform: 'translateY(100%)'
        })
      .animate({
            transform: 'translateY(0%)'
      }, 700, 'linear')    
})
```
实际效果，请查看案例演示（鼠标点击进行翻页操作）
<iframe src="http://sandbox.runjs.cn/show/qtzuloay" width="320" height="480" ></iframe>

### 双页视差滑动
在第三种的基础上提供一种视差效果，让当前页面的离开和即将呈现的页面运动频率不一致，以达到视觉上的美感
![genie.github.io](/assets/73.png)

```js
var index=1;
var isAnimating = false;
$('body').on('click', function(){
    if(isAnimating) return;
    isAnimating = true;
    index++;
    if(index==6) index=1;
    var from = $('.page-'+(index-1));
    var to = $('.page-'+index);
    
    from
      .css({
            transform: 'translateY(0%)'
        })
      .animate({
            transform: 'translateY(-100%)'
      }, 1000, 'linear', function(){
          from.addClass('hide')
            isAnimating = false;
      })
            
    to.removeClass('hide')
      .css({
            transform: 'translateY(100%)'
        })
      .animate({
            transform: 'translateY(0%)'
      }, 700, 'linear')    
})
```

实际效果，请查看案例演示（鼠标点击进行翻页操作）
<iframe src="http://sandbox.runjs.cn/show/52pijjre" width="320" height="480" ></iframe>


## 结语


以上，轻拍。

(EOF)
