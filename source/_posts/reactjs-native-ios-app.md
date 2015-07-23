title: 深入浅出 React Native：使用 JavaScript 构建原生应用
date: 2015-07-23 09:23:32
tags: "reactjs"
---
![genie.github.io](/assets/41.jpg)
数月前，Facebook 对外宣布开源了著名的React Native框架，这个框架允许你使用 JavaScript开发原生的iOS应用！基于PhoneGap使用JavaScript和HTML5开发 iOS应用已经有好几年了，那 React Native 有什么牛的？
<!--more--> 
React Native 真的很牛，让大家兴奋异常的主要原因有两点：

1. 可以基于 React Native使用 JavaScript 编写应用逻辑，UI 则可以保持全是原生的。这样的话就没有必要就 HTML5 的 UI 做出常见的妥协；

2. React引入了一种与众不同的、略显激进但具备高可用性的方案来构建用户界面。长话短说，应用的 UI 简单通过一个基于应用目前状态的函数来表达。

React Native 的关键就是，以把 React 编程模式的能力带到移动开发来作为主要目标。它的目标不是跨平台一次编写到处执行，而是一次学习跨平台开发。这个是一个非常大的区别。这篇教程只介绍 iOS 平台，不过你一旦掌握了相关的概念，就可以应用到 Android 平台，快速构建 Android 应用。

如果之前只用过 Objective-C 或者 Swift 写应用的话，你很可能不会对使用 JavaScript 来编写应用的愿景感到兴奋。尽管如此，作为一个 Swift 开发者来说，上面提到的第二点应该可以激起你的兴趣！

你通过 Swift，毫无疑问学习到了新的更多有效的编码方法和技巧，鼓励转换和不变性。然而，构建 UI 的方式还是和使用 Objective-C 的方式一致。仍然以 UIKit 为基础，独断专横。

通过像 virtual DOM 和 reconciliation 这些有趣的概念，React 将函数式编程直接带到了 UI 层。

这篇教程将带着你一路构建一个简单的汉字学习应用：

![genie.github.io](/assets/42.png)

如果你之前一点 JavaScript 都没写过，别担心。这篇教程带着你进行一步一步进行编码。React 使用 CSS 属性来定义样式，一般比较容易读也比较容易理解。

想要学习更多，下一篇文章再叙！



