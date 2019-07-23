### 19.6.26 reactDom

1.直接使用 js 包
有顺序
react.development.js
react-dom.development.js
babel.min.js 引那都行

```html
<script src="./js/react.development.js"></script>
<script src="./js/react-dom.development.js"></script>
<script src="./js/babel.min.js"></script>
<script type="text/babel"></script>
```

虚拟 dom
//解析

<script type='text/babel'>
普通
```js
	<script type='text/babel'>
    //虚拟dom
    //babel 用来解析react中的jsx语法  
    // javascriptXml 既可以写js也可以写XML语法

    //1.编写虚拟DOM 不要加引号 react包
    const vDom=<h1>O(∩_∩)O哈哈~ HelloWord</h1> 

    //2.渲染虚拟DOM 用react-dom 包
    // ReactDOM是react-dom的内置对象，用来操作虚拟DOM

    // ReactDOM.render(虚拟dom,要渲染的实际Dom元素)

    ReactDOM.render(vDom,document.querySelector('#div'))


</script>

````
循环渲染
```js
<script type='text/babel'>
    //react循环渲染
     // 0编写数据4
     const arr=['O(∩_∩)O','O(∩_∩)O~','╭(╯^╰)╮'];

    // 1.编写虚拟DOM
        // for 过程性代码   map 指令性代码
        // !在jsx中如果使用变量需要用{}
       const uDom=(<ul>
            {arr.map((item,index)=>(<li key={index}>{item}</li>))}
       </ul>)

    // 2.渲染虚拟Dom
       ReactDOM.render(uDom,document.querySelector('#div'))

</script>
````

#### react 基本使用

虚拟 Dom

- 作用
  提升页面性能，因为每个页面的虚拟 Dom 只渲染一次
  jsx 语法
- 特点  
   1.该语法包含 js 和 Xml,可以写逻辑也可以写标签  
   2.在使用变量时用{}  
   3.组件的虚拟 dom 必须有一个唯一的根元素

#### react 组件（核心内容）(hooks 了解)

1.函数组件

```js
	<script type='text/babel'>
	//    1.函数组件(工厂函数)
		//函数组件return的是虚拟Dom对象
		// ! 函数名首字母必须大写
		function Wb(){
			return (
				<div>wo te are lei</div>
			)
		}
		//2.渲染组件
		ReactDOM.render(<Wb />,document.querySelector('#div1'))

	</script>
```

- 优缺点
  代码简洁，易于编写，但在一些核心操作上逻辑不清楚

  2.类组件（es6 的类封装的组件 sa）
  (1) 类组件的类依赖于 React.Component 属性

- 优缺点
  核心逻辑清晰，易于维护，但编写较复杂（推荐）

#### this 指向

组件中内置对象的 this 都指向组件本身

#### 组件的三大核心属性

- 1.state
  react 的 state 相当于 vue 的 data,用来存储状态/数据
  获取 state this.state.xxx
  操作 state this.setState({
  content:""
  })
  state 中的数据可以灵活使用{boolean?1:2}
- 2.props 传值 插件 父传子
  2.1 在组件标签中参入属性
  2.2 在组件中通过 组件对象.props.属性 传入属性
  2.3 props-types 插件 用来规定传入输下去的必须性，及设置默认属性
  获取{this.props.xx}

```js
	const grong={
        name:"weigong",
        age:102,
        sex:"ii"
    }
	ReactDOM.render(<Com1 {...grong} />,document.querySelector("#box1"))

	- 插件
	prop-types.js 该插件是用来规定传入props中数据的必要性及编写默认数据的
	1.规定属性是否必须传 组件名.propType={}
		 Com2.propType={
			name: PropTypes.string.isRequired
		}
	2.规定默认属性值
		Com2.defaultProps={
            name:"狗剩"
        }
```

- 3.refs 获取/操作虚拟 Dom
  3.1 获取和操作的都是虚拟 Dom

  3.2 组件对象的 ref 和 refs 配合获取虚拟 Dom

- 用法
  在虚拟 DOM 节点上添加 ref 属性
  在组件中获取 组件对象.refs.属性值
  <input placeholder="点击按钮打印" ref='inp1' />{' '}
  this.refs.inp1.value

