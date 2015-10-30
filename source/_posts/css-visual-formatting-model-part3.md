title: "CSS核心可视化格式模型: 框的生成 part3"
date: 2015-10-29 11:35:04
tags: "CSS"
---
本文描述了CSS 2.1中可能产生的框的类型。在某种程度上，框的类型会影响其在视觉格式化模型中的表现。CSS属性中的`display`属性用来指定框的类型。

我们经常用到块元素、行内元素的概念，那么，到底什么是块元素，什么是行内元素，它们有什么特点，怎么形成的，有什么作用呢？什么是块框，什么又是行内框呢？下面，请大家跟我一起走近W3C标准，看个究竟吧。
<!--more-->
### 块级元素和块框(block box)
`块级元素`是源文档中那些在视觉上被格式化为块（如：段落）的元素。某些 'display' 特性的取值会产生块级元素：'block'，'list-item' 和 'table'。


`块级框`是参与块格式化上下文的框。每个块级元素生成一个`主要的块级框`来包含其子框和生成的内容，同时任何定位方案都会与这个主要的框有关。某些块级元素还会在主要框之外产生额外的框：例如“list-item”元素。这些额外的框会相对于主要框来放置。

**除了table框，和可替换元素，一个块级框同时也是一个块容器框**。一个`块容器框`要么只包含`块级框`，要么创建一个`行格式化上下文`而只包含行`内级框`。

并非所有的`块容器框`都是`块级框`：不可替换的行内块和不可替换的table cell也是`块容器`但不是`块级框`。是`块级框`的`块容器`称作`块框`。

三个术语：块级框（block-level box）、块容器框（block container box）和块框（block box）在意义明确的时候简称为块（block）。

![block_box](https://cloud.githubusercontent.com/assets/12219371/10836964/17376f9c-7eef-11e5-91a9-5545f5b4387c.jpg)


`块级元素`（不包含 table），会形成仅包含`块框`或仅包含`行内框`的`主块框`( principal block box )。`主块框`会为子孙元素建立`包含块`，生成内容，并且也是涉及所有定位体系的框。`主块框`参与block formatting context。

> 某些块级元素在主块框之外生成额外的框, 这些额外的框根据主块框来定位。 例如，`<li>` 元素


### 匿名块框

```html
<DIV>
  Some text
  <P>More text</P>
</DIV>
```

<DIV style="border: 1px solid #ff0;"> <p style="border: 1px solid #f00;">Some text</p> <P style="border: 1px solid #f0f;">More text</P> </DIV>

上面的代码形成了三个框，分别是：div对应的块框，P对应的块框，以及包含 “Some text” 的`匿名块框`。

换句话说：如果一个`块框`（如上例中为DIV生成的框）在其中包含另外一个块框（如上例中的P），那么，我们强迫它只能包含块框。因此，上面的 “Some text” 被强制加到一个匿名的块框里面。

当一个`行内框`包含一个`块框(block box)`时，这个`行内框 (inline box)` （和与它处于同一`行框(line box)`内的祖先行内框）会围绕着`块框`被截断。断点之前和之后的`行框(line boxes)`会被分别封闭到`匿名的块框`里，并且，这个`块框`会成为这些`匿名块框`的兄弟框。当这样的行内框受到相对定位的影响时，相对定位也会影响块框。

来看个实际的行框包含一个块框的例子：
```html
<div style="width: 200px; border: 1px solid gold;">
   <span style="border: 1px solid red;">This is anonymous text before the P.
       <P style="width: 100px; border: 1px solid green;">This is the content of P.</P>
         This is anonymous text after the P.
   </span>
</div>
```

<div style="width: 200px; border: 1px solid gold;"> <span style="border: 1px solid red;">This is anonymous text before the P. <P style="width: 100px; border: 1px solid green;">This is the content of P.</P> This is anonymous text after the P. </span> </div>

上述代码中，SPAN 元素包含匿名文本区块 C1，后跟块级元素 P ，最后是匿名文本区块 C2。最后的框(boxes)是围绕 SPAN 的DIV形成的块框，包含 C1 的匿名块框，P 的块框，和另一个包含 C2 的匿名块框。

> 注意，行框(line box)和行内框(inline box)是两个不同的概念，后续会说到行框(line box)。

匿名块框的特性(properties)从包含它的非匿名块框那里继承而来（比如，例1中，匿名块框会继承包含它的 DIV 特性）。不可继承特性会使用初始值。比如，字体，匿名框会从DIV继承，但是margin值会是 0 。

匿名块框不会影响元素的原有特性设置。如例2中 SPAN 设置了 border，产生匿名块框后，C1 C2还是被红色的边框包围。

注意，块框会占据一整行。


### 行级元素和行内框(inline box)

`行级元素`是源文档中那些不形成新的内容块的元素；内容在行内分布（如，段落内着重的文本`em`, `span`, `i`, 行内图形 `img`等等）。某些'display'特性的值形成行内元素：'inline'，'inline-table'和 'inline-block'。`行级元素`生成`行级框`，而这些框会参与某个`行格式化上下文`。

1）一个行级框以其内容参与了包含它的行格式化上下文则可称之为`行内框`。 例如'display'值是'inline'的非替换元素会生成一个行内框。

2）一个行级框以单一不透明框的形式(不可拆分, 当成一个整体)参与了包含它的行格式化上下文则可称之为`原子行级框`。例如可替换的行级元素、行内块元素'inline-block'、行内表格元素'inline-table'。



### 匿名行内框

任何直接被包含在一个块容器元素（而不是行内元素）中的文本必须视为匿名行内元素。
在如下的文档中:

```html
<P>Some <EM>emphasized</em> text</P>
```

P元素生成一个`块框`，其内还有几个`行内框`。"emphasized"的框是一个行内元素（`<em>`）产生的行内框，而其它的框（"Some" 和 "text"）是块级元素（P）产生的`行内框`。后者就称为`匿名行内框`，因为它们没有与之相关的行级元素，所以，这些框被叫做`匿名行内框`。

这样的行内框从其父块框那里继承可以继承的属性。非继承属性取它们的初始值。例子中，初始匿名框的颜色继承自P，而背景是透明的。

空格内容会根据 'white-space' 特性被压缩，不会创建任何匿名行内框。

`匿名行内框`和`匿名块框`可以被统称为`匿名框`。

###  控制框与display属性

####'display'特性
值：      inline | block | list-item | run-in | compact | marker |table | inline-table | table-row-group | table-header-group |table-footer-group | table-row | table-column-group | table-column |table-cell | table-caption | none | inherit
初始值：    inline
适用于：    所有元素
可否继承：   否
百分比：    N/A
媒介：     所有

- block
该值使一个元素生成一个块框。
- inline-block
该值使一个元素生成一个块框，自身在文档流中像一个行内元素，跟替换元素相似。元素的内部按照块框格式化，自身按照一个行内替换元素格式化。
- inline
该值使一个元素生成一个或多个行内框。
- list-item
该值使一个元素（如HTML中的LI）生成一个原始块框和一个列表项行内框。要了解列表和列表格式化的信息，请参见列表一节。
- none
该值使一个元素在格式化结构中不显示（换言之，该元素对布局没有影响）。子孙元素也不产生任何框；该行为不能由设置子孙元素的 'display' 属性而被覆盖。

> 请注意 'none' 的显示特性并不生成一个不可见的框；它根本不生成框。CSS包含了机制使一个元素能够在格式化结构中生成框而影响格式化，但本身不可见( visible 特性)。

