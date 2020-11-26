#React
## React的介绍
**React：是一个用于构建用户界面的JavaScript库，起源于Facebook的内部项目，用于架设Instagram的网站，2013年5月开源，具有较高的性能，代码逻辑简单。**
React 特点
1.声明式设计 −React采用声明范式，可以轻松描述应用。

2.高效 −React通过对DOM的模拟，最大限度地减少与DOM的交互。

3.灵活 −React可以与已知的库或框架很好地配合。

4.JSX − JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但我们建议使用它。

5.组件 − 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。

6.单向响应的数据流 − React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。
##React的安装
我们要使用React要引用三个库：
+ react.min.js - React 的核心库
+ react-dom.min.js - 提供与 DOM 相关的功能
+ babel.min.js - Babel 可以将 ES6 代码转为 ES5 代码，这样我们就能在目前不支持 ES6 浏览器上执行 React 代码。Babel 内嵌了对 JSX 的支持。通过将 Babel 和 babel-sublime 包（package）一同使用可以让源码的语法渲染上升到一个全新的水平。
##React元素渲染
元素是构成React应用的最小单位，它用于描述屏幕上输出的内容。
将元素渲染到DOM中：
```
<div id="example"></div>

const element = <h1>Hello,word!</h1>
ReactDOM.render(
    element,
    document.getElmentById("example")
);
```
###更新元素渲染
React 元素都是不可变的。当元素被创建之后，你是无法改变其内容或属性的。目前更新界面的唯一办法是创建一个新的元素，然后将它传入 ReactDOM.render() 方法：
```
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>现在是 {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('example')
  );
}
 
setInterval(tick, 1000);
```
*React 只会更新必要的部分值得注意的是 React DOM 首先会比较元素内容先后的不同，而在渲染过程中只会更新改变了的部分。*
+ 1. 使用 ES6 类写法，用 this.props.属性名 来取值。
+ 2. 可以多层 props 来传值，在 ReactDOM.render 定义属性值，传给调用方法 App，再在调用的ES6类调用中用 props.属性直接赋值过去。
```
var myStyle = {color:'red',textAlign:'center'}


class Url extends React.Component {
  render() {
    return <h1>网站地址：{this.props.url}</h1>;
  }
}
class Nickname extends React.Component {
  render() {
    return <h1>网站地址：{this.props.nickname}</h1>;
  }
}

function App(props) {
    return (
        <div>
            <Name name={props.name}/>
            <Url  url={props.url}/>
            <Nickname  nickname={props.nickname}/>
        </div>
    );
}

ReactDOM.render(
     <App name={"菜鸟教程"} url={"http://www.runoob.com"} nickname={"Runoob"}/>,
    document.getElementById('example')
);
```
## React JSX
**JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。

我们不需要一定使用 JSX，但它有以下优点：**
+ JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
+ 它是类型安全的，在编译过程中就能发现错误。
+ 使用 JSX 编写模板更加简单快速。


<font style="color:red;">
注意:

由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性</font>



### 使用JSX
jsx是js的扩展，在jsx中可以使用HTML里的标签,代码中嵌套多个 HTML 标签，需要使用一个标签元素包裹它
```
ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('example')
);
```

### JavaScript 表达式
我们可以在 JSX 中使用 JavaScript 表达式。表达式写在花括号 {} 中。实例如下：
```
ReactDOM.render(
    <div>
      <h1>{1+1}</h1>
    </div>
    ,
    document.getElementById('example')
);
```

### 样式
React 推荐使用内联样式。我们可以使用 camelCase 语法来设置内联样式. React 会在指定元素数字后自动添加 px 。以下实例演示了为 h1 元素添加 myStyle 内联样式：
```
var myStyle = {
    fontSize: 100,
    color: '#FF0000'
};
ReactDOM.render(
    <h1 style = {myStyle}>菜鸟教程</h1>,
    document.getElementById('example')
);
```

通过 style 添加内联样式的时候
```
ReactDOM.render(
    <h1 style = {{fontSize:12}}>菜鸟教程</h1>,
    document.getElementById('example')
);
```

