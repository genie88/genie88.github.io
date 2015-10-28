title: "移动H5页面开发系列——part5:SVG元素在移动H5页面动画的应用"
date: 2015-10-23 09:18:09
tags: "html5"
---
本文包括SVG的概要知识介绍，以及SVG在H5移动页面的应用介绍。
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

<div><svg width="300px" height="300px"><line x1="100" y1="200" x2="250" y2="50" stroke="#000" stroke-width="5"/></svg></div>



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
<div><svg width="300px" height="150px"><rect x="20" y="20" width="250px" height="125px" rx="5" ry="5" fill="teal"/></svg></div>



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
<div><svg width="300px" height="300px"><circle cx="50" cy="50" r="50" fill="teal"></circle></svg></div>



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
<div><svg width="300px" height="300px"><ellipse cx="150" cy="150" rx="100" ry="75" fill="blue" /></svg></div>


5. 多边形

我们可以通过在points属性上的多组 x-y 坐标点来定义我们的多边形元素。这些坐标点通过直线线段来连接
SVG中使用`<polygon>`元素来定义多边形。示例如下：
```html
<svg width="300px" height="150px">
   <polygon points="0,50 50,0 150,0 200,50 150,100 50,100" fill="teal"></polygon>
</svg>
```

实际显示效果：
<div><svg width="300px" height="150px"><polygon points="0,50 50,0 150,0 200,50 150,100 50,100" fill="teal"></polygon></svg></div>

6. 折线

SVG中使用`<polyline>`元素来定义多边形，定义方式与多边形类似。示例如下：
```html
<svg width="300px" height="150px">
   <polyline points="10 10, 50 50, 75 175, 175 150, 175 50, 225 75, 225 150, 300 150" fill="none" stroke="#000"/>
</svg>
```

实际显示效果：
<div><svg width="300px" height="150px"><polyline points="10 10, 50 50, 75 175, 175 150, 175 50, 225 75, 225 150, 300 150" fill="none" stroke="#000"/></svg></div>


### SVG 中的路径
路径( Path )比基本图形更强大和灵活，可以用来创建任何一个基本图形。使用路径你可以创建直线和曲线，也可以把它们连接起来，组成其它的形状。你可以结合两者来创建复杂的路径和子路径。路径可以被填充、描边或者用于剪裁其他元素。它们可以同时做这三种效果甚至更多。

以下是一个路径的使用示例，
```html
<svg width="600" height="400">
  <path d="M 50 50 l 0 300 l 200 0 l 0 -300 l -200 0" fill="none" stroke="#000" stroke-width="2px" />
</svg>
```

<div><svg width="600" height="400"><path d="M 50 50 l 0 300 l 200 0 l 0 -300 l -200 0" fill="none" stroke="#000" stroke-width="2px"/></svg></div>

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

曲线指令一共有三组，和直线指令一样，指令字母大写表示坐标位置是绝对坐标，指令字母小写表示坐标位置是相对坐标。

- 三次贝塞尔曲线指令 (C, c, S, s)
- 二次贝塞尔曲线指令 (Q, q, T, t)
- 椭圆弧线 (A, a)

#### 2.1 三次贝塞尔曲线指令

三次贝塞尔曲线指令的格式为：
```sh
C (or c) x1,y1 x2,y2 x,y
```

这里,
`x1`,`y1` 是曲线起点的控制点坐标
`x2`,`y2` 是曲线终点的控制点坐标
`x`,`y` 是曲线的终点坐标

曲线的起点是上一条指令的终点，所以我们不需要再次设置。示例如下：
```html
<svg width="600" height="300">
  <path d="M100,200
           C100,100  400,100  400,200"
   fill="none" stroke="#000" stroke-width="2px" />
</svg>
```

<div><svg width="600" height="300"><path d="M100,200 C100,100  400,100  400,200" fill="none" stroke="#000" stroke-width="2px"/></svg></div>

#### 2.2 二次贝塞尔曲线指令

二次贝塞尔曲线指令只需要一个控制点，同时作为起点控制点和终点控制点。
```sh
Q (or q) x1,y1 x,y
```

这里,
`x1`,`y1` 是曲线起点和终点的控制点坐标
`x`,`y` 是曲线的终点坐标

```html
<svg width="600" height="300">
    <path d="M100,200
             Q250,100 400,200"
     fill="none" stroke="#000" stroke-width="2px" />
</svg>
```

<div><svg width="600" height="300"><path d="M100,200 Q250,100 400,200" fill="none" stroke="#000" stroke-width="2px"/></svg></div>

二次贝塞尔曲线指令也有一个快捷方法，(T 或 t)指令可以用来平滑多条曲线之间的连接。它和三次贝塞尔曲线指令中的快捷方式(S 或 s)是同样的效果，也有助于通过对称的控制点来平滑地开始绘制第二条曲线。

```html
<svg width="600" height="300">
  <path d="M100,200
           Q250,100 400,200
           T600 200"
    fill="none" stroke="#000" stroke-width="2px" />
</svg>
```

#### 2.3 椭圆弧线

椭圆弧线指令用于绘制一段椭圆片段。若rx和ry的值相同，则绘制出圆。
```sh
A (or a) rx ry  x-axis-rotation  large-arc-flag  sweep-flag  x y
```

这里,
`x`,`y` 是弧线的终点
`rx` 是弧线在x轴方向的半径
`ry` 是弧线在y轴方向的半径
`x-axis-rotation` 是与x轴夹角的度数

在下面这个示例中，看起来好像有两个相同尺寸的彩色椭圆，但是这其实是四段不同的弧线：
```html
<svg width="600" height="300">
<path d="M250,100  A120,80 0 0,0 250,200"
    fill="none" stroke="red" stroke-width="5" />
<path d="M250,100  A120,80 0 1,1 250,200"
    fill="none" stroke="green" stroke-width="5"/>
<path d="M250,100  A120,80 0 1,0 250,200"
    fill="none" stroke="purple" stroke-width="5"/>
<path d="M250,100  A120,80 0 0,1 250,200"
    fill="none" stroke="blue" stroke-width="5"/>
</svg>
```

<div><svg width="600" height="300"><path d="M250,100  A120,80 0 0,0 250,200" fill="none" stroke="red" stroke-width="5" /><path d="M250,100  A120,80 0 1,1 250,200" fill="none" stroke="green" stroke-width="5"/><path d="M250,100  A120,80 0 1,0 250,200" fill="none" stroke="purple" stroke-width="5"/>
<path d="M250,100  A120,80 0 0,1 250,200" fill="none" stroke="blue" stroke-width="5"/></svg></div>

