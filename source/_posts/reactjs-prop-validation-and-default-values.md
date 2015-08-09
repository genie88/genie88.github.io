title: React的属性
date: 2015-08-07 08:19:15
tags: ReactJs
---
Properties(属性)对于React就像Attribute对于HTML。事实上, 在JSX中property的使用就像attribute的使用一样。如果你熟悉HTML的话, 你就会知道HTML元素可以通过标签内的attribute的值来实现个性化。properties属性可以把单纯的组件变成可配置的界面元素。属性是组件重用的关键和对层级组织组件很有帮助。如果我们想要根据外部的信息来改变组件的外观或者行为时，就可以使用Properties!
<!--more--> 

##Prop定义
可以采用JSX的语法，直接为组件创建属性，如下代码所示创建了名称为foo和bar的两个属性。
```js
 var component = <Component foo={x} bar={y} />;
```
那么，就可以在组件内部通过this.props对象分别得到这两个属性的值。
```js
var foo = this.props.foo ,
    bar = this.props.bar ;
```
一般来说，React组件的props属性是只读的。Props 应该被当作禁止修改。修改 props 对象可能会导致预料之外的结果，所以最好不要去修改 props 对象。因此，下面的代码时不合理的，应该尽力避免使用：
```js
var component = <Component />;
    component.props.foo = x; // 不好
    component.props.bar = y; // 同样不好
```

可以采用 JSX 的新特性 ...延展的语法来快速注入和定义属性，
```js
  var props = {};
  props.foo = x;
  props.bar = y;
  var component = <Component {...props} />;
```
传入对象的属性会被复制到组件内。它能被多次使用，也可以和其它属性一起用。注意顺序很重要，后面的会覆盖掉前面的。也就是说
```js
var props = { foo: 'default' };
var component = <Component {...props} foo={'override'} />;
console.log(component.props.foo); // 'override'

```


##Prop验证
React提供了属性验证和声明式的默认值供我们开发时选用。React库为组件的props提供了很多验证器 (validator) 来验证传入数据的有效性。当向 props 传入无效数据时，JavaScript 控制台会抛出警告。注意为了性能考虑，只在开发环境验证 propTypes。

下面用例子来说明不同验证器的区别：
```js
 React.createClass({
  propTypes: {
    // 可以声明 prop 为指定的 JS 基本类型。默认
    // 情况下，这些 prop 都是可传可不传的。
    optionalArray: React.PropTypes.array,
    optionalBool: React.PropTypes.bool,
    optionalFunc: React.PropTypes.func,
    optionalNumber: React.PropTypes.number,
    optionalObject: React.PropTypes.object,
    optionalString: React.PropTypes.string,

    // 所有可以被渲染的对象：数字，
    // 字符串，DOM 元素或包含这些类型的数组。
    optionalNode: React.PropTypes.node,

    // React 元素
    optionalElement: React.PropTypes.element,

    // 用 JS 的 instanceof 操作符声明 prop 为类的实例。
    optionalMessage: React.PropTypes.instanceOf(Message),

    // 用 enum 来限制 prop 只接受指定的值。
    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),

    // 指定的多个对象类型中的一个
    optionalUnion: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
      React.PropTypes.instanceOf(Message)
    ]),

    // 指定类型组成的数组
    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),

    // 指定类型的属性构成的对象
    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),

    // 特定形状参数的对象
    optionalObjectWithShape: React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }),

    // 以后任意类型加上 `isRequired` 来使 prop 不可空。
    requiredFunc: React.PropTypes.func.isRequired,

    // 不可空的任意类型
    requiredAny: React.PropTypes.any.isRequired,

    // 自定义验证器。如果验证失败需要返回一个 Error 对象。不要直接
    // 使用 `console.warn` 或抛异常，因为这样 `oneOfType` 会失效。
    customProp: function(props, propName, componentName) {
      if (!/matchme/.test(props[propName])) {
        return new Error('Validation failed!');
      }
    }
  },
  /* ... */
});
```

##单个子级
React.PropTypes.element 可以限定只能有一个子级传入。
```js
var MyComponent = React.createClass({
  propTypes: {
    children: React.PropTypes.element.isRequired
  },

  render: function() {
    return (
      <div>
        {this.props.children} // 有且仅有一个元素，否则会抛异常。
      </div>
    );
  }

});
```


##默认Prop值
React 支持以声明式的方式来定义 props 的默认值。
```js
var ComponentWithDefaultProps = React.createClass({
  getDefaultProps: function() {
    return {
      value: 'default value'
    };
  }
  /* ... */
});
```
当父级没有传入 props 时，getDefaultProps() 可以保证 this.props.value 有默认值。得益于此，你可以直接使用 props，而不必写手动编写像下面一样一些重复或无意义的代码。
```js
React.createClass({
  render: function() {
    var value = this.props.value || 'default value';
    return <div>{value}</div>;
  }
});
```
注意 getDefaultProps 的结果会被缓存然后再进行渲染Render。但是每次Render之前都会进行Prop验证。

##传递 Props：小技巧
有一些常用的 React 组件只是对 HTML 做简单扩展。通常，你想少写点代码来把传入组件的 props 复制到对应的 HTML 元素上。这时 JSX 的 spread 语法会帮到你：
```js
var CheckLink = React.createClass({
  render: function() {
    // 这样会把 CheckList 所有的 props 复制到 <a>
    return <a {...this.props}>{'√ '}{this.props.children}</a>;
  }
});

React.render(
  <CheckLink href="/checked.html">
    Click here!
  </CheckLink>,
  document.getElementById('example')
);
```
