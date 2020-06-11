## **标题：基础小白快速打造炫酷个人网站**

## 效果展示：<http://lw688-lw.stor.sinaapp.com/lw/index.html>

## 课程介绍

在这个互联网时代，如何把自己推销出去很重要，word制作简历，打印铺打印，面试网站建立个人简历都很重要，但是大家都是一致的，平平无奇，那我们如何在芸芸众网络中，让我们的简历与众不同，让用人单位更好的了解你。

我们可以去互联网建立一个自己的个人展示网站，网站包含自己的介绍、个人经历、个人作品，技能介绍等，对面试非常有帮助，尤其是一些应届毕业生，提高逼格和薪资必不可少，可以将个人网站部署到免费的云服务和空间供别人浏览。

案例展示：

 苹果5C   <https://www.dowebok.com/demo/2014/77/index8.html>

360安全路由器  <https://www.dowebok.com/demo/2014/77/index10.html>

接下来我就带大家去利用 jQuery 的插件fullPage.js ，css3动画库animate.css搭建个人展示网站；

## 关于fullPage.js

fullPage.js 是一个基于 jQuery 的插件，它能够很方便、很轻松的制作出全屏网站。如今我们经常能见到全屏网站，尤其是国外网站。这些网站用几幅很大的图片或色块做背景，再添加一些简单的内容，显得格外的高端大气上档次。

### 兼容性

fullPage.js 兼容所有的现代浏览器，以及一些旧版浏览器，如 Internet Explorer 9，Opera 12 等都能兼容。 可兼容支持 CSS3 的浏览器与非支持 CSS3 的浏览器，适用于旧版浏览器。 同时，手机、平板电脑和触摸屏电脑还提供触屏支持。

### ullPage.js的功能

支持鼠标滚动、支持前进后退和键盘控制、多个回调函数、支持手机、平板触摸事件、支持 CSS3 动画、支持窗口缩放、窗口缩放时自动调整、可设置滚动宽度、背景颜色、滚动速度、循环选项、回调、文本对齐方式等等

官网： <https://alvarotrigo.com/fullPage/zh/>

<https://github.com/alvarotrigo/fullPage.js/tree/master/lang/chinese#fullpagejs>

## 个人网站准备工作

### 插件引用

01、引入fullpage.css

02、插件依赖于jQuery，所以你还需要下载jQuery，并且在Fullpage插件之前引入。

```html
<link rel="stylesheet" type="text/css" href="fullpage/jquery.fullPage.css" />
<script src="fullpage/jquery.min.js"></script>
<script type="text/javascript" src="fullpage/jquery.fullPage.js"></script>
```

03 、对于内容比较多的页面，可以设置右侧的滚动条，但是默认情况下无法滚动，你需要jquery.slimscroll.min.js文件来自定义滑条滚动效果。

如果 scrollOverflow 设置为 true，一般情况下我们不需要设置；

```html
<script type="text/javascript" src="/fullpage/jquery.slimscroll.min.js"></script>
```

### HTML 结构

用一个div盒子嵌套类名为section的盒子，需要几屏就在里面嵌套几个，最外层的大盒子需要设置一个id="fullpage"，作为我们初始化插件使用；

```html
<div id="fullpage">
    <div class="section">第一屏</div>
    <div class="section">第二屏</div>
    <div class="section">第三屏</div>
    <div class="section">第四屏</div>
</div>
```

### 初始化fullPage插件

```js
    <script>
        // 初始化插件
        $(function(){
            $('#fullpage').fullpage({

            });
        })
    </script>
```

### 基本框架完成

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 引入fullpage的css -->
    <link rel="stylesheet" href="css/fullpage.min.css">
    <!-- 引入对应的JS文件 -->
    <script src="js/jQuery.js"></script>
    <script src="js/fullpage.min.js"></script>
    <script>
        // 初始化插件
        $(function(){
            $('#fullpage').fullpage({

            });
        })
    </script>
    <style>
        .section {
            font-size: 160px;
            font-weight: 700;
        }
    </style>
</head>
<body>
    <div id="fullpage">
        <div class="section">1</div>
        <div class="section">2</div>
        <div class="section">3</div>
        <div class="section">4</div>
    </div>
