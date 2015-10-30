title: "CSS核心可视化格式模型: 常规流中的格式化上下文 part5"
date: 2015-10-29 11:35:12
tags: "CSS"
---

在上文中，大致介绍了可视化模型中的定位体系。其中，常规流是最为基础的。这次就和大家分享常规流的一些布局要点和重要的概念。
<!--more-->
在常规流中的框（boxes，元素形成的矩形区域），都属于一个格式化的上下文中，可能是块的，也可能是行内的，但不可能同时是行内的又是块的。`块框`参与`块格式化上下文(block formatting context)`。`行内框`参与`行内格式化上下文(inline formatting context)`。

### 块格式化上下文(Block formatting contexts)

**如何触发**
有这几种框会为其内容创建新的块格式化上下文：浮动元素，绝对定位元素，inline-blocks，table-cells，table-captions，以及 'overflow'不是 'visible'的元素，会创建新的block formatting context。


> 在CSS3中，对这个概念做了改动：http://www.w3.org/TR/css3-box/#block-level0 CSS3中，将Block formatting context 叫做 flow root。对于触发方式也做了修改：The value of ‘position’ is neither ‘static’ nor ‘relative’ (见[CSS3]).从上下文（context）变成了根（root），这个概念确实挺费解的。可见，CSS3中的描述更加准确，position在 ‘fixed’ 的时候也会创建 flow root。这并不是CSS2.1的疏忽，因为 position:fixed 本身就是 position:absolute 的一个子类。

注意，display:table 本身并不产生 block formatting contexts。但是，它可以产生匿名框，其中包含 display:table-cell 的框会产生 block formatting context。总之，对于 display:table 的元素，产生 block formatting contexts 的是匿名框而不是 display:table。

**它做了什么**
这也是一个比较抽象的概念。可以把它想象成一个大箱子，里面装着很多元素，箱子可以隔开里面的元素和外面的元素。好像JS中的闭包，保护其中的元素。它可以包含浮动元素，可以阻止margin折叠，可以防止元素被浮动元素覆盖……

块格式化内容是个重要的概念，它对宽高的计算，margin折叠，定位等都有一定的影响。后续会有详细的说明。

在块格式化上下文中，框会从`包含块`的顶部开始，一个接一个地，垂直向下地摆放。两个兄弟框之间的垂直距离取决于'margin'属性。在同一个块格式化上下文中，相邻的块级框之间的垂直外边距会出现折叠。

在块格式化上下文中，每一个`元素左外边`与`包含块`的左边相接触（对于从右到左的格式化，右外边接触右边），即使存在浮动也是如此（尽管一个元素的内容区域会由于浮动而压缩），除非这个元素也创建了一个新的block formatting context。

**现实意义**
Block formatting context 表现的很像普通的块框，那么它比较特殊的地方在哪里呢？
1. 可以包含浮动元素
2. 不被浮动元素覆盖
3. 阻止父子元素的 margin 折叠


### 行内格式化上下文（inline formatting contexts）

**什么是行框**

在行格式化上下文中，框会从包含块的顶部开始，一个接一个地水平摆放。摆放这些框的时候，它们在水平方向上的外边距(margin)、边框(border)、内边距(padding)所占用的空间都会被考虑在内。在垂直方向上，这些框可能会以不同形式来对齐：它们可能会把底部或顶部对齐，也可能把其内部的文本基线对齐(vertical-align属性控制)。能把在一行上的框都完全包含进去的一个矩形区域，被称为该行的`行框(line box)`。

```html
<p style="background-color:silver; font-size:30px;">TEXT1<span style="border:3px solid blue;">text in span</span>great1<em style="border:3px solid red;">thx a lot</em>bee<strong style="border:3px solid green;">give me 5!</strong>Aloha!</p>
```

<p style="background-color:silver; font-size:30px;">TEXT1<span style="border:3px solid blue;">text in span</span>great1<em style="border:3px solid red;">thx a lot</em>bee<strong style="border:3px solid green;">give me 5!</strong>Aloha!</p>

以上代码中，无换行符及空格，共形成了7个行内框。行框的宽度由它的包含块和其中的浮动元素决定。高度的确定由行高度计算规则决定，后面会介绍。

