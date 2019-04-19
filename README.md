# 面向对象编程
- 用对象的方式编程 
- 面向对象写法
优点：
  - 代码可复用
  - 提高性能
  - 提高开发效率
过程式编程 又叫流水式编程
-  缺点：可复用 
- 优点：简单

 系统的内置对象  
  var arr=[];
  arr.push();
  
 继承
 new 创建实例的过程
使用new关键字调用函数（new ClassA(…)）的具体步骤

```javaScript
1. 创建空对象；
　　var obj = {};

2. 设置新对象的constructor属性为构造函数的名称，设置新对象的__proto__属性指向构造函数的prototype对象；
　　obj.__proto__ = ClassA.prototype;

3. 使用新对象调用函数，函数中的this被指向新实例对象：
　　ClassA.call(obj);　　//{}.构造函数();          

4. 将初始化完毕的新对象地址，保存到等号左边的变量中

5. 如果构造函数return出来的一个新对象，那就这个对象就会取代整个new出来的结果

```

### new 的时候都做了哪些？
- 创建一个新的实例对象
- 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）
- 执行构造函数中的代码（为这个新对象添加属性）
- 返回新对象。


当一个函数没有设置返回值是，它的返回值为unde
如果有返回值 返回返回值
最后一种，就是new的过程返回新对象

```es5写法

```


```es6写法

```

假如说代码有了使用场景，不能添加和修改
backWeek
设计原则和设计模式
开放封闭原则 super()

``` 
<!-es6-!>
  class proson {
    constructor(name,age){
       this.name = name;
       this.age = age;
    }
    speack(){
        console.log(`我是${this.name},我今年${this.age}`)
    }
}
let a = new proson('小红',14); //我是小红,我今年14
a.speack()
class xiaoming extends proson{
    constructor(name,age,sex){
        super(name,age)
        this.sex = sex
    }
    speack(){
        console.log(`我是${this.name},我今年${this.age},性别${this.sex}`)
    }
}
let x = new xiaoming('小明','14','男'); //我是小明,我今年14,性别男
x.speack()
```

用es5写继承
```javaScript
  function person(name,age){
    this.name=name;
    this.age=age;
}
person.prototype.speack=function(){
    console.log("我是"+this.name+",我今年"+this.age);
}

children.prototype=new person();


function children(name,age,sex){
    person.call(this,name,age);
    this.sex=sex;
}
children.prototype.speack=function(){
    console.log("我是"+this.name+",我今年"+this.age+"性别"+this.sex);
}

var pro=new person("李二",30)
var chd=new children("李四",18,"男")
pro.speack()
chd.speack()

```

## 继承中的问题
  容易造成内存浪费（使用prototype公共的)

原型链
  对象与原型之间的链接叫原型链
  原型链的最外层Object.prototype

显示继承
- call 属性 (改变this指向)（only属性）
```js
  person.call(this,name,age);
```


- 继承方法
```js
1.
children.prototype=new person();
2.代码效率低，性能不好（特殊）
extend(person.prototype,children.prototype)
function extend(obj1,obj2){
    for(attr in obj1){
        obj2[attr]=obj1[attr];
    }
}
```

# 面向对象概念

## 1.什么是面向对象
- 把客观对象抽象成属性数据或数据的相关操作，把内部细节和不相关的信息隐藏起来，吧同一类数据和操作绑定在一起，封装成类，并且允许分成不同层次进行抽象，通过继承实现属性和操作的共享
  - 面相对象的分析 OOA （Object-Oriented Analysis）
  - 面相对象的设计 OOD （Object-Oriented Design）
  - 面相对象的编程 OOP （Object Oriented Progra mming）
### 1.1概念
类，对象（实例）
  父类是公共的
  ```js
    class Animal{
        constructor(name){
            this.name = name;
        }
        eat(){
            console.log(`${this.name} eat`);
        }
    }
    let animal = new Person('动物');
    animal.eat();
  ```
### 1.2继承
- 子类继承父类
- 继承可以摆公共的方法抽离出来，提高服用，减少冗(rong)余
```js
   class Animal{
      constructor(name){
          this.name = name;
      }
      eat(){
          console.log(`${this.name}eat`);
      }
      speak (){

      }
  }
  let animal = new Animal('动物');
  animal.eat()

  class Dog extends Animal{
      constructor(name,age){
          super(name);
          this.age=age
      }
      speak (){
          console.log(`${this.name} is barking`)
      }
  }
  let dog = new Dog('狗',5);
  dog.eat();
  dog.speak();
```

