## vue
### 测试（白盒和黑盒）
  - 白盒测试主要针对的是程序代码逻辑，黑盒测试主要针对的是程序所展现给用户的功能，简单的说就是前者测试后台程序后者测试前台展示功能。
### 0.0 vue面试题
https://segmentfault.com/a/1190000016344599

#### 0.1 对于MVVM框架的理解


MVVM 是 Model-View-ViewModel 的缩写。
Model代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑。
View 代表UI 组件，它负责将数据模型转化成UI 展现出来。
ViewModel 监听模型数据的改变和控制视图行为、处理用户交互，简单理解就是一个同步View 和 Model的对象，连接Model和View。
在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。
ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

#### 0.2 Vue的生命周期

beforeCreate（创建前） 在数据观测和初始化事件还未开始
created（创建后） 完成数据观测，属性和方法的运算，初始化事件，$el属性还没有显示出来
beforeMount（载入前） 在挂载开始之前被调用，相关的render函数首次被调用。实例已完成以下的配置：编译模板，把data里面的数据和模板生成html。注意此时还没有挂载html到页面上。
mounted（载入后） 在el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用。实例已完成以下的配置：用上面编译好的html内容替换el属性指向的DOM对象。完成模板中的html渲染到html页面中。此过程中进行ajax交互。
beforeUpdate（更新前） 在数据更新之前调用，发生在虚拟DOM重新渲染和打补丁之前。可以在该钩子中进一步地更改状态，不会触发附加的重渲染过程。
updated（更新后） 在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。调用时，组件DOM已经更新，所以可以执行依赖于DOM的操作。然而在大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。该钩子在服务器端渲染期间不被调用。
beforeDestroy（销毁前） 在实例销毁之前调用。实例仍然完全可用。
destroyed（销毁后） 在实例销毁之后调用。调用后，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不被调用。

- 1.什么是vue生命周期？
答： Vue 实例从创建到销毁的过程，就是生命周期。从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、销毁等一系列过程，称之为 Vue 的生命周期。

- 2.vue生命周期的作用是什么？
答：它的生命周期中有多个事件钩子，让我们在控制整个Vue实例的过程时更容易形成好的逻辑。

- 3.vue生命周期总共有几个阶段？
答：它可以总共分为8个阶段：创建前/后, 载入前/后,更新前/后,销毁前/销毁后。

- 4.第一次页面加载会触发哪几个钩子？
答：会触发 下面这几个beforeCreate, created, beforeMount, mounted 。

5.DOM 渲染在 哪个周期中就已经完成？
答：DOM 渲染在 mounted 中就已经完成了。

#### 0.3 Vue实现数据双向绑定的原理：Object.defineProperty（）

vue实现数据双向绑定主要是：采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty（）来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应监听回调。当把一个普通 Javascript 对象传给 Vue 实例来作为它的 data 选项时，Vue 将遍历它的属性，用 Object.defineProperty 将它们转为 getter/setter。用户看不到 getter/setter，但是在内部它们让 Vue 追踪依赖，在属性被访问和修改时通知变化。

#### 0.4 Vue组件间的参数传递
- 1.父组件与子组件传值
父组件传给子组件：子组件通过props方法接受数据;
子组件传给父组件：$emit方法传递参数
- 2.非父子组件间的数据传递，兄弟组件传值
eventBus，就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。项目比较小时，用这个比较合适。

#### 0.5 Vue的路由实现：hash模式 和 history模式
- hash模式(默认)：在浏览器中符号“#”，#以及#后面的字符称之为hash，用window.location.hash读取；
特点：hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面。
   hash 模式下，仅 hash 符号之前的内容会被包含在请求中，如 http://www.xxx.com，因此对于后端来说，即使没有做到对路由的全覆盖，也不会返回 404 错误。

- history模式：history采用HTML5的新特性；且提供了两个新方法：pushState（），replaceState（）可以对浏览器历史记录栈进行修改，以及popState事件的监听到状态变更。
   history 模式下，前端的 URL 必须和实际向后端发起请求的 URL 一致，如 http://www.xxx.com/items/id。后端如果缺少对 /items/id 的路由处理，将返回 404 错误。
 
#### 0.6 Vue与Angular以及React的区别？
##### 1.与AngularJS的区别
- 相同点：
都支持指令：内置指令和自定义指令；都支持过滤器：内置过滤器和自定义过滤器；都支持双向数据绑定；都不支持低端浏览器。

- 不同点：
AngularJS的学习成本高，比如增加了Dependency Injection特性，而Vue.js本身提供的API都比较简单、直观；在性能上，AngularJS依赖对数据做脏检查，所以Watcher越多越慢；Vue.js使用基于依赖追踪的观察并且使用异步队列更新，所有的数据都是独立触发的。

