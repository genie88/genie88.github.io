title: 使用 JavaScript 构建原生应用实战篇（三）
date: 2015-07-30 15:14:30
tags: ReactJs
---
![genie.github.io](/assets/41.jpg)
再上一篇文章我们已经学会了如何利用ReactJs Native制作我们的入门hello world应用，掌握来ReactJs Native应用的运行和调试方式。从这篇文章开始，我们真正的开始构建实际的应用程序。
<!--more-->
我们的汉字学习卡片应用使用IOS标准的栈式导航，基于 UIKit 的 navigation controller。ReacctJs针对这个原生组件进行了包装，在类库里面的名字叫做NavigatorIOS，让我们首先把它添加到我们的应用中。

在 `index.ios.js` 文件中，把上一篇文章中新建的类`Hanzi`  重命名为`HelloWorld`：

“Hello World” 这几个字你还需要让它显示一会儿，但它不再是应用的根组件了。

接下来，在 HelloWorld 这个组件下面添加如下这个类：
```js
class Hanzi extends React.Component {
  render() {
    return (
      <React.NavigatorIOS
        style={styles.container}
        initialRoute={{
          title: 'Property Finder',
          component: HelloWorld,
        }}/>
    );
  }
}
```

构造一个navigation controller，应用一个样式，并把初始路由设为 Hello World 组件。在 Web开发中，路由就是一种定义应用导航的一种技术，即定义页面——或者说是路由——与 URL 的对应关系。

在同一个文件中，更新样式定义，包含如下 container 的样式：
```js
var styles = React.StyleSheet.create({
  text: {
    color: 'black',
    backgroundColor: 'white',
    fontSize: 30,
    margin: 80
  },
  container: {
    flex: 1
  }
});
```

注意这个flex属性点用法。相信你已经看到了用基本的 CSS 属性来控制外间距（margin），内间距（padding）还有颜色（color）。不过，可能你还不太了解要如何使用弹性盒子属性（flexbox），flexbox 是新增的 CSS3 规范，用它就能很便利地布局界面。但是React Native上对其的实现和标准还是有一点不同。如果你感兴趣可以参考相关的文档和链接。不过不用着急，我们在后面的文章中也会讲到它的详细用法。

你可以在xcode中开启模拟器，看看应用加上了导航栏的新UI的样子。

这就是包含了 root view 的导航栏控制器，目前 root view 就是 “Hello World”。应用已经有了基础的导航结构，到添加真实 UI 的时候了。

#创建列表页
为简单起见，我们所有的代码都放到一个文件中。回到文件的顶部，我们先引入需要的一些包含在React系统类库中的变量。
```js
'use strict';

var React = require('react-native');
var {
  StyleSheet,
  Text,
  TextInput,
  View,
  ListView,
  TouchableHighlight,
  ActivityIndicatorIOS,
  Image,
  Component,
  NavigatorIOS
} = React;
```

你会注意到，位于引入react-native 所在位置的前面有一个严格模式标识，紧接着的声明语句是新知识。

这是一种解构赋值，准许你获取对象的多个属性并且使用一条语句将它们赋给多个变量。解构同样适用于操作数组，更多细节请戳[这里](https://github.com/sebmarkbage/ecmascript-rest-spread)。
这样声明的好处是在接下来的代码中可以省略掉 React 前缀；比如，你可以直接引用 StyleSheet ，而不再需要 React.StyleSheet。

然后继续添加如下的UI样式：
```js
var styles = StyleSheet.create({
  description: {
    marginBottom: 20,
    fontSize: 18,
    textAlign: 'center',
    color: '#656565'
  },
  container: {
    padding: 30,
    marginTop: 65,
    alignItems: 'center'
  },
  row : {
    margin:20,
    width: 320,
    flexDirection: 'row',
    alignItems: 'center',
    alignSelf: 'stretch'
  },
  header: {
    marginTop: 64,
    padding: 30,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#29DF9A',
  }, 
  welcomeMsg: {
    fontSize: 55,
    color: '#FFF',
    fontWeight: 'bold',
    marginBottom:20,
  },
  getStart: {
    fontSize: 15,
    fontWeight: 'bold',
    color: '#FFF'
  },
  separator: {
    height: 1,
    backgroundColor: '#dddddd'
  },
  status: {
    fontSize: 15,
    flex: 1,
    color: '#29DF9A'
  },
  title: {
    flex: 4,
    fontSize: 20,
    color: '#656565'
  }
});
```
添加的同时，不要忘记或者多添加了每个样式之间的逗号。同样，以上都是标准的 CSS 属性。和 Interface Builder 相比，这样设置样式缺少了可视化，但是比起在 `viewDidLoad()`中逐个设置视图属性的做法更友好！感觉就像是在编写CSS文件，痛快淋漓！要记住的就是CSS里面的双字节属性都要改成驼峰法命名。我们再一次的用到了flex属性，与此同时的还有flexDirection、justifyContent和alignItems属性，它们之间时协同工作的！

找到之前的HelloWorld类，我们现在需要重新把它命名为`StudyListScreen`,然后添加如下的代码：
```js
class StudyListScreen extends Component {

  constructor(props) {
    super(props);
    var dataSource = new ListView.DataSource({
      rowHasChanged: (r1, r2) => r1.guid !== r2.guid
    });
    var listData = [
      {title: 'Animals', status: '96%'}, 
      {title: 'Time', status: '50%'}, 
      {title: 'Actions', status: 'study'}, 
      {title: 'Places', status: 'study'},
      {title: 'Plants', status: 'study'},
      {title: 'Foods', status: 'study'}
    ];
    this.state = {
      dataSource: dataSource.cloneWithRows(listData)
    };
  }
  renderRow(rowData, sectionID, rowID) {
    return (
      <View>
      <TouchableHighlight
          underlayColor='#84EFC6'>
        <View style={styles.row}>
          <Text style={styles.title}>{rowData.title}</Text>
          <Text style={styles.status}>{rowData.status}</Text>
        </View>
      </TouchableHighlight>
      <View style={styles.separator}/>
      </View>
    );
  }
  render() {
    return (
      <View >
        <View style={styles.header}>
          <Text style={styles.welcomeMsg}>你好</Text>
          <Text style={styles.getStart}>Let us get started!</Text>
        </View>
        <ListView
          dataSource={this.state.dataSource}
          renderRow={this.renderRow.bind(this)}
          keyboardDismissMode="on-drag"
          keyboardShouldPersistTaps={true}
          automaticallyAdjustContentInsets={false}
          showsVerticalScrollIndicator={true}/>
      </View>
      
    );
  }
}
```

我们除了常规的`render()`方法外，还用到了一个`constructor`构造函数，里面定义了listData变量和初始状态，用来暂时模拟列表数据。在`render()`方法里面，我们定义了一个ListView的组件，用来展示我们的学习列表。renderRow函数在ListView的属性里面用到，用于定义列表的每个item如何生成和展示。
```js
renderRow={this.renderRow.bind(this)}
```

最后，修改我们的主应用类Hanzi，讲里面的初始路由设置成我们新定义的这个UI组件。
```js
class Hanzi extends Component {
  render() {
    return (
      <NavigatorIOS
        style={styles.nav}
        initialRoute={{
          title: 'Hanzi',
          component: StudyListScreen,
        }}/>
    );
  }
}
```
现在返回到模拟器，然后按下 Cmd+R 刷新界面。不要被效果惊艳到哦😏！
![genie.github.io](/assets/45.png)

好吧，今天的课程就到这里，下一篇文章在继续吧！