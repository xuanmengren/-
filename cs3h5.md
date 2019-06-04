## ps常规
-    ctrl+j 复制图层
-   ctrl+r 标尺
```css
    倍图
    .icon {
    background-image: url(example.png);
    background-size: 200px 300px;
    height: 300px;width: 200px;
    }
    @media only screen and (-Webkit-min-device-pixel-ratio: 1.5),
        only screen and (-moz-min-device-pixel-ratio: 1.5),
        only screen and (-o-min-device-pixel-ratio: 3/2),
        only screen and (min-device-pixel-ratio: 1.5) {
            .icon {
                    background-image: url(example@2x.png);
            }
    }   
```
     <link rel="icon" href="favicon.ico">图标 

## css3基础
### 圆角
    border-radius
    border-top-left-radius
    两个角一起写需要上下在前，左右在后
### 渐变
    线性渐变
    background:linear-gradient(red,green);从上到下
    background:linear-gradient(to left,red,green)从左到右
    径向渐变
     background:radial-gradient(yellow,purple);
### 盒子阴影
    box-shadow: apx bpx cpx dpx yellow;
    a 控制水平位置 正值偏左   0 两边均等
    b 控制水平位置 正值靠下   0 上下均等
    c 模糊程度     
    d 阴影范围
### 过渡
    transition:all 1s; all所有  1s 时间
    transition-delay: 1s;      1s 延迟

### 2d 3d转换
    transfrom
    - translate 位移 translateX translateY
        transform: translate(200px,200px);
    - rotate  旋转  rotateX rotateY
        transform: rotate(200deg,200deg); deg度数
    - scale 缩放  scaleX scaleY
        transform: scale(2,2);   x,y
    - skew 倾斜  skewX  skewY
        transform:skew(30deg,30deg);
    - maxtrix  矩阵 (兼容不好) 组合起来

    - 组合 
        transfrom：translate(200px,200px) rotate(200deg,200deg) scale(2,2) skew(30deg,30deg);
    ! 多个显示只有最后一个实现，想要多个实现，组合成一个

### 动画    

    @keyframes	规定动画。	3
    animation	所有动画属性的简写属性，除了 animation-play-state 属性。	3

    animation-name	规定 @keyframes 动画的名称。	3
    animation-duration	规定动画完成一个周期所花费的秒或毫秒。	3
    animation-timing-function	规定动画的速度曲线。	3
    animation-delay	规定动画何时开始。	3
    animation-iteration-count	规定动画被播放的次数。	3
    animation-direction	规定动画是否在下一周期逆向地播放。	3
    animation-play-state	规定动画是否正在运行或暂停。	3
    animation-fill-mode	规定对象动画时间之外的状态。





### 弹性盒子

#### 父类设置
display:flex/inline-flex
    flex:弹性布局
    inline-flex 内联块级弹性布局
控制主轴方向
    flex-direction:row/column/row-reverse/column-reverse
控制换行
    flex-wrap:
        nowrap
        wrap
        wrap-reverse
控制主轴排序方式(对齐)
    jistify-content
        flex-start 左对齐
        flex-end 右对齐
        center 居中
        space-between 两端对齐中间居中（项目之间间隔相等）
        space-around 两侧间隔相等，（项目边距与边框间隔大一倍）


    align-items
        flex-start 上对齐
        flex-end  下对齐
        center 中对齐
        stretch 不设高度或为auto是充满整屏
        baseline 根据字的下划线

#### 子类设置

    flex 设置宽度比例
    flex:1/2/3/4
    order排序
    1234
    可以设置order:-1;提到前面

用弹性盒子不生效的属性
float：浮动
清除浮动
vertical-align


### @media媒体查询
响应式布局
同一个网页用于多个设备，手机，ipad，pc
<meta name="viewport" content="width=device-width, initial-scale=1.0">

移动端head设置
<meta name="viewport" content="width=device-width，initial-scale=1.0,maximun-scale=1,minimun-scale=1,user-scalable=no" />
user-scalable=no yes,no是否可以缩放
@media only screen and (min-width:960px) and (max-width:1200px){}

### 伪类 
伪类 :
伪元素 ::



## h5移动端

### 语义化更好的内容标签
header  头部信息
footer  底部信息
nav 导航
section  段，节，区域

### 带功能