### SVG 中的标记（Marker）
SVG 连接标记（markers）用于标记一条线或路径的开始、中间个结束位置。你可以在路径的开始处使用圆形或方形表示，在路径的结束处使用一个三角箭头表示。
```html
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
      <!-- 定义一个圆形标记 -->
      <marker id="markerCircle" markerWidth="8" markerHeight="8" refX="5" refY="5">
          <circle cx="5" cy="5" r="3" style="stroke: none; fill:#000000;"/>
      </marker>
      <!-- 定义一个箭头（三角形）标记 -->
      <marker id="markerArrow" markerWidth="13" markerHeight="13" refX="2" refY="6"
             orient="auto" markerUnits="strokeWidth">
          <path d="M2,2 L2,11 L10,6 L2,2" style="fill: #000000;" />
      </marker>
  </defs>
  <path d="M100,10 L150,10 L150,60"
        style="stroke: #6666ff; stroke-width: 1px; fill: none;
                     marker-start: url(#markerCircle);  <!-- 在Path路径中使用标记 -->
                     marker-end: url(#markerArrow);
                   "/>
</svg>        
```

<div><svg xmlns="http://www.w3.org/2000/svg"><defs><marker id="markerCircle" markerWidth="8" markerHeight="8" refX="5" refY="5"><circle cx="5" cy="5" r="3" style="stroke: none; fill:#000000;"/></marker><marker id="markerArrow" markerWidth="13" markerHeight="13" refX="2" refY="6" orient="auto" markerUnits="strokeWidth"><path d="M2,2 L2,11 L10,6 L2,2" style="fill: #000000;" /></marker></defs><path d="M100,10 L150,10 L150,60" style="stroke: #6666ff; stroke-width: 1px; fill: none;marker-start: url(#markerCircle);marker-end: url(#markerArrow);"/></svg></div>

> `marker-start`, `marker-mid`, `marker-end` 这三个CSS属性会将标记分别放置在路径的开始、中间和结束位置。

> 可以设置markerUnits="strokeWidth" 使得标记进行缩放来适应路径描边的大小


### SVG 中的clipPath

SVG剪裁路径是指根据指定的路径或形状来剪裁SVG图形。应用了剪裁路径的图形，在剪裁路径内部的图形可以被显示出来，在剪裁路径之外的图形会被隐藏。

来看一个简单例子：
```html
<defs>
  <clipPath id="clipPath">
      <rect x="15" y="15" width="40" height="40" />
  </clipPath>
</defs>
<circle cx="25" cy="25" r="20"
      style="fill: #0000ff; clip-path: url(#clipPath); " />   
```
这个例子定义了一个矩形的剪裁路径（<clipPath>中的<rect>元素）。在后面的SVG圆形中，通过style属性的clip-path指向了这个剪裁路径。

<div><svg><defs><clipPath id="clipPath"><rect x="15" y="15" width="40" height="40" /></clipPath></defs> <circle cx="25" cy="25" r="20" style="fill: #0000ff; clip-path: url(#clipPath); "/></svg></div>


> 你可以使用任何图形来作为剪裁路径或者被剪裁的对象。可以是文字、圆形、椭圆、多边形或自定义路径。

### SVG DEFS元素、SYMBOL元素和USE元素
1) DEFS元素
SVG的 `<defs>` 元素用于预定义一个元素使其能够在SVG图像中重复使用。例如你可以将一些图形制作为一个组，并用 `<defs>` 元素来定义它，然后你就可以在SVG图像中将它当做简单图形来重复使用。
```html
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
      <g>
          <rect x="100" y="100" width="100" height="100" />
          <circle cx="100" cy="100" r="100" />
      </g>
  </defs>
</svg>                            
```

> 哪些元素可以被定义为defs中的元素呢？
  1) 任何图形元素，如：rect，line等
  2) g元素
  3) symbol元素

2) SYMBOL元素
SVG `<symbol>`元素用于定义可重复使用的符号。

```html
<svg xmlns="http://www.w3.org/2000/svg" width="500" height="100">
    <symbol id="shape2">
        <circle cx="25" cy="25" r="25" style="fill:#bf55ec;"/>
    </symbol>
    <use xlink:href="#shape2" x="50" y="25" />
</svg>                          
```

3) USE 元素

在`<defs>`元素中定义的图形不会直接显示在SVG图像上。要显示它们需要使用`<use>`元素来引入它们。SVG `<use>`元素可以在SVG图像中多次重用一个预定义的SVG图形，包括 `<g>` 元素和`<symbol>`元素。

`<use>`元素通过 `xlink:href` 属性来引入`<g>`元素。注意在ID前面要添加一个#。在 `<use>` 元素中，通过x和y属性来指定重用图形的显示位置， 通过style属性来重新定义样式。注意在 `<g>` 元素中的图形的定位点都是0,0，在使用 `<use>` 元素来引用它的时候，它的定位点被转换为 `<use>` 元素x和y属性指定的位置。

```html
<svg xmlns="http://www.w3.org/2000/svg">  
  <defs>
    <g id="shape">
        <rect x="50" y="50" width="50" height="50" />
        <circle cx="50" cy="50" r="50" />
    </g>
  </defs>
  <use xlink:href="#shape" x="50" y="50" />
  <use xlink:href="#shape" x="200" y="50" style="stroke: #00ff00; fill: none;"/> 
</svg> 
```



### SVG元素的样式属性


SVG元素不同于普通的HTML元素，具有特殊的一些样式属性。这些属性的声明可以通过SVG元素属性的方式直接声明，也可以通过CSS样式表中进行声明。下面的链接中给出了所有的可用属性列表：
[官方文档]：http://www.w3.org/TR/SVG11/styling.html

以下是一些CSS2规范之中未定义的，SVG独有的部分样式属性：
fill: 元素的填充颜色
fill-opacity: 元素的填充颜色透明度
stroke: 元素的笔画颜色
stroke-width: 元素的笔画宽度
stroke-linecap: 定义元素顶点样式
stroke-dasharray: 虚线样式虚线长度
stroke-dashoffset: 虚线样式的偏移长度
stroke-linejoin: 定义元素之间的连接点的形状
stroke-opacity: 元素的笔画颜色透明度


可以使用CSS来为SVG图形添加样式。给SVG图形添加样式就是改变它们的外观，可以修改描边颜色和宽度，填充颜色，透明度等等。

> TIPS: SVG图形可以使用的CSS属性和HTML元素可以使用CSS属性稍微有一些不同，但是绝大部分的属性还是相同的。