</body>
</html>
```

## 操作步骤

### 设置背景

sectionsColor  可以设置每一屏的背景颜色；

语法如下：

```js
// 设置每屏的背景颜色
sectionsColor:['#f00','#0f0','#00f','#f0f']
```

### 设置导航

#### 侧边小圆点

navigation取值为true表示显示侧边的小圆点导航

```js
//显示右侧的导航圆点
navigation:true
```

如果想要更改小圆点的样式可以直接去F12产看代码，找到对应的代码利用css的层叠属性将原有的颜色覆盖掉；

```css
#fp-nav ul li a span {
    background: #fff;
}
```

#### 绑定导航菜单设置

**Menu** --- 默认值：false，是一个选择器可以用来指定要与滚动互动的导航菜单，有点类似与Bootstrap的滚动监听。这样到滚动到某个section时，对应的菜单会被自动添加active类。

为了让自定义导航菜单和屏幕section互动，需要给菜单添加一个HTML5的自定义属性（data-menuanchor），需要和锚文本设置相同的内容，例如下面的示例代码：

**注意：**这个选项不会自动生成一个导航菜单，仅仅是给指定的菜单中当前菜单项添加一个active活动类。

​           必须配合

```html
    <ul id="menu">
        <li data-menuanchor="page1"><a href="#page1">首页</a></li>
        <li data-menuanchor="page2"><a href="#page2">个人简介</a></li>
        <li data-menuanchor="page3"><a href="#page3">专业技能</a></li>
        <li data-menuanchor="page4"><a href="#page4">作品展示</a></li>
        <li data-menuanchor="page5"><a href="#page5">联系方式</a></li>
    </ul>
```

```js
$('#fullpage').fullpage({
    // 给每一屏设置对应的锚点
    anchors:['page1','page2','page3','page4','page5'],
    // 绑定菜单，设定的相关属性与 anchors 的值对应后，菜单可以控制滚动
    menu: '#menu'
});
```

### 设置效果循环滚动

```js
// 设置效果循环滚动
continuousVertical:true,
```

### 设置页面加载运动曲线easingcss3

`cubic-bezier` 又称**三次贝塞尔**，主要是为 `animation` 生成速度曲线的函数，规定是 `cubic-bezier(<x1>, <y1>, <x2>, <y2>)`

以上的设置x1和y1表示刚开始的速度，x2和y2表示结束的速度变化

资料网站：<https://www.runoob.com/cssref/func-cubic-bezier.html>

```js
 easingcss3: 'cubic-bezier(0.175, 0.885, 0.320, 2)'
```

<https://www.runoob.com/cssref/func-cubic-bezier.html>

## 完成对应的css布局



## 利用回调函数添加对应动画

#### afterLoad设置滚动到某一个屏幕

afterLoad滚动到某一屏后的回调函数，接收 anchorLink 和 index 两个参数，anchorLink 是锚链接的名称，index 是序号，从1开始计算

```js
        //当加载某一屏的时候去执行一个函数，link代表锚点名称,index代表当前的屏幕，index从1开始计算
        afterLoad: function (link, index) {
            // 第一屏的时候
            if (index == 1) {
                
            }
            // 第二屏的时候
            if (index == 2) {
                
            }
            // 第三屏的时候
            if (index == 3) {
               
            }
            // 第四屏
            if (index == 4) {
               
            }
            // 第无屏
            if (index == 5) {
               
            }
        }
```

#### onLeave设置鼠标离开后的动画

onLeave  滚动前的回调函数，接收 index、nextIndex 和 direction 3个参数：index 是离开的“页面”的序号，从1开始计算；nextIndex 是滚动到的“页面”的序号，从1开始计算；direction 判断往上滚动还是往下滚动，值是 up 或 down。

```js
        //当从index（当前的所在的屏幕）屏幕去往nextIndex（要从当前去往的屏幕）屏幕，dir当前滚动的方向
        onLeave: function (index, nextIndex, dir) {
            // 第一屏的时候
            if (index == 1) {
            
            }
            // 第二屏的时候
            if (index == 2) {
        
            }
            // 第三屏的时候
            if (index == 3) {
 
            }
            // 第四屏
            if (index == 4) {
            }
            // 第无屏
            if (index == 5) {
                
            }
        }
```

fullpage回调函数配合animate.min.css可以完成对应的动画效果；

### animate.min.css简介

强大的跨平台的预设css3动画库，内置了很多典型的css3动画，兼容性好使用方便

中文网  <http://www.animate.net.cn/>

#### 第一步. 引入animate.css文件

也可以使用http://www.bootcdn.cn/animate.css/的服务

```html
<head>
  <link rel="stylesheet" href="animate.min.css">
</head>
```

#### 第二步. 给指定的元素加上指定的动画样式名

第一个animated是必须添加的样式名，第二个是指定的动画样式名。

```html
<div class="animated fadeInUp"></div>
```

#### 配合JQ语法添加删除动画

```js
$('选择器').addClass('类名')
$('选择器').removeClass('类名')
```

## 免费空间上传

网址    <https://www.sinacloud.com/>

控制台    -----    云应用SAE  ----  存储与CDN  -----   Storage   ---  Bucket管理 ----   新建Bucket ---  管理文件 ---- 上传压缩包

上传完压缩包以后就会自动解压一份，打开可以这季节点击 index.html 访问

![](C:\Users\admin\Desktop\个人简介网站\相关资料\新浪云\00.png)



**================================     一些资料        ============================**



## fullpage.js报如下错的解决办法

```
控制台报错：fullPage: Fullpage.js version 3 has changed its license to GPLv3 and it requires a `licenseKey` option. Read about it here:

解决办法：

在fullpage.js文件中查找licenseKey，删除如下代码