### 注释
1、在标签内部的注释需要花括号
2、在标签外的的注释不能使用花括号
```
ReactDOM.render(
    /*注释 */
    <h1>孙朝阳 {/*注释*/}</h1>,
    document.getElementById('example')
);
```
### 数组
JSX 允许在模板中插入数组，数组会自动展开所有成员:
```
var arr = [
  <h1>菜鸟教程</h1>,
  <h2>学的不仅是技术，更是梦想！</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);
```

## React 组件
实例：
```
function HelloMessage(props) {
    return <h1>Hello World!</h1>;
}
 
const element = <HelloMessage />;
 
ReactDOM.render(
    element,
    document.getElementById('example')
);
```
我们可以用一个函数来定义一个组件：
```
function HelloMessage(props) {
    return <h1>Hello World!</h1>;
}
```
我们还可以使用ES6的class来定义一个组件：
```
class Welcome extends React.Component {
  render() {
    return <h1>Hello World!</h1>;
  }
}
```
<font style="color:red;">注意，原生 HTML 元素名以小写字母开头，而自定义的 React 类名以大写字母开头，比如 HelloMessage 不能写成 helloMessage。除此之外还需要注意组件类只能包含一个顶层标签，否则也会报错。</font>

### 复合组件
我们可以通过创建多个组件来合成一个组件，即把组件的不同功能点进行分离
```
function Name(props) {
    return <h1>网站名称：{props.name}</h1>;
}
function Url(props) {
    return <h1>网站地址：{props.url}</h1>;
}
function Nickname(props) {
    return <h1>网站小名：{props.nickname}</h1>;
}
function App() {
    return (
    <div>
        <Name name="菜鸟教程" />
        <Url url="http://www.runoob.com" />
        <Nickname nickname="Runoob" />
    </div>
    );
}
 
ReactDOM.render(
     <App />,
    document.getElementById('example')
);
```
## React State(状态)
React State(状态)机制：React 把组件看成是一个状态机（State Machines）。通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。
```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
 
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
 
ReactDOM.render(
  <Clock />,
  document.getElementById('example')
);
```
### 将生命周期方法添加到类中

在具有许多组件的应用程序中，在销毁时释放组件所占用的资源非常重要。

每当 Clock 组件第一次加载到 DOM 中的时候，我们都想生成定时器，这在 React 中被称为挂载。

同样，每当 Clock 生成的这个 DOM 被移除的时候，我们也会想要清除定时器，这在 React 中被称为卸载。

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
 
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
 
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
 
  tick() {
    this.setState({
      date: new Date()
    });
  }
 
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
 
ReactDOM.render(
  <Clock />,
  document.getElementById('example')
  ```
实例解析：
componentDidMount() 与 componentWillUnmount() 方法被称作生命周期钩子。
在组件输出到 DOM 后会执行 componentDidMount() 钩子，我们就可以在这个钩子上设置一个定时器。this.timerID 为定时器的 ID，我们可以在 componentWillUnmount() 钩子中卸载定时器。

代码执行顺序：
1. 当 "<Clock />" 被传递给 ReactDOM.render() 时，React 调用 Clock 组件的构造函数。 由于 Clock 需要显示当前时间，所以使用包含当前时间的对象来初始化 this.state 。 我们稍后会更新此状态。
2. React 然后调用 Clock 组件的 render() 方法。这是 React 了解屏幕上应该显示什么内容，然后 React 更新 DOM 以匹配 Clock 的渲染输出。
3. 当 Clock 的输出插入到 DOM 中时，React 调用 componentDidMount() 生命周期钩子。 在其中，Clock 组件要求浏览器设置一个定时器，每秒钟调用一次 tick()。
4. 浏览器每秒钟调用 tick() 方法。 在其中，Clock 组件通过使用包含当前时间的对象调用 setState() 来调度UI更新。 通过调用 setState() ，React 知道状态已经改变，并再次调用 render() 方法来确定屏幕上应当显示什么。 这一次，render() 方法中的 this.state.date 将不同，所以渲染输出将包含更新的时间，并相应地更新 DOM。
5. 一旦 Clock 组件被从 DOM 中移除，React 会调用 componentWillUnmount() 这个钩子函数，定时器也就会被清除。
### 数据自顶向下流动

这通常被称为自顶向下或单向数据流。 任何状态始终由某些特定组件所有，并且从该状态导出的任何数据或 UI 只能影响树中下方的组件。如果你想象一个组件树作为属性的瀑布，每个组件的状态就像一个额外的水源，它连接在一个任意点，但也流下来。

```
function FormattedDate(props) {
  return <h2>现在是 {props.date.toLocaleTimeString()}.</h2>;
}
 
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
 
  tick() {
    this.setState({
      date: new Date()
    });
  }
 
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <FormattedDate date={this.state.date} />
      </div>
    );
  }
}
 
