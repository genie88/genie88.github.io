title: 移动H5页面开发系列——part5:SVG元素在移动H5页面动画的应用
date: 2015-10-23 09:18:09
tags: "html5"
---
在之前的文章中，我们了解了H5移动页面的主要特点，适用场景和设计技巧，也欣赏、学习了一些经典的H5移动页面案例，本文将重点分析下H5移动页面的换场动画的实现原理和技巧。
![genie.github.io](/assets/57.png)
<!--more--> 

### 什么是SVG
SVG是"Scalable Vector Graphics"的简称。中文可以理解成“可缩放矢量图形”。SVG是可缩放矢量图形，1999年由万维网联盟发布,于2013年成为W3C推荐标准。

- SVG是指可伸缩矢量图形
- SVG用来定义用于网络的基于矢量的图形
- SVG使用XML格式定义图形
- SVG图像在放大或缩小（改变尺寸）的情况下，其图形质量不会受受损失
- SVG是W3C的一个标准

### SVG有哪些优势

SVG也是用来图形化的技术，那么它与位图相比有什么优势呢？(随着屏幕多样化的出现，特别是Retina的出现，对于图形在Web中的应用更具挑战性。) 先来看一张示例图：
![svg-1](https://cloud.githubusercontent.com/assets/12219371/10684851/bcd051c8-7984-11e5-9fb1-9885856090ad.png)
从图中可以明显看出，位图与SVG图PK出来的结果。


与其他图像格式相比，使用SVG的优势在于：
- SVG可被非常多的工具读取和修改（比如记事本）
- SVG与JPEG和GIF图像比起来，尺寸更小，且可压缩性更强。
- SVG是可伸缩的
- SVG图像可在任何的分辨率下被高质量地打印
- SVG可在图像质量不下降的情况下被放大
- SVG图像中的文本是可选的，同时也是可搜索的（很适合制作地图）
- SVG可以与Java技术一起运行
- SVG是开放的标准
- SVG文件是纯粹的XML


### 浏览器中如何使用SVG元素
要在浏览器中显示（前提是浏览器支持），可以通过几种方法来实现：
- 指向SVG文件地址
- 将SVG直接嵌套在HTML中

而将SVG图像嵌入到HTML文件有多种方法：
1. 使用`<iframe>`元素来嵌入SVG图像

```html
<iframe src="path/to/demo.svg" width="200" height="200" ></iframe>
```

2. 使用`<img>`元素来嵌入SVG图像

嵌入SVG图像还可以使用`<img>`元素加载图像一样。只需要将src的属性值更换成SVG图像对应的url，如：
```html
<img src="path/to/demo.svg"  width="300" />
```

3. 将SVG图像作为背景图像嵌入

可以通过background-image属性将SVG图像当做背景图片一样嵌入到HTML页面中。如下面的例子所示：
```css
div {
    background: url('http://www.w3cplus.com/sites/default/files/blogs/2014/1411/girls.svg') no-repeat center;
    background-size : 200px 200px;
}
```

4. 直接使用`<svg>`元素

还可以直接使用`<svg>`元素，通过代码将SVG图像嵌入到HTML代码中。如：
```html
<svg enable-background="new 0 0 145 145" id="Layer_1" version="1.1" viewBox="0 0 145 145" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <g>
        <path d="M49.823,71.043c0.97,0.317,1.875,0.565,2.726,0.76c0.576-0.435,1.197-0.869,1.86-1.301   C51.934,70.79,49.823,71.043,49.823,71.043z" fill="#FFFFFF"/>
    </g>
</svg>
```

> TIPS: 使用`<svg>`元素嵌入SVG图像，还可以通过CSS给其定义一些样式，实现一些样式效果。

5. 使用`<embed>`元素来嵌入SVG图像
(不推荐使用)
早期将SVG图像嵌入到HTML页面中都是通过`<embed>`元素。
```html
<embed src="http://www.w3cplus.com/sites/default/files/blogs/2014/1411/girls.svg" width="300" height="220" type="image/svg+xml" pluginspage="http://www.adobe.com/svg/viewer/install/" />
```

5. 使用`<object>`元素来嵌入SVG图像
(不推荐使用)
```html
<object data="http://www.w3cplus.com/sites/default/files/blogs/2014/1411/girls.svg" width="300" height="200" type="image/svg+xml" codebase="http://www.adobe.com/svg/viewer/install/" />
```

> TIPS: 建议使用`<img>`和`<svg>`这两种方式。当SVG图像是给元素做背景图时，可以使用background-image方式引入。

### SVG的跨浏览器兼容性
<iframe src="http://caniuse.com/svg/embed" width="100%" height="320"></iframe>

### SVG文件的组成
一个独立的SVG文件，也就是平时看到的以扩展名.svg结尾的文件，主要包括：

- XML声明
- `<svg>`根元素包括一个用来描述SVG的XML声明空间。

1. XML声明

XML声明其实和HTML文档的DTD声明是类似的，示例如下：
```xml
<!---类似于HTML文档的DTD声明 <!DOCTYPE html> -->
<?xml version="1.0"?>
```

2. SVG的XML声明空间
第二部分是SVG的XML声明空间，这一部分类似于HTML中的命名空间声明，示例如下：
```xml
<!---类似于HTML文档的HTML中的命名空间声明 <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en"> -->
<svg xmlns="http://www.w3.org/2000/svg">
```


### SVG 中的基本组成元素
SVG 中包含几种预定义的基本几何元素。包括直线、矩形、圆形、椭圆、折线、多边形等。下面的链接给出SVG所有元素的列表。

!(https://developer.mozilla.org/en-US/docs/Web/SVG/Element)

1. 直线

- x1 起点x坐标 
- y1 起点y坐标
- x2 终点x坐标 
- y2 终点y坐标 

SVG中使用`<line>`元素来定义直线。示例如下：
```html
<svg width="300px" height="300px">
  <line x1="100" y1="200" x2="250" y2="50" stroke="#000" stroke-width="5" />
</svg>
```

实际显示效果：
<svg width="300px" height="300px">
  <line x1="100" y1="200" x2="250" y2="50" stroke="#000" stroke-width="5" />
</svg>

2. 矩形

- x 左上角x坐标 
- y 左上角y坐标
- rx x方向的圆角半径
- ry y方向的圆角半径
- width 宽度
- height 高度

SVG中使用`<rect>`元素来定义矩形。示例如下：
```html
<svg width="300px" height="150px">
  <rect x="20" y="20" width="250px" height="125px" rx="5" ry="5" fill="teal" />
</svg>
```

实际显示效果：
<svg width="300px" height="150px">
  <rect x="20" y="20" width="250px" height="125px" rx="5" ry="5" fill="teal" />
</svg>


3. 圆形

- cx 圆心x坐标 
- xy 圆心y坐标
- r 半径

SVG中使用`<circle>`元素来定义圆形。示例如下：
```html
<svg width="300px" height="300px">
   <circle cx="50" cy="50" r="50" fill="teal"></circle>
</svg>
```

实际显示效果：
<svg width="300px" height="300px">
   <circle cx="50" cy="50" r="50" fill="teal"></circle>
</svg>


4. 椭圆形

- cx 圆心x坐标 
- xy 圆心y坐标
- rx x方向半径
- ry y方向半径

SVG中使用`<ellipse>`元素来定义椭圆形。示例如下：
```html
<svg width="300px" height="300px">
   <ellipse cx="150" cy="150" rx="100" ry="75" fill="blue" />
</svg>
```

实际显示效果：
<svg width="300px" height="300px">
   <ellipse cx="150" cy="150" rx="100" ry="75" fill="blue" />
</svg>

5. 多边形

我们可以通过在points属性上的多组 x-y 坐标点来定义我们的多边形元素。这些坐标点通过直线线段来连接
SVG中使用`<polygon>`元素来定义多边形。示例如下：
```html
<svg width="300px" height="150px">
   <polygon points="0,50 50,0 150,0 200,50 150,100 50,100" fill="teal"></polygon>
</svg>
```

实际显示效果：
<svg width="300px" height="150px">
   <polygon points="0,50 50,0 150,0 200,50 150,100 50,100" fill="teal"></polygon>
</svg>

6. 折线

SVG中使用`<polyline>`元素来定义多边形，定义方式与多边形类似。示例如下：
```html
<svg width="300px" height="150px">
   <polyline points="10 10, 50 50, 75 175, 175 150, 175 50, 225 75, 225 150, 300 150" fill="none" stroke="#000"/>
</svg>
```

实际显示效果：
<svg width="300px" height="150px">
   <polyline points="10 10, 50 50, 75 175, 175 150, 175 50, 225 75, 225 150, 300 150" fill="none" stroke="#000"/>
</svg>


### SVG 中的路径
路径( Path )比基本图形更强大和灵活，可以用来创建任何一个基本图形。使用路径你可以创建直线和曲线，也可以把它们连接起来，组成其它的形状。你可以结合两者来创建复杂的路径和子路径。路径可以被填充、描边或者用于剪裁其他元素。它们可以同时做这三种效果甚至更多。

以下是一个路径的使用示例，
```html
<svg width="600" height="400">
  <path d="M 50 50 l 0 300 l 200 0 l 0 -300 l -200 0" fill="none" stroke="#000" stroke-width="2px" />
</svg>
```

<svg width="600" height="400">
  <path d="M 50 50 l 0 300 l 200 0 l 0 -300 l -200 0" fill="none" stroke="#000" stroke-width="2px" />
</svg>

路径(d)可以使用不同的指令，移动到一个新的点，然后绘制不同的直线和曲线。下面将重点介绍这些指令。
1. 直线指令

这里有五种不同的直线指令，你可以使用它们来创建路径。

- moveto(M 或 m):移动到新的位置
- lineto(L 或 l):从当前坐标画一条直线到一个新坐标
- horizontal lineto(H 或 h):画一条水平线到新坐标
- vertical lineto(V 或 v):画一条垂直线到新坐标
- closepath(Z 或 z):关闭当前路径

> TIPS:  实际应用中使用指令字母即可。指令字母大写表示坐标位置是绝对位置，指令字母小写表示坐标位置时相对位置。

2. 曲线指令



### SVG元素的样式属性

SVG元素不同于普通的HTML元素，具有特殊的一些样式属性。这些属性的声明可以通过SVG元素属性的方式直接声明，也可以通过CSS样式表中进行声明。下面的链接中给出了所有的可用属性列表：
!(https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute)

fill:元素的填充颜色
fill-opacity:元素的填充颜色透明度
stroke:元素的笔画颜色
stroke-width:元素的笔画宽度
stroke-opacity:元素的笔画颜色透明度


### 几个重要的 SVG 概念
［参考链接： http://www.zhangxinxu.com/wordpress/2014/08/svg-viewport-viewbox-preserveaspectratio/］
`viewport`、`viewBox`和`preserveAspectRatio`是SVG中基础而且必须了解的几个部分。

1. viewport

表示SVG可见区域的大小，或者可以想象成舞台大小，画布大小。SVG中超出视窗边界的区域会被裁切并且隐藏。
```
<svg width="500" height="300"></svg>
```

2. viewBox属性
viewBox顾名思意是“视区盒子”的意思, 直观的解释就是我们拿一个放大倍数为1.0的方形放大镜来观察svg的一部分视野，然后讲这个视野 铺满整个viewport。

viewBox属性接收四个参数值，包括：`<min-x>`, `<min-y>`, `width` 和 `height`。
`<min-x>` 和 `<min-y>` 值决定viewBox的左上角，width和height决定视窗的宽高。这里要注意视窗的宽高不一定和父`<svg>`元素的宽高一样。`<width>`和`<height>`值为负数是不合法的。值为0的话会禁止元素的渲染。

> TIPS: 注意视窗的宽度也可以在CSS中设置为任何值。例如：设置width:100%会让SVG视窗在文档中自适应。无论viewBox的值是多少，它会映射为外层SVG元素计算出的宽度值。

示例如下：
```html
<svg width="400" height="300" viewBox="0,0,40,30" style="border:1px solid #cd0000;">
    <rect x="10" y="5" width="20" height="15" fill="#cd0000"/>
</svg>
```

3. preserveAspectRatio
preserveAspectRatio属性的值为空格分隔的两个值组合而成。例如 ：
```js
preserveAspectRatio="xMidYMid meet"
```
第1个值表示，viewBox如何与Viewport对齐；
|--|--|
| 值 | 含义|
|xMin|viewport和viewBox左边对齐|
|xMid|viewport和viewBox x轴中心对齐|
|xMax|viewport和viewBox右边对齐|
|YMin|viewport和viewBox上边缘对齐。注意Y是大写。|
|YMid|viewport和viewBox y轴中心点对齐。注意Y是大写。|
|YMax|viewport和viewBox下边缘对齐。注意Y是大写。|

第2个值表示，如何维持高宽比（如果有）。
|--|--|
| 值 | 含义|
|meet|保持纵横比缩放viewBox适应viewport|
|slice|保持纵横比同时比例小的方向放大填满viewport|
|none|扭曲纵横比以充分适应viewport|

为了更形象化，可以观看互动演示案例
http://sarasoueidan.com/demos/interactive-svg-coordinate-system/index.html

### SVG 中的坐标系统

［前方高能，注意警戒!!］
［前方高能，注意警戒!!］
［前方高能，注意警戒!!］

理解了SVG的viewport等概念之后，我们来深入了解SVG的从标系统。SVG的坐标系统分为三种类型：
- 初始坐标系统
- 转换坐标系统
- 嵌套坐标系统


1. 初始坐标系统

**初始视窗坐标系** 是一个建立在视窗(VIEWPORT)上的坐标系。原点(0,0)在视窗的左上角，X轴正向指向右，Y轴正向指向下，初始坐标系中的一个单位等于视窗中的一个"像素"（更确切的说是一个单位）。这个坐标系统类似于通过CSS盒模型在HTML元素上建立的坐标系。

**初始用户坐标系** 是通过VIEWBOX建立在SVG画布上的坐标系。这个坐标系一开始和初始视窗坐标系完全一样-它自己的原点位于视窗左上角，x轴正向指向右，y轴正向指向下。使用viewBox属性，初始用户坐标系统-也称当前坐标系，或使用中的用户空间-可以变成与视窗坐标系不一样的坐标系。如下图所示：

> 初始用户坐标系统-也称当前坐标系，或使用中的用户空间-可以变成与视窗坐标系不一样的坐标系。

假设有一个SVG:
```html
<svg width="300" height="300">
</svg>
```
那么这个SVG的大小是300*300，其是由坐标(0,0)、(300，0)、(300,300)和(0,300)组成的一个矩形画布：

> TIPS: 这里没有设置具体的单位值，表示的就是SVG画布大小是300*300个单位，默认情况下就是px。

为了让大家更好理解SVG最初坐标，来看个示例。示例中，创建了一个300*300像素(px)的SVG，然后使用<rect>在<svg>中绘制了一个矩形，这个矩形的起始点是(20,20)，其宽度是100px，高度是50px。如下：
```html
<svg width="300" height="300">
  <rect x="20" y="20" width="100" height="50" style="stroke: #f36; fill: rgba(123,123,23,.5);"/>
</svg>
```
实际的效果如下：
<svg width="300" height="300">
  <rect x="20" y="20" width="100" height="50" style="stroke: #f36; fill: rgba(123,123,23,.5);"/>
</svg>

到现在为止，我们还没有声明viewBox属性值。SVG画布的用户坐标系统和视窗坐标系统完全一样。

下图中，视窗坐标系的"标尺"是灰色的，用户坐标系（viewBox）的是蓝色的。由于它们在这个时候完全相同，所以两个坐标系统重合了。
![initial-coordinate-systems](https://cloud.githubusercontent.com/assets/12219371/10686536/a9fc6ad8-7997-11e5-8ddc-02edc3ed0b82.jpg)

上面SVG中的鹦鹉的外框边界是200个单位（这个例子中是200个像素）宽和300个单位高。鹦鹉基于初始坐标系在画布中绘制。

> **新用户空间**（即，新当前坐标系）也可以通过在容器元素或图形元素上使用transform属性来声明变换。

可以使用viewBox属性声明自己的用户坐标系。如果你选择的用户坐标系统和视窗坐标系统宽高比（高比宽）相同，它会延伸来适应整个视窗区域。然而，如果你的用户坐标系宽高比不同，你可以用preserveAspectRatio属性来声明整个系统在视窗内是否可见，你也可以用它来声明在视窗中如何定位。

回顾之前所讲的ViewBox四个参数：`<min-x>`, `<min-y>`, `width` 和 `height` 。其中设置width和height可以分别改变X方向和Y方向的坐标系比例，`<min-x>`和`<min-y>`则可以讲用户坐标系进行X方向和Y方向进行平移变换(类似于css3中点tanslate变换)




2. 转换坐标系统

可以使用transform属性来对元素的坐标系统进行变换。transform属性中使用的变换函数类似于CSS中transform属性使用的CSS变换函数。可用的SVG变换有：矩阵(Matrix), 旋转(Rotate), 缩放(Scale), 移动(Translate), 和倾斜(Skew)。 

```html
 matrix(<a> <b> <c> <d> <e> <f>)

 translate(<tx> [<ty>]) // 可用空格或逗号分隔，默认使用用户坐标系单位

 scale(<sx> [<sy>]) //用空格或者逗号分隔，它们是无单位值。

 skewX(<skew-angle>)  skewY(<skew-angle>) //默认单位是度

 //可选的cx和cy值代表无单位的旋转中心点。如果没有设置cx和cy，旋转点是当前用户坐标系的原点
 rotate(<rotate-angle> [<cx> <cy>]) 
```

要注意的是，transform属性的作用对象是元素所在的坐标系统，而不是元素本身。在SVG规范中，transform属性的作用是 **在被添加的元素上建立新用户空间坐标系（当前坐标系）** (效果与viewBox类似)

实际上，在HTML元素上应用CSS3变换时，也是对HTML元素坐标系发生了变换，当你把变换组合使用时最明显。

HTML和SVG的变换还是有一些不同，主要的不同在于SVG元素和HTML元素的坐标系不同。HTML元素的坐标系建立在元素自身上。而在SVG中，元素的坐标系是 **初始坐标系** 或 **当前用户空间坐标系** 。


也就是说，当你在一个SVG元素上添加transform属性，元素获取当前使用的用户坐标系的一个“副本”。你可以当做给发生变换的元素创建一个新“层”，新层实际上是当前用户坐标系的副本（the viewBox）。然后，元素新的当前坐标系被在transform属性中声明的变换函数改变，因此导致元素自身的变换。这看起来好像是元素在变换后的坐标系中重新绘制。

只有正确理解这一点，才能理解SVG变换的一些特点。

![svg-transforms-fig2](https://cloud.githubusercontent.com/assets/12219371/10689792/4ce89eca-79b0-11e5-9ea7-753edab25d03.png)

请注意，某个变换元素上的当前用户坐标系变换是独立于其他同级变换元素的，也就是说，一个元素的变换并不会改变其他同级元素的当前坐标系。

> TIPS: 组合变换
很多时候你可能想要在一个元素上添加多个变换。添加多个变换意味着“组合”变换。
当变换组合时，最重要的是意识到，和HTML元素变换一样，当这个系统发生了之前的变换后在添加下一个变换到坐标系中。
例如，如果你要在一个元素上添加旋转，接下来移动，移动变换会根据新的坐标系统，而不是初始的没有旋转时的系统。

> TIPS: 嵌套变换和变换的继承性
当变换元素的子元素也需要变换时会发生变换嵌套。添加到子元素上的变换会累积父元素上添加的变换和它本身的变换。
也就是说，子元素自动从父元素上获得变换，最后执行添加在它自身的变换。





3. 嵌套坐标系统

在`<svg>`元素中可以嵌套`<svg>`元素。外面的`<svg>`创建一个Viewport和坐标系统，而且嵌套在里面的`<svg>`也可以创建一个Viewport和坐标系统。这种方式就是在大的画布中绘制一个小的画布，我们就可以使用这种技术实现下面的效果：

```html
<svg width="600px" height="300px" viewBox="0 0 250 250">
  <circle cx="35" cy="35" r="35" style="stroke: black; fill: none;"/>
  <rect x="150" y="50" width="200" height="100" style="stroke: blue; 
        fill: none;"/>
  <svg x="150px" y="50px" width="200px" height="100px" viewBox="0 0 125 125" preserveAspectRatio="xMaxYMax meet">
    <circle cx="35" cy="35" r="35" style="stroke: black; fill: rgba(0,0,0,.5);"/>
  </svg>
</svg>
```

实际的现实效果如下：
<svg width="600px" height="300px" viewBox="0 0 250 250">
  <circle cx="35" cy="35" r="35" style="stroke: black; fill: none;"/>
  <rect x="150" y="50" width="200" height="100" style="stroke: blue; 
        fill: none;"/>
  <svg x="150px" y="50px" width="200px" height="100px" viewBox="0 0 125 125" preserveAspectRatio="xMaxYMax meet">
    <circle cx="35" cy="35" r="35" style="stroke: black; fill: rgba(0,0,0,.5);"/>
  </svg>
</svg>





### SVG 中的属性




### SVG 中的SMIL动画实现

### SVG与CSS3的关系
1. 使用CSS属性变换SVGs

2. 使用CSS属性定义动画




### 结语

(未完，待续)
以上，轻拍。
(EOF)

### 参考文章
1. http://www.w3cplus.com/html5/svg-introduction-and-embedded-html-page.html
2. http://www.w3cplus.com/html5/svg-file-structure.html
