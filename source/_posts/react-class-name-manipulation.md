title: 如何在React中优雅的操作组件的ClassName
date: 2015-08-25 09:48:59
tags: ReactJs
---
通常，我们经常需要根据组件的状态或者属性为组件指定不同的样式类名。
<!--more--> 
例如，以下的代码或许经常出现在我们的代码中：
```html
// inside some `<Message />` React component
render: function() {
  var classString = 'message';
  if (this.props.isImportant) {
    classString += ' message-important';
  }
  if (this.props.isRead) {
    classString += ' message-read';
  }
  // 'message message-important message-read'
  return <div className={classString}>Great, I'll be there.</div>;
}
```
咋一眼看，好像没有啥问题，但是如果状态或者属性个数变得异常多了呢？就非常难于阅读，容易让人一头雾水了，出错的概率也比较大。

幸好，React已经为我们想到了这一点。在React的`addon`里面有一个`classSet()`方法能够为我们解决这一个难题：
```html
render: function() {
  var cx = React.addons.classSet;
  var classes = cx({
    'message': true,
    'message-important': this.props.isImportant,
    'message-read': this.props.isRead
  });
  // same final string, but much cleaner
  return <div className={classes}>Great, I'll be there.</div>;
}
```
而且，`classSet()`方法还能够为我们自动拼接类名：
```html
render: function() {
  var cx = React.addons.classSet;
  var importantModifier = 'message-important';
  var readModifier = 'message-read';
  var classes = cx('message', importantModifier, readModifier);
  // Final string is 'message message-important message-read'
  return <div className={classes}>Great, I'll be there.</div>;
}
```
有了它，是不是感觉操作className的时候轻松多了？