1) 使用属性来添加CSS样式，例如：
```html
<circle stroke="#000000" fill="#00ff00" />  
```

2) 使用STYLE属性，例如：
```html
<circle style="stroke: #000000; fill:#00ff00;" />       
```


3) 使用内联样式表，例如：
这种使用内联样式表的工作方式和在HTML元素上使用内联样式表是完全相同的。
```html
<svg xmlns="http://www.w3.org/2000/svg">   
    <style type="text/css" >
      <![CDATA[
        circle {
           stroke: #006600;
           fill:   #00cc00;
        }
      ]]>
    </style> 
    <circle  cx="40" cy="40" r="24"/>
</svg>  
```

4) 使用CLASS样式来添加CSS样式，例如：
```html
<svg xmlns="http://www.w3.org/2000/svg">
    <style type="text/css" >
      <![CDATA[
        circle.myGreen {
           stroke: #006600;
           fill:   #00cc00;
        }
       circle.myRed {
       stroke: #660000;
       fill:   #cc0000;
    }
      ]]>
    </style>
    <circle  class="myGreen" cx="40" cy="40"  r="24"/>
    <circle  class="myRed"   cx="40" cy="100" r="24"/>
</svg>  
```

5) 使用外部样式表来添加CSS样式。当你在使用外部样式表的时候，样式表是一个单独的文件，这和CSS外部样式表是相同的。你需要使用下面的语法来将外部样式表引入。例如：
```html
<?xml-stylesheet type="text/css" href="svg-stylesheet.css" ?> 
```

6) 在 HTML 页面中使用 STYLE 标签。如果你将一个 SVG 嵌入到一个 HTML 页面中，你可以在 HTML 页面中使用 style 标签来为 SVG 图形设置样式。这和在HTML页面中对DOM元素设置样式的方式是完全相同的。例如：
```html
<html>
<body>
<style>
  circle {
     stroke: #006600;
     fill  : #00cc00;
  }
</style>
<svg>
  <circle cx="40" cy="40" r="24" />
</svg>
</body>
</html>       
```




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

可以观察不同取值的变化：
![preserveaspectratio](https://cloud.githubusercontent.com/assets/12219371/10748383/917f302a-7c9a-11e5-9506-1c3787bd6c0c.png)

为了更形象化，可以观看互动演示案例
http://sarasoueidan.com/demos/interactive-svg-coordinate-system/index.html

### SVG 中的坐标系统

［前方高能，注意警戒!!］
［前方高能，注意警戒!!］
［前方高能，注意警戒!!］

[官方文档说明]：http://www.w3.org/TR/SVG11/coords.html

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

<div><svg width="300" height="300"><rect x="20" y="20" width="100" height="50" style="stroke: #f36; fill: rgba(123,123,23,.5);"/></svg></div>

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
<svg width="600px" height="300px" viewBox="0 0 250 250"> <circle cx="35" cy="35" r="35" style="stroke: black; fill: none;"/> <rect x="150" y="50" width="200" height="100" style="stroke: blue; fill: none;"/> <svg x="150px" y="50px" width="200px" height="100px" viewBox="0 0 125 125" preserveAspectRatio="xMaxYMax meet"> <circle cx="35" cy="35" r="35" style="stroke: black; fill: rgba(0,0,0,.5);"/> </svg> </svg>

如果你不声明子SVG的x和y属性，它们默认是0。如果你不声明height和width属性，`<svg>`会是父SVG宽度和高度的100%。

除了可以通过嵌套`<svg>`外，也可以使用例如`<use>`, `<symbol>`的元素来建立新的viewport和用户坐标系: 
```
<svg>
    <symbol id="my-symbol" viewBox="0 0 300 200">
        <!-- contents of the symbol -->
        <!-- this content is only rendered when `use`d -->
    </symbol>
    <use xlink:href="#my-symbol" x="?" y="?" width="?" height="?">
</svg>
```


### SVG 中的SMIL动画

SMIL是Synchronized Multimedia Integration Language（同步多媒体集成语言）的首字母缩写简称。SMIL开发组和SVG开发组合作开发了SMIL动画规范，在规范中制定了一个基本的XML动画特征集合。SVG吸收了SMIL动画规范当中的动画优点，并提供了一些SVG继承实现。

SMIL允许你做下面这些事情：
- 动画元素的数值属性（X, Y, …）
- 动画属性变换（平移或旋转）
- 动画颜色属性
- 沿着运动路径运动

> 浏览器对SMIL动画的支持非常的好，它可以在除了IE浏览器和Opera Mini 浏览器之外的所有现代浏览器中工作。完整的支持列表可以查看 Can I Use 网站。如果你需要为 SMIL 动画提供一个回退方法，你可以使用 Modernizr 。如果浏览器不支持 SMIL ，你可以为它们提供一些回退方法。

#### 通过XLINK:HREF指定动画目标

不论使用4个动画元素中的哪一个，你都需要为它指定一个动画目标。可以使用xlink:href属性来指定动画目标。这个属性指向将要执行动画的元素。这个元素必须在当前的SVG文档中。动画元素也可以嵌套在SVG元素中。如果没有为动画元素指定xlink:href属性，那么动画的目标元素就是当前动画元素的直接父元素。

```html
<rect id="cool_shape" ... />
<animate xlink:href="#cool_shape" ... />    
```



#### SVG animation元素及效果概览

SVG animation包含五大元素
1. `<set>`

set意思设置，此元素没有动画效果。可以实现基本的延迟功能。即，可以在特定时间之后修改某个属性值（也可以是CSS属性值）
```html
<svg width="320" height="320" xmlns="http://www.w3.org/2000/svg">
  <g> 
    <text font-family="microsoft yahei" font-size="120" y="160" x="160">
      马
      <set attributeName="x" attributeType="XML" to="60" begin="3s" />
    </text>
  </g>
</svg>
```

<svg width="320" height="320" xmlns="http://www.w3.org/2000/svg"> <g> <text font-family="microsoft yahei" font-size="120" y="160" x="160"> 马 <set attributeName="x" attributeType="XML" to="60" begin="3s" /> </text> </g> </svg>

2. `<animate>`

基础动画元素。实现单属性的动画过渡效果。类似Snap.svg的animate()方法支持的动画效果。类似于CSS3中的transition属性
```html
<svg width="320" height="320" xmlns="http://www.w3.org/2000/svg">
  <g> 
    <text font-family="microsoft yahei" font-size="120" y="160" x="160">
    马
      <animate attributeName="x" from="160" to="60" begin="0s" dur="3s" repeatCount="indefinite" />
    </text>
  </g>
</svg>
```

<svg width="320" height="320" xmlns="http://www.w3.org/2000/svg"> <g> <text font-family="microsoft yahei" font-size="120" y="160" x="160"> 马 <animate attributeName="x" from="160" to="60" begin="0s" dur="3s" repeatCount="indefinite" /> </text> </g> </svg>

3. `<animateColor>` (被废弃)

4. `<animateTransform>`

实现transform变换动画效果的。与CSS3的transform变换及Snap.svg.js中的transform()方法都是一个路数。
```html
<svg width="320" height="320" xmlns="http://www.w3.org/2000/svg">
  <g> 
    <text font-family="microsoft yahei" font-size="80" y="100" x="100">马</text>
    <animateTransform attributeName="transform" begin="0s" dur="3s"  type="scale" from="1" to="1.5" repeatCount="indefinite"/>
  </g>
</svg>
```

<svg width="320" height="320" xmlns="http://www.w3.org/2000/svg"> <g> <text font-family="microsoft yahei" font-size="80" y="100" x="100">马</text> <animateTransform attributeName="transform" begin="0s" dur="3s"  type="scale" from="1" to="1.5" repeatCount="indefinite"/> </g> </svg>

5. `<animateMotion>`

animateMotion元素可以让SVG图形沿着特定的`<path>`路径运动。
```
<svg width="360" height="200" xmlns="http://www.w3.org/2000/svg">
  <text font-family="microsoft yahei" font-size="40" x="0" y="0" fill="#cd0000">马
    <animateMotion path="M10,80 q100,120 120,20 q140,-50 160,0" begin="0s" dur="3s" rotate="auto" repeatCount="indefinite"/>
  </text>
  <path d="M10,80 q100,120 120,20 q140,-50 160,0" stroke="#cd0000" stroke-width="2" fill="none" />
</svg>
```

<svg width="360" height="200" xmlns="http://www.w3.org/2000/svg"> <text font-family="microsoft yahei" font-size="40" x="0" y="0" fill="#cd0000">马 <animateMotion path="M10,80 q100,120 120,20 q140,-50 160,0" begin="0s" dur="3s" rotate="auto" repeatCount="indefinite"/> </text> <path d="M10,80 q100,120 120,20 q140,-50 160,0" stroke="#cd0000" stroke-width="2" fill="none" /> </svg>

#### SVG animation参数详解
参考文献：
http://www.zhangxinxu.com/wordpress/2014/08/so-powerful-svg-smil-animation/
http://www.htmleaf.com/ziliaoku/qianduanjiaocheng/201506222088.html
http://www.htmleaf.com/ziliaoku/qianduanjiaocheng/201506242101.html

1. attributeName = 动画属性的名称

① 可以是元素直接暴露的属性，例如，对于本文反复出现的「马」对应的text元素上的x, y或者font-size; 
② 可以是CSS属性。例如，透明度opacity。

2. attributeType 动画属性的类型

`可选值: “CSS | XML | auto”`

attributeType支持三个固定参数，CSS/XML/auto。用来表明attributeName属性值的列表。x,y以及transform就属于XML, opacity就属于CSS。 auto为默认值，自动判别的意思。

3. from, to, by, values

类似于CSS3中的关键帧定义。
from = `<value>` :  动画的起始值,缺省默认值。
to = `<value>` : 指定动画的结束值。
by = `<value>` : 动画的相对变化值。
values = `<list>` : 用分号分隔的一个或多个值，可以看出是动画的多个关键值点。

也就是from-to动画、from-by动画、to动画、by动画以及values动画。
```html
<svg width="320" height="200" xmlns="http://www.w3.org/2000/svg">
    <text font-family="microsoft yahei" font-size="120" y="150" x="160">
        马
        <animate attributeName="x" values="160;40;160" dur="3s" repeatCount="indefinite" />
    </text>
</svg>
```

4. begin, end

begin指动画开始的时间。

可选值包括:
`time-value| offset-value | syncbase-value | event-value | repeat-value | accessKey-value | media-marker-value | wallclock-sync-value | indefinite`

1) `time-value`: 表示具体的时间值，常见单位有 "h"|"min"|"s"|"ms"，默认单位为s 。时间值还支持 hh:mm:ss 这种写法，因此，`90s` 我们也可以使用 `01:30` 表示。