function App() {
  return (
    <div>
      <Clock />
    </div>
  );
}
 
ReactDOM.render(<App />, document.getElementById('example'));
```

### React Props
state 和 props 主要的区别在于 props 是不可变的，而 state 可以根据与用户交互来改变。这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。
使用Props
```
function HelloMessage(props) {
    return <h1>Hello {props.name}!</h1>;
}
 
const element = <HelloMessage name="Runoob"/>;
 
ReactDOM.render(
    element,
    document.getElementById('example')
);
```
默认 Props
你可以通过组件类的 defaultProps 属性为 props 设置默认值，实例如下：
```
class HelloMessage extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}
 
HelloMessage.defaultProps = {
  name: 'Runoob'
};
 
const element = <HelloMessage/>;
 
ReactDOM.render(
  element,
  document.getElementById('example')
);
```
#### State 和 Props组合使用
  以下实例演示了如何在应用中组合使用 state 和 props 。我们可以在父组件中设置 state， 并通过在子组件上使用 props 将其传递到子组件上。在 render 函数中, 我们设置 name 和 site 来获取父组件传递过来的数据。
  ```
  class WebSite extends React.Component {
  constructor() {
      super();
 
      this.state = {
        name: "菜鸟教程",
        site: "https://www.runoob.com"
      }
    }
  render() {
    return (
      <div>
        <Name name={this.state.name} />
        <Link site={this.state.site} />
      </div>
    );
  }
}
 
 
 
class Name extends React.Component {
  render() {
    return (
      <h1>{this.props.name}</h1>
    );
  }
}
 
class Link extends React.Component {
  render() {
    return (
      <a href={this.props.site}>
        {this.props.site}
      </a>
    );
  }
}
 
ReactDOM.render(
  <WebSite />,
  document.getElementById('example')
);
```
#### Props 验证

<font style="color:red;">React.PropTypes 在 React v15.5 版本后已经移到了 prop-types 库。</font>
    <script src="https://cdn.bootcss.com/prop-types/15.6.1/prop-types.js"></script>

Props 验证使用 propTypes，它可以保证我们的应用组件被正确使用，React.PropTypes 提供很多验证器 (validator) 来验证传入数据是否有效。当向 props 传入无效数据时，JavaScript 控制台会抛出警告。
```
var title = "菜鸟教程";
// var title = 123;
class MyTitle extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.title}</h1>
    );
  }
}
 
MyTitle.propTypes = {
  title: PropTypes.string   //tiele的值要为string类型，不然JavaScript控制台会报错！
};
ReactDOM.render(
    <MyTitle title={title} />,
    document.getElementById('example')
);
```

## React 事件处理
### React的基本使用

React 元素的事件处理和 DOM 元素类似。但是有一点语法上的不同:
+ React 事件绑定属性的命名采用驼峰式写法，而不是小写。
+ 如果采用 JSX 的语法你需要传入一个函数作为事件处理函数，而不是一个字符串(DOM 元素的写法)；
HTML通常写法：
```
<button onclick="activateLasers()">
  激活按钮
</button>
```
React中的语法：
```
<button onClick={activateLasers}>
  激活按钮
