title: 使用 JavaScript 构建原生应用实战篇（二）
date: 2015-07-24 12:59:12
tags: ReactJs
---
![genie.github.io](/assets/41.jpg)
在开始“汉语卡片学习应用”之前，先来个简单的 Hello World App 热热身。本篇文章将带你使用Racter-native制作一个入门级的Hello World应用。
<!--more-->
使用xcode IDE 打开上一篇文章中初始化创建的xcode工程项目。在你钟爱的编辑器（我通常用sublime Text）其中打开 index.ios.js，删除当前的内容，因为你要从头构建你自己的应用。然后在文件顶部增加下面这样一行：：
```js
'use strict';
```
这行代码是用于开启 javascript的严格模式（Strict Mode），严格模式的错误预防处理可以有所提高，JavaScript的一些语言缺陷也可以避免。简而言之就是，JavaScript在这种模式下工作地更好！

然后，加上这一行：
```js
var React = require('react-native');
```
没错，这句代码是将 react-native 模块加载进来，并将它赋值给变量 React 的。React Native 使用同 Node.js 相同的模块加载方式：require，这个概念可以等同于 Swift 中的“链接库”或者“导入库”。

在 require 语句的下面，加上这一段：
```js
var styles = React.StyleSheet.create({
  text: {
    color: 'black',
    backgroundColor: 'white',
    fontSize: 35,
    margin: 90
  }
});
```
以上代码定义了一段应用在 “Hello World” 文本上的样式。如果你曾接触过Web开发，是不是觉得很熟悉？没错，React Native 使用的是 CSS 来定义应用界面的样式。已经支持绝大部分的样式定义，而且支持最新的部分CSS3样式。

现在我们来关注应用本身吧！依然是在相同的文件下，将以下代码添加到样式代码的下面：
```js
class Hanzi extends React.Component {
  render() {
    return React.createElement(React.Text, {style: styles.text}, "Hello World!");
  }
}
```
什么？JavaScript class的语法竟然可以用了！没错，类 (class) 是在ES6中被引入的，虽然JavaScript一直在进步，但Web开发者受困于兼容浏览器的状况中，不能怎么使用JS的新特性。React Native运行在JavaScriptCore中是，也就是说，你可以使用JS的新特性啦，完全不用担心兼容什么的呢。

Hanzi 继承了 React.Component（React UI的基础模块）。组件包含着不可变的属性，可变的状态变量以及暴露给渲染用的方法。这会你做的应用比较简单，只用一个渲染方法就可以啦。

React Native 组件并不是 UIKit 类，它们只能说是在某种程度上等同。框架只是将 React 组件树转化成为原生的UI。

最后一步啦，将这一行加在文件末尾：
```js
React.AppRegistry.registerComponent('hanzi', function() { return Hanzi });
```
AppRegistry 定义了App的入口，并提供了根组件。

保存 index.ios.js，回到Xcode中。确保 Hanzi 规划（scheme）已经勾选了，并设置了相应的 iPhone 模拟器，然后生成并运行你的项目。几秒之后，你应该就可以看到 “Hello World” 应用正在运行了：
![genie.github.io](/assets/43.jpg)
你当前的应用程序会使用 React.createElement 来构建应用 UI ,React会将其转换到原生环境中。在当前情况下，你的JavaScript代码是完全可读的,但一个更复杂的 UI 与嵌套的元素将迅速使代码变成一大坨。 

确保应用程序仍在运行,然后回到你的文本编辑器中，编辑 index.ios.js 。修改组件 render 方法的返回语句如下:
```js
return <React.Text style={styles.text}>Hello World (Again)</React.Text>;
```
这是 JSX ，或 JavaScript 语法扩展,它直接在你的 JavaScript 代码中混合了类似 HTML 的语法;如果你是一个 web 开发人员,应该对此不陌生。在本篇文章中将一直使用 JSX 语法，习惯之后就不会觉得jsx语法有什么不妥了 。

把你的改动保存到 index.ios.js 中，并返回到模拟器。按下 Cmd + R ,你将看到你的应用程序刷新,并显示更新的消息 “Hello World(again)”。

重新运行一个 React Native 应用程序像刷新 web 浏览器一样简单!:]

因为你会使用相同的一系列 JavaScript 文件,您可以让应用程序一直运行,只在更改和保存 index.ios.js 后刷新即可。

这个 “Hello World” 已经够大家玩耍了,从下一篇文章开始将要真正的构建实际的应用程序了!