2) `offset-value`: 表示偏移值，数值前面有`+`或`-`. 应该指相对于 `document` 的 `begin` 值而言。

3) `syncbase-value`: 基于同步确定的值。语法为：`[元素的id].begin/end +/-` 时间值。 就是说借用其他元素的begin值再加加减减，这个可以准确实现两个独立元素的动画级联效果。

OK，看完下面的例子一定会豁然开朗，对于上面的offset-value也会有一定的认知。
```html
<svg width="320" height="200" xmlns="http://www.w3.org/2000/svg">
    <text font-family="microsoft yahei" font-size="120" y="160" x="160">马
        <animate id="x" attributeName="x" to="60" begin="0s" dur="3s" fill="freeze" />
        <animate attributeName="y" to="100" begin="x.end" dur="3s" fill="freeze" />
    </text>
</svg>
```

可以看到，后面 `attributeName` 为 `y` 的元素的 `begin` 值是 `x.end`。 `x.end` 中的 `x` 就是上面一个 `animate` 元素的 `id` 值，而 `end` 是动画元素都有的一个属性，动画结束的时间。因此，`begin="x.end"` 意思就是，当 `id` 为 `x` 的元素动画结束的时候，我执行动画。非常类似于PowerPoint动画的“上一个动画之后”的选项。
当然，我们还可以增加一些偏移值，例如 `begin="x.end-1s"`, 就表示 `id` 为 `x` 的元素动画结束前一秒开始纵向移动。

4) `event-value`: 这个表示与事件相关联的值。类似于PowerPoint动画的“点击执行该动画”。语法是：  `[元素的id].[事件类型] +/- 时间值`。 
```html
<svg id="svg" width="320" height="200" xmlns="http://www.w3.org/2000/svg">
    <circle id="circle" cx="100" cy="100" r="50"></circle>
    <text font-family="microsoft yahei" font-size="120" y="160" x="160">马
        <animate attributeName="x" to="60" begin="circle.click+2s" dur="3s" />
    </text>
</svg>
```

<svg id="svg" width="320" height="200" xmlns="http://www.w3.org/2000/svg"> <circle id="circle" cx="100" cy="100" r="50"></circle> <text font-family="microsoft yahei" font-size="120" y="160" x="160">马 <animate attributeName="x" to="60" begin="circle.click+2s" dur="3s" /> </text> </svg>