</button>
```

+ 在 React 中另一个不同是你不能使用返回 false 的方式阻止默认行为， 你必须明确的使用 preventDefault。
```
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('链接被点击');
  }
 
  return (
    <a href="#" onClick={handleClick}>
      点我
    </a>
  );
}
```
### React 里的this指向问题
React里的组件回调函数中的 this，类的方法默认是不会绑定 this 的。如果你忘记绑定 this.handleClick 并把它传入 onClick, 当你调用这个函数的时候 this 的值会是 undefined。
可以在属性初始化时，绑定this的指向
```
class LoggingButton extends React.Component {
  // 这个语法确保了 `this` 绑定在  handleClick 中
  // 这里只是一个测试
  handleClick = () => {
    console.log('this is:', this);
  }
 
  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

你也可以在回调函数中使用箭头函数
```
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }
 
  render() {
    //  这个语法确保了 `this` 绑定在  handleClick 中
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Click me
      </button>
    );
  }
}
```
### 向事件处理程序传递参数
通常我们会为事件处理程序传递额外的参数。例如，若是 id 是你要删除那一行的 id，以下两种方式都可以向事件处理程序传递参数：
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
上面两个例子中，参数 e 作为 React 事件对象将会被作为第二个参数进行传递。通过箭头函数的方式，事件对象必须显式的进行传递，但是通过 bind 的方式，事件对象以及更多的参数将会被隐式的进行传递。
值得注意的是，通过 bind 方式向监听函数传参，在类组件中定义的监听函数，事件对象 e 要排在所传递参数的后面，例如:
```
class Popper extends React.Component{
    constructor(){
        super();
        this.state = {name:'Hello world!'};
    }
    
    preventPop(name, e){    //事件对象e要放在最后
        e.preventDefault();
        alert(name);
    }
    
    render(){
        return (
            <div>
                <p>hello</p>
                {/* 通过 bind() 方法传递参数。 */}
                <a href="https://reactjs.org" onClick={this.preventPop.bind(this,this.state.name)}>Click</a>
            </div>
        );
    }
}
```

#### React 点击事件的 bind(this) 如何传参?
需要通过 bind 方法来绑定参数，第一个参数指向 this,第二个参数开始才是事件函数接收到的参数:
```
<button onClick={this.handleClick.bind(this, props0, props1, ...}></button>
 
handleClick(porps0, props1, ..., event) {
    // your code here
}
```
事件：this.handleclick.bind(this，要传的参数)

函数：handleclick(传过来的参数，event)



## React 条件渲染

### 普通的if条件渲染
在 React 中，你可以创建不同的组件来封装各种你需要的行为。然后还可以根据应用的状态变化只渲染其中的一部分。React 中的条件渲染和 JavaScript 中的一致，使用 JavaScript 操作符 if 或条件运算符来创建表示当前状态的元素，然后让 React 根据它们来更新 UI。

```
function UserGreeting(props) {
  return <h1>欢迎回来!</h1>;
}

function GuestGreeting(props) {
  return <h1>请先注册。</h1>;
}

function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}
 
ReactDOM.render(
  // 尝试修改 isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('example')
);
```

### 元素变量

你可以使用变量来储存元素。它可以帮助你有条件的渲染组件的一部分，而输出的其他部分不会更改。实例的元素变量就是一个函数，它返回一个元素组件，可以被其他组件使用。

```
<script type="text/babel">
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;

    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}
//元素变量
function UserGreeting(props) {  
  return <h1>欢迎回来!</h1>;
}

function GuestGreeting(props) {
  return <h1>请先注册。</h1>;
}

function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      登陆
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      退出
    </button>
  );
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('example')
);
</script>
```

### 与运算符 &&

*与运算符在react中的使用：你可以通过用花括号包裹代码在 JSX 中嵌入任何表达式 ，也包括 JavaScript 的逻辑与 &&，它可以方便地条件渲染一个元素。*

```
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          您有 {unreadMessages.length} 条未读信息。
        </h2>
      }
    </div>
  );
}
 
const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('example')
);
```
### 三目运算符

```
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}
```

### 阻止组件渲染
在极少数情况下，你可能希望隐藏组件，即使它被其他组件渲染。让 render 方法返回 null 而不是它的渲染结果即可实现。组件的 render 方法返回 null 并不会影响该组件生命周期方法的回调。例如，componentWillUpdate 和 componentDidUpdate 依然可以被调用。

## React 列表 & Keys

### 列表的渲染
使用 map() 方法遍历数组生成了一个 1 到 5 的数字列表:
```
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}
 
const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('example')
);
```

### key

+ **key的使用**
Keys 可以在 DOM 中的某些元素被增加或删除的时候帮助 React 识别哪些元素发生了变化。因此你应当给数组中的每一个元素赋予一个确定的标识。

+ **用keys提取组件**
元素的 key 只有在它和它的兄弟节点对比时才有意义。比方说，如果你提取出一个 ListItem 组件，你应该把 key 保存在数组中的这个 "ListItem" 元素上，而不是放在 ListItem 组件中的"li"标签元素上。
```
function ListItem(props) {
  // 对啦！这里不需要指定key:
  return <li>{props.value}</li>;
}
 
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 又对啦！key应该在数组的上下文中被指定这里定义了唯一的key值
    <ListItem key={number.toString()}
              value={number} />
 
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
 
const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('example')
);
```

### 元素的 key 在他的兄弟元素之间应该唯一

数组元素中使用的 key 在其兄弟之间应该是独一无二的。然而，它们不需要是全局唯一的。当我们生成两个不同的数组时，我们可以使用相同的键。

```
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}
 
const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('example')
);
```

### 在 jsx 中嵌入 map()

```
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />

  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

**JSX 允许在大括号中嵌入任何表达式，所以我们可以在 map() 中这样使用：**

```
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
 
      )}
    </ul>
  );
}
```

## React 组件 API

*在本章节中我们将讨论 React 组件 API。我们将讲解以下7个方法:*
+ 设置状态：setState
+ 替换状态：replaceState
+ 设置属性：setProps
+ 替换属性：replaceProps
+ 强制更新：forceUpdate
+ 获取DOM节点：findDOMNode
+ 判断组件挂载状态：isMounted

### 设置状态:setState
    
>setState(object nextState[, function callback])

参数说明
+ nextState，将要设置的新状态，该状态会和当前的state合并
+ callback，可选参数，回调函数。该函数会在setState设置成功，且组件重新渲染后调用。

<font style="color:red;">合并nextState和当前state，并重新渲染组件。setState是React事件处理函数中和请求回调函数中触发UI更新的主要方法。</font>

*关于setState*
不能在组件内部通过this.state修改状态，因为该状态会在调用setState()后被替换。setState()并不会立即改变this.state，而是创建一个即将处理的state。setState()并不一定是同步的，为了提升性能React会批量执行state和DOM渲染。setState()总是会触发一次组件重绘，除非在shouldComponentUpdate()中实现了一些条件渲染逻辑。

```
class Counter extends React.Component{
  constructor(props) {
      super(props);
      this.state = {clickCount: 0};
      this.handleClick = this.handleClick.bind(this);
  }
  