### 1.3封装 
- 把数据封装起来
- 减少耦合，不该外部访问的不要让外部访问
- 利于数据的接口权限管理
- es6 目前不支持，一般认为_开头的都会是私有的，不要使用
- 实现
  - public:公有修饰符,可以在类内或者类外使用public修饰的属性或行为,默认修饰符
  - protected: 受保护的修饰符，可以本类和子类中使用potected修饰的属性和行为
  - pivate: 私有修饰符，只可以在类内使用private修饰的属性和行为

```ts
  class Animal {
  public name;
  protected age;
  private weight;
  constructor(name,age,weight) {
      this.name=name;
      this.age=age;
      this.weight=weight;
  }
}
class Person extends Animal {
  private money;
  constructor(name,age,weight,money) {
      super(name,age,weight);
      this.money=money;
  }
  getName() {
      console.log(this.name);
  }
  getAge() {
      console.log(this.age);
  }
  getWeight() {
      console.log(this.weight);
  }
}
let p=new Person('zfpx',9,100,100);
console.log(p.name);
console.log(p.age);
console.log(p.weight);


```
### 1.4多态
- 同一个接口可以不同实现
- 保持接口的开放性和灵活性
- 面向接口编程

```ts

 class Animal{
       public name;
       potected age;
       pivate weight;
       constructor(name,age,weight){
           this.name = name;
           this.age = age;
           this.weight = weight;
       }
   }
   class Person extends Animal {
    private money;
    constructor(name,age,weight,money) {
        super(name,age,weight);
        this.money=money;
    }
    speak() {
        console.log('你好!');
    }    
}
class Dog extends Animal {
    private money;
    constructor(name,age,weight) {
        super(name,age,weight);
    }
    speak() {
        console.log('汪汪汪!');
    }    
}

let p=new Person('zfpx',10,10,10);
p.speak();
let d=new Dog('zfpx',10,10);
d.speak();
```

## 2.1什么事设计
- 按哪一种思路或者标准来实现功能
- 功能相同，可以有不同的设计方案
- 需求如果不断变化，设计的作用才能体现出来
## 2.2 SOLID 五大设计原则

首字母|代指|概念
-|-|-|
S|单一职责原则|单一功能原则认为对象应该仅具有一种单一功能的概念
O|开放封闭原则|开闭原则“软件体应该是对于拓展的开放，但是对于修改封闭的概念
L|里式替换原则|里氏替换原则认为“程序中的对象应该是可以在不改变程序正确的前提下被它的子类所替换”的概念，参考 契约式设计
I|接口隔离原则|接口隔离原则认为“多个特定客户端要好于一个宽泛用途接口的概念
D|依赖反转原则|依赖翻转原则认为一个方法应遵从“依赖于抽象而不是一个实例的概念。依赖注入是该原则的一种实现方式

### 2.2.1 S 单一职责原则
- Single responsibility principle
- 一个程序只做好一件事
- 如果功能特别复杂就进行拆分

### 2.2.2 O 开放封闭原则
- Open Closed Principle
- 对拓展开放，对修改关闭
- 增加需求是，拓展性代码，而非修改已有代码

### 2.2.3 L 里式替换原则
- Liskov Substitution Principle
- 子类能覆盖父类
- 父类能出现的地方子类就能出现
- js使用比较少

### 2.2.4 I 接口隔离原则
- Interface Segregation Principle
- 保持接口的单一独立，避免出来（胖）接口
- js 没有忌口，使用较少


### 2.2.5 依赖倒置原则
- Dependence Inversion Principle
- 面向接口编程，依赖于抽象而不依赖于具体实现
- 使用方只关注接口而不关注具体类的实现
- JS中使用较少（没有接口，弱类型）

## 3 23种设计模式

### 1.创建型 
   - *工厂模式（工厂方法模式、抽象工厂模式、简单工厂模式）
   -  建造者模式
   -  *单例模式
   -  *原型模式
### 2. 结构型模式
   -  适配器模式
   -  装饰器模式
   -  *代理模式
   -  外观模式
   -  *桥接模式
   -  *组合模式
   -  享元模式
### 3. 行为型
   -  策略者模式
   -  模板方法模式
   -  **观察者模式
   -  迭代器模式
   -  职责连链模式
   -  命令模式
   -  备忘录模式
   -  状态模式
   -  访问者模式
   -  中介者模式
   -  解释器模式

## 4工厂模式

###  4.1简单工厂模式

- 简单工厂模式是由一个工厂对象决定创建出哪一种产品类的实例

