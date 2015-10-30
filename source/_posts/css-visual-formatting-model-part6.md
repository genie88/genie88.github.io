title: "CSS核心可视化格式模型: 浮动(Float) part6"
date: 2015-10-29 17:04:40
tags: "CSS"
---
浮动是可视化格式模型中非常重要的一节。浮动跟`堆叠层级(stack level)`也有一定的关系。**可视化模型是一个3维的模型，并不是二维的**。元素在页面上的排列，从我们的角度看是二维的，元素的位置可以用x，y轴坐标来表示。但是，元素和元素之间的位置如果有所重叠，谁显示在前面，就涉及到另一个轴：z轴。我们经常使用的 z-index 就是如此得来的。浮动框在整个模型中，z轴坐标比常规流中的值要高，所以会飘在它上面。也可以把这个模型看作是 Photoshop中的图层，我们就好像在好多层玻璃上画框框，这些玻璃都叠在一起，我们只能透过一个窗口(浏览器可见窗口)来看这些玻璃重叠后的图画。浮动可以看作其中的一个图层。

<!--more-->

### 浮动概述
**浮动和文字环绕**
`浮动框`就是一个框在当前行被向左或向右挪动(偏移)，它不在常规流中，浮动框由浮动元素的框组成。`浮动框( float, “floated” or “floating” box)`最有趣的特性是内容可以沿着它的边缘渲染（或设置'clear'属性禁止此特性）。内容排列在沿着左浮动框的右边排列，而沿着右浮动框的左边排列，也就是我们常说的文字环绕效果。
请看下面的例子：
```html
<P style="margin: 2em; border: 1px solid red; width: 200px;"> 
    <span style="width:100px; height:100px; background-color:green; margin:20px;float:left;"></span>
    The SPAN box is floated to the left. The content that follows is formatted to the
    right of the float, starting on the same line as the float.
</p>
```

<P style="margin: 2em; border: 1px solid red; width: 200px;"> <span style="width:100px; height:100px; background-color:green; margin:20px;float:left;"></span> The SPAN box is floated to the left. The content that follows is formatted to the right of the float, starting on the same line as the float. </p>

如上图，文字和绿色的块之间有空白，可见，文字是围绕绿块的 margin 排列的。

**浮动框的放置**

一个`浮动框`，会被向左或向右偏移，直到它的`外边界`( outter edge，又叫margin edge ) 接触到它 `包含块` 的边界或另一个`浮动元素的外边界` ，如果存在一个行框，浮动框的顶边会和当前行框的顶部对齐。

如果水平方向没有足够的空间放置浮动元素，它将向下移动，直到有足够的空间或没有更多的浮动元素为止。

**浮动元素会缩短行框**
由于浮动框并不在常规流中，在该浮动框之前或之后创建的非定位框垂直排列，就好象浮动框并不存在一样。然而，浮动框之后创建的行框 会被缩短，比便为浮动元素的 margin 框提供空间。如果被缩短的行框无法再容纳更多的内容，它将向下移动，直到有足够的空间或没有更多的浮动元素为止。当前行里浮动框前的任何内容，都将被重新排列到该浮动另一侧的第一个可用行里。也就是说，如果在遇到左浮动框之前，行内框被放置到行上，剩余的行框空间足够容纳该左浮动框，那么，左浮动框就会被放置在该行上，并与该行框的顶端对齐，然后，已经在行上的行内框被相应地移动到该浮动框的右侧（右侧成了该左浮动框的另一侧），反之亦然，对于 rtl 和 右浮动框也是一样。
如上图中的文字环绕的例子，包含文字的行框被缩短，是包含块减去浮动元素的 margin 宽度。其中，The content两字，分别被放到了两行，因为，一行中的剩余空间无法再容纳content。

**TABLE 元素、块级替换元素、BFC元素和浮动元素**
TABLE 元素、块级替换元素或者在常规流中创建了 block formatting contexts 的元素，它们的  border box 在同一个  block formatting contexts  中，一定不能覆盖任何浮动元素。如果有必要，实现工具应该通过把元素放置到前面浮动元素的下面，以清理先前说到的元素，但是，如果有足够的空间，也可以把它紧临浮动元素放置。它们可能造成所说元素的 border box 比10.3.3中定义的要短。
例如：
```html
<div id="C" style="margin: 2em; border: 1px solid red; width: 200px; overflow: hidden;"> 
    <div id="A" style="width:50px; height:50px; background-color:green; margin:20px; float: left;">A</div>
    <div id="B" style=" width:50px; background-color:blue; overflow:hidden;">B</div>
</div>
```

