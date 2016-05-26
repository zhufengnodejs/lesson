title: T.React
speaker: 珠峰培训
url: https://github.com/zhufengpeixun
transition: slide3
files: /js/demo.js,/css/demo.css,/js/zoom.js
theme: blue
usemathjax: yes

[slide]
##React
React 是一个用于<span class="text-danger">构建用户界面</span>的JavaScript<span class="text-danger">库</span>

[note]
许多人使用React作为MVC架构的V层。 尽管React并没有假设过你的其余技术栈， 但它仍可以作为一个小特征轻易地在已有项目中使用
React为了更高的性能而使用虚拟DOM作为其实现。 它同时也可以由服务端Node.js渲染,而不需要过重的浏览器DOM支持
React实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。
有了组件化的实现，我们可以很直观的将一个复杂的页面分割成若干个独立组件，再将这些独立组件组合完成一个复杂的页面。这样既减少了逻辑复杂度，又实现了代码的重用

[/note]


[slide]
##安装React
```
bower install react --save
bower install babel --save
```

[slide]
##React初体验
```
  <script src="../bower_components/react/react.js"></script>
  <script src="../bower_components/react/react-dom.js"></script>
  <script src="../bower_components/babel/browser.js"></script>
```
* `script`中的`type`属性为`text/babel`,因为React独有的JSX语法,跟JavaScript不兼容  {:&.rollIn}
* react.js 是 React 的*核心*库
* react-dom.js 是提供与*DOM*相关的功能
* browser.js 的作用是将`JSX`语法转为`JavaScript`语法


[slide]
##ReactDOM.render
`ReactDOM.render` 是 `React` 的最基本方法，用于将<span class="text-danger">模板</span>转为<span class="text-danger">HTML</span>语言，并插入指定的 DOM 节点
```
ReactDOM.render(<h1>Hello, world!</h1>,document.getElementById('app'));
```
上面代码将一个h1标题，插入app元素内部

[slide]
##JSX 语法
* 遇到 HTML 标签（以 < 开头），就用 HTML 规则解析
* 遇到代码块（以 { 开头），就用 JavaScript 规则解析
```
var names = ['刘德华', '范冰冰', '郭跃'];
ReactDOM.render(
  <div>
  {
    names.map(function (name) {
      return <div>Hello, {name}!</div>
    })
  }
  </div>,
  document.getElementById('app')
);
```

[slide]
##组件
React.createClass
React 允许将代码封装成<span class="text-danger">组件</span>，然后像插入普通<span class="text-danger">HTML标签</span>一样，在网页中插入这个组件
* 组件类的第一个字母必须<span class="text-danger">大写</span>  {:&.rollIn}
* 组件类能且只能包含<span class="text-danger">一个顶层标签</span> 
* 组件<span class="text-danger">实例中的属性</span>可以在组件类中通过`this.props.属性名`获取 
```
var Message = React.createClass({
    render: function() {
        return <h1>Hello {this.props.name}</h1>;
    }
});
```

[slide]
##PropTypes
组件类的`PropTypes`属性，就是用来验证传入组件实例的属性是否符合要求
```
 propTypes: {
        title: React.PropTypes.string.isRequired,
    }
```

[slide]
##this.props.children
`this.props`对象的属性与组件实例的属性一一对应，但是有一个例外，就是`this.props.children`属性。它表示组件的<span class="text-danger">所有子节点</span>
```
 React.Children.map(this.props.children, function (child) {
                        return <li>{child}</li>;
                    })
```

[slide]
##数据流
* React中数据的流向是单向的，即从<span class="text-danger">父节点流向子节点</span>（子组件只需要从父组件获取props渲染即可） {:&.rollIn}
* 组件内部有自己的状态，这些状态只能组件<span class="text-danger">内部修改</span>，保持独立性
* getDefaultProps 定义初始化`props`钩子函数
* getInitialState 定义初始化`state`钩子函数

[slide]
##state和props
* state 每一个组件都有自己的state，一开始有一个初始状态，然后用户互动，导致<span class="text-danger">状态变化</span>，从而触发<span class="text-danger">重新渲染UI</span>  {:&.rollIn}
* props 通过`props`可以把任意类型的数据属性传递给组件
* state存放的是不稳定的，<span class="text-danger">容易变化</span>的组件数据，而且state只存在于组件的内部
* 把props当成是组件的数据源，一般用来存放组件初始后<span class="text-danger">不变的数据和属性</span>
* `this.props`表示那些一旦定义，就不再改变的特性，而`this.state`是会随着用户互动而产生变化的特性。


[slide]
##组件的生命周期
* React为每个组件都提供了简洁的生命周期API，去响应组件在不同阶段（<span class="text-danger">创建</span>时，<span class="text-danger">存在</span>时，<span class="text-danger">销毁</span>时）执行相应的操作，更精确的管理每一个组件。  {:&.rollIn}
* 钩子函数 在组件生命周期中<span class="text-danger">某个确定的时间点</span>执行的函数
* 实例化（渲染前） 
    * getDefaultProps()  生命周期中只会执行一次,获取<span class="text-danger">默认的属性</span>  {:&.rollIn}
    * getInitialState() 生命周期中只会执行一次,获取<span class="text-danger">初始状态</span>
    * componentWillmount() 将要把这个组件<span class="text-danger">插入到DOM</span>中
    * render() 插入这个组件到DOM中
* 组件存在期（渲染为真实的DOM）
    * componentDidMount()   {:&.rollIn}
这个组件已经插入到DOM中
    * shouldComponentUpdate() 判断组件<span class="text-danger">是否需要更新</span>
    * componentWillUpdate() 将要<span class="text-danger">执行组件更新</span>
    * componentWillUnmount() 组件将要从DOM中<span class="text-danger">移除</span>
* 销毁期
    * componentDidUnmount() 组件<span class="text-danger">销毁</span>

[slide]
##获取真实的DOM节点
* 组件并不是真实的DOM节点,叫做<span class="text-danger">虚拟DOM</span>,只有当它插入文档以后,才会变成真实的DOM  {:&.rollIn}
* 所有的 DOM 变动，都先在虚拟 DOM 上发生，然后再将实际发生变动的部分，反映在真实 DOM上
* 组件的子元素必须要有一个`ref`属性，然后在组件中才可以通过`this.refs.[refName]`获取此真实的DOM元素

[slide]
##ajax加载数据
组件的数据来源，通常是通过`Ajax`请求从服务器获取，可以使用`componentDidMount`方法设置 Ajax 请求，等到请求成功，再用` this.setState`方法修改状态，从而重新渲染UI

[slide]
##mixin
让不同的组件共用同一部分逻辑，实现代码重用