progress   进度条
- 属性   max   value
```css
    /* 改变进度条样式 */
    progress{
     width: 168px;
     height: 5px;
     color:#f00;
     background:#EFEFF4;
    border-radius: 0.1rem;
 }
  progress::-webkit-progress-bar{     
   background-color: burlywood;
    border-radius: 0.2rem;
}
/* 表示已完成进度背景色 */
progress::-webkit-progress-value{
     background: red;
    border-radius: 0.2rem; 
 }
```


dialog  对话框
- 默认样式 diaplay:none;

details   带详细信息标题 默认隐藏,只显示里面summary标签  open='open' 打开
- 里标签   summary 标题标签

bdi 可拖拽  默认无作用 
- 属性 draggable='true' 可拖拽 

figure 放图片，图表，代码等
- 里标签 figcaption 图表的标题  可以放图表的上或下

article 文章/博客标签

section 电池电量控制
- 里标签 meter 属性 max value  low警告  high也是警告

aside 侧边栏

canvas  画布容器 属性  width height  ????

embed   属性 src


### input新增属性 type类型
color 拾色器
date 
datetime
datetime-local
email
month
number
range
search
tel        maxlength
url 统一资源定位符    协议名、域名，文件夹，文件名
week
time


### 视频和音频
video 
- 属性 
    src  引入地址
    controls='controls' 控制器
    autoplay='autoplay' 自动播放
    loop='loop'循环播放
    muted='muted' 静音播放
    preload 刷新网页是否加载     'metadata'加载   'none'不加载
    poster='地址' 封面

audio
- 属性
    src  引入地址
    controls='controls' 
    autoplay='autoplay' 自动播放
    loop='loop'循环播放
    muted='muted' 静音播放
    preload 刷新网页是否加载     'metadata'加载   'none'不加载


## rem
px像素是兼容所有浏览器，是一个固定值
em 是根据父级缩放字体比例，每次都需要设置父级的宽度
rem 是根据根元素html的缩放比例，ie6-ie8不兼容热门，所以为了兼容性rem px都会写，移动端用rem比较方便网页默认字体16px,html 100%
100%=16px  1px=6.25$, 10px=62.5%
1rem=10px 12px=1.2rem

注意：谷歌浏览器有默认最小值12px,当到达最小值就不会再小了
 
 ## 移动端问题
移动端文件命名标准;
- css
    common.css 公共的
    base.css   基础的
    文件.css  


标准盒模型和怪异盒模型如何设置？
标准盒模型
![](https://images2017.cnblogs.com/blog/1258515/201710/1258515-20171023230013051-545804378.png)
box-sizeing:content-box
在标准模式下，一个块的总宽度= width + margin(左右) + padding(左右) + border(左右)
怪异盒模型
![](https://images2017.cnblogs.com/blog/1258515/201710/1258515-20171023230320941-1160589931.png)
box-sizing:border-box;
一个块的总宽度= width + margin(左右)（即width已经包含了padding和border值）

移动端a标签点击有背景如何去除？
    1.取消a标签在移动端点击时的蓝色
    -webkit-tap-highlight-color: rgba(255, 255, 255, 0);
    -webkit-user-select: none;
    -moz-user-focus: none;
    -moz-user-select: none;
    2.使用图片作为a标签的点击按钮时，当触发touchstart的时候，往往会有一个灰色的背景
    a,a:hover,a:active,a:visited,a:link,a:focus{
        -webkit-tap-highlight-color:rgba(0,0,0,0);
        -webkit-tap-highlight-color: transparent;
        outline:none;
        background: none;
        text-decoration: none;
    }
input框点击时边框颜色统一，如何实现？
input{outline:none} 
 input:focus { outline: none; }

 自己添加的样式 公共样式
 eg:
 l_left{
     float:left;
 }
 l-right{
     float:right;
 }
 清除浮动


 ## 学海石崖
背景图
background:url() no-repeat;
background-position:5px 5px;
background-size:;

input{
    outline:none;
} 
input:focus{
    outline:none;
    border:1px solid #666;
}

base.css\

/* 禁用iPhone中Safari的字号自动调整 */
html {
  -webkit-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
  /* 解决IOS默认滑动很卡的情况 */
  -webkit-overflow-scrolling : touch;
    height: 100%;
    width: 100%;
}

/* 禁止缩放表单 */
input[type="submit"], input[type="reset"], input[type="button"], input {
  resize: none;
  border: none;
}

/* 取消链接高亮  */
body, div, ul, li, ol, h1, h2, h3, h4, h5, h6, input, textarea, select, p, dl, dt, dd, a, img, button, form, table, th, tr, td, tbody, article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section {
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}