<div id="C" style="margin: 2em; border: 1px solid red; width: 200px; overflow: hidden;"> <div id="A" style="width:50px; height:50px; background-color:green; margin:20px; float: left;">A</div> <div id="B" style=" width:50px; background-color:blue; overflow:hidden;">B</div> </div>

这时，B的宽度为50px，它和浮动元素A的包含块都是C，宽度为200px。浮动元素在放置后，还有足够的空间放置B，所以，B 被紧挨着A 的margin 框被放置。

将B的宽度改为150px，这时：
<div id="C" style="margin: 2em; border: 1px solid red; width: 200px; overflow: hidden;"> <div id="A" style="width:50px; height:50px; background-color:green; margin:20px; float: left;">A</div> <div id="B" style=" width:150px; background-color:blue; overflow:hidden;">B</div> </div>

需要注意的时，这种方式与使用 clear 特性清除浮动不同。后面将介绍 clear 特性。

### 浮动属性详解
浮动特性非常有用，3大布局核心之一。虽然如此，它涉及内容过多，浏览器兼容性问题也很多。它的定位不仅涉及` 包含块`，还涉及到了`行框`，`块框`，还有`行内框`等内容；并且，各浏览器对其的支持还有不少兼容性问题。

**适用于哪些元素**
可设置给任意元素，但只适用于生成非绝对定位框的元素。
例：
```html
<div style="width:500px; height:150px; border:1px solid green; position:relative;">
    <div style="width:100px; height:100px; float:right; position:absolute; border:1px solid red;">absolute</div>
    <div style="width:100px; height:100px; float:right; position:relative; border:1px solid red;">relative</div>
</div>
```

实际效果如下：

<div style="width:500px; height:150px; border:1px solid green; position:relative;"> <div style="width:100px; height:100px; float:right; position:absolute; border:1px solid red;">absolute</div> <div style="width:100px; height:100px; float:right; position:relative; border:1px solid red;">relative</div> </div>

可见，对于绝对定位的元素，浮动没有任何效果。这也体现了浮动和绝对定位之间的一种平衡。


**特性值的含义**
该属性指定框应当向左右移动或者不移动。特性值有如下含义：
left: 该元素产生一个向左浮动的`块框`。内容在该框的右边排列，就是之前所说的文字环绕，起点是框的顶部（会受'clear'属性的影响）。
right: 与left类似，框向右侧浮动，内容在该框的左侧排列，从顶部开始。
none: 该框不浮动。


**浮动细则**

1. 对于根元素的浮动，浏览器应该当作 none
根元素无所谓是否浮动，没有实际意义。

2. 左浮动框的`左外边界`(margin edge)不可以出现在它`包含块`左边界之左。对于右浮动的元素也有类似规则

也就是说左浮动元素的左 margin 最多紧贴包含块的左边界。
```html
<div style="width:500px; border:2px solid red; overflow:hidden;">
    <div class="sub" style="float:left;width: 100px; height: 100px; background-color: green; margin:0 20px;">left</div> 
    <div class="sub" style="float:right;width: 100px; height: 100px; background-color: green; margin:0 20px;">right</div> 
</div>
```

示意图：
<div style="width:500px; border:2px solid red; overflow:hidden;"> <div class="sub" style="float:left;width: 100px; height: 100px; background-color: green; margin:0 20px;">left</div> <div class="sub" style="float:right;width: 100px; height: 100px; background-color: green; margin:0 20px;">right</div> </div>

3. 如果当前框是左浮动框，并且在源文档中存在更早生成的左浮动框，那么对于任意这些先前的框，要么当前框的左外边出现在先前框的右外边之右，要么它的顶部必须在先前框的底部之下。对于向右浮动的框也有类似的规则。

也就是说，浮动元素的定位受先前生成的浮动框的影响。后面的浮动元素，需要紧挨着先前同向浮动元素的 margin 边进行定位，如果空间不足，则折行，放置到它之前元素的下面。
例如：
```html
<div style="width:500px; border:2px solid red; overflow:hidden;">
    <div class="sub" style="float:left;width: 200px; height: 100px; background-color: green; margin:10px;">left1</div>
    <div class="sub" style="float:left;width: 200px; height: 100px; background-color: green; margin:10px;">left2</div>
    <div class="sub" style="float:left;width: 200px; height: 100px; background-color: green; margin:10px;">left3</div>
</div>
```