##### 2.与React的区别
- 相同点：
React采用特殊的JSX语法，Vue.js在组件开发中也推崇编写.vue特殊文件格式，对文件内容都有一些约定，两者都需要编译后使用；中心思想相同：一切都是组件，组件实例之间可以嵌套；都提供合理的钩子函数，可以让开发者定制化地去处理需求；都不内置列数AJAX，Route等功能到核心包，而是以插件的方式加载；在组件开发中都支持mixins的特性。
- 不同点：
React采用的Virtual DOM会对渲染出来的结果做脏检查；Vue.js在模板中提供了指令，过滤器等，可以非常方便，快捷地操作Virtual DOM。

#### 0.7 vue路由的钩子函数
首页可以控制导航跳转，beforeEach，afterEach等，一般用于页面title的修改。一些需要登录才能调整页面的重定向功能。

beforeEach主要有3个参数to，from，next：

to：route即将进入的目标路由对象，

from：route当前导航正要离开的路由

next：function一定要调用该方法resolve这个钩子。执行效果依赖next方法的调用参数。可以控制网页的跳转。

#### 0.8 vuex是什么？怎么使用？哪种功能场景使用它？

- vuex
只用来读取的状态集中放在store中； 改变状态的方式是提交mutations，这是个同步的事物； 异步逻辑应该封装在action中。
- 使用
在main.js引入store，注入。新建了一个目录store，….. export 。

- 场景有：
单页应用中，组件之间的状态、音乐播放、登录状态、加入购物车