支持的事件类型包括：`load`, `focus`, `endEvent`, `repeat` 等

> TIPS: 这类与事件关联的SVG需要内联在页面中。

5) `repeat-value` 指某动画重复多少次结束之后开始执行动画。语法为： `[元素的id].repeat(整数) +/- 时间值`
```html
<svg width="320" height="200" xmlns="http://www.w3.org/2000/svg">
    <text font-family="microsoft yahei" font-size="120" y="160" x="160">马
        <animate id="x" attributeName="x" to="60" begin="0s" dur="3s" repeatCount="indefinite" />
        <animate attributeName="y" to="100" begin="x.repeat(2)" dur="3s" fill="freeze" />
    </text>
</svg>
```

<svg width="320" height="200" xmlns="http://www.w3.org/2000/svg"> <text font-family="microsoft yahei" font-size="120" y="160" x="160">马 <animate id="x" attributeName="x" to="60" begin="0s" dur="3s" repeatCount="indefinite" /> <animate attributeName="y" to="100" begin="x.repeat(2)" dur="3s" fill="freeze" /> </text> </svg>

6) `accessKey-value` 定义快捷键。即按下某个按键动画开始。语法为：`accessKey(character)`。 `character` 表示快捷键所在的字符，举个例子，按下 `s` 键动画开始执行。SVG 代码如下：
```html
<svg width="320" height="200" xmlns="http://www.w3.org/2000/svg">
    <text font-family="microsoft yahei" font-size="120" y="160" x="160">马
        <animate attributeName="x" to="60" begin="accessKey(s)" dur="3s" repeatCount="indefinite" />
    </text>
</svg>
```


7) `wallclock-sync-value`: 指真实世界的时钟时间定义。时间语法是基于在ISO8601中定义的语法。

8) `indefinite`: 表示“无限等待”。需要 `beginElement()`方法触发或者指向该动画元素的超链接(SVG中的a元素)。
下面代码是 `beginElement()` 方法触发的例子：
```html
<svg id="svg" width="320" height="200" xmlns="http://www.w3.org/2000/svg">
    <text font-family="microsoft yahei" font-size="120" y="160" x="160">马
        <animate attributeName="x" to="60" begin="indefinite" dur="3s" />
    </text>
</svg>
```

对应的js代码触发动画:
```js
var animate = document.getElementsByTagName("animate")[0];
if (animate) {
    document.getElementById("svg").onclick = function() {
        animate.beginElement();
    };
}
```

超链接触发的例子参见下面：

```html
<svg width="320" height="200" font-family="microsoft yahei" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
     <text font-size="120" y="160" x="160">马
          <animate id="animate" attributeName="x" to="60" begin="indefinite" dur="3s" repeatCount="indefinite" />
     </text>
     <a xlink:href="#animate">
          <text x="10" y="20" fill="#cd0000" font-size="30">点击我</text>
     </a>
</svg>
```

<svg width="320" height="200" font-family="microsoft yahei" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"> <text font-size="120" y="160" x="160">马 <animate id="animate" attributeName="x" to="60" begin="indefinite" dur="3s" repeatCount="indefinite" /> </text> <a xlink:href="#animate"> <text x="10" y="20" fill="#cd0000" font-size="30">点击我</text> </a> </svg>

> 如果动画的begin属性未显式指明或者解析异常，那么将会使用默认的`0`值，即文档开始后立即执行动画。

5. dur

dur属性值比较简单：常规时间值 | "indefinite"。

6. calcMode, keyTimes, keySplines

这几个参数是控制动画执行速度，类似CSS3动画中的`timing-function`。
1) calcMode 属性支持4个值：`discrete | linear | paced | spline`。

- discrete: from值直接跳到to值。类似于step(1, end)
- linear: animateMotion元素以外元素的calcMode默认值。动画从头到尾的速率都是一致的。
- paced: 通过插值让动画的变化步调平稳均匀。仅支持线性数值区域内的属性，这样点之间“距离”的概念才能被计算（如 position, width, height等）。如果`paced`指定，任何 `keyTimes` 或 `keySplines`值将会失效。
- spline: 插值定义贝塞尔曲线。spline点的定义在keyTimes属性中，每个时间间隔控制点由keySplines定义。

2) keyTimes = “<list>”
   跟上面提到的<list>类似，都是分号分隔一组值。keyTimes 是关键时间点的意思。前面提到过 values 也是多值，这里有一些约定的规则：首先，keyTimes 值的数目要和 values 一致，如果是 from/to/by 动画，keyTimes 就必须有两个值。然后对于 linear 和 spline 动画，第一个数字要是0, 最后一个是1。 

   最后，每个连续的时间值必须比它前面的值大或者相等。

> paced模式下，keyTimes会被忽略；keyTimes定义错误，也会被忽略；dur为indefinite也会被忽略。

3) keySplines = “<list>”
   keySplines表示的是与keyTimes相关联的一组贝塞尔控制点（默认0 0 1 1）。每个控制点使用4个浮点值表示：x1 y1 x2 y2. 只有模式是spline时候这个参数才有用，也是分号分隔，值范围0~1，总是比keyTimes少一个值。

> 如果keySplines值不合法或个数不对，是没有动画效果的。

```html
<animate attributeName="x" dur="5s" values="0; 20; 160" calcMode="linear" />
<animate attributeName="x" dur="5s" values="0; 20; 160" calcMode="paced"/>
<animate attributeName="x" dur="5s" values="0; 80; 160" keyTimes="0; .8; 1" calcMode="linear"/>
<animate attributeName="x" dur="5s" values="0; 80; 160" keyTimes="0; .8; 1" calcMode="spline"  keySplines=".5 0 .5 1; 0 0 1 1" />
```

以最后一个为例，values 确定动画的关键位置，keyTimes 确定到这个关键点需要的时间，keySplines 确定的是每个时间点段之间的贝塞尔曲线，也就是具体的缓动表现。这与CSS3中的 transition 动画和animation动画效果类似，只不过是这里的特殊情况。transition动画里面，values 值就两个，所以，keyTimes 只能是 0;1, 贝塞尔曲线就只有一个，要不 ease, 要不 linear 等。而animation动画里面，values 值和keyTimes 可以定义多个，同时也能定义一个贝塞尔曲线作为时间函数。
```css
@keyframes bounce {
    0% {
        left: 0;
    }
    80% {
        left: 80px;
        animation-timing-function: ease-in;
    }
    100% {
        left: 160px;
        animation-timing-function: linear;
    }
}                
```