示意图：

<div style="width:500px; border:2px solid red; overflow:hidden;"> <div class="sub" style="float:left;width: 200px; height: 100px; background-color: green; margin:10px;">left1</div> <div class="sub" style="float:left;width: 200px; height: 100px; background-color: green; margin:10px;">left2</div> <div class="sub" style="float:left;width: 200px; height: 100px; background-color: green; margin:10px;">left3</div> </div>

如上图中，把left2当作当前元素，那么，它前面有left1生成的浮动框，所以，它会贴着left1的右 margin 边排列。而到left3 的时候，剩余的空间已经不能够放置它了，所以，折行放置。

4. 左浮动框的右外边不可以出现在它右侧的任何右浮动框的左外边之右。对于向右浮动的元素也有类似的规则。

注意，以上说的是右侧，不是下侧，此规则不包括左浮动框下面的右浮动框。就是说，同一行中的左浮动元素和有浮动元素不能够有互相折叠的现象。
```html
<div id="container" style="width:200px; overflow:hidden; border:1px solid red;">
    <div class="sub" style="float:left;width: 100px; height: 100px; background-color: green; margin: 10px;">left</div>
    <div class="sub" style="float:right;width: 100px; height: 100px; background-color: green; margin: 10px;">right</div> 
</div>
```

示意图：

<div id="container" style="width:200px; overflow:hidden; border:1px solid red;"> <div class="sub" style="float:left;width: 100px; height: 100px; background-color: green; margin: 10px;">left</div> <div class="sub" style="float:right;width: 100px; height: 100px; background-color: green; margin: 10px;">right</div> </div>

以上两个浮动元素的包含块宽度为200px，无法在一行放置，所以，右浮动元素只好折行显示了。
宽度设置成300px之后，则可以放到一行。



5. 浮动框的顶外边不能高于它包含块的顶部。当一个浮动框发生在两个margin折叠的中间时，浮动元素的定位好像它有另一个空的块级父框位于常规流中。那个空父框的定位规则在margin 折叠一节有说明。

第一句好理解，说的是顶边不能超出包含块，跟左边右边不能超出一个道理。
后面的规则是说，当浮动框处于两个发生margin折叠的地方时，会被当作被包含在一个空的块框中，它上面和下面的margin会穿过它发生margin折叠，当它不存在。
```html
<style type="text/css">
    div {
       width: 100px;
       height: 100px;
       background-color: green;
       color: white;
       margin: 50px;
    }
</style>
<div>A</div>
<div style="float:left; margin:10px; background-color: red;">O</div>
<div>B</div>
```
以上代码中，3个 div 的包含块是初始包含块。O 处于 A 和 B 的中间，A和B在理论上应当发生margin 折叠。那么，发生了么？
看截图：


6. 浮动框的顶边不可以高于源文档中先前元素产生的块框或浮动框的顶

7. 浮动框的顶边不可以高于源文档中先前元素产生的包含一个框的任何行框的顶。
在前面的内容中说到过，浮动元素会缩短行框。

8. 左浮动框左边如果有另外一个左浮动框，它的右外边不可以出现在它包含块的右边之右。（或者比较宽松的要求是：一个左浮动不可以超出右边，除非它已经尽可能地靠左排列。）对于向右浮动的元素也有类似的规则。
此条规则也是限定浮动元素的位置范围，不可超出包含块。

9. 浮动框要放置得尽可能的高。
在符合所有规则的情况下，尽可能的向上放，注意6、7两条关于其顶边的规则。

10. 左浮动框必须尽量靠左放置，右浮动框必须尽量靠右放置。在更高的位置和更靠左或靠右的位置间，选择前者。
和第9条，可以算是浮动的大规则吧，尽量的向上向左/右放。

这几条规则中说到的其他元素，都和浮动元素处于相同的 block formatting context 中。

### 总结
可见，浮动的规则却是很让人迷惑，但从这几条规则中你也不难发现，浮动的宗旨是，**在不溢出包含块的情况下，尽量的靠上靠左/右放置，但是不能高于它前面生成的块框、浮动框和行框的顶**。