**行内框在行框中垂直方向上的对齐**
行框的高度总是足够容纳所包含的所有框。不过，它可能高于它包含的最高的框（例如，框对齐会引起基线对齐）。当一个框 B 的高度小于包含它的行框的高度时，B 在行框中垂直方向上的对齐决定于 ‘vertical-align’ 特性。 ‘vertical-align’ 默认值为基线( ‘baseline  ’)对齐。

```html
<p style="background-color:silver; width:500px; ">
    <span style="border:1px solid blue; font-size:50px;">text in span</span>
    <em style="border:1px solid yellow; font-size:30px; vertical-align:top;">great1</em>
</p>
```

<p style="background-color:silver; width:500px; "> <span style="border:1px solid blue; font-size:50px;">text in span</span> <em style="border:1px solid yellow; font-size:30px; vertical-align:top;">great1</em> </p>

EM所形成的行内框内容的顶端与行中最高元素的顶外边界对齐(vertical-align:top)。



**行内框可能被分割**
当几个行级框在水平方向上无法塞得进同一个行框时，它们会被分布在两个或多个垂直堆放的行框中。行框会以既没有垂直间距,也没有重叠的方式被垂直堆放起来。

如果一个行内框超出包含它的行框的宽度，它会被分割成几个框，并且这些框会被分布到几个行框内。如果一个行框不能被分割（例如，行内框只包含单个字符，或者语言特殊的断字规则不允许在行内框里换行，或者行内框受到带有nowrap或pre值的 ‘white-space’ 特性的影响），这时，行内框会溢出行框。
如果一个行内框被分割，margin、padding 和 border 在所有分割处没有视觉效果。
行内框还可能由于双向文本处理（bidirectional text processing）而在同一个行框内被分割为好几个框。
修改上面例子中 P 元素的宽度为100px：

```html
<p style="background-color:silver; width:100px; ">
    <span style="border:1px solid blue; font-size:50px;">text in span</span>
    <em style="border:1px solid yellow; font-size:30px; vertical-align:top;">great1</em>
</p>
```

<p style="background-color:silver; width:100px; "> <span style="border:1px solid blue; font-size:50px;">text in span</span> <em style="border:1px solid yellow; font-size:30px; vertical-align:top;">great1</em> </p>

发现，因为行框宽度限制(100px)，第一个 SPAN 元素形成的行内框，被分割成了3段。


**行框的范围**
通常，行框的左边接触到其`包含块`的左边，右边接触到其`包含块`的右边。然而，浮动元素可能会处于包含块边缘和行框边缘之间。总之，尽管在相同的行内格式化上下文中的行框通常拥有相同的宽度（包含块的宽度），它们可能会因浮动元素缩短了可用宽度，而在宽度上发生变化。同一行内格式化上下文中的行框通常高度不一样（如，一行包含了一个比较高的图形，而其它行只包含文本）。
```html
<p style="background-color:silver; width:500px;overflow:hidden; ">
    <span style="border:1px solid blue; font-size:50px; float:left;">FLOAT</span>
    <em style="border:1px solid yellow; font-size:30px;">great1</em>
    <span style="border:1px solid yellow;">good</span>
</p>
```

<p style="background-color:silver; width:500px;overflow:hidden; "> <span style="border:1px solid blue; font-size:50px; float:left;">FLOAT</span> <em style="border:1px solid yellow; font-size:30px;">great1</em> <span style="border:1px solid yellow;">good</span> </p>

**行内框的水平对齐**
当一行中行内框宽度的总和小于包含它们的行框的宽，它们在水平方向上的对齐，取决于`text-align` 特性。如果其值是 `justify`，用户端也可以拉伸行内框(除了 inline-table 和 inline-block 框)中的空间和文字。
```html
<p style="background-color:silver; width:500px;overflow:hidden; text-align:center; ">
    <span style="border:1px solid blue; font-size:50px; float:left;">FLOAT</span>
    <em style="border:1px solid yellow; font-size:30px;">great1</em>
    <span style="border:1px solid yellow;">good</span>
</p>
```

可见，对齐的时候是根据行框(line box)的宽度，居中对齐。

**空的行内框应该被忽略**
不包含文本，保留空白符，margin/padding/border 非0的行内元素，以及其他常规流中的内容(比如，图片，inline blocks 和 inline tables)，并且不是以换行结束的行框，必须被当作零高度行框对待。就 margin 折叠而言，这种行框必须被忽略。
```html
<div style="border:1px solid red; width:100px;height:100px;margin-bottom:50px;">DIV1</div>
<span><em><strong></strong></em></span>
<div style="border:1px solid red; width:100px;height:100px;margin-top:50px;">DIV2</div>
```

