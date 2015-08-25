title: 如何利用Ajax初始化React组件的状态
date: 2015-08-25 09:45:30
tags: ReactJs
---
如果我们需要在初始化组件的状态，我们可以在组件完成加载后进行，也就是在方法 `componentDidMount`中进行。当响应返回后，首先通过`this.isMounted()`来判断组件的状态是否为Mounted，如果是则将数据存储在state中，这将会保证触发render函数并更新UI.
<!--more--> 
以下是一个完整的例子：
```js
var UserGist = React.createClass({
  getInitialState: function() {
    return {
      username: '',
      lastGistUrl: ''
    };
  },

  componentDidMount: function() {
    $.get(this.props.source, function(result) {
      var lastGist = result[0];
      if (this.isMounted()) {
        this.setState({
          username: lastGist.owner.login,
          lastGistUrl: lastGist.html_url
        });
      }
    }.bind(this));
  },

  render: function() {
    return (
      <div>
        {this.state.username}'s last gist is
        <a href={this.state.lastGistUrl}>here</a>.
      </div>
    );
  }
});

React.render(
  <UserGist source="https://api.github.com/users/octocat/gists" />,
  mountNode
);
```