- vuex关系图
![](https://segmentfault.com/img/bVOAAF?w=701&h=551)

state
Vuex 使用单一状态树,即每个应用将仅仅包含一个store 实例，但单一状态树和模块化并不冲突。存放的数据状态，不可以直接修改里面的数据。
mutations
mutations定义的方法动态修改Vuex 的 store 中的状态或数据。
getters
类似vue的计算属性，主要用来过滤一些数据。
action 
actions可以理解为通过将mutations里面处里数据的方法变成可异步的处理数据的方法，简单的说就是异步操作数据。view 层通过 store.dispath 来分发 action。

```js
const store = new Vuex.Store({ //store实例
      state: {
         count: 0
             },
      mutations: {                
         increment (state) {
          state.count++
         }
          },
      actions: { 
         increment (context) {
          context.commit('increment')
   }
 }
})
```
modules
项目特别复杂的时候，可以让每一个模块拥有自己的state、mutation、action、getters,使得结构非常清晰，方便管理。

```js
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
 }
const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
 }

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
})
```
#### 0.9 vue-cli如何新增自定义指令？
- 1.创建局部指令
```js
var app = new Vue({
    el: '#app',
    data: {    
    },
    // 创建指令(可以多个)
    directives: {
        // 指令名称
        dir1: {
            inserted(el) {
                // 指令中第一个参数是当前使用指令的DOM
                console.log(el);
                console.log(arguments);
                // 对DOM进行操作
                el.style.width = '200px';
                el.style.height = '200px';
                el.style.background = '#000';
            }
        }
    }
})
```

- 2.全局指令
```js
Vue.directive('dir2', {
    inserted(el) {
        console.log(el);
    }
})
```
- 3组件的使用
```html
<div id="app">
    <div v-dir1></div>
    <div v-dir2></div>
</div>
```
##### vue如何自定义一个过滤器？

```html
    <div id="app">
     <input type="text" v-model="msg" />
     {{msg| capitalize }}
    </div>
```

```js
    var vm=new Vue({
    el:"#app",
    data:{
        msg:''
    },
    filters: {
      capitalize: function (value) {
        if (!value) return ''
        value = value.toString()
        return value.charAt(0).toUpperCase() + value.slice(1)
      }
    }
})
```

全局定义过滤器:

```js
    Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
    })
```

### 1.1 vue指令
#### 1.1.1 v-text
- 详情：
    更新元素的 textContent。如果要更新部分的 textContent ，需要使用 {{ Mustache }} 插值。
- 用法：
    ```html
    <div v-text="tx"></div>
    相当于
    <div>{{tx}}</div>
    ```       
#### 1.1.2 v-html
- 详情：
    更新元素的 innerHTML 。注意：内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译 。如果试图使用 v-html 组合模板,可以重新考虑通过是否通过使用组件来替代。
- ！注意：
    在网站上动态渲染任意 HTML 是非常危险的，因为容易导致 XSS 攻击。只在可信内容上使用 v-html，不能出现在用户提交的内容上。

- 用法：
    ```html
    可以解析元素
    <div v-html='tx'></div>
    相当于
    <div>{{tx}}</div>
    ```   
#### 1.1.3 v-if
- 详情: 
    根据判断条件判断元素是否销毁，显示
- 用法

 v-else
 v-else-if  
#### 1.1.4 v-show
- 详情: 
    根据表达式之真假值，切换元素的 display CSS 属性。
    当条件变化时该指令触发过渡效果。
- 用法
```html
    <div v-show="Boolean">显示</div>
```
#### 1.1.5 v-for
- 详情: 
    基于源数据多次渲染元素或模板块
- 用法

```html
    <div v-for="(item,index) in arr" :key='index'>{{index}}=>{{item}}</div>
```
#### 1.1.6 v-on
- 缩写 @
- 详情: 
    绑定事件监听器
    用在普通元素上时，只能监听 原生 DOM 事件。用在自定义元素组件上时，也可以监听子组件触发的自定义事件
- 用法
```html
    <div v-on:click="btn">点击弹窗</div>
``` 
#### 1.1.7 v-bind
- 缩写 ：
- 详情: 
    动态地绑定一个或多个特性，或一个组件 prop 到表达式。
    在绑定 class 或 style 特性时，支持其它类型的值，如数组或对象
    在绑定 prop 时，prop 必须在子组件中声明。可以用修饰符指定不同的绑定类型
- 用法
```html
    <div v-bind:style="sty">zz</div>
    <div v-bind:class="className">zz</div>
``` 
#### 1.1.8 v-model
- 用法
    在表单控件或者组件上创建双向绑定
- 限定
   - input
   - select
   - textarea
   - components
- 用法
```html
    <input type="text" v-model="ivalue">
    <div>{{ivalue}}</div>
```

#### 1.1.9 v-slot
- 缩写 #
- 限制
   - template
   - 组件 (对于一个单独的带 prop 的默认插槽)
- 用法
    提供具名插槽或需要接收 prop 的插槽。
```html
    - 匿名插槽

    - 具名插槽
```

#### 1.1.10 v-pre

- v-pre将跳过编译过程  
- 用法
    跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。

```html
    <div v-pre>不会编译{{ivalue}}</div>
```

#### 1.1.11 v-cloak
- 用法
这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 [v-cloak] { display: none } 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。
#### 1.1.12 v-once
- 详细
只渲染元素和组件一次。随后的重新渲染,元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。
```html
    <div v-once>只更新一次{{ivalue}}</div>
```

### ??
ref在那块使用 在组件挂载之后使用 mounted
对象的空指针为null 返回为undefined

子组件方法在
self 
this.$refs.子组件.方法

### 1.2 特殊特性 

#### 1.2.1 key

- key 的特殊属性主要用在 Vue 的虚拟 DOM 算法，在新旧 nodes 对比时辨识 VNodes。如果不使用 key，Vue 会使用一种最大限度减少动态元素并且尽可能的尝试修复/再利用相同类型元素的算法。使用 key，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。
- 有相同父元素的子元素必须有独特的 key。重复的 key 会造成渲染错误。

场景：
-  它也可以用于强制替换元素/组件而不是重复使用它。当你遇到如下场景时它可能会很有用：
 - 完整地触发组件的生命周期钩子
 - 触发过渡
 ```html
    <transition>
  <span :key="text">{{ text }}</span>
    </transition>
 ```
 当 text 发生改变时，<span> 会随时被更新，因此会触发过渡。

 #### 1.2.2 ref
 - 在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；
 - 在子组件上，引用就指向组件实例：'

 ref的生命周期
 - 在初始渲染的时候你不能访问它们 - 它们还不存在

```html
    <!-- 子组件在父挂载 -->
    <once ref="once"></once>
    this.$refs.once.方法

    <!-- 在dom中 -->
    <div ref="dom"></div> 
    this.$refs.dom
```
 #### 1.2.3 is ??

 用于动态组件且基于 DOM 内模板的限制来工作。

 ```html
<!-- 当 `currentView` 改变时，组件也跟着改变 -->
<component v-bind:is="currentView"></component>

<!-- 这样做是有必要的，因为 `<my-row>` 放在一个 -->
<!-- `<table>` 内可能无效且被放置到外面 -->
<table>
  <tr is="my-row"></tr>
</table>
 ```

 ### 1.3 生命周期
 ![](https://cn.vuejs.org/images/lifecycle.png)
 #### 1.3.1 beforeCreate
 - 详情
    在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。

#### 1.3.2 created
- 详情
    在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见
#### 1.3.3 beforeMount
- 详情
    在挂载开始之前被调用：相关的 render 函数首次被调用。
    该钩子在服务器端渲染期间不被调用。
#### 1.3.4 mounted
- 详情
    el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。
- 注意：
    注意 mounted 不会承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 vm.$nextTick 替换掉 mounted：
    ```js
        mounted: function () {
        this.$nextTick(function () {
            // Code that will run only after the
            // entire view has been rendered
        })
        }
    ```
#### 1.3.5 beforeUpdate
- 详情(当data里的数据发生变化是运行)
    数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。
#### 1.3.6 updated
- 详情
    当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用计算属性或 watcher 取而代之。
- 注意：
    updated 不会承诺所有的子组件也都一起被重绘。如果你希望等到整个视图都重绘完毕，可以用 vm.$nextTick 替换掉 updated：
    ```js
        updated: function () {
            this.$nextTick(function () {
                // Code that will run only after the
                // entire view has been re-rendered
            })
        }
    ```
#### 1.3.7 beforeDestroy
- 详情（data发生改变）
    实例销毁之前调用。在这一步，实例仍然完全可用。
#### 1.3.8 destroyed
- 详情 
    Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

### 1.4 选项 / 数据
#### 1.4.1 data
- 详情
    Vue 实例的数据对象。Vue 将会递归将 data 的属性转换为 getter/setter，从而让 data 的属性能够响应数据变化。
#### 1.4.2 props
- 详情
    props 可以是数组或对象，用于接收来自父组件的数据。props 可以是简单的数组，或者使用对象作为替代，对象允许配置高级选项，如类型检测、自定义验证和设置默认值。
- 限制
    - type: 可以是下列原生构造函数中的一种：String、Number、Boolean、Array、Object、Date、Function、Symbol、任何自定义构造函数、或上述内容组成的数组。会检查一个 prop 是否是给定的类型，否则抛出警告。Prop 类型的更多信息在此。

    - default: any
为该 prop 指定一个默认值。如果该 prop 没有被传入，则换做用这个值。对象或数组的默认值必须从一个工厂函数返回。
    - required: Boolean
定义该 prop 是否是必填项。在非生产环境中，如果这个值为 truthy 且该 prop 没有被传入的，则一个控制台警告将会被抛出。
    - validator: Function
自定义验证函数会将该 prop 的值作为唯一的参数代入。在非生产环境下，如果该函数返回一个 falsy 的值 (也就是验证失败)，一个控制台警告将会被抛出。你可以在这里查阅更多 prop 验证的相关信息。

```html
<!-- 父传子 -->
<!-- 父组件 -->
    <once :val="value"></one>  
    import Once from './Once'
    data(){
       value1:"父组件要穿给子组件的值", 
    } 
    //挂载
    components:{
        once:Once
    } 
<!-- 子组件 -->
    <div>{{val}}</div> 
    <!-- 1.静态 -->
    props: ["val"]
    <!-- 2.动态 -->
    props:{
        val:{
            限制
        }
    }
```
####  1.4.3 computed
- 详细
    计算属性将被混入到 Vue 实例中。所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例。
- 注意
    注意如果你为一个计算属性使用了箭头函数，则 this 不会指向这个组件的实例，不过你仍然可以将其实例作为函数的第一个参数来访问。
    ```js
        computed: {
            aDouble: vm => vm.a * 2
        }
    ```
    计算属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。注意，如果某个依赖 (比如非响应式属性) 在该实例范畴之外，则计算属性是不会被更新的。
#### 1.4.5 watch
- 详情
    一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性。
```js
    data(){return{a:1}}
    watch:{
        a(val,oldval){}
    }
```
#### 1.4.6 methods
- 详情
    methods 将被混入到 Vue 实例中。可以直接通过 VM 实例访问这些方法，或者在指令表达式中使用。方法中的 this 自动绑定为 Vue 实例。


### 1.5 子父组件的通信
 $on(event,callback)
- 用法
    监听当前实例上的自定义事件。事件可以由vm.$emit触发。回调函数会接收所有传入事件触发函数的额外参数。
$emit( eventName, […args] )
- 用法
    触发当前实例上的事件。附加参数都会传给监听器回调。

```js
    1.方法一
    // 子组件 Once内容
    mounted(){
        this.$emit("shu",参数)
    }

    // 父组件(挂载的子组件)内容
    <once v-on:shu="fn"></once> 
    mounted(){
        fn(data){
            console.log(data)
        }
    }

    2.方法二
    // 子组件 Once内容
    methods: {
        eleFn(){
            this.$emit("shu",参数)
            this.$on("shu",function(){
                console.log(data)
            })
        }   
    }
    // 父组件(挂载的子组件)内容
    <once ref="once"></once>
    mounted(){
        this.$refs.once.eleFn()
    }
```

## 2 vueX
###  2.1什么是vuex
- Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。