```js

class Plants{
    constructor(name){
        this.name=name;
    }
    eat(){
        console.log("吃"+this.name)
    }
}

class Apple extends Plants{
    constructor(name){
        super(name);
        this.taste="甜"
    }
}

class Orange extends Plants{
    constructor(name){
        super(name);
        this.taste="酸"
    }
}
//static 修饰符  修饰函数为静态方法  直接可以被类调用 但不可以继承
class  Factory{
    static created(name){
        switch (name){
            case "apple":
                return new Apple("苹果")
            case "orange":
                return new Orange("橘子")
        }
    }
}

let apple=Factory.created("apple");
apple.eat();

```

###  4.1.3经典场景
#### 4.1.3.1 jQuery
```js
    class jQuery{
  constructor(selector){
      let elements = Array.from(document.querySelectorAll(selector));
      let length = elements?elements.length:0;
      for(let i=0;i<length;i++){
          this[i]=elements[i];
      }
      this.length = length;
  }
  html(){

  }
}
window.$ = function(selector){
 return new jQuery(selector);
}
```

### 4.2工厂方法模式
- 工厂方法模式Factory Method，又称多态性工厂模式。
- 在工厂方法模式中，核心的工厂类不在负责所有产品的创建，而是将具体创建的工作交给子类去做

```js
class Plants{
    constructor(name){
        this.name=name;
    }
    eat(){
        console.log("吃"+this.name)
    }
}

class Apple extends Plants{
    constructor(name){
        super(name);
        this.taste="甜"
    }
}

class Orange extends Plants{
    constructor(name){
        super(name);
        this.taste="酸"
    }
}


class AppleFactory{
    created(){
        return new Apple("苹果")
    }
}
class OrangeFactory{
    created(){
        return new Orange("橘子")
    }
}

const setting={
    "apple":new  AppleFactory(),
    "orange":new OrangeFactory()
}

var apple=setting["apple"].created().eat()
var orange= setting["orange"].created().eat()

```

### 4.3抽象工厂模式

- 抽象工厂模式是指当有多个抽象角色时，使用的一种工厂模式
- 抽象工厂模式可以向客户端提供一个接口，是客户端在不必制定产品的具体的情况下，创建多个产品族中的产品对象

```js
    class AppleButton{
    render(){
        console.log("苹果按钮")
    }
}

class AppleIcon{
    render(){
        console.log("苹果图标")
    }
}

class OrangeButton{
    render(){
        console.log("橘子按钮")
    }
}

class OrangeIcon{
    render(){
        console.log("橘子图标")
    }
}

class AppleFactory{
    button(){
        return new AppleButton()
    }
    icon(){
        return new AppleIcon()
    }
}

class OrangeFactory{
    button(){
        return new OrangeButton()
    }
    icon(){
        return new OrangeIcon()
    }
}

const settings={
    "apple":new AppleFactory(),
    "orange":new OrangeFactory()
}

let apple=settings["apple"]
apple.button().render()
apple.icon().render()

```

## 5.单例模式
- 单例模式，是一种常用的软件设计模式。
- 在它的核心结构中只包含一个被称为单例的特殊类。
- 通过单例模式可以保证系统中，应用该模式的一个类只有一个实例。即一个类只有一个对象实例。
### 5.1 ES5单例模式

```
let  Window = function(name) {
    this.name=name;
}
Window.prototype.getName=function () {
    console.log(this.name);
}
Window.getInstance=(function () {
    let window=null;
    return function (name) {
        if (!window)
           window=new Window(name);
        return window;
    }
})();
let window=Window.getInstance('zfpx');
window.getName();
```

### 5.2 透明单例

```
let Window=(function () {
    let window;
    let Window=function (name) {
        if (window) {
            return window;
        } else {
            this.name=name;
            return (window=this);
        }
    }
    Window.prototype.getName=function () {
        console.log(this.name);
    }
    return Window;
})();

let window1=new Window('zfpx');
let window2=new Window('zfpx');
window1.getName();
console.log(window1 === window2)

```

### 5.3 单例与构建分离

```
function Window(name) {
    this.name=name;
}
Window.prototype.getName=function () {
    console.log(this.name);
}

let createSingle=(function () {
    let instance;
    return function (name) {
        if (!instance) {
            instance=new Window();
        }
        return instance;
    }
})();

let window1=new createSingle('zfpx');
let window2=new createSingle('zfpx');
window1.getName();
console.log(window1 === window2)
```

### 5.4 封装变化

