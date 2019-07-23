## 学习jquery

### 简介
#### 什么是jquery
    jQuery是一个JavaScript函数库。

    jQuery是一个轻量级的"写的少，做的多"的JavaScript库。

    jQuery库包含以下功能：

    HTML 元素选取
    HTML 元素操作
    CSS 操作
    HTML 事件函数
    JavaScript 特效和动画
    HTML DOM 遍历和修改
    AJAX
    Utilities
    提示： 除此之外，Jquery还提供了大量的插件。

#### jquery 安装
    1.直接下载
    https://jquery.com/download/
    下载 jQuery
    有两个版本的 jQuery 可供下载：
    Production version - 用于实际的网站中，已被精简和压缩。
    Development version - 用于测试和开发（未压缩，是可读的代码）
    <script src="jquery-1.10.2.min.js"></script>
    2.网络
    <script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js">

#### 加载运行函数
    jQuery 入口函数:
        $(document).ready(function(){
            // 执行代码
        });
        或者
        $(function(){
            // 执行代码
        });

    JavaScript 入口函数:
    window.onload = function () {
        // 执行代码
    }
    jQuery 入口函数与 JavaScript 入口函数的区别：

 jQuery 的入口函数是在 html 所有标签(DOM)都加载之后，就会去执行。
 JavaScript 的 window.onload 事件是等到所有内容，包括外部图片之类的文件加载完后，才会执行。
 ![](https://www.runoob.com/wp-content/uploads/2019/05/20171231003829544.jpeg)

#### 选择器
- 标签
- 类名
- id

语法|描述
-|-|
$("*") | 选取所有元素
$(this)| 选取当前 HTML 元素 
$("p.intro")  |选取 class 为 intro 的 <p> 元素 
$("p:first")|选取第一个 <p> 元素 
$("ul li:first")|选取第一个 <ul> 元素的第一个 <li> 元素 
$("ul li:first-child")|选取每个 <ul> 元素的第一个 <li> 元素 
$("[href]")|选取带有 href 属性的元素 
$("a[target='_blank']")|选取所有 target 属性值等于 "_blank" 的 <a> 元素 
$("a[target!='_blank']")|选取所有 target 属性值不等于 "_blank" 的 <a> 元素 
$(":button")|选取所有 type="button" 的 <input> 元素 和 <button> 元素 
$("tr:even")|选取偶数位置的 <tr> 元素 
$("tr:odd")|选取奇数位置的 <tr> 元素

#### 事件

鼠标事件|键盘事件|表单事件|文档/窗口事件
-|-|-|-|
click|keypress|submit|load
dblclick|keydown|change|resize
mouseenter|keyup|focus|scroll
mouseleave|	 |blur|unload
hover| | |

### jquery效果
#### - 1.显示隐藏
    $(ele).show(speed，循环，函数)
    $(ele).hide(speed，循环，函数)
    $(ele).toggle(speed，循环，函数) 
    - speed
    可选的 speed 参数规定隐藏/显示的速度，可以取以下值："slow"、"fast" 或毫秒。
    - 循环的方式
        swing linear

#### - 2.淡入淡出
    jQuery fadeIn(speed,callback)//淡入
    jQuery fadeOut(speed,callback)//淡出
    jQuery fadeToggle(speed,callback)//双向
    jQuery fadeTo(speed,opacity,callback)//允许渐变为给定的不透明度（值介于 0 与 1 之间）。

    - speed 属性
        可选的 speed 参数规定效果的时长。它可以取以下值：() "slow"、"fast" 或毫秒。

#### - 3.滑动
    slideDown(speed,callback) 向下滑动
    slideUp(speed,callback) 收回
    slideToggle(speed,callback) 双向

    - speed 属性
        可选的 speed 参数规定效果的时长。它可以取以下值：() "slow"、"fast" 或毫秒。

#### - 4.动画
    $(selector).animate({params},speed,callback);自定义动画
    必需的 params 参数定义形成动画的 CSS 属性。
    可选的 speed 参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。
    可选的 callback 参数是动画完成后所执行的函数名称。

    - 属性使用相对值
     也可以定义相对值（该值相对于元素的当前值）。需要在值的前面加上 += 或 -=：
        height:'+=150px',
        width:'+=150px'
    - 使用预定义值
     您甚至可以把属性的动画值设置为 "show"、"hide" 或 "toggle"：
        height:'toggle'
    - 使用队列功能（依次执行）
        div.animate({height:'300px',opacity:'0.4'},"slow");
        div.animate({width:'300px',opacity:'0.8'},"slow");
        div.animate({height:'100px',opacity:'0.4'},"slow");
        div.animate({width:'100px',opacity:'0.8'},"slow");

#### - 5.停止动画
    $(selector).stop(stopAll,goToEnd);
    可选的 stopAll 参数规定是否应该清除动画队列。默认是 false，即仅停止活动的动画，允许任何排入队列的动画向后执行。
    可选的 goToEnd 参数规定是否立即完成当前动画。默认是 false。
    默认地，stop() 会清除在被选元素上指定的当前动画。

#### - 6.链式

### 操作dom
#### 1.捕获获取内容和属性
获得内容 - text()、html() 以及 val()
获取属性 - attr()

#### 2.设置内容和属性
text() - 设置或返回所选元素的文本内容
html() - 设置或返回所选元素的内容（包括 HTML 标记）
val() - 设置或返回表单字段的值

- 回调
$().txt(function(){return xx})

设置属性 - attr("src","http") -attr({a:1,B:2})

- 回调
$().txt('src',function(){return http})

#### 3.添加元素
$("p").append("追加文本"); - 在被选元素的结尾插入内容
$("p").prepend("在开头追加文本"); - 在被选元素的开头插入内容
    $("body").append(txt1,txt2,txt3);
$("img").after("在后面添加文本"); - 在被选元素之后插入内容
$("img").before("在前面添加文本"); - 在被选元素之前插入内容

- 区别
    append/prepend 是在选择元素内部嵌入。
    after/before 是在元素外面追加。
#### 4. 删除元素
    remove() - 删除被选元素（及其子元素）
    empty() -  empty() 方法删除被选元素的子元素。

- 过滤 $("p").remove(".italic");

#### 5.css 类
addClass() - 向被选元素添加一个或多个类
removeClass() - 从被选元素删除一个或多个类
toggleClass() - 对被选元素进行添加/删除类的切换操作
css() - 设置或返回样式属性

#### 6.css() 方法
css("propertyname"); 返回属性值
css("propertyname","value");设置单个属性值
css({"propertyname":"value","propertyname":"value",...});设置多个属性值

#### 7.元素尺寸
![](https://www.runoob.com/images/img_jquerydim.gif)
width()  方法设置或返回元素的宽度（不包括内边距、边框或外边距）。
height()
innerWidth() 方法返回元素的宽度（包括内边距）。
innerHeight()
outerWidth() 方法返回元素的宽度（包括内边距和边框）。
outerHeight()

!设置了 box-sizing 后，width() 获取的是 css 设置的 width 减去 padding 和 border 的值

### 遍历
#### 向上查找
    parent() 方法返回被选元素的直接父元素。
    parents() 方法返回被选元素的所有祖先元素，它一路向上直到文档的根元素 (<html>)。
        使用可选参数来过滤对祖先元素的搜索。$("span").parents("ul");
    parentsUntil() parentsUntil() 方法返回介于两个给定元素之间的所有祖先元素。
        $("span").parentsUntil("div");

#### 后代
    children() 
        children() 方法返回被选元素的所有直接子元素。
        该方法只会向下一级对 DOM 树进行遍历。
    find()
        find() 方法返回被选元素的后代元素，一路向下直到最后一个后代。
        $("div").find("span");

#### 同辈
    siblings() 方法返回被选元素的所有同胞元素。
        $("h2").siblings("p"); <h2> 的同胞元素的所有 <p> 元素：
    next()  方法返回被选元素的下一个同胞元素。
        该方法只返回一个元素。
    nextAll() 方法返回被选元素的所有跟随的同胞元素。
    nextUntil() 方法返回介于两个给定参数之间的所有跟随的同胞元素。
        $("h2").nextUntil("h6"); 返回介于 <h2> 与 <h6> 元素之间的所有同胞元素：
    prev()
    prevAll()
    prevUntil()
        prev(), prevAll() 以及 prevUntil() 方法的工作方式与上面的方法类似，只不过方向相反而已：它们返回的是前面的同胞元素（在 DOM 树中沿着同胞之前元素遍历，而不是之后元素遍历）。

#### 过滤
    三个最基本的过滤方法是：first(), last() 和 eq()，它们允许您基于其在一组元素中的位置来选择一个特定的元素。
    其他过滤方法，比如 filter() 和 not() 允许您选取匹配或不匹配某项指定标准的元素。

 first() 方法返回被选元素的首个元素。
 last() 方法返回被选元素的最后一个元素
 eq() 方法返回被选元素中带有指定索引号的元素。索引从0开始
 filter() 方法允许您规定一个标准。不匹配这个标准的元素会被从集合中删除，匹配的元素会被返回。
     $("p").filter(".url"); 返回带有类名 "url" 的所有 <p> 元素：
not() 方法返回不匹配标准的所有元素。
    $("p").not(".url"); 下面的例子返回不带有类名 "url" 的所有 <p> 元素：

#### jquery_ajax

#### 什么是ajax
    AJAX = 异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。
    简短地说，在不重载整个网页的情况下，AJAX 通过后台加载数据，并在网页上进行显示。
    使用 AJAX 的应用程序案例：谷歌地图、腾讯微博、优酷视频、人人网等等。


#### scrollTop网页偏移量
兼容 获取
$("html").scrollTop()+$("body").scrollTop()//body.sroll一般为0

设置
$("html,body").scrollTop(200)

#### 自动触发事件
 $('a').trigger("click") 触发事件冒泡，有默认行为
$('a').triggerHandler('click') 无事件冒泡，无默认行为
！在a标签中用 trigger triggerHandler都不会触发a标签默认事件，所有要写在其他地方，不能写在a标签中

#### jquery自定义事件
用trigger
条件
1.事件不能通过eventName添加,通过on
2.事件通过trigger触发

```egg
    $('ele').on('事件'，callback)
    $('ele).trigger('事件')
```

#### 事件命名空间
触发单一click
条件；
    通过on绑定
    通过trigger触发

$('ele').on('click.aa',callback)
$('ele).trigger('click.aa')

！利用trigger触发子元素带命名空间的事件，父元素相同也会触发
利用trigger触发子元素带命名空间的事件，子元素和父元素带相同的也会触发 

#### 事件委托
delegate

$('ul').delegate('li','click',callback)

let add=$('代码片段');
xx.append(add)//添加
add.remove()//删除

#### Dom节点
append(content|fn) 向每个匹配的元素内部追加内容。父标签内容后
    $(".box").appendTo('<div>哈哈</div>')
appendTo(content) 把所有匹配的元素追加到另一个指定的元素元素集合中。
    $("<div>哈哈</div>").appendTo('.box')
prepend(content|fn)  向每个匹配的元素内部前置内容。 父标签内容前

prependTo(content) 把所有匹配的元素前置到另一个、指定的元素元素集合中。

after(content|fn)  在每个匹配的元素之后插入内容。

before() 在每个匹配的元素之前插入内容。
    $(".box").eq(2).before('<div>哈哈</div>')
insertAfter 把所有匹配的元素插入到另一个、指定的元素元素集合的后面。
     $('<div>哈哈</div>').insertAfter($(".box").eq(2))
insertBefore(content) 把所有匹配的元素插入到另一个、指定的元素元素集合的前面。

wrap(html|element|fn) 把所有的段落用一个新创建的div包裹起来 每个匹配的都用单独的一个
    $(".uli").wrap("<div></div>")

unwrap()  移出元素的父元素

wrapAll  所有选中的移到同一个
wrapInner() 在元素里
replaceWith() 替换选中的
replaceAll()
empty() 删除选中节点的全部子元素
remove() 删除选中节点
detach() 删除保留事件或方法
clone() 克隆  true||false 一个布尔值（true 或者 false）指示事件处理函数是否会被复制。


has 选中含有此节点的父节点
$("ul:has(li)")
parent 查找含有子元素的
$(".box:parent")
:hidden 匹配所有不可见元素，或者type为hidden的元素
visible 匹配所有的可见元素