<div style="border:1px solid red; width:100px;height:100px;margin-bottom:50px;">DIV1</div> <span><em><strong></strong></em></span><div style="border:1px solid red; width:100px;height:100px;margin-top:50px;">DIV2</div>

可见，span 和其中的空`行内框`都被忽略。


### 常规流中的相对定位

**相对对定位元素(position:relative)在常规流中的占位是未偏移前的位置**
一旦一个框按照`常规流(normal flow)`或者是`浮动(float)`得到定位，它还可以相对该位置而偏移。这就是相对定位。按照这种方式偏移一个框(B1)不会对后续的框(B2)有影响：
● B2在定位时，就好象B1没有发生偏移一样。
● B1偏移后，B2不会重新定位。

也就是说，B2只认没有偏移之前的B1，B1的偏移不对B2产生任何影响，相对定位的元素，是处于常规流中的，这点需要注意，另外，相对定位是相对于元素的自身定位，并且，在常规流中还占据原来的位置。这也意味着相对定位可能产生框的重叠。

**相对定位元素溢出包含块时，应由浏览器提供滚动条**
然而，如果相对定位引起overflow:auto 或 overflow:scroll 框的溢出，浏览器必须允许用户访问内容，即，需要创建需要的滚动条，这可能会影响布局。
例：
```html
<div style="width:100px; height:100px; overflow:auto; border:2px solid blue;">
    <div style="width:20px; height:20px; background-color:red; position:relative; top:100px; left:100px;">A</div>
</div>
```

<div style="width:100px; height:100px; overflow:auto; border:2px solid blue;"> <div style="width:20px; height:20px; background-color:red; position:relative; top:100px; left:100px;">A</div> </div> 

其中，红色的小块 A 定位的时候，已经超出外面蓝色框的显示范围了，已经溢出。根据标准，应该出现滚动条，以保证用户可以正常的访问 A 中的内容。


**相对定位元素的尺寸**
相对定位元素的尺寸，会保持它在常规流中的尺寸。包括换行以及原来为它保留的位置。


**如何偏移以及计算后的值**
对于一个相对定位的元素，’left’ 和 ‘right’ 会水平的位移框而不会改变它的大小。’left’会将框向右移动，’right’会将框向左移动。由于 ‘left’ 或者 ‘right’ 不会造成框被拆分或者拉伸，所以，计算后的值(computed value)总是：left = -right。

1) 如果 left 和 right 的值都是 ‘auto’ （它们的初始值），计算后的值(computed value)为 0（例如，框区留在其原来的位置）。
2) 如果 left 为 ‘auto’，计算后的值(computed value)为 right 的负值（例如，框区根据 right 值向左移）。
3) 如果 right 被指定为 ‘auto’，其计算后的值(computed value)为 left 值的负值。
```html
<div style="width:20px; height:20px; background-color:red; position:relative; left:100px;"></div>
```
如上述代码中，DIV 元素是相对定位的元素，它的left 值是 ‘100px’， right 没有设置，默认为”auto”，那么，right 特性计算后的值应该是 -left，即’right:-100px’。

4) 如果 left 和 right 都不是 auto，那么定位就显得很牵强，其中一个不得不被舍弃。如果包含块的 direction 属性是 ‘ltr’，那么 left 将获胜，right 值变成 "-left"。如果包含块的 direction 属性是 ‘rtl’，那么 right 获胜，left 值将被忽略。
```html
<div style="width:100px; height:100px; overflow:auto; border:1px solid blue;">
    <div style="width:20px; height:20px; background-color:red; position:relative; left:60px; right:80px;"></div>
</div>
```


top 和 bottom 属性将相对定位元素向上或者向下移动，而不改变其大小。top 把框向下移动，而 bottom 将其向上移动。由于 top 和 bottom 没有造成框被拆分或者拉伸，计算值总是 top=-bottom，如果两个都是auto，其计算值就都是0，如果其中之一是auto，它就是另一个的负值。如果都不是auto，bottom被忽 略（例如，bottom的计算值会是top值的负值）。
注意：在脚本环境中，动态移动相对定位框区能够产生动画效果（见“visibility属性”部分）。虽然 相对定位可以用于创建上标或者下标，行高并不会被自动调整以适应定位需要。
