```
function Window(name) {
    this.name=name;
}
Window.prototype.getName=function () {
    console.log(this.name);
}

let createSingle=function (Constructor) {
    let instance;
    return function () {
        if (!instance) {
            Constructor.apply(this,arguments);
            Object.setPrototypeOf(this,Constructor.prototype)
            instance=this;
        }
        return instance;
    }
};
let CreateWindow=createSingle(Window);
let window1=new CreateWindow('zfpx');
let window2=new CreateWindow('zfpx');
window1.getName();
console.log(window1 === window2)
```

### 5.5 命名空间
- `用户编写的代码与内部的类/函数/常量/或第三方类/函数/常量之间的名字冲突。
- 为很长的标识符名称创建一个别名（或简短）的名称，提高源代码的可读性。
- 例如jQuery

```jQ
  let $ = {
      ajax(){}
      get(){}
      post(){}
  }
let utils={};
utils.def=function (namespace,fn) {
    let namespaces=namespace.split('.');
    let fnName=namespaces.pop();
    let current=utils;
    for (let i=0;i<namespaces.length;i++){
        let namespace=namespaces[i];
        if (!current[namespace]) {
            current[namespace]={};
        }
        current=current[namespace];
    }
    current[fnName]=fn;
}
utils.def('dom.attr',function (key) {
    console.log('dom.attr');
});
utils.def('dom.html',function (html) {
    console.log('dom.html');
});
utils.def('string.trim',function () {
    console.log('string.trim');
});
utils.dom.attr('src');
utils.string.trim(' aaa ');
```

### 5.6 场景
- 模态窗口

```
class Login{
    constructor() {
        this.element=document.createElement('div');
        this.element.innerHTML=(
            `
            用户名 <input type="text"/>
            <button>登录</button>
            `
        );
        this.element.style.cssText='width: 100px; height: 100px; position: absolute; left: 50%; top: 50%; display: block;';
        /* this.element.style.width='100px';
        this.element.style.height='100px';
        this.element.style.position='absolute';
        this.element.style.left='50%';
        this.element.style.top='50%'; */
        document.body.appendChild(this.element);
    }
    show() {
        this.element.style.display='block';
    }
    hide() {
        this.element.style.display='none';
    }
}
Login.getInstance=(function () {
    let instance;
    return function () {
        if (!instance) {
            instance=new Login();
        }
        return instance;
    }
})();

document.getElementById('showBtn').addEventListener('click',function (event) {
    Login.getInstance().show();
});
document.getElementById('hideBtn').addEventListener('click',function (event) {
    Login.getInstance().hide();
});
```

- store

```
function createStore(reducer) {
    let state;
    let listeners=[];
    function getState() {
        return state;
    }
    function dispatch(action) {
        state=reducer(state,action);
        listeners.forEach(l=>l());
    }
    function subscribe(listener) {
        listeners.push(listener);
        return () => {
            listeners = listeners.filter(item => item!=listener);
            console.log(listeners);
        }
    }
    dispatch({});
    return {
        getState,
        dispatch,
        subscribe
    }
}
let store = createStore();
```

### 5.7 缓存

```
let express=require('express');
let fs=require('fs');
let cache={};
let app=express();
app.get('/user/:id',function (req,res) {
    let id=req.params.id;
    let user=cache.get(id);
    if (user) {
        res.json(user);
    } else {
        fs.readFile(`./users/${id}.json`,'utf8',function (err,data) {
            let user=JSON.parse(data);
            cache.put(id,user);
            res.json(user);
        });
    }
});

app.get('/user',function (req,res) {
    let user=req.query;
    fs.writeFile(`./users/${user.id}.json`,JSON.stringify(user),(err) => {
        console.log(err);
        res.json({code: 0,data: '写入成功'});
    });
});
app.listen(3000);
```

### 5.8LRU缓存
- 为LRU Cache 设计一个数据结构，支持两个操作:
   - get: 如果key在cache中,则返回对应的value值,否则返回-1
   - set: 如果key不在cache中,则将该key和value插入cache中，（注意，如果cache已满，则必须把最近最久未使用的元素从cache中删除 ，如果key在cache中，则重置value的值。

```
class LRUCache{
    constructor(capacity) {
        this.capacity=capacity;
        this.members=[];
    }
    put(key,value) {
        let found=false;
        let oldestIndex=-1;
        let oldestAge=-1;
        for (let i=0;i<this.members.length;i++){
            let member=this.members[i];
            if (member.age > oldestAge) {
                oldestIndex=i;
                oldestAge=member.age;
            }
            if (member.key==key) {
                this.members[i]={key,value,age: 0};
                found=true;
            } else {
                member++;
            }
        }
        if (!found) {
            if (this.members.length>=this.capacity) {
                this.members.splice(oldestIndex,1);
            }
            this.members[this.members.length]={
                key,
                value,
                age:0
            }
        }
    }
    get(key) {
        for (let i=0;i<this.members.length;i++){
            let member=this.members[i];
            if (member.key==key) {
                member.age=0;
                return member.value;
            }
        }    
        return -1;
    }
}