7. repeatCount, repeatDur

repeatCount表示动画执行次数，可以是合法数值或者”indefinite“（动画循环到电脑死机）。
repeatDur定义重复动画的总时间。可以是普通时间值或者”indefinite（”动画循环到电脑死机）。
例如这个：
```html
<animate attributeName="x" to="60" dur="3s" repeatCount="indefinite" repeatDur="10s" />
```


8. fill

fill表示动画间隙的填充方式。支持参数有：freeze | remove. 其中remove是默认值，表示动画结束直接回到开始的地方。freeze“冻结”表示动画结束后像是被冻住了，元素保持了动画结束之后的状态。

9. accumulate, additive

accumulate 是累积的意思。支持参数有：none | sum。 默认值是 none 。如果值是 sum 表示动画结束时候的位置作为下次动画的起始位置。

additive控制动画是否附加。支持参数有：replace | sum. 默认值是 replace 。如果值是 sum 表示动画的基础知识会附加到其他低优先级的动画上，
举两个例子，下面是例子1：
```html
<img ...>
   <animateMotion begin="0" dur="5s" path="[some path]" additive="sum" fill="freeze" />
   <animateMotion begin="5s" dur="5s" path="[some path]" additive="sum" fill="freeze" />
   <animateMotion begin="10s" dur="5s" path="[some path]" additive="sum" fill="freeze" />
</img>
```
这里轮到第二个动画的时候，路径是从第一个动画路径结束地方开始的，于是，3个动画完美无缝连接起来了。

例子2：
```html
<animateTransform attributeName="transform" type="scale" from="1" to="3" dur="10s" repeatCount="indefinite" additive="sum"/>
<animateTransform attributeName="transform" type="rotate" from="0 30 20" to="360 30 20" dur="10s" fill="freeze" repeatCount="indefinite" additive="sum"/>;
```
这里，两个动画同时都是transform，都要使用一个type属性，好在这个例子additive="sum"是累加的而不是replace替换。于是，我们就可以是实现一边旋转一边放大的效果。

10. restart

restart控制重新开启动画的规则。支持的参数有：always | whenNotActive | never.
- always 是默认值，表示总是，也就是点一次圈圈，马儿跑一下。
- whenNotActive 表示动画正在进行的时候，是不能重启动画的。
- never 表示动画是一波流。

#### 动画的暂停与播放
SVG animation中是有内置的API可以暂停和启动动画的。语法为：
```js
// svg指当前svg DOM元素
svg.pauseAnimations(); // 暂停
svg.unpauseAnimations(); // 重启动
```

附上SMIL动画规范的官方文档链接：http://www.w3.org/TR/2001/REC-smil-animation-20010904/


####  <ANIMATE>实例：变形动画
在 SMIL 中，SVG <path> 元素的 d 属性是可以被动画的元素属性之一。d 属性是你绘制的图形的轮廓的数据。我们可以通过这个属性来制作 SVG 路径变形动画。要制作 SVG 路径变形动画，你可以指定 attributeName 属性为 d，然后设置 from 和 to 值来指定开始和结束图形。你也可以使用 values 属性来指定中间值。

下面是一个路径变形动画的小例子：
```html
<svg viewBox="0 0 100 100" width="500" height="150">
  <path fill="#1EB287" d="M 5.15151 0 C 52.5758 2.57575 52.5758 2.57575 100 5.15151 C 97.4242 52.5758 97.4242 52.5758 94.8485 100 C 47.4242 97.4242 47.4242 97.4242 0 94.8485 C 2.57575 47.4242 2.57575 47.4242 5.15151 0 Z">
    <animate attributeName="d" dur="1440ms" repeatCount="indefinite" keyTimes="0;
                       .0625;
                       .208333333;
                       .3125;
                       .395833333;
                       .645833333;
                       .833333333;
                       1" calcMode="spline" keySplines="0,0,1,1;
                         .42,0,.58,1;
                         .42,0,1,1;
                         0,0,.58,1;
                         .42,0,.58,1;
                         .42,0,.58,1;
                         .42,0,.58,1" values="M 0,0 
                     C 50,0 50,0 100,0
                     100,50 100,50 100,100
                     50,100 50,100 0,100
                     0,50 0,50 0,0
                     Z;

                     M 0,0 
                     C 50,0 50,0 100,0
                     100,50 100,50 100,100
                     50,100 50,100 0,100
                     0,50 0,50 0,0
                     Z;

                     M 50,0 
                     C 75,25 75,25 100,50 
                     75,75 75,75 50,100
                     25,75 25,75 0,50
                     25,25 25,25 50,0
                     Z;

                     M 25,50 
                     C 37.5,25 37.5,25 50,0 
                     75,50 75,50 100,100
                     50,100 50,100 0,100
                     12.5,75 12.5,75 25,50
                     Z;

                     M 25,50 
                     C 37.5,25 37.5,25 50,0 
                     75,50 75,50 100,100
                     50,100 50,100 0,100
                     12.5,75 12.5,75 25,50
                     Z;

                     M 50,0
                     C 77.6,0 100,22.4 100,50 
                     100,77.6 77.6,100 50,100
                     22.4,100, 0,77.6, 0,50
                     0,22.4, 22.4,0, 50,0
                     Z;
                     
                     M 50,0
                     C 77.6,0 100,22.4 100,50 
                     100,77.6 77.6,100 50,100
                     22.4,100, 0,77.6, 0,50
                     0,22.4, 22.4,0, 50,0
                     Z;
                     
                     M 100,0 
                     C 100,50 100,50 100,100
                     50,100 50,100 0,100
                     0,50 0,50 0,0
                     50,0 50,0 100,0
                     Z;"></animate>
    <animate attributeName="fill" dur="1440ms" repeatCount="indefinite" keyTimes="0;
                       .0625;
                       .208333333;
                       .3125;
                       .395833333;
                       .645833333;
                       .833333333;
                       1" calcMode="spline" keySplines="0,0,1,1;
                         .42,0,.58,1;
                         .42,0,1,1;
                         0,0,.58,1;
                         .42,0,.58,1;
                         .42,0,.58,1;
                         .42,0,.58,1" values="#1eb287;
                     #1eb287;
                     #1ca69e;
                     #188fc2;
                     #188fc2;
                     #bb625e;
                     #ca5f52;
                     #1eb287;"></animate>
  </path>
</svg>
```


