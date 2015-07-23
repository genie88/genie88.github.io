title: 使用 JavaScript 构建原生应用实战篇（一）
date: 2015-07-23 19:32:59
tags: "ReactJs"
---
![genie.github.io](/assets/41.jpg)
这篇教程将带着你一路构建一个汉语卡片学习应用。如果你之前一点 JavaScript 都没写过，别担心。这篇教程带着你进行一步一步进行编码。
<!--more--> 
##准备工作
React Native 框架托管在 GitHub 开源仓库上。你可以通过两种方式获取到它：使用 git 克隆仓库，或者下载一个 zip 压缩包文件。如果你的机器上已经安装了 React Native，在着手编码前还有其他几个因素需要考虑。

React Native 依赖于 Node.js，即 JavaScript 运行时来创建 JavaScript 代码。如果你已经安装了 Node.js，那就可以上手了。
首先，使用 Homebrew 官网提供的指引安装 Homebrew，然后在终端执行以下命令：
```sh
brew install node
```
接下来，使用 homebrew 安装 watchman，一个来自Facebook 的观察程序：
```sh
brew install watchman
```
通过配置 watchman，React 实现了在代码发生变化时，完成相关的重建的功能。就像在使用 Xcode 时，每次保存文件都会进行一次创建。

接下来使用 `npm` 工具安装 React Native CLI 工具：
```sh
npm install -g react-native-cli
```
这使用 Node 包管理器 `npm` 下载并安装 CLI 工具，并且全局安装；`npm` 在功能上与 CocoaPods 或者 Carthage 类似。

浏览到你想要创建 React Native 应用的文件夹下，使用 CLI 工具构建项目：
```sh
react-native init demo
```
现在，已经创建了一个初始项目，包含了创建和运行一个 React Native 应用所需的一切。

如果仔细观察了创建的文件夹和文件，你会发现一个 node_modules 文件夹，包含了 React Native 框架。你也会发现一个 index.ios.js 文件，这是 CLI 工具创建的一个空壳应用。最后，会出现一个 Xcode 项目文件和一个 iOS 文件夹，包含了少量的代码用来引入 bootstrap 到你的项目中。

打开 Xcode ,并打开刚才创建的初始项目文件，编译并运行改项目。如果一切顺利的话，模拟器将会启动并且展示下面的画面：
![genie.github.io](/assets/42.jpg)

那么，恭喜你，你的React Native 开发环境已经部署好了。