#### todolist 思路

- 总结 1.当多个子组件共用同一条数据时，我们要将数据存放在父组件 state 中 2.当子组件箱操作父组件的数据时，要
  （1）在父组件中设置操作的函数
  （2）将函数传入子组件 props
  （3）子组件中调用函数并将函数作为实参传入 3.绑定事件要注意，处理函数才能调用，如果想向处理函数传参，可以用匿名函数包住

```js
<script type='text/babel'>

    class Com1 extends React.Component{
        constructor(props){
            super(props);
            this.state={
                arr:["哥伟荣","章思博","往大爷"]
            }
        }
        //子组件向父组件传值
        //1.在父组件定义函数
        add=(val)=>{
            //功能是将子组件的input到父组件中
            let {arr}=this.state;
            arr.unshift(val);
            this.setState({arr})
        }

        deletApp=(idx)=>{
            // console.log(idx)
            let {arr}=this.state;
            arr.splice(idx,1);
            // console.log(arr)
            this.setState({arr})
        }
        componentDidMount(){
            console.log(this.refs.num1)
        }

        //当多个子组件都要用到同一数据的时候，我们要将数据写在父组件中，并使用props传入子组件

        render(){
            return (
                <div className="contBox">
                    <h1>to do list</h1>
                    <Add ref="num1" num={this.state.arr.length} fn={this.add} />
                    <Show arrs={this.state.arr} defn={this.deletApp} />
                </div>
            )
        }
    }

    class Add extends React.Component{
        click=()=>{
            //1.获取input输入的数组
            let val=this.refs.inp.value
            val=val.trim();
            if(val==''){
                return false;
            }
            //2.添加到app组件的state的data中
            //子传父第二步，子调用父组件函数
            this.props.fn(val)
            this.refs.inp.value="";
        }
        at=()=>{
            console.log("haha")
        }
        render(){
            return (
                <div>
                    <input ref='inp' />
                    <button onClick={this.click} >Add#{this.props.num}</button>
                </div>
            )
        }
    }
    class Show extends React.Component{
        delet=(i)=>{
            //点谁删谁 根据索引确定
            // console.log(i)
            this.props.defn(i)
        }
        render(){
            let {arrs}=this.props
            return (
                <div>
                    <ul>
                        {
                            arrs.map((item,index)=>{
                                return (
                                    <li key={index}>{item}{" "} <button onClick={()=>{
                                        this.delet(index)
                                    }}>删除</button></li>
                                )
                            })
                        }
                    </ul>
                    <div>当前已有{arrs.length}条内容</div>
                </div>
            )
        }
    }
    ReactDOM.render(<Com1 />,document.querySelector("#box1"))
</script>
```

#### 可控组件与非可控组件区别

1.可控组件和非可控组件
（1）可控组件
使用 ref 获取的组件虚拟 DOM - 优势：操作方便 - 缺点：性能不好
（2）非可控组件 e.target.value
使用 onChange 事件动态获取组件数据 - 优势：操作数据，节省性能，更符合 react 框架数据控制页面思想 - 缺点：操作较复杂

#### react 生命周期

1.挂载前：componentWillMount  
2.挂载后：componentDidMount  
3.数据更新前：componentWillUpdate  
4.数据更新后：componentDidUpdate  
5.组件卸载前：componentWillUnmount  
6.render 渲染  
生命周期中
（1）componentWillMount->render(渲染页面)->ComponentDidMount
(2) componentWillUpdate->render->componentDidUpdate

//卸载当前组件
ReactDOM.unmountComponentAtNode(document.querySelector('#box1'))

#### react 组件渲染机制及数据更新机制 diff 算法

diff 算法 react 的核心 虚拟 DOM 的初始化与更新虚拟 Dom 进行对比，如果更新，对实际上 DOM 进行局部渲染

1. react 没有双向数据绑定 MVC
2. react 的渲染和数据更新机制
   （1）当组件内数据发生变化时，首先会触发虚拟 Dom 进行相应改变
   （2）将改变后的虚拟 Dom 和自谦的虚拟 Dom 进行对比，确定改变的部分（diff 算法）
   （3）局部刷新实际 Dom 中需要改变的部分