let cache=new LRUCache(3);
cache.put('1',1);
cache.put('2',2);
cache.put('3',3);
console.log(cache.get('1'));
console.log(cache.get('2'));
console.log(cache.get('3'));
cache.put('4',4);
console.log(cache.get('1'));
console.log(cache.get('4'));
console.log(cache);
```

## 6原型模式

### 6.1原型模式

```js
    function Person(name) {
    this.name=name;
    this.getName=function () {
        console.log(this.name);
    }
}
let p1 = new Person('张三');
let p2=new Person('李四');
console.log(p1.getName===p2.getName);
```

```js
    function Person(name) {
    this.name=name;
}
Person.prototype.getName = function () {
    console.log(this.name);
}
let p1 = new Person('张三');
let p2=new Person('李四');
console.log(p1.getName===p2.getName);
```

### 6.2函数和对象

- 函数是一种对象
- 对象都是函数创建的

```js
//函数是一种对象
function Person() {}
console.log(Person instanceof Object);


//对象都是通过函数创建的
let p1=new Person();
let obj1={name: 'zfpx'}
let obj=new Object();
obj2.name='zfpx';
```

- 无论什么时候，只要创建了一个新函数，就会根据一组特定的规则为该函数创建一个 prototype属性，这个属性指向函数的原型对象。在默认情况下，所有原型对象都会自动获得一个 constructor（构造函数）属性，这个属性包含一个指向 prototype 属性所在函数的指针。它们与构造函数没有直接的关系。

- 每当代码读取某个对象的某个属性时，都会执行一次搜索，目标是具有给定名字的属性。搜索首先从对象实例本身开始。如果在实例中找到了具有给定名字的属性，则返回该属性的值；如果没有找到， 则继续搜索指针指向的原型对象，在原型对象中查找具有给定名字的属性。如果在原型对象中找到了这个属性，则返回该属性的值。也就是说，在我们调用 person1.sayName() 的时候，会先后执行两次搜 索。

- 虽然可以通过对象实例访问保存在原型中的值，但却不能通过对象实例重写原型中的值。

- 当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性；换句话说，添加这个属性只会阻止我们访问原型中的那个属性，但不会修改那个属性。即使将这个属性设置为 null ，也 只会在实例中设置这个属性，而不会恢复其指向原型的连接。不过，使用 delete 操作符则可以完全删除实例属性，从而让我们能够重新访问原型中的属性。

- 自定义函数的prototype是由Object创建，所以它的proto指向的就是Object.prototype

- Object.prototype的proto指向的是null

- 自定义函数Foo.proto指向Function.prototype

- 自定义函数Foo.proto指向Function.prototype

- Object.proto指向Function.prototype

- Function.proto指向Function.prototype

- Function.prototype的proto也指向Object.prototype

### 6.3原型链

- 访问一个对象的属性时，先在基本属性中查找，如果没有，再沿着proto这条链向上找，这就是原型链
- hasOwnProperty可以区分一个属性到底是自己的还是从原型中找到

```js
    function Foo(){
    this.a = 10;
}
Foo.prototype.b = 20;

let f1  = new Foo();
console.log(f1.a);
console.log(f1.b);
```

### 6.4原型的优势

- 可以随意扩展
- 可以重写继承的方法

```js
let obj = {};
console.log(obj.toString());
let arr = [1,2,3];
console.log(arr.toString());

```
##7.

## 8.观察者模式
### 1.1编译原理：

### 1.2理解作用域：
-引擎
    - 从头到尾负责整个 JavaScript 程序的编译及执行
-编译器
    - 负责语法分析及代码生成等脏活累活
-作用域
    - 负责收集并维护由所有声明的标识符（变量）组成的一系列查询，并实施一套非常严格的规则，
    确定当前执行的代码对这些标识符的访问权限。

function foo(a) {
var a;
a=2
var b = a;
return 2 + 2;
console.log(2+2)
}
var c = foo( 2 );