<svg viewBox="0 0 100 100" width="500" height="150"> <path fill="#1EB287" d="M 5.15151 0 C 52.5758 2.57575 52.5758 2.57575 100 5.15151 C 97.4242 52.5758 97.4242 52.5758 94.8485 100 C 47.4242 97.4242 47.4242 97.4242 0 94.8485 C 2.57575 47.4242 2.57575 47.4242 5.15151 0 Z"> <animate attributeName="d" dur="1440ms" repeatCount="indefinite" keyTimes="0; .0625; .208333333; .3125; .395833333; .645833333; .833333333; 1" calcMode="spline" keySplines="0,0,1,1; .42,0,.58,1; .42,0,1,1; 0,0,.58,1; .42,0,.58,1; .42,0,.58,1; .42,0,.58,1" values="M 0,0 C 50,0 50,0 100,0 100,50 100,50 100,100 50,100 50,100 0,100 0,50 0,50 0,0 Z; M 0,0 C 50,0 50,0 100,0 100,50 100,50 100,100 50,100 50,100 0,100 0,50 0,50 0,0 Z; M 50,0 C 75,25 75,25 100,50 75,75 75,75 50,100 25,75 25,75 0,50 25,25 25,25 50,0 Z; M 25,50 C 37.5,25 37.5,25 50,0 75,50 75,50 100,100 50,100 50,100 0,100 12.5,75 12.5,75 25,50 Z; M 25,50 C 37.5,25 37.5,25 50,0 75,50 75,50 100,100 50,100 50,100 0,100 12.5,75 12.5,75 25,50 Z; M 50,0 C 77.6,0 100,22.4 100,50 100,77.6 77.6,100 50,100 22.4,100, 0,77.6, 0,50 0,22.4, 22.4,0, 50,0 Z; M 50,0 C 77.6,0 100,22.4 100,50 100,77.6 77.6,100 50,100 22.4,100, 0,77.6, 0,50 0,22.4, 22.4,0, 50,0 Z; M 100,0 C 100,50 100,50 100,100 50,100 50,100 0,100 0,50 0,50 0,0 50,0 50,0 100,0 Z;"></animate> <animate attributeName="fill" dur="1440ms" repeatCount="indefinite" keyTimes="0; .0625; .208333333; .3125; .395833333; .645833333; .833333333; 1" calcMode="spline" keySplines="0,0,1,1; .42,0,.58,1; .42,0,1,1; 0,0,.58,1; .42,0,.58,1; .42,0,.58,1; .42,0,.58,1" values="#1eb287; #1eb287; #1ca69e; #188fc2; #188fc2; #bb625e; #ca5f52; #1eb287;"></animate> </path> </svg>


### SVG与CSS3的关系
1. 使用CSS属性变换SVG

- 需要符合css3属性规范

 例如：函数参数必须逗号隔开；rotate()函数不接受`<cx>`和`<cy>`值, 旋转中心使用transform-origin属性声明。另外，CSS变换函数接受角度和坐标单位，例如角度的rad(radians)和坐标的px,em等。

- 使用SVG自身的变换规则

 SVG元素也可以使用CSS 3D变换在三维空间中变换。依然要注意SVG元素坐标系与HTML元素上的坐标系的不同

> 通过CSS来变换SVG元素非常类似于通过CSS来变换HTML元素在语法层面上相同，但是实际变换规则不同。

2. 使用CSS属性定义动画

SVG元素可以像HTML元素一样，使用CSS keyframes和animation属性或者CSS transitions来制作各种动画效果。大多数情况下，一个复杂的动画效果需要组合多种变换效果：旋转、倾斜、缩放以及他们的转换和过渡效果。

多数情况下，SVG元素和HTML元素在使用transform和transform-origin上是相同的。但它们之间也有不同之处:
1) SVG元素不能使用box model来管理，因此，它没有margin、padding、border或content boxes。
2) 默认情况下，一个HTML元素的transform原点位于该元素的(50%, 50%)的地方，这里是元素的中心点。与之不同，SVG 元素的 transform 原点位于当前用户坐标系统的原点上，这个点是画布的左上角位置。[如果有不理解的地方，参阅前文的SVG的坐标系统相关章节]

> TIPS: 如果希望显式的改变坐标原点，可以使用transform-origin属性来明确的设置HTML元素或者SVG元素的原点位置。
    在HTML元素上设置转换原点是一件非常简单的事情：你设置的任何值都是相对于元素的border box。
    在SVG中，transform原点可以使用百分比值或一个绝度值（如像素）来设置。如果你使用百分比值来设置transform-origin，这个值被设置为相对于元素的bounding box，它包括用于绘制边框的stroke。如果你使用一个绝对值来来设置transform-origin，那么这个值被设置为相对于用户的当前坐标系统，即SVG的画布。如果我们要将上例中的`<div>`和`<rect>`都使用百分比来设置其transform原点到中心，代码如下：

```html 
<!DOCTYPE html>
<style>
  div, rect {
  transform-origin: 50% 50%;
}
</style>                             
```

> Firefox浏览器仍不支持使用百分比来设置transform的原点。

### SVG 与 javascript
当SVG嵌入到HTML页面的时候，你可以使用javascript来操作SVG元素，就像操作其他HTML元素一样。例如，我们可以通过javascript来修改SVG元素属性，使它产生动画效果，或者在SVG图像上监听鼠标事件等等。
1) 通过ID获取SVG的引用
```js
var svgElement = document.getElementById("rect1");       
```

2) 读取/修改属性值
```js
var svgElement = document.getElementById("rect1");
var width = svgElement.getAttribute("width");       
svgElement.setAttribute("width", "100");  
```

2) 读取/修改CSS属性
```js
var svgElement = document.getElementById("rect1");
svgElement.style.stroke = "#ff0000";    
```

> 要注意的是，在某些SVG的CSS属性中，属性名称带有-连接符，例如stroke-width。这时候我们就需要通过['']结构来引用它。

4) 事件监听
支持 DOM0 级事件和 DOM2 级和 DOM3 级事件。

```html
<rect x="10" y="10" width="100" height="75"
      style="stroke: #000000; fill: #eeeeee;"
      onmouseover="this.style.stroke = '#ff0000'; this.style['stroke-width'] = 5;"
      onmouseout="this.style.stroke = '#000000'; this.style['stroke-width'] = 1;"
/> 
```


```js
var svgElement = document.getElementById("rect1");
svgElement.addEventListener("mouseover", mouseOver);
function mouseOver() {
    alert("事件被触发!");
}    
```


### SVG在移动页面的应用


#### 使用SVG中的Symbol元素制作图标
［参考文献］
http://isux.tencent.com/16292.html
http://io-meter.com/2014/07/20/replace-icon-fonts-with-svg/
https://css-tricks.com/svg-symbol-good-choice-icons/

