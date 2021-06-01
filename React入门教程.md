## React 入门教程

### 基础知识：

使用 React 需要引用三个库：

1. react.js：这是 React 的核心库，那里面就是涉及到 react.js 功能的实现
2. react-dom.js：react-dom.js 提供了与 DOM 相关的内容
3. Browser.js：作用是将 JSX 语法转化成 JavaScript 语法（这一步很消耗时间，在时间上线的时候，应该在服务器上完成）

React 的渲染方式：

> ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。

```js
ReactDOM.render(<h1>Hello, world!</h1>, document.getElementById("example"));
```

JSX 语法规范:
当遇到 HTMl 标签(以<开头的)就用 HTML 规则解析;当遇到代码块(以{开头的)就用 javascript 规则解析.

```js
var names = ["Alice", "Emily", "Kate"];

ReactDOM.render(
	<div>
		{names.map(function (name) {
			return <div>Hello, {name}!</div>;
		})}
	</div>,
	document.getElementById("example")
);
```

组件思想:
一个页面使用不同的部分组成,这每个部分都可以封装成一个组件.
当我用这些组件就像用 HTML 标签一样,插入我们想要的地方.
React.createClass 方法

> 组件使用注意事项: 组件类的第一个字母必须大写，否则会报错，比如 HelloMessage 不能写成 helloMessage。另外，组件类只能包含一个顶层标签，否则也会报错。
> 组件的用法和原生 HTML 标签完全一致,可以任意加入属性，比如 \<HelloMessage name="John"\> ，就是 HelloMessage 组件加入一个 name 属性，值为 John。组件的属性可以在组件类的 this.props 对象上获取，比如 name 属性就可以通过 this.props.name 读取。上面代码的运行结果如下。

组件特殊的属性:this.props.children

this.props 对象的属性和组件的属性一一对应,但是有一个例外,就是 this.props.children 属性,它表示组件的所有子节点

```js
var NotesList = React.createClass({
	render: function () {
		return (
			<ol>
				{React.Children.map(this.props.children, function (child) {
					return <li>{child}</li>;
				})}
			</ol>
		);
	},
});

ReactDOM.render(
	<NotesList>
		<span>hello</span>
		<span>world</span>
	</NotesList>,
	document.body
);
```

**注意**<div style='color:red;'>这里需要注意， this.props.children 的值有三种可能：如果当前组件没有子节点，它就是 undefined ;如果有一个子节点，数据类型是 object ；如果有多个子节点，数据类型就是 array 。所以，处理 this.props.children 的时候要小心。

React 提供一个工具方法 React.Children 来处理 this.props.children 。我们可以用 React.Children.map 来遍历子节点，而不用担心 this.props.children 的数据类型是 undefined 还是 object。</div>
