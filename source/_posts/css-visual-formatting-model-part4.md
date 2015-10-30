title: "CSS核心可视化格式模型: 定位体系(Position Scheme) part4"
date: 2015-10-29 11:35:07
tags: "CSS"
---

曾经提到了：在可视化格式模型中，每一个元素都会根据盒子模型产生0个或多个box，而这些box的布局会受四大因素的影响，其中之一，就是定位体系。
<!--more-->
- 常规流式布局(Normal flow)

常规流，是对 normal flow的直译。
流者，动也。偏旁是三点水，说明，跟水有关系，水的流动是连续不间断的，也是有先后顺序的。在这里，我们把它当作可以流动的(位置可变)，有先后顺序(元素顺序加载)的体系。在文档加载的时候，好像流水似的，一点点的漫过整个画布。还有一种说法是，浏览器在解析HTML CSS JS 的时候的一个流式的过程，从html起始标签开始 到html结束标签截止。

之所以是常规，是因为，这是相对于后面的浮动和定位的一个概念，**浮动和定位元素都脱离了当前的常规流** 。

在 CSS2.1中，常规流包括块框(block boxes)的块格式化上下文(blok formatting context后续会讲到)，行内框(inline boxes)的行内格式化上下文(inline formatting context 后续会讲到)，块框或行内框的相对定位。

- 浮动(Floats)

浮动，顾名思义，相对于常规流来讲，它漂浮在常规流的上方。
在浮动模型中，一个框(box)首先根据常规流布局，再将它从流中取出并尽可能地向左或向右偏移。内容可以沿浮动区的侧面排列。

- 绝对定位(Absolute positioning)

在绝对定位模型中，一个框(box)整个地从常规流向中脱离（它对后续的兄弟元素没有影响），并根据它的包含块来分配其位置。这包含两种情况`position:absolute 和 fixed`。 其中 `fixed` 是 `absolute` 的一种特殊情况。


### 选择定位方案：”position”特性
`float`和`position` 这两个CSS特性决定了使用哪种CSS2.1定位算法来计算框的位置。

1) **static**
该框(box)是一个常规框，布局根据常规流(见上述说明)。'left' 、’right’、’bottom’和 'top'属性不适用。
```html
<div style="position:static;"></div>
```
如上代码，设置了静态布局（流式布局），如果 `position`没有设置，默认值也是`static`。这时，设置'left' 、'right'、'bottom'和 'top'，无效。

2) **relative**
框的位置根据常规流计算（被称为常规流中的位置）。然后框相对于它的常规位置而偏移。如果框 B 是相对定位的，其后框的定位计算并不考虑B的偏移。 table-row-group, table-header-group, table-footer-group, table-row, table-column-group, table-column, table-cell, 和 table-caption 元素的'position:relative' 效果没有被定义。
```html
<div style="position:static; width:100px;">
    <div id="A" style="background-color:green;">A</div>
    <div id="B" style="position:relative;top:70px; left:50px;background-color:red;">B</div>
    <div id="C" style="background-color:blue;">C</div>
</div>
```

<div style="position:static; width:100px;"> <div id="A" style="background-color:green;">A</div> <div id="B" style="position:relative;top:70px; left:50px;background-color:red;">B</div> <div id="C" style="background-color:blue;">C</div> </div>

根据标准，B 的位置应该相比自身原位置偏移，而 C 在放置的时候，会当 B 仍然在原位置。

> 注意，相对定位的元素处于常规流中，没有脱离常规流。

3) **absolute**
框的位置（可能还有它的尺寸）是由'left'，'right'，'top'和'bottom'特性决定。这些特性指定了框相对于它包含块的偏移量。绝对定位的框从常规流中脱离。这意味着它们对其后的兄弟元素的定位没有影响。另外，尽管绝对定位框有外边距(margin)，它们不会和其它任何 margin 发生折叠（Collapsing margins）。
```html
<div style="position:absolute; width:300px; border:2px solid yellow;">
    <div id="A" style="background-color:green;height:50px;">A</div>
    <div id="B" style="position:absolute;top:70px; left:50px; height:50px; background-color:red;">B</div>
    <div id="C" style="background-color:blue;height:50px;">C</div>
</div>
```

<div style="position:absolute; width:300px; border:2px solid yellow;"> <div id="A" style="background-color:green;height:50px;">A</div> <div id="B" style="position:absolute;top:70px; left:50px; height:50px; background-color:red;">B</div> <div id="C" style="background-color:blue;height:50px;">C</div> </div>

4) **fixed**
框位置的计算根据'absolute'模型，不过框要额外地根据一些参考而得到固定。应用于手持终端、投影设备、屏幕、TTY、电视媒体类型时，框相对于 viewport固定，滚动时不移动。应用于打印媒介类型时，框被渲染于每一页，并相对于页框固定，就好象是通过viewport查看该页一样（例如，打印预览）。对于其他的媒介类型，表现没有被定义。跟绝对定位一样，fixed定位元素的margin不会和任何其他 margin发生margin折叠。

> 对根元素的 position，用户端(UA)可以视为“static”。


### 框偏移: 'top'，'right'，'bottom'，'left'

如果一个元素的'position'特性值不是'static'，该元素被称为`定位元素`。定位的元素生成定位框，其定位基于四个特性：'top'，'right'，'bottom'，'left'。

值：这四个特性的值可以是：<length> | <percentage> | auto | inherit 之一

`<length>`
偏移量是距离参照边的固定值。

`<percentage>`
偏移量是`包含块`宽度（对于'left'和'right'）或高度（对于'top' 和'bottom'）的百分比。对于'top'和'bottom'，如果包含块的高度没有显式指定（即它取决于内容的高度），百分比值将解释为'auto'。

`auto`
该值的效果取决于与之相关的属性中的哪一个也设置了'auto'。详细的内容请参见绝对定位，非替换元素的宽度和高度一节。后续会跟大家分享。

初始值：‘auto’
适用于：定位的元素，即 position特性的值为非 ‘static’的值。
可否继承 ：否
百分比值：百分比值基于`包含块`的高度(top, bottom)或者宽度(left, right)
计算值：对于position:relative 参见相对定位(后续会介绍)；对于position:static 取值auto；其他情况，如果值为长度，取相应的绝对长度，如果标值为百分比，取指定的值，否则，取auto。

定位作用的具体位置：
1) 对于绝对定位元素(absolutely positioned)的框，这四个特性的值表示，**元素的外边界(margin边界)相对于`包含块`的边界的位移**。
2) 对于相对定位元素(relatively positioned)的框，偏移量相对于它自己的相应的边界。比如，top是相对于它的顶边界，right相对于右边界。
