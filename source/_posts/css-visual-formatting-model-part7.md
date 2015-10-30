title: "CSS核心可视化格式模型: 控制紧接浮动的排列-clear 特性 part7"
date: 2015-10-29 17:04:44
tags: "CSS"
---
在前面的帖子中，我们已经讲了可视化模型中布局的两大方面：1. 常规流  2. 浮动，布局3大部分只剩下了绝对定位。前面的帖子中也零星的提到过关于绝对定位的某些特性，但都不够细致系统。

### 绝对定位（Absolute positioning）

1) **相对包含块偏移定位**
在绝对定位模型中，一个框明确地基于它的包含块偏移。不是父元素，这点需注意。所以，绝对定位元素的定位，关键是确定其包含块。

2) **完全脱离常规流**
它完全脱离了常规流（对后继的兄弟节点没有影响）。这一点又与浮动元素不同，浮动元素会对后继的行框产生影响，而且，后面声明的绝对定位元素也不会受前面定义的绝对元素的影响。可以这么理解，**常规流中的元素，都在同一个层上，浮动是处于常规流之上的一个特殊层，可能会对常规流中的元素有影响。但是绝对定位的元素不会，可以把每个绝对定位的框看做一个单独的图层，独来独往**。所以，说它完全脱离了常规流也不无道理。
注意一点，绝对元素定位的 top 和 left 值跟绝对元素未脱离常规流之前在常规流中位置有关。

看这个例子：
```html
<div style="position:absolute; width:100px; height:100px; background-color:red;">absolute</div>
<div style="height:50px; border:1px solid blue; width:200px;">DIV 中的普通文本元素</div>
<div style="position:absolute; left:60px; width:100px; height:100px; background-color:green;">absolute</div>
```

<div style="position:absolute; width:100px; height:100px; background-color:red;">absolute</div> <div style="height:50px; border:1px solid blue; width:200px;">DIV 中的普通文本元素</div> <div style="position:absolute; left:60px; width:100px; height:100px; background-color:green;">absolute</div>

以上例子中，两个绝对定位元素都未声明其 top 特性，那么top就会取它在常规流中的位置。
中间的DIV在常规流中，影响了后面的绝对定位元素的位置，但是没有受到前面的绝对定位元素的影响。


3) **绝对定位元素生成的包含块**
一个绝对定位框会为它的常规流子元素和定位派生元素(不包含 fiexed 定位的元素)生成一个新的包含块。不过，绝对定位元素的内容不会在其它框的周围排列。
注意，绝对定位框还会创建 block formatting contexts。

4) **堆叠层次**
它们可能会掩盖另一个框的内容，或者被另外一个框掩盖，这取决于互相重合的框的`堆叠层次(Stact Level)`。 也就是我们前面说的三维的可视化模型，除了X轴，Y轴，还有Z轴。


### 固定定位（Fixed positioning）

**固定定位是绝对定位的一个子类**。唯一的区别是，对于固定定位框，它的`包含块`由可是窗口(viewport)创建。对于连续媒介，固定定位框并不随着文档的滚动而移动。从这个意义上说，它们类似于固定的背景图形。对于页面媒介，固定定位框在每页里重复。对于需要在每一页底部放置一个签名时，这个方法非常有用。