if(!isOK){
　　showError('error', 'Fullpage.js version 3 has changed its license to GPLv3 and it requires a `licenseKey` option. Read about it here:');
　　showError('error', 'https://github.com/alvarotrigo/fullPage.js#options.');
}

删除后将下一行的else也删掉，变成如下代码
if(l && l.length < 20){
　　console.warn('%c This website was made using fullPage.js slider. More info on the following website:', msgStyle);
　　console.warn('%c https://alvarotrigo.com/fullPage/', msgStyle);
}
```



## 相关选项设置

|                                   |        |             |                                                              |
| --------------------------------- | ------ | ----------- | ------------------------------------------------------------ |
| verticalCentered                  | 字符串 | true        | 内容是否垂直居中                                             |
| resize                            | 布尔值 | false       | 字体是否随着窗口缩放而缩放                                   |
| **slidesColor**                   | 函数   | 无          | 设置背景颜色                                                 |
| **anchors**                       | 数组   | 无          | 定义锚链接                                                   |
| scrollingSpeed                    | 整数   | 700         | 滚动速度，单位为毫秒                                         |
| easing                            | 字符串 | easeInQuart | 滚动动画方式                                                 |
| **menu**                          | 布尔值 | false       | 绑定菜单，设定的相关属性与 anchors 的值对应后，菜单可以控制滚动 |
| navigation                        | 布尔值 | false       | 是否显示项目导航                                             |
| navigationPosition                | 字符串 | right       | 项目导航的位置，可选 left 或 right                           |
| navigationColor                   | 字符串 | #000        | 项目导航的颜色                                               |
| navigationTooltips                | 数组   | 空          | 项目导航的 tip                                               |
| slidesNavigation                  | 布尔值 | false       | 是否显示左右滑块的项目导航                                   |
| slidesNavPosition                 | 字符串 | bottom      | 左右滑块的项目导航的位置，可选 top 或 bottom                 |
| controlArrowColor                 | 字符串 | #fff        | 左右滑块的箭头的背景颜色                                     |
| loopBottom                        | 布尔值 | false       | 滚动到最底部后是否滚回顶部                                   |
| loopTop                           | 布尔值 | false       | 滚动到最顶部后是否滚底部                                     |
| loopHorizontal                    | 布尔值 | true        | 左右滑块是否循环滑动                                         |
| **autoScrolling**                 | 布尔值 | true        | 是否使用插件的滚动方式，如果选择 false，则会出现浏览器自带的滚动条 |
| **scrollOverflow**                | 布尔值 | false       | 内容超过满屏后是否显示滚动条                                 |
| css3                              | 布尔值 | false       | 是否使用 CSS3 transforms 滚动                                |
| paddingTop                        | 字符串 | 0           | 与顶部的距离                                                 |
| paddingBottom                     | 字符串 | 0           | 与底部距离                                                   |
| fixedElements                     | 字符串 | 无          |                                                              |
| normalScrollElements              |        | 无          |                                                              |
| keyboardScrolling                 | 布尔值 | true        | 是否使用键盘方向键导航                                       |
| touchSensitivity                  | 整数   | 5           |                                                              |
| **continuousVertical**            | 布尔值 | false       | 是否循环滚动，与 loopTop 及 loopBottom 不兼容                |
| animateAnchor                     | 布尔值 | true        |                                                              |
| normalScrollElementTouchThreshold | 整数   | 5           |                                                              |



### 相关方法

| moveSectionUp()        | 向上滚动                                 |
| ---------------------- | ---------------------------------------- |
| moveSectionDown()      | 向下滚动                                 |
| moveTo(section, slide) | 滚动到                                   |
| moveSlideRight()       | slide 向右滚动                           |
| moveSlideLeft()        | slide 向左滚动                           |
| setAutoScrolling()     | 设置页面滚动方式，设置为 true 时自动滚动 |
| setAllowScrolling()    | 添加或删除鼠标滚轮/触控板控制            |
| setKeyboardScrolling() | 添加或删除键盘方向键控制                 |
| setScrollingSpeed()    | 定义以毫秒为单位的滚动速度               |

### 回调函数

| afterLoad      | 滚动到某一屏后的回调函数，接收 anchorLink 和 index 两个参数，anchorLink 是锚链接的名称，index 是序号，从1开始计算 |
| -------------- | ------------------------------------------------------------ |
| onLeave        | 滚动前的回调函数，接收 index、nextIndex 和 direction 3个参数：index 是离开的“页面”的序号，从1开始计算；nextIndex 是滚动到的“页面”的序号，从1开始计算；direction 判断往上滚动还是往下滚动，值是 up 或 down。 |
| afterRender    | 页面结构生成后的回调函数，或者说页面初始化完成后的回调函数   |
| afterSlideLoad | 滚动到某一水平滑块后的回调函数，与 afterLoad 类似，接收 anchorLink、index、slideIndex、direction 4个参数 |
| onSlideLeave   | 某一水平滑块滚动前的回调函数，与 onLeave 类似，接收 anchorLink、index、slideIndex、direction 4个参数 |

































