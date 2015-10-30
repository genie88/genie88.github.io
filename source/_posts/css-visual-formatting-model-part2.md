title: "CSS核心可视化格式模型: 包含块(containing block) part2"
date: 2015-10-29 11:34:59
tags: 'css'
---

上文说到，一个元素box的定位和尺寸，有时候会跟某一矩形框有关，这个矩形框，就被称作元素的`包含块`。`包含块（Containing Block）`是视觉格式化模型的一个重要概念，它也可以理解为一个矩形，而这个矩形的作用是为它里面包含的元素提供一个参考，元素的尺寸和位置的计算往往是由该元素所在的`包含块`决定的。而元素会为它的子孙元素创建包含块，那么是不是说，元素的包含块就是它的父元素呢？答案是否定的。一个元素包含块的确定，跟元素自身和它的祖先元素的样式等有关系。
<!--more-->


1) 根元素的包含块
根元素，就是处于文档树最顶端的元素，它没有父节点。根元素存在的包含块，被叫做`初始包含块` (initial containing block)。具体跟用户端有关。
- 在(X)HTML中，根元素是html元素（尽管有的浏览器会不正确地使用body元素）
- 而初始包含块的direction属性与根元素相同。

2) `static`和`relative`定位的元素

对于其它元素：如果该元素的定位（position）为 `relative` （相对定位）或者 `static`（静态定位），它的包含块由它最近的块级、单元格 （table cell）或者行内块（inline-block）祖先元素的`内容框(Content Box)`创建。

3) `position:fixed` 定位的元素

如果元素是固定定位 (“position:fixed”) 元素，那么它的包含块是当前可视窗口。

4) `position: absolute` 定位的元素

如果元素是绝对定位（`position: absolute`）元素，包含块由离它最近的 position 属性为 `absolute`、`relative` 或者 `fixed` 的祖先元素创建。

> 在CSS3规范中，tansform属性会改变绝对定位元素的包含块。这种情况下包含块由离它最近的 tansform 属性不为 `none`的祖先元素创建。须注意的是，固定定位也是绝对定位的一种。



4.1) 如果其祖先元素是行内元素，则包含块取决于其祖先元素的 `direction` 特性

- 如果 'direction'  是 'ltr'，包含块的顶、左边是祖先元素生成的第一个框的顶、左内边距边界(padding edges) ，右、下边是祖先元素生成的最后一个框的右、下内边距边界(padding edges) 。

举例如下：
```html
<p style="border:1px solid red; width:200px; padding:20px;">
    T
    <span style="background-color:#C0C0C0; position:relative;">
      这段文字从左向右排列，红 XX 和 蓝 XX 和黄 XX 都是绝对定位元素，它的包含块是相对定位的SPAN。
      可以通过它们绝对定位的位置来判断它们包含块的边缘。
    <em style="position:absolute; color:red; top:0; left:0;">XX</em>
    <em style="position:absolute; color:yellow; top:20px; left:0;">XX</em>
    <em style="position:absolute; color:blue; bottom:0; right:0;">XX</em>
    </span>
</p>
```


实际效果如下：

<p style="border:1px solid red; width:200px; padding:20px;"> T <span style="background-color:#C0C0C0; position:relative;"> 这段文字从左向右排列，红 XX 和 蓝 XX 和黄 XX 都是绝对定位元素，它的包含块是相对定位的SPAN。 可以通过它们绝对定位的位置来判断它们包含块的边缘。 <em style="position:absolute; color:red; top:0; left:0;">XX</em> <em style="position:absolute; color:yellow; top:20px; left:0;">XX</em> <em style="position:absolute; color:blue; bottom:0; right:0;">XX</em> </span> </p>

以上代码中，文字采取默认从左到右的方式排列。红 XX 和 蓝 XX 和黄 XX 都是绝对定位元素，它的包含块是相对定位的SPAN。它们定位需要参照包含块，按照标准来说，它们包含块的左顶边是 SPAN形成的第一个框（即第一行的灰色部分）的顶、左内边距边，包含块的右、下边是SPAN 生成的最后一个框（最后一行灰色的部分）的右、下内边距边界。


- 如果 'direction'  是 'rtl'，包含块的顶、右边是祖先元素生成的第一个框的顶、右内边距边界(padding edges) ，左、下边是祖先元素生成的最后一个框的左、下内边距边界(padding edges) 。
例如：

```html
<p style="border:1px solid red; width:200px; padding:20px; direction:rtl;">
    T
    <span style="background-color:#C0C0C0; position:relative;">
     这段文字从右向左排列，红 XX 和 蓝 XX 和黄 XX 都是绝对定位元素，它的包含块是相对定位的SPAN。
     可以通过它们绝对定位的位置来判断它们……
    <em style="position:absolute; color:red; top:0; left:0;">XX</em>
    <em style="position:absolute; color:yellow; top:20px; left:0;">XX</em>
    <em style="position:absolute; color:blue; bottom:0; right:0;">XX</em>
    </span>
</p>
```

<p style="border:1px solid red; width:200px; padding:20px; direction:rtl;"> T <span style="background-color:#C0C0C0; position:relative;"> 这段文字从右向左排列，红 XX 和 蓝 XX 和黄 XX 都是绝对定位元素，它的包含块是相对定位的SPAN。 可以通过它们绝对定位的位置来判断它们…… <em style="position:absolute; color:red; top:0; left:0;">XX</em> <em style="position:absolute; color:yellow; top:20px; left:0;">XX</em> <em style="position:absolute; color:blue; bottom:0; right:0;">XX</em> </span> </p>


4.2) 其他情况下，如果祖先元素不是行内元素，那么包含块的区域应该是祖先元素的内边距边界。

```html
<div id=”container” style="padding:50px; background-color:#c0c0c0; position:relative; width:200px; height:200px;">
    <div id=”div1” style="width:100%;height:100%;border:2px solid blue;">
               <div id=”content” style="border:1px solid red; position:absolute; left:0; top:0;">absolute element</div>
    </div>
</div>
```

<div id=”container” style="padding:50px; background-color:#c0c0c0; position:relative; width:200px; height:200px;"> <div id=”div1” style="width:100%;height:100%;border:2px solid blue;"> <div id=”content” style="border:1px solid red; position:absolute; left:0; top:0;">absolute element</div> </div> </div>


如上代码中，content的父元素虽是 div1，但，按照标准它的包含块应该是 container。

如果不存在这样的祖先元素，那么它的包含块就是初始包含块。

> 这个概念比较复杂，但最重要的是弄清楚，包含块是由哪个祖先元素创建的，以及创建的包含块区域。




