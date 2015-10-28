title: "移动H5页面开发系列——part4:移动H5页面精灵动画的实现原理"
date: 2015-10-23 09:18:09
tags: "html5"
---
本文将重点分析下H5移动页面的精灵动画的实现原理和技巧。

![genie.github.io](/assets/57.png)
<!--more--> 
动画就是一系列连续的画面按顺序呈现出来而已，只是，在电影电视中，这些画面实现已经被准备好了，而在电脑程序中，我们见到每一瞬间的画面都是即时绘制的。这里借用2D游戏中的术语，将H5移动页面中出现的每个元素称之为“动画精灵”。

# 精灵动画的原理
1）transition动画
可以实现初始和结束两个关键状态的简单动画，浏览器会自动计算并生成补间动画。

2）animation动画
可以实现多关键点的复杂动画，浏览器会自动计算并生成补间动画。每个动画区间可以单独采用不同的时间函数（timing-function）进行控制。

3）animation steps实现帧动画
这种动画的实现原理和2D游戏中精灵动画的实现原理最为相似，采用一组连续的sprite运动图，通过快速改变元素图片（或者背景图片显示位置），实现运动效果。这种技术可以在一定程度上弥补CSS3动画在制作复杂动画上的缺陷，但是因为需要较大的图片作为基础，需要牺牲一定的带宽。
![genie.github.io](http://img.xiaoho.com/2014/12/test.png)
```css
.sprite{ 
    width:90px;
    height:100px;
    background:url(http://img.xiaoho.com/2014/12/test.png) no-repeat 0 0; 
    -webkit-animation:run 350ms steps(1, start) infinite 0s;
} 

@-webkit-keyframes run { 
    0% { background-position:0; } 
    20% { background-position:-90px 0; } 
    40% { background-position:-180px 0; } 
    60% { background-position:-270px 0; } 
    80% { background-position:-360px 0; } 
    100% { background-position:-450px 0; } 
} 
```

<iframe src="http://sandbox.runjs.cn/show/szm3ydzu" width="100%" height="500"></iframe>

4) svg动画
svg内容请移步文章《移动H5页面开发系列——part5:SVG元素在移动H5页面动画的应用》相关章节内容。

# 精灵动画的几种常见方式

按照动画的作用可以分为以下几大类：
- 入场动画
- 出场动画
- 强调动画

## 入场动画


####向下滑入(从顶部滑入)
向下滑入的实现关键是同时改变元素的tranlateY值。同理也可以实现从底部滑入的效果。
```css
@keyframes fadeInDown {
  from {
    transform: translate3d(0, -100%, 0);
    visibility: visible;
  }
  to {
    transform: translate3d(0, 0, 0);
  }
}
```

####向下渐入(从顶部飞入)
向下渐入的实现关键是同时改变元素的tranlateY值和透明度值来实现。同理也可以实现从底部飞入的效果。
```css
@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translate3d(0, -2000px, 0);
  }
  to {
    opacity: 1;
    transform: none;
  }
}
```

####向右渐入(从左侧飞入)
向下渐入的实现关键是同时改变元素的tranlateX值和透明度值来实现。同理也可以实现从右侧飞入的效果。
```css
@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translate3d(-2000px, 0, 0);
  }
  to {
    opacity: 1;
    transform: none;
  }
}
```

#### 渐大出现
渐大出现的实现关键是同时改变元素的scale值和透明度值来实现。
```css
@keyframes zoomIn {
  from {
    opacity: 0;
    transform: scale3d(.3, .3, .3);
  }
  50% {
    opacity: 1;
  }
}
```


#### 旋转飞入
旋转飞入出现的关键是同时改变元素的rotate值、translateX值和透明度值来实现。类似的也可以实现旋转飞出的动画
```css
@keyframes rollIn {
  from {
    opacity: 0;
    transform: translate3d(-100%, 0, 0) rotate3d(0, 0, 1, -120deg);
  }
  to {
    opacity: 1;
    transform: none;
  }
}
```


#### 加速飞入
加速飞入的关键是同时改变元素translateX值和透明度值来实现，同时采用X方向的扭曲（skewX）来模拟加速运动过程中导致的惯性变形现象，使得动画显得更加真实。类似的也可以实现加速飞出的动画。

```css
@keyframes lightSpeedIn {
  from {
    transform: translate3d(100%, 0, 0) skewX(-30deg);
    opacity: 0;
  }
  60% {
    transform: skewX(20deg);
    opacity: 1;
  }
  80% {
    transform: skewX(-5deg);
    opacity: 1;
  }
  to {
    -webkit-transform: none;
    transform: none;
    opacity: 1;
  }
}
```


## 出场动画
出场动画的实现原理和入场动画的实现原理一致，再次不做过多解释。

## 强调动画
一些局部细节如果还是渐现显示，会枯燥没什么感觉，例如标题、按钮等，需要一种强调。例如可以采用 flash（闪烁）、bounce（ 弹跳）、swing（摇摆）等方式进行强调，吸引用户的视觉焦点。 


####闪烁动画
闪烁动画的实现关键是动态改变元素的透明度值来实现。
```css
@keyframes flash {
  from, 50%, to {
    opacity: 1;
  }
  25%, 75% {
    opacity: 0;
  }
}
```


