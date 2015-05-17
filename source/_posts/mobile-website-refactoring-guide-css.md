title: "移动端网页重构指南 – CSS篇"
date: 2015-05-17 14:14:26
tags: "css"
---

### 前言
本文主要介绍移动重构CSS相关部分，包括编码、字体、touch相关、硬件加速、兼容问题等。
<!--more-->
###基础篇

####编码
```css
@charset "UTF-8";
```
####字体设置
```css
body { 
    font-family: "Helvetica Neue", Helvetica, STHeiTi, sans-serif; 
}
```
####盒模型
```css
*, *:before, *:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```
####上下拉动滚动条时卡顿、慢
```css
E {
    -webkit-overflow-scrolling: touch;
    overflow-scrolling: touch;
}
```
Android3+和iOS5+支持CSS3的新属性为overflow-scrolling

####禁止复制、选中文本
```css
E {
    -webkit-user-select: none;
    -moz-user-select: none;
    -khtml-user-select: none;
     user-select: none;
}
```
解决移动设备可选中页面文本(视产品需要而定)

####长时间按住页面出现闪退
```css
E {
    -webkit-touch-callout: none;
}
```
####iphone及ipad下输入框默认内阴影
```css
E {
    -webkit-appearance: none; 
}
```
####更改输入框placeholder的颜色
```css
input::-webkit-input-placeholder { color:#999; }
input:focus::-webkit-input-placeholder { color:#333; }
placeholder的文字在ios下可以换行，android不行
```
####ios和android下触摸元素时出现半透明灰色遮罩
```css
E {
    -webkit-tap-highlight-color:rgba(255,255,255,0)
}
```
设置alpha值为0就可以去除半透明灰色遮罩，备注：transparent的属性值在android下无效。

####active兼容处理
```html
<body ontouchstart="">
```
####动画定义3D启用硬件加速
```css
E {
    -webkit-transform:translate3d(0, 0, 0)
    transform: translate3d(0, 0, 0);
}
```
注意：3D变形会消耗更多的内存与功耗

####Retina屏的1px边框
```css
E {
    border-width: thin;
}
```
####webkit mask 兼容处理
某些低端手机不支持css3 mask，可以选择性的降级处理。
比如可以使用js判断来引用不同class：
```js
if( 'WebkitMask' in document.documentElement.style){
    alert('支持mask');
} else {
    alert('不支持mask');
}
```
####旋转屏幕时，字体大小调整的问题
```css
html, body, form, fieldset, p, div, h1, h2, h3, h4, h5, h6 {
    -webkit-text-size-adjust:100%;
}
```
####transition闪屏
```css
/*设置内嵌的元素在 3D 空间如何呈现：保留3D */ 
-webkit-transform-style: preserve-3d;
 
/* 设置进行转换的元素的背面在面对用户时是否可见：隐藏 */
-webkit-backface-visibility:hidden;
```

####圆角bug
某些Android手机圆角失效
```css
background-clip: padding-box;
```

####其它最佳实践

- 慎用box-shadow和gradients

- box-shadows与gradients往往都是页面的性能杀手，尤其是在一个元素同时都使用了它们。

- 尽可能让动画元素不在文档流中，以减少重排(reflow)。可以使用绝对定位。position: absolute;

- 以下四个属性对动画的效率较高, 可以充分利用
```css
Position：transform: translate(npx, npx);
Scale： transform: scale(n);
Rotation：transform: rotate(ndeg);
Opactity: opacity：0…1;
```
参考：http://www.html5rocks.com/en/tutorials/speed/high-performance-animations/