3.由于 react 虚拟 Dom 局部刷新页面，因此性能优化

### 工程化构建 react 项目(react 脚手架)

#### .react 安装

https://github.com/facebook/create-react-app
第一种

1.  cnpm install -g create-react-app
2.  create-react-app my-app 创建 react 项目
3.  cd my-app/
4.  npm start 运行项目

第二种
npx create-react-app my-app
cd my-app
npm start

安装报错 err npm install --save --save-exact --loglevel error react react-dom react-scr
npm config set registry https://registry.npm.taobao.org
//检验是否成功
npm config get registry

    //然后再重新执行create-react-app
    create-react-app my-app

#### react 使用

src 文件夹 将所有 react 的代码都存储在该文件中
名称|作用
-|-|
commponents|存放组件
redux|存放所有 redux 状态管理组件
index.js|入口 js 文件
app.jsx|根组件（在 react 所有）

模块构建项目的编写顺序
1.index.js
渲染根组件的代码 2.在 index.js 中引入根组件并编写根组件 3.创建 components 文件夹，并编写子组件

#### react 组件传值

子传父：父元素给子元素传入参数，子元素调用
父传子：父组件给属性，子元素用 props 接收
兄弟组件传值：子传父，父传给另一个子(麻烦)

pubsub （publish-subscribe[发布-订阅]） 插件

- 作用
  用来解决所有组件传值问题
- 原理
  组件 A 发布数据，组件 B 接收数据
- 安装
  npm install pubsub-js
- 用法 1.在发送数据的组件中引入 pubSub 模块 子组件 1
  import PubSub from 'pubsub-js'
  2.pubsub 模块 发布数据
  模块.publish(key,val) 3.接收数据 在要接收数据的组件中引入 pubsub 模块 子组件 2 4.接收数据
  模块.subscribe(key,callback(key,val))

#### react 路由

- 使用插件实现 react-router

##### npm 加载

引包 7
npm install react-router-dom

import {Route,NavLink,Switch} from 'react-router-dom'

##### react-router 中常用模块为

    1.Route  配置路由的模块  属性
        (1). path 对于路由to属性
        (2). component 对应显示属性
    2.Link/NavLink 用来路由链接 相当于 router-link
        (1).路由链接必须设置to属性来规定跳转的组件路径
        (2).
    3.Switch 路由显示 等同于 router-view

    4.BrowserRouter 一般包裹带路由的根组件 App
    .路由组件(包含路由的组件中)需要写在react-router-dom的router组件中
        在index.js BrowserRouter 一般用在浏览器路由
        import {BrowserRouter} from 'react-router-dom'
        <BrowserRouter><App /></BrowserRouter>
    5.在react-router-dom中暴露了多个模块需要使用结构赋值的方式引入

-navLink link 区别
navLink 可以设置样式（激活太样式）
link 不可以设置样式

#### react 组件规范

    components 一般子组件文件
    pages 配置组件

#### react 路由传参

##### params 写法

1.路由链接 to 属性路径的最后拼接 "/\${id}" 数据可以传字符串之外的其他类型，但会强制转换为字符串

```html
      <NavLink to={`/home/msg/msgDetail/${item.id}`} > {item.contxt}</NavLink>
```

2. 在 route 组件的 path 路径最后添加 "/:数据名"

```html
<Switch>
  <Route path="/home/msg/msgDetail/:id" component="{MsgDetail}"></Route>
</Switch>
```

3.在路由目标组件中的 props 中的 match 中的 params
this.props.match.params.数据名

##### react 路由的 API 写法

类似于 vue history 路由
1.push

- 作用
  跳转之后还能回到原页面 （有记录依次返回）
- 用法
  （组件对象）this.props.history.push("路径")
  ！如果 props 是一个空对象，就不能使用 api 跳转路由

  2.replace

- 作用
  跳转之后可以返回，但回不到原页面 （无记录，直接返回）
