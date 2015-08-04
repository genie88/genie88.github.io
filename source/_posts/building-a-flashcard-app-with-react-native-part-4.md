title: 使用 JavaScript 构建原生应用实战篇（四）
date: 2015-08-04 12:51:45
tags: ReactJs
---
![genie.github.io](/assets/41.jpg)
上一篇文章我们已经学会了如何利用ReactJs Native构建基础的应用界面。这一篇文章我们要学习如何响应用户操作，了解React Native的事件处理。
<!--more-->
在 `index.ios.js` 文件中，我们新建一个视图组件`StudyScreen`，现在就让它里面什么内容也没有吧。添加如下代码:
```js
class StudyScreen extends Component {
  render(){
    return (
      <View style={styles.container}>
        
      </View>
    );
  }
}
```
找到上一篇文章创建的`StudyListScreen`组件，将其里面的renderRow函数修改成如下所示：
```js
  renderRow(rowData, sectionID, rowID) {
    return (
      <View>
      <TouchableHighlight
          onPress={()=> this.onListPressed(rowData)}
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
```
我们增加了onPress这一个属性的定义，
```js
onPress={()=> this.onListPressed(rowData)}
```
也就是说，当用户点击到我们的学习列表ListView中的某个Row时，就会触发这个该事件响应处理函数。里面的语句将会被执行。
`onListPressed`这个函数还没有被定义，我们来完善一下它。我们在renderRow函数的上面添加如下代码：
```js
  onListPressed(data) {
    console.log(data);
    this.props.navigator.push({
      title: data.title,       //新视图的标题
      component: StudyScreen,  //新视图中展示的组件
      passProps: data,         //传递给新视图的数据
    });
  }
```
这样，当用户点击列表的某项时，就会向我们的栈式导航栏中压入一个新的视图窗口。在iphone模拟器中刷新看下我们的实际操作效果吧。
![genie.github.io](/assets/45.png)![genie.github.io](/assets/46.png)
如果我们按下`cmd＋D`组合键，我们可以看到React提供给我们使用的调试选项。
![genie.github.io](/assets/47.png)
选择使用chrome进行调试，将会打开一个新的tab调试页面。按下cmd＋option＋j打开控制台，可以看到如下的调试信息输出。
![genie.github.io](/assets/48.png)
没错，打印的如下信息
```js
Object {title: "Animals", status: "96%"}
```
就是onListPressed函数中的调试语句输出
```js
console.log(data);
```
怎么样，非常简单吧？相信到这里你已经对ReactNative有了更深入的认识。接下来，我们将集中精力于我们刚才留空的`StudyScreen`组件页面。
找到之前创建的`StudyScreen`组件的定义，将其修改成：
```js
class StudyScreen extends Component {
  constructor(props) {
    super(props);
    this.state = {
      loading: false,
      cardData: {
          definition: 'learn',
          chinese: '学习',
          pinyin: 'xue xi'
      }
    };
  }

  render(){
    var spinner = this.state.loading ?
          ( <ActivityIndicatorIOS
            hidden='true'
            size='large'/> ) :
          ( <Card cardData={this.state.cardData}></Card>);
    return (
      <View style={styles.container}>
        {spinner}
        <View style={styles.row}>
          <TouchableHighlight 
            style={[styles.button, styles.buttonPrimary]}
            underlayColor='#84EFC6'>
            <Text style={styles.buttonText}>Got it!</Text>
          </TouchableHighlight>
          <TouchableHighlight 
            style={[styles.button, styles.buttonDanger]}
            underlayColor='#D982EE'>
            <Text style={styles.buttonText}>Not yet</Text>
          </TouchableHighlight>
        </View>
      </View>
    );
  }
}
```
然后添加对应的样式：
```js
  card: {
    padding: 20,
    flexDirection: 'column',
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: 'white',
    shadowColor: "black",
    shadowOpacity: 0.3,
    shadowRadius: 3,
    shadowOffset: {
      height: 0,
      width: 0
    },
    width: 290,
    height: 290,
  },
  definition: {
    fontSize: 30,
    textAlign: 'center',
    marginBottom: 20
  },
  chinese: {
    flex: 1,
    fontSize: 80,
    fontFamily: 'STHeitiTC-Light'
  },
  pinyin: {
    flex: 1,
    fontSize: 40,
  },
  description: {
    marginBottom: 20,
    fontSize: 18,
    textAlign: 'center',
    color: '#656565'
  },

  row : {
    margin:20,
    width: 320,
    flexDirection: 'row',
    alignItems: 'center',
    alignSelf: 'stretch'
  },

  buttonText: {
    fontSize: 18,
    color: 'white',
    alignSelf: 'center'
  },

  button: {
    height: 36,
    flex: 1,
    flexDirection: 'row',
    borderWidth: 1,
    borderRadius: 8,
    margin:20,
    marginBottom: 10,
    alignSelf: 'stretch',
    justifyContent: 'center'
  },

  buttonDanger: {
    backgroundColor: '#BB27DD',
    borderColor: '#BB27DD',
  },

  buttonPrimary: {
    backgroundColor: '#29DF9A',
    borderColor: '#29DF9A',
  },

  nav: {
    flex: 1  
  },
```
是不是觉得信手拈来，相当简单了？看下完成后的效果图。
![genie.github.io](/assets/49.png)