  handleClick() {
    this.setState(function(state) {
      return {clickCount: state.clickCount + 1};
    });
  }
  render () {
    return (<h2 onClick={this.handleClick}>点我！点击次数为: {this.state.clickCount}</h2>);
  }
}
ReactDOM.render(
  <Counter />,
  document.getElementById('example')
);
```

**替换状态：replaceState**
>replaceState(object nextState[, function callback])

+ nextState，将要设置的新状态，该状态会替换当前的state。
+ callback，可选参数，回调函数。该函数会在replaceState设置成功，且组件重新渲染后调用。

replaceState()方法与setState()类似，但是方法只会保留nextState中状态，原state不在nextState中的状态都会被删除。

**设置属性：setProps**
>setProps(object nextProps[, function callback])

+ nextProps，将要设置的新属性，该状态会和当前的props合并
+ callback，可选参数，回调函数。该函数会在setProps设置成功，且组件重新渲染后调用。

设置组件属性，并重新渲染组件。

props相当于组件的数据流，它总是会从父组件向下传递至所有的子组件中。当和一个外部的JavaScript应用集成时，我们可能会需要向组件传递数据或通知React.render()组件需要重新渲染，可以使用setProps()。

更新组件，我可以在节点上再次调用React.render()，也可以通过setProps()方法改变组件属性，触发组件重新渲染。

**替换属性：replaceProps**

>replaceProps(object nextProps[, function callback])

+ nextProps，将要设置的新属性，该属性会替换当前的props。
+ callback，可选参数，回调函数。该函数会在replaceProps设置成功，且组件重新渲染后调用。

replaceProps()方法与setProps类似，但它会删除原有 props。

**强制更新：forceUpdate**

>forceUpdate([function callback])

参数说明
+ callback，可选参数，回调函数。该函数会在组件render()方法调用后调用。
+ forceUpdate()方法会使组件调用自身的render()方法重新渲染组件，组件的子组件也会调用自己的render()。但是，组件重新渲染时，依然会读取this.props和this.state，如果状态没有改变，那么React只会更新DOM。

forceUpdate()方法适用于this.props和this.state之外的组件重绘（如：修改了this.state后），通过该方法通知React需要调用render()

一般来说，应该尽量避免使用forceUpdate()，而仅从this.props和this.state中读取状态并由React触发render()调用。

**获取DOM节点：findDOMNode**

>DOMElement findDOMNode()
返回值：DOM元素DOMElement

如果组件已经挂载到DOM中，该方法返回对应的本地浏览器 DOM 元素。当render返回null 或 false时，this.findDOMNode()也会返回null。从DOM 中读取值的时候，该方法很有用，如：获取表单字段的值和做一些 DOM 操作。

**判断组件挂载状态：isMounted**

>bool isMounted()
返回值：true或false，表示组件是否已挂载到DOM中

## React 组件生命周期

组件的生命周期可分成三个状态：

+ Mounting：已插入真实 DOM
+ Updating：正在被重新渲染
+ Unmounting：已移出真实 DOM

生命周期的方法有：

+ componentWillMount 在渲染前调用,在客户端也在服务端。

+ componentDidMount : 在第一次渲染后调用，只在客户端。之后组件已经生成了对应的DOM结构，可以通过this.getDOMNode()来进行访问。 如果你想和其他JavaScript框架一起使用，可以在这个方法中调用setTimeout, setInterval或者发送AJAX请求等操作(防止异步操作阻塞UI)。

+ componentWillReceiveProps 在组件接收到一个新的 prop (更新后)时被调用。这个方法在初始化render时不会被调用。

+ shouldComponentUpdate 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。
可以在你确认不需要更新组件时使用。

+ componentWillUpdate在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。

+ componentDidUpdate 在组件完成更新后立即调用。在初始化时不会被调用。

+ componentWillUnmount在组件从 DOM 中移除之前立刻被调用。

*以下实例在 Hello 组件加载以后，通过 componentDidMount 方法设置一个定时器，每隔100毫秒重新设置组件的透明度，并重新渲染：*

```
class Hello extends React.Component {
 