- 用法
  组件对象。props.history.replace("路径")

  3.返回原页面默认
  this.props.history.goForward(); 向前 -》
  this.props.history.goBack(); 后退 《-

  4.路由组件的样式改进 ---封装自己的路由组件
  （1）引入默认路由链接组件
  (2）在暴露出的组件写入路由链接组件，并将 props 中的所有属性传入路由链接组件
  (3) 如果想写入样式， 需要在路由链接中写入类名 active,之后，给 active 绑定样式即可

  5.嵌套路由子路由必须包含父路由·

#### redux

cnpm install redux --save

项目的数据集中管理工具.0

- 特点  
   1.易于理解，好上手  
   2.不仅限于 react 使用，其他框架也能使用
- 使用 redux 的场景  
   1.数据量较庞大的项目；  
   2.各组件之间交互较多的项目  
   3.某一组件的数据要全局共享

路径 1：store(存储数据)--》组件

    1.在 index 文件中引入模块 createStore,使用 createStore 创建对象
    ```js
         import { createStore } from "redux"; let store = createStore(controller[参入 reducer 实参]);
     ```

    2.编写 reducer reducer 函数必须返回数据
    ```js
        //reduce 参数有两个参数，第一个是 state 用来存放数据
        // 第二个是 action，用于接收实际的 action 对象
        export function controller(state = 2, action) {
        //判断 action(设计图)，根据 action 来决定我们具体的操作
        return state;
        }
    ```

    3.在 index 文件中将 store 对象传入要使用数据的组件
    ```js
         <App store={store} />
    ```

    4.在组件中使用 store.getState()方法即可获取到 reducer 中返回的数据（state）

路径 2：actionCreator--》reducer--。store-->组件
redux 工作流
![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1562320898794&di=353bb8681cb9dc2bc8801cca916ef5de&imgtype=0&src=http%3A%2F%2Fimg1.ph.126.net%2F4aIL0ACPE0NOzrAAHl1nyw%3D%3D%2F6597821832612316651.jpeg)

- redux 执行流程：
  react 改变 store 数据，先要判断 action 中的方法，通过 store.dispatch(action)把数据给 store，store 又把数据给 reducers，在 reducers 做处理，reducer 可以接收 state，单是绝不能修改 state，所以要深拷贝，然后再把新的 store 给返回，就自动更新了 store，最后在组件中使用 store.subscribe()，就可以监控到 store 是否有变化，如果有，执行对应方法即可。

步骤： 1.在 index 入口文件 引入
import { createStore } from "redux";  
let store = createStore(controller);

controller 为自定义函数写在 reducers 文件

```js
//reduce参数有两个参数，第一个是state 用来存放数据
// 第二个是action，用于接收实际的action对象
export function controller(state = { age: 14 }, action) {
  console.log(state);
  // 判断action(设计图)，根据action来决定我们具体的操作
  if (action.type === "ADD") {
    return state;
  } else if (action.type === "JIAN") {
    return state;
  } else {
    return state;
  }
}
```

2.在 index 中根文件

```js
let render = function() {
  //   console.log("zou");
  ReactDOM.render(<App store={store} />, document.getElementById("root"));
};
//页面的首次渲染
render();
store.subscribe(render);
```

3.页面
this.props.store.dispatch({ type: "JIAN", data: num });

##### subscribe

!。当用户操作数据之后，组件数据不会自动更新，redux 的 store 对象为我们提供了一个方法 subscribe

- 用法  
   store.subscribe(回调函数)
- 作用
  当 store 数据发生改变的时候，就会执行回调函数

### 总结

#### react jsx 语法

JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。
（1）我们不需要一定使用 JSX，但它有以下优点：

- JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
- 它是类型安全的，在编译过程中就能发现错误。
- 使用 JSX 编写模板更加简单快速。

（2）用法
a.可以直接写虚拟 Dom(HTML 标签)
b.可以直接将 js 数据渲染到页面的虚拟 DOm 中，需要加{}包裹

####　 react-ui 移动端 Ant Design Mobile 1.安装
npm install antd-mobile --save

#### react-redux 插件

- 作用
  解决 react 组件和 react 耦合性过高的问题
- redux 代码的缺陷
  redux 和 react 组件的耦合 代码耦合性较高
- 安装插件 react-redux
  react-redux 中解决耦合性问题的主要是组件 provider 和函数 connect

##### 插件使用

1.使用 provider 将要引入 store 的组件包裹起来,解决数据变化监听

```js
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.querySelector("#root")
);
我们要将store通过Provider组件传入，因为Provider
```

2.在要使用 store 数据的组件中，彻底的清除 redux 代码，更换为 react 代码

```js
//使用插件 import PropTypes from "prop-types";
static propTypes = {
    //加法，减法，state
    Add: PropTypes.func.isRequired,
    Jian: PropTypes.func.isRequired,
    count: PropTypes.number.isRequired
  };

将 this.props.store.dispath()
改为 this.props.Add(num)
```

3.引入 connect 函数

```js
import { connect } from "react-redux"; //见下
```

作用
(1)将当前组件进行转换(类似于 bind)，并将转换后的新组件返回出来，新组件将会传入用户输入内容

4.调用 connect 函数，实现返回组件新功能

```js
//count数字 add函数 jian函数
export default connect(
  state => {
    return { count: state };
  },
  { Add, Jian } //connect函数调用传入的实参是组件需要的数据 第二个实参对象中属性值是action中生成的action函数
  // connect函数会自动将回调函数返回的对象和对象实参进行结构赋值，将结构的键值作为新属性传入
)(App); //转换后新组件
```

#### ui 组件和容器组件

- ui 组件 1
  主要用来展示数据集页面内容，一般不操作数据(redux 共享数据)
- 容器组件
  主要操作 redux 共享数据，一般不包括虚拟 dom 等

子组件共享数据

```js
import React from "react";
import PropTypes from "prop-types";
import { connect } from "react-redux"; //加工son组件，从而传入connect数据
class Son extends React.Component {
  static propTypes = {
    count: PropTypes.number.isRequired
  };
  render() {
    return <div>{this.props.count}</div>;
  }
}
export default connect(state => {
  return { count: state };
})(Son);
```

- 步骤 1.将 provider 包裹根组件 2.将 app 加工成容器组件

#### cerate- 安装手脚架报错

清除缓存
npm cache clean --force

#### redux-thunk 是 redux 的插件

- redux-thunk 实现异步代码
- 作用
  一般用于向后台发送请求，获取数据并操作
- redux-thunk 编写步骤
  1.store.js 中引入 redux-thunk(redux-thunk)使用集中暴露，因此引入不需要解构
  2.store.js 中引入 applayMiddleware 函数（在 redux 中引），因此是为了使用中间件
  3.store.js 中在 let store = createStore(count, applyMiddleware(thunk));

  ```js
  import { createStore, applyMiddleware } from "redux";
  //引入 redux-thunk
  import thunk from "redux-thunk";
  ```

  4.将组件中异步操作 state 的代码修改为同步(直接调用 actions 提供的函数)
  5.Actions 中编写异步操作 state 的函数
  (1)异步操作 state 的 action 函数需要返回一个函数，函数的形参会接收到 store 的 dispatch 方法
  (2)手动使用 dispatch 方法发布 action 对象

#### redux 实现实际效果

1.搭建框架
(1)Ui 组件
(2)编写 redux 代码
(3)编写唯一的容器组件（根组件的容器组件）  
2.使用 redux 的数据
(1)使用 react-redux 传入的数据渲染页面
(2)操作 redux 数据
① 注意：操作数据的时候，在 reducer 中返回 state 数据需要解构（适用于 state 是引用类型数据）

#### redux react-redux 总结

##### redux

在 reducer 中 return state 如果 state 是一个引用类型，将无法重新渲染页面

技术难点：监听 redux 的 state 变化的机制 类似 diff 算法，如果直接返回 state，会导致监听机制比对不出前后数据的差异，因此无法触发更新。如果返回解构，会将 state 内容暴露出来，数据变化就可以被监听
Return state（[...state]）

1.Actions action 对象的工厂函数
2.Reducers 操作 state 数据的函数
3.Store 创建 store 传入 reducer 并将 store 对象暴露出去
4.Action-types

Redux 方法： 1.在组件中获取 state 数据 store.getState() 2.在组件中操作 state 数据 store.dispatch(action 对象) 3.订阅数据变化 store.subscribe(回调函数)

##### react-redux 简化 redux 代码,降低了 redux 代码的耦合度

ui 组件 不写 redux 代码

容器组件
a.引入 ui 组件使用 connect 函数加工 ui 组件
b.在渲染容器组件的时候需要使用 Provider 组件包裹，在 Provider 中传入 store 对象
！当路由组件被引入 ui 组件是，需要注意将数据传入路由组件才能传数据的时候需要在路由组件中使用 connect 函数封装为容器组件

##### react-thunk 用来辅助 redux 中异步代码的编写

1.store.js 中引入 redux-thunk(redux-thunk)使用集中暴露，因此引入不需要解构
store.js 中引入 applayMiddleware 函数（在 redux 中引），因此是为了使用中间件
store.js 中在 let store = createStore(count, applyMiddleware(thunk));

```js
import { createStore, applyMiddleware } from "redux";
//引入 redux-thunk
import thunk from "redux-thunk";
```

2.改变传入组件的 action 工厂函数（添加异步代码，并添加手动 dispatch 的代码)

