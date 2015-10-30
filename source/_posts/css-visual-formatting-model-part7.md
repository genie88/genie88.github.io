title: "CSS核心可视化格式模型: 控制紧接浮动的排列-clear 特性 part7"
date: 2015-10-29 17:04:44
tags: "CSS"
---
浮动带给我们一个不属于常规流的世界: 它不能超出它的包含块，它的位置跟在它之前的元素生成的框有关系(详见前面的浮动规则)…… 那么，它对处于它后面的元素有什么关系呢？对于块框，会认为它不存在，行框会绕着它排列！有没有方法使块框也可以在它后面排列，而不再当它不存在呢？答案是肯定的。W3C总是透着一种非常人性化的味道。`clear` 特性就是做的这件事。从某种意义上来说，clear 是对浮动框和常规流中框的一种关系上的平衡。
<!--more-->

### clear特性

该特性表明一个元素框的哪一边不可以和先前的浮动框相邻。`clear`特性不考虑它自身包含的浮动子元素和不处于同一个Block formatting context中的浮动元素。

**1) clear 特性值的作用**

left/right/both：生成框的间隙，是指设置足够的(空白区)，以使元素的`顶边框边界`(top border edge)放置到由源文档中较早元素生成的任何左浮动框/右浮动框/左右浮动框的`底外边`(bottom outer edge，即底margin边)之下。
none：对考虑到浮动后的框的位置没有约束。

简单点儿说，就是设置了clear的元素的`顶边框边界`要放在相关的浮动元素的`底外边`之下。注意这两种元素接触边界的区别。一个是borer，一个是margin。

一个直观的例子：

```html
<div style="height:200px;">
    <div style="width:300px; height:100px; background-color:green; float:left; border:5px solid red;">
        float
    </div>
    <div style="clear:left; width:300px; height:50px; background-color:green; border:5px solid yellow; margin-top:50px;">
        clearance
    </div>
</div>
```


<div style="height:200px;"> <div style="width:300px; height:100px; background-color:green; float:left; border:5px solid red;"> float </div> <div style="clear:left; width:300px; height:50px; background-color:green; border:5px solid yellow; margin-top:50px;"> clearance </div> </div>

设置了clear的元素的margin-top是50px，没起作用，为什么呢？注意，应该是设置了clear的元素的top border edge对齐，不是margin edge。
如果想让它们之间有50px的间距，怎么办？只需将设置浮动元素的margin-bottom为50px即可。

```html
<div style="height:200px;">
    <div style="width:300px; height:100px; background-color:green; float:left; border:5px solid red; margin-bottom:50px;">
        float
    </div>
    <div style="clear:left; width:300px; height:50px; background-color:green; border:5px solid yellow;">
        clearance
    </div>
</div>
```


<div style="height:200px;"> <div style="width:300px; height:100px; background-color:green; float:left; border:5px solid red; margin-bottom:50px;"> float </div> <div style="clear:left; width:300px; height:50px; background-color:green; border:5px solid yellow;"> clearance </div> </div>

> 此处仅为示例，实际情况下我们经常将clear框设置为0px高的不可见div

**2)浮动元素上的 clear**

为 clear 特性被赋予浮动元素时，它将导致浮动框定位规则的修正，另外一条限制（第10条）被追加：

> 浮动框区的上外边界（top margin edge）必须低于前面所有左浮框的下外边界（在clear:left时），或者右浮框区（clear:right），或者两个框区(clear:both)。

例子：
```html
<div id="Container" style="width:300px; height:100px; border:1px solid gold; ">
    <div id="DIV1" style="float:right; width:150px; height: 50px; background-color:green; ">float:right;</div>
    <div id="DIV2" style="float:left; width:100px; height: 50px; background-color:red; clear:right;">clear:right float:left;</div>
</div>
```

应该是这种效果：


> 在IE6、IE7和IE8(Q)中，这个规则没有被遵守。请大家注意这个兼容性问题。尽量少在浮动元素上设置clear属性。