  constructor(props) {
      super(props);
      this.state = {opacity: 1.0};
  }
 
  componentDidMount() {
    this.timer = setInterval(function () {
      var opacity = this.state.opacity;
      opacity -= .05;
      if (opacity < 0.1) {
        opacity = 1.0;
      }
      this.setState({
        opacity: opacity
      });
    }.bind(this), 100);
  }
 
  render () {
    return (
      <div style={{opacity: this.state.opacity}}>
        Hello {this.props.name}
      </div>
    );
  }
}
 
ReactDOM.render(
  <Hello name="world"/>,
  document.body
);
```

*以下实例初始化 state ， setNewnumber 用于更新 state。所有生命周期在 Content 组件中。*

```
class Button extends React.Component {
  constructor(props) {
      super(props);
      this.state = {data: 0};
      this.setNewNumber = this.setNewNumber.bind(this);
  }
  
  setNewNumber() {
    this.setState({data: this.state.data + 1})
  }
  render() {
      return (
         <div>
            <button onClick = {this.setNewNumber}>INCREMENT</button>
            <Content myNumber = {this.state.data}></Content>
         </div>
      );
    }
}
 
 
class Content extends React.Component {
  componentWillMount() {
      console.log('Component WILL MOUNT!')
  }
  componentDidMount() {
       console.log('Component DID MOUNT!')
  }
  componentWillReceiveProps(newProps) {
        console.log('Component WILL RECEIVE PROPS!')
  }
  shouldComponentUpdate(newProps, newState) {
        return true;
  }
  componentWillUpdate(nextProps, nextState) {
        console.log('Component WILL UPDATE!');
  }
  componentDidUpdate(prevProps, prevState) {
        console.log('Component DID UPDATE!')
  }
  componentWillUnmount() {
         console.log('Component WILL UNMOUNT!')
  }
 