####弹跳动画
弹跳动画的实现关键是动态改变元素的tranlateY值， 通过改变timing－function可以控制弹跳到不同阶段的运动速度。
```css
@keyframes bounce {
  from, 20%, 53%, 80%, to {
    animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
    transform: translate3d(0,0,0);
  }
  40%, 43% {
    animation-timing-function: cubic-bezier(0.755, 0.050, 0.855, 0.060);
    transform: translate3d(0, -30px, 0);
  }
  70% {
    animation-timing-function: cubic-bezier(0.755, 0.050, 0.855, 0.060);
    transform: translate3d(0, -15px, 0);
  }
  90% {
    transform: translate3d(0,-4px,0);
  }
}
```

####摇摆动画
摇摆动画的实现关键是动态改变元素的rotateZ值。
```css
@keyframes swing {
  20% {
    transform: rotate3d(0, 0, 1, 15deg);
  }
  40% {
    transform: rotate3d(0, 0, 1, -10deg);
  }
  60% {
    transform: rotate3d(0, 0, 1, 5deg);
  }
  80% {
    transform: rotate3d(0, 0, 1, -5deg);
  }
  to {
    transform: rotate3d(0, 0, 1, 0deg);
  }
}
```


这里仅演示部分的动画效果，更多动画效果，请移步 http://daneden.github.io/animate.css/

# 精灵动画的组合与叠加

1) 同一元素，同时运用不同的动画效果，生成新的动画效果（动效叠加）
- 采用特殊的keyframe关键帧定义
- 可以采用子父元素嵌套实现

需求举例：
```
一颗星星从上往下滑落，一边滑落时一边闪烁
```

由于CSS3并未提供给一个元素同时添加多个动画效果的方法，就是说一个元素，只能给它定义一个动画效果，不能同时定义。根据需求，我们可以写出如下的关键帧定义:
```
.star{
    animation: dropFlash 6s infinite linear;
}
@keyframes dropFlash {
  from {
    transform: translate3d(0, -100%, 0);
    opacity: 1;
  }
  50%{
    opacity: 1;
  }
  25%, 75% {
    opacity: 0;
  }
  to {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
}
```

但是发现这样的代码很难实现复用，所以我们将动画效果进行拆分，分别定义了如下两个动画序列： drop  和 flash

```css
@keyframes drop {
  from {
    transform: translate3d(0, -100%, 0);
  }
  to {
    transform: translate3d(0, 0, 0);
  }
}
```

```css
@keyframes flash {
  from, 50%, to {
    opacity: 1;
  }
  25%, 75% {
    opacity: 0;
  }
}
```

我们在star元素的上一层，在套用一个父元素，分别用于实现不同的动画效果，实现了不同动画效果的叠加。
```html
<div class="star-wrapper">
    <div class="star"></div>
</div>
<style>
    .star-wrapper{
        animation: drop 6s infinite linear;
    }
    .star{
        animation: flash 6s infinite linear;
    }
</style>
```


2) 同一元素，不同时间段的动画相互衔接，构成动画序列（时间组合）
- 可以采用特殊的keyframe关键帧定义
- 或者采用js脚本控制动画切换
- 可以采用子父元素嵌套实现＋animation-delay实现

需求举例：
```
一颗星星从上往下滑落，当滑落到指定位置时闪烁两次
```

动画分解：1. 从上往下滑落 (单次动画) 2. 闪烁 (单次动画)




需求举例：
```
一颗星星从上往下滑落，当滑落到指定位置时开始闪烁
```

动画分解：1. 从上往下滑落 (单次动画) 2. 闪烁 (循环动画)





3) 不同元素，在同一时间段的动画相互配合，构成动画画面（空间组合）
可以采用视差效应或者相对运动实现不同的动画效果

需求举例：
```
运动员在赛场上跑步，但是需要保持运动员一直固定在屏幕中央。
```

可以采用运动员原地跑步运动，移动变换不同的背景，让背景持续向左移动，产生运动员持续向右跑动的效果。


2) 不同元素，不同时间段的动画相互衔接，构成动画场景（时间空间组合）
可以采用animation-delay实现动画之间的延时效果
或者采用js脚本控制动画切换



# 精灵动画的播放暂停控制

精灵动画的播放暂停控制有两类方法，主要包括：
- js动态直接切换动画相关class类名，或者animation属性

js动态增加动画相关类名时，动画立即开始，删除动画相关类名时，动画立即结束。这种控制方式比较适合页面的换场动画的开启和结束。
例如：
```js
//开始换场动画
$fromPage.addClass('animation-slideToTop');
$toPage.addClass('animation-slideFromBottom');

setTimeout(function(){
  //换场动画结束后
  $fromPage.removeClass('animation-slideToTop');
  $toPage.removeClass('animation-slideFromBottom');
}, 600);
```

- animation-play-state: paused | running

由于CSS3的animation规范中提供了一个 animation-play-state 属性，js 可以控制这个属性的 paused 和 running 来控制动画。这类方法适合页面的精灵动画的开启。

为方便切换，可以先定义如下的样式类
```css
.page-active{
    animation-play-state: running;
}
```

然后在js脚本中可以切换这个类实现动画播放暂停控制。
```js
//页面中的精灵动画开始播放
$toPage.addClass('page-active');

//页面中的精灵动画停止播放
$toPage.removeClass('page-active');
```





# 结语


以上，轻拍。

(EOF)

参考文献
http://daneden.github.io/animate.css/