随着高清屏幕的普及，相比使用png等位图而言，使用SVG等矢量图形是一种全新的设计方式。更重要的是相比位图而言，SVG有着无可比拟的优势。总结来说，SVG具有以下优势：

- SVG是矢量图形文件，可以随意改变大小，而不影响图标质量
- 可以用CSS样式来自由定义图标颜色，比如颜色/尺寸等效果（整体或者局部改变）
- 所有的SVG可以全部在一个文件中，节省HTTP请求
- 使用SMIL、CSS3或者是javascript可以制作充满灵性的交互动画效果
- 由于SVG也是一种XML节点的文件，可以使用gzip的方式把文件压缩到很小

> 字体图标也是一种基于矢量图形的技术封装

网站icomoon提供免费的svg图标下载。访问 https://icomoon.io 点击你需要下载的图形，选中它，然后点击下载按钮。

每个图标都以symbol的方式进行定义
```html
<symbol id="icon-image" viewBox="0 0 1024 1024">
  <title>image</title>
  <path class="path1" d="M959.884 128c0.040 0.034 0.082 0.076 0.116 0.116v767.77c-0.034 0.040-0.076 0.082-0.116 0.116h-895.77c-0.040-0.034-0.082-0.076-0.114-0.116v-767.772c0.034-0.040 0.076-0.082 0.114-0.114h895.77zM960 64h-896c-35.2 0-64 28.8-64 64v768c0 35.2 28.8 64 64 64h896c35.2 0 64-28.8 64-64v-768c0-35.2-28.8-64-64-64v0z"></path>
  <path class="path2" d="M832 288c0 53.020-42.98 96-96 96s-96-42.98-96-96 42.98-96 96-96 96 42.98 96 96z"></path>
  <path class="path3" d="M896 832h-768v-128l224-384 256 320h64l224-192z"></path>
</symbol>
```

使用图标的时候只需
```html
<svg class="icon icon-image"><use xlink:href="#icon-image"></use></svg>
```


#### 利用SVG特性制作高级动画


##### 基于SVG的path动画
利用SVG的Path，可以制作生成许多复杂的动画，其中之一便是Path的变形动画。在《移动H5页面开发系列——part2:移动H5页面优秀案例赏析》一文中，新百伦的运动鞋宣传页面案例《青春是一种什么颜色？》的背景颜色动画就可以使用Path变形动画进行实现。

```
<svg viewBox="0 0 320 480 " width="320" height="480">
  <path fill="tomato" d="M0 100 L0 480 L320 480 L320 100 Q250,80 100,110 T0,0">
    <animate attributeName="d" dur="4440ms" repeatCount="indefinite" keyTimes="0;0.3;0.6;1"  calcMode="spline" 
    keySplines="0,0,1,1;0,0,1,1;0,0,1,1;" 
    values="M0 400 L0 480 L320 480 L320 400 Q500,350 300,380 T0,400;
            M0 300 L0 480 L320 480 L320 300 Q400,250 300,280 T0,300;
            M0 200 L0 480 L320 480 L320 200 Q450,250 200,210 T0,200;
            M0 100 L0 480 L320 480 L320 100 Q250,80  100,110 T0,0"></animate>
  </path>
</svg>
```

实际效果可以刷查看下面的案例：
<iframe src="http://sandbox.runjs.cn/show/lk7nbykz" width="100%" height="500"></iframe>

##### 基于线条的描绘动画： 

另外一种动画是利用SVG特性实现线条的描绘动画和图像的上色动画。


线条的描绘动画，CSS3比较难实现，这里可以用SVG实现，主要代码如下：

```css
.path {
  stroke-dasharray: 1000;
  stroke-dashoffset: 1000;
  animation: dash 5s linear forwards;
}

@keyframes dash {
  to {
    stroke-dashoffset: 0;
  }
}
```

实际效果可以刷新页面查看：
<iframe src="http://sandbox.runjs.cn/show/7hujlkjt" width="100%" height="500"></iframe>

参考文献：https://jakearchibald.com/2013/animated-line-drawing-svg/

##### 细节动画
由于SVG是一种类似DOM节点组成的文本文档，所以我们可以很精细的控制SVG图形的每一个部分，并且可以使用SMIL动画、CSS3动画或者是javascript来制作动画效果，可用于制造一些高品质的细腻逼真的动画，精确刻画每一个动画细节。
<iframe src="http://sandbox.runjs.cn/show/anzvpikn" width="100%" height="320"></iframe>

更多例子，请参考下面的链接：
http://fang.youku.com/2014/timet
http://codepen.io/ghepting/pen/xnezB
http://codepen.io/TimPietrusky/pen/vKuja
http://www.html5tricks.com/demo/html5-svg-smile-faces/index.html
http://www.gbtags.com/gb/demoviewer/4001/9ca6f6cd-65cc-4d9a-8fed-613f9c0cba6c/svg-page-loading.html.htm
http://www.html5tricks.com/demo/html5-svg-shanche-animation/index2.html


#### SVG 的缺点
1) 渲染成本
理论上讲，SVG的效率可能会不如PNG好，这是因为它需要运行时的计算和对应平台的渲染绘制。而且对于PNG来说的另一优势是在开启硬件加速的设备上，绘制Bitmap一个非常快速的过程。

2) 渲染效果
不同的浏览器乃至不同的平台的抗锯齿处理千差万别，你的图标如果多边形比较多，在底分辨屏幕上的效果可能千差万别，特别是如果赶上蛋疼的用户关掉抗锯齿，图标会惨不忍睹的。

3) Fallback的支持
SVG虽然有很多很好的特性，但是无论是web的ie8-还是mobile上的Android2.3-，都得做一套fallback。

4) 文件大
由于SVG以XML的方式描述图像，其文件大小通常是icon-font的数倍。如果大家对icon image进行优化，会发现如果icon / logo较小的时候用位图反而更有利于节省带宽。所以大家如果用SVG还是用icon-font，自然也就一目了然。在一些应用场景，SVG会有自身的优势，因此要酌情使用。但多数情况下，web开发以及浏览器开发的人，处理font的经验相对于矢量图要多一些。

### 结语

没有结语。
以上，轻拍。
(EOF)

### 参考文章
1. http://www.w3cplus.com/html5/svg-introduction-and-embedded-html-page.html
2. http://www.w3cplus.com/html5/svg-file-structure.html
3. http://www.htmleaf.com/ziliaoku/qianduanjiaocheng/201507082192.html