    render() {
      return (
        <div>
          <h3>{this.props.myNumber}</h3>
        </div>
      );
    }
}
ReactDOM.render(
   <div>
      <Button />
   </div>,
  document.getElementById('example')
);
```

## React AJAX

>React 组件的数据可以通过 componentDidMount 方法中的 Ajax 来获取，当从服务端获取数据时可以将数据存储在 state 中，再用 this.setState 方法重新渲染 UI。
当使用异步加载数据时，在组件卸载前使用 componentWillUnmount 来取消未完成的请求。

以上代码使用 jQuery 完成 Ajax 请求。
```
class UserGist extends React.Component {
  constructor(props) {
      super(props);
      this.state = {username: '', lastGistUrl: ''};
  }
 
 
  componentDidMount() {
    this.serverRequest = $.get(this.props.source, function (result) {
      var lastGist = result[0];
      this.setState({
        username: lastGist.owner.login,
        lastGistUrl: lastGist.html_url
      });
    }.bind(this));
  }
 
  componentWillUnmount() {
    this.serverRequest.abort();
  }
 
  render() {
    return (
      <div>
        {this.state.username} 用户最新的 Gist 共享地址：
        <a href={this.state.lastGistUrl}>{this.state.lastGistUrl}</a>
      </div>
    );
  }
}
 
ReactDOM.render(
  <UserGist source="https://api.github.com/users/octocat/gists" />,
  document.getElementById('example')
);
```

## React 表单与事件

### 表单

>HTML 表单元素与 React 中的其他 DOM 元素有所不同,因为表单元素生来就保留一些内部状态。
在 HTML 当中，像 input, textarea, 和 select 这类表单元素会维持自身状态，并根据用户输入进行更新。但在React中，可变的状态通常保存在组件的状态属性中，并且只能用 setState() 方法进行更新。

一个简单的实例
在实例中我们设置了输入框 input 值 value = {this.state.data}。在输入框值发生变化时我们可以更新 state。我们可以使用 onChange 事件来监听 input 的变化，并修改 state。

```
class HelloMessage extends React.Component {
  constructor(props) {
      super(props);
      this.state = {value: 'Hello Runoob!'};
      this.handleChange = this.handleChange.bind(this);
  }
 
  handleChange(event) {
    this.setState({value: event.target.value});
  }
  render() {
    var value = this.state.value;
    return <div>
            <input type="text" value={value} onChange={this.handleChange} /> 
            <h4>{value}</h4>
           </div>;
  }
}
ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);
```

### React 事件


以下实例演示通过 onClick 事件来修改数据：

```
class HelloMessage extends React.Component {
  constructor(props) {
      super(props);
      this.state = {value: 'Hello Runoob!'};
      this.handleChange = this.handleChange.bind(this);
  }
  
  handleChange(event) {
    this.setState({value: '菜鸟教程'})
  }
  render() {
    var value = this.state.value;
    return <div>
            <button onClick={this.handleChange}>点我</button>
            <h4>{value}</h4>
           </div>;
  }
}
ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);
```

## React Refs

>React 支持一种非常特殊的属性 Ref ，你可以用来绑定到 render() 输出的任何组件上。
这个特殊的属性允许你引用 render() 返回的相应的支撑实例（ backing instance ）。这样就可以确保在任何时间总是拿到正确的实例。

你可以通过使用 this 来获取当前 React 组件，或使用 ref 来获取组件的引用，实例如下：
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();  }
  render() {
    return <div ref={this.myRef} />;  }
}
 
ReactDOM.render(
  <MyComponent />,
  document.getElementById('example')
);
```