```js
//异步提交action对象，写法不同于普通action对象
export let Async = data => {
  //异步提交不返回action返回对像，在函数内部进行异步操作
  return dispatch => {
    //编写异步代码 形参dispatch会接收到store对象，的dispatch方法
    Axios.get().then(res => {
      dispatch({ type: "Add", data: res });
    });
  };
  //异步的action对象方法，一般用于向后台发送请求，获取数据并操作
};
```

#### react-redux 传递 axios 效果分析逻辑

异步 redux 代码的逻辑 1.引入 redux-thunk 插件 使用 applyMiddleware 调用 2.在 actions.js 中编写 axiso 代码，获取后台数据 3.在 redux 中获取 action 对象的 data 属性值
(1)一般响应数据都是对象或数组，redux 中返回数据结构需要根据数据类型决定

#### redux 注意事项

2.组件
函数组件：名称首字母大写 工厂函数
类组件：名称首字母大写 es6 类概念编写
所有类组件都继承 React.Component
在 render 函数返回虚拟 dom 结构是，不要换行

3.生命周期(常用生命周期)
componentWillMount
render
componentDidMount (发送 axios 请求)
componentwillUpdate
render
componentDidupdate

4.组件的三大特性

    （1）state 组件内的数据管理
    （2）props 组件父传数据给子组件
    Prop-types 插件 建议使用 规定
    static propTypes={
    属性名:PropTypes.数据类型.isRequired
    Func 函数 isRequired 必须传
    }

    （3）refs (onChange) 获取虚拟 dom
    onChange 监听 dom 值改变
    currentTarget 当前
    target 可能冒泡
    通过事件对象的 currentTarget 属性
    e.currentTarget 获取到发生变化 dom 元素

5.react 脚手架工具

      create-react-app3.0.1
      全局安装 支持 es6 模块引入及抛出语法，
      也支持 common.js 语法 require xx ''

      public 共同公有的 index.html
      pack.json 命令
      "react-script" 运行命令
      src 文件夹
      index.js 项目入口

6.组件的拆分
import 引入 机制
a.引入数据包
b.引入组件和 js 文件
c.引入 css/sass 样式

    export 暴露机制
    a.分散暴露 export 引入需要结构{模块名}
    b.集中暴露 export default 直接使用模块名

7.react-router-dom 路由
(1) 根组件必须使用 Router/BrowserRouter 组件包裹
(2)使用路由 引入 Switch Route Link 路由 api 二级路由才能使用
(3) push replace history goForword goBack
(4)路由传参 params

人生若只如初见，何事秋风悲画扇。
等闲变却故人心，却道故人心易变。
骊山语罢清宵半，泪雨霖铃终不怨。
何如薄幸锦衣郎，比翼连枝当日愿。
