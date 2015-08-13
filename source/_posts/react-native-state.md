title: React的state 工作原理
date: 2015-08-10 22:31:03
tags: ReactJs
---
![genie.github.io](/assets/50.png)
React 把用户界面当作简单状态机。把用户界面想像成拥有不同状态然后渲染这些状态，可以轻松让用户界面和数据保持一致。React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。React 来决定如何最高效地更新 DOM。今天我们来探讨下React中的state机制和工作原理。
<!--more--> 

##什么是组件的State
State时组件的基本状态，类似于AngularJs中的$scope变量，当我们在事件处理函数中改变和调整State的值时，React会自动调用render()方法实现视图的刷新，完成视图模型到视图的单向绑定和刷新。
![genie.github.io](/assets/50.png)
![genie.github.io](/assets/51.png)

##哪些组件应该有 State
大部分组件的工作应该是从 props 里取数据并渲染出来。但是，有时需要对用户输入、服务器请求或者时间变化等作出响应，这时才需要使用 State。

> 最佳实践： 尝试把尽可能多的组件无状态化。

这样做能隔离state，把它放到最合理的地方，也能减少冗余，同时易于解释程序运作过程。

常用的模式是创建多个只负责渲染数据的无状态（stateless）组件，在它们的上层创建一个有状态（stateful）组件并把它的状态通过 props 传给子级。这个有状态的组件封装了所有用户的交互逻辑，而这些无状态组件则负责声明式地渲染数据。


##哪些应该作为 State
 > 如何区别State和Prop ？
 State是组件可变的动态属性，而Prop是外部传入的静态属性


 State应该包括那些可能被组件的事件处理器改变并触发用户界面更新的数据。 真实的应用中这种数据一般都很小且能被 JSON 序列化。当创建一个状态化的组件时，想象一下表示它的状态最少需要哪些数据，并只把这些数据存入 this.state。在 render() 里再根据 state 来计算你需要的其它数据。你会发现以这种方式思考和开发程序最终往往是正确的，因为如果在 state 里添加冗余数据或计算所得数据，需要你经常手动保持数据同步，不能让 React 来帮你处理。

##哪些不应该 作为 State？
state应该仅包括能表示用户界面状态所需的最少数据。因此，它不应该包括：

* 计算所得数据
不要担心根据 state 来预先计算数据 —— 把所有的计算都放到 render() 里更容易保证用户界面和数据的一致性。例如，在 state 里有一个数组（listItems），我们要把数组长度渲染成字符串， 直接在 render() 里使用 this.state.listItems.length + ' list items' 比把它放到 state 里好的多。

* React 组件
在 render() 里使用当前 props 和 state 来创建它。

* 基于 props 的重复数据
尽可能使用 props 来作为惟一数据来源。把 props 保存到 state 的一个有效的场景是需要知道它以前值的时候，因为未来的 props 可能会变化。

##如何初始化state
可以采用`getInitialState()`方法来进行state状态的初始化。
```js
  getInitialState: function() {
    return {liked: false};
  },
```

##如何改变state
需要注意的是，state变量应该作为组件的私有属性，更新和改变state状态只能在组件内部进行。可以采用`this.setState()`方法来进行state状态的更新。
```js
handleClick: function(event) {
    this.setState({liked: !this.state.liked});
}
```
也可以采用`replaceState()`方法来进行状态的替换。
```js
handleClick: function(event) {
    this.replaceState({liked: !this.state.liked});
}
```

##完整的例子
下面的代码是一个完整的例子。
```js
var LikeButton = React.createClass({
  getInitialState: function() {
    return {liked: false};
  },
  handleClick: function(event) {
    this.setState({liked: !this.state.liked});
  },
  render: function() {
    var text = this.state.liked ? 'like' : 'haven\'t liked';
    return (
      <p onClick={this.handleClick}>
        You {text} this. Click to toggle.
      </p>
    );
  }
});

React.render(
  <LikeButton />,
  document.getElementById('example')
);
```

