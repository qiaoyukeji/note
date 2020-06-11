## 1. 浮动

### 1.1传统网页布局的三种方式
网页布局的本质——用CSS来摆放盒子。把盒子摆放到相应位置.
CSS提供了三种传统布局方式（简单说，就是盒子如何进行排列顺序）:
- 普通流（标准流）
- 浮动 
- 定位

### 1.2 标准流（普通流/文档流）
 1. 块级元素会独占一行,从上向下M赡扫冽。
    - 常用元素：div、hr、p、hl~h6、ul、o1、dl、form、table

2. 行内元素会按照顺序,从左到右111赡排列，碰到父元素边缘则自动换行。
   - 常用元素：span、a、i、em等

以上都是标准流布局，我们前面学习的就是标准流，	。
这三种布局方式都是用来摆放盒子的，盒子摆放到合适位置，布局自然就完成了。

> 注意：实际开发中，一个页面基本都包含了这**三种布局方式**（后面移动端学习新的布局方式） 。

### 1.3 为什么需要浮动？

提问：我们用标准流能很方便的实现如下效果吗？
1. 如何让多个块级盒子(div)水平排列成一行？

![image-20200416224418952](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416224420.png)

比较难，虽然转换为行内块元素可以实现一行显示，但是他们之间会有大的空白缝隙，很难控制。

提问：我们用标准流能很方便的实现如下效果吗？

2. 如何实现两个盒子的左右对齐？

   ![image-20200416224605330](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416224607.png)

总结： 有很多的布局效果，标准流没有办法完成，此时就可以利用浮动完成布局。 因为浮动可以改变元素标
签默认的排列方式.
浮动最典型的应用：可以让多个块级元素一行内排列显示。
网页布局第一准则：==多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动。==

### 1.4 什么是浮动？
float 属性用于创建浮动框，将其移动到一边，直到左边缘或右边缘触及包含块或另一个浮动框的边缘。

    选择器 { float: 属性值; }

![image-20200416224850183](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416224851.png)

### 1.5 浮动特性（重难点）
加了浮动之后的元素,会具有很多特性,需要我们掌握的.
1. ==浮动元素会脱离标准流(脱标)==
2. 浮动的元素会一行内显示并且元素顶部对齐
3. 浮动的元素会具有行内块元素的特性.
  

设置了浮动（float）的元素最重要特性：
1. 脱离标准普通流的控制（浮） 移动到指定位置（动）, （俗称==脱标==）
2. 浮动的盒子==不再保留原先的位置==

![image-20200416230118904](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416230120.png)


> 如果多个盒子都设置了浮动，则它们会按照属性值==一行内显示并且顶端对齐排列。==

![image-20200416230314962](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416230316.png)

==注意： 浮动的元素是互相贴靠在一起的（不会有缝隙），如果父级宽度装不下这些浮动的盒子， 多出的盒子会另起一行对齐==

> 浮动元素会具有行内块元素特性。

任何元素都可以浮动。不管原先是什么模式的元素，添加浮动之后具有==行内块元素==相似的特性。
- 如果块级盒子没有设置宽度，默认宽度和父级一样宽，但是添加浮动后，它的大小根据内容来决定
- 浮动的盒子中间是没有缝隙的，是紧挨着一起的 
- 行内元素同理

### 1.6 浮动元素经常和标准流父级搭配使用
为了约束浮动元素位置, 我们网页布局一般采取的策略是: 
==先用标准流的父元素排列上下位置, 之后内部子元素采取浮动排列左右位置. 符合网页布局第一准侧.==

![image-20200416231112014](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416231113.png)

![image-20200416231253489](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416231255.png)

```html
 <style>
        .box {
            width: 1200px;
            height: 460px;
            background-color: pink;
            margin: 0 auto;
        }
        .left {
            width: 230px;
            height: 460px;
            background-color: purple;
            float: left;
        }
        .right {
            width: 970px;
            height: 460px;
            background-color: skyblue;
            float: right;
        }
    </style>

<body>
    <div class="box">
        <div class="left">左</div>
        <div class="right">右</div>
    </div>
</body>
```

![](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416231843.png)

![image-20200416231923981](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416231925.png)

```html
<style>
        * {
            margin: 0;
            padding: 0;
        }
        li {
            list-style: none;
        }
        .box {
            width: 1226px;
            height: 285px;
            background-color: pink;
            margin: 0 auto;
        }
        .box li {
            width: 296px;
            height: 285px;
            background-color: purple;
            float: left;
            margin-right: 14px;
        }
        .box .last {
            /* 注意权重问题 */
            margin-right: 0;
        }
    </style>

<body>
    <ul class="box">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li class="last">4</li>
    </ul>
</body>
```

![image-20200416233151628](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416233153.png)

![image-20200417123403450](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200418125959.png)


网页布局第二准侧.
> ==先设置盒子的大小, 之后设置盒子的位置==

```html
<style>
        .box {
            width: 1226px;
            height: 614px;
            background-color: pink;
            margin: 0 auto;
        }

        .left {
            width: 234px;
            height: 614px;
            background-color: purple;
            float: left;
        }

        .right {
            width: 992px;
            height: 614px;
            background-color: skyblue;
            float: left;
        }

        .right>div {
            width: 234px;
            height: 300px;
            background-color: pink;
            float: left;
            margin-left: 14px;
            margin-bottom: 14px;
        }
    </style>

<body>
    <div class="box">
        <div class="left">左</div>
        <div class="right">
            <div>1</div>
            <div>2</div>
            <div>3</div>
            <div>4</div>
            <div>5</div>
            <div>6</div>
            <div>7</div>
            <div>8</div>
        </div>
    </div>
</body>
```

![image-20200417124810438](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200417124811.png)

##  2. 常见网页布局

### **2.1 常见网页布局**

![image-20200417125206116](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200417125207.png)

![image-20200417125223185](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200417125224.png)

### 2.2 浮动布局注意点


1. 浮动和标准流的父盒子搭配。
    - ==先用标准流的父元素排列上下位置, 之后内部子元素采取浮动排列左右位置==
2. 一个元素浮动了，理论上其余的兄弟元素也要浮动。
    - 一个盒子里面有多个子盒子，如果其中一个盒子浮动了，那么其他兄弟也应该浮动，以防止引起问题。
    - ==浮动的盒子只会影响浮动盒子后面的标准流,不会影响前面的标准流.==

我们前面浮动元素有一个标准流的父元素, 他们有一个共同的特点,都是有高度的.
> 但是, 所有的父盒子都必须有高度吗?   

理想中的状态, 让子盒子撑开父亲. 有多少孩子,我父盒子就有多高.
>但是不给父盒子高度会有问题吗?

## 3. 清除浮动
### 3.1 为什么需要清除浮动？
由于父级盒子很多情况下，不方便给高度，但是子盒子浮动又不占有位置，最后父级盒子高度为 0 时，就会影响下面的标准流盒子。

![image-20200417131839207](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200417131840.png)

> 由于浮动元素不再占用原文档流的位置，所以它会对后面的元素排版产生影响

### 3.2 清除浮动本质
- 清除浮动的本质是清除浮动元素造成的影响
- 如果父盒子本身有高度，则不需要清除浮动
- ==清除浮动之后，父级就会根据浮动的子盒子自动检测高度。父级有了高度，就不会影响下面的标准流了==

### 3.3 清除浮动方法

    选择器{clear:属性值;}

![image-20200417132204302](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200417132205.png)

我们实际工作中， 几乎只用==clear: both;==
==清除浮动的策略是: 闭合浮动.==

> 具体方法
1. 额外标签法也称为隔墙法，是 W3C 推荐的做法。
2. **父级添加 overflow 属性**
3. **父级添加after伪元素**
4. **父级添加双伪元素**

> 1. 额外标签法  

额外标签法也称为隔墙法，是 W3C 推荐的做法。
额外标签法会在浮动元素末尾添加一个空的标签。例如 `<div style=”clear:both”></div>`，或者其他标签（如`<br />`等）。
- 优点： 通俗易懂，书写方便
- 缺点： 添加许多无意义的标签，结构化较差  

==注意： 要求这个新的空标签必须是块级元素。==

总结:
1. 清除浮动本质是? 
清除浮动的本质是清除浮动元素脱离标准流造成的影响
2. 清除浮动策略是?
闭合浮动. 只让浮动在父盒子内部影响,不影响父盒子外面的其他盒子.
3. 额外标签法?
隔墙法, 就是在最后一个浮动的子元素后面添加一个额外标签, 添加 清除浮动样式.
实际工作可能会遇到,但是不常用

> 2. 父级添加 overflow

可以给父级添加 overflow 属性，将其属性值设置为 hidden、 auto 或 scroll 。
子不教,父之过,注意是给父元素添加代码
- 优点：代码简洁
- 缺点：无法显示溢出的部分

> 3. :after 伪元素法

:after 方式是额外标签法的升级版。也是给父元素添加
```html
.clearfix:after { 
 content: ""; 
 display: block; 
 height: 0; 
 clear: both; 
 visibility: hidden; 
} 
.clearfix { /* IE6、7 专有 */ 
 *zoom: 1;
}
```
- 优点：没有增加标签，结构更简单
- 缺点：照顾低版本浏览
- 代表网站： 百度、淘宝网、网易等

> 4. 双伪元素清除浮动

也是给给父元素添加
```css
.clearfix:before,
.clearfix:after { 
    content:""; 
    display:table; 
}
.clearfix:after { 
    clear:both;
    }
.clearfix { 
    *zoom:1;
    }
```
- 优点：代码更简洁
- 缺点：照顾低版本浏览器
- 代表网站：小米、腾讯等

### 3.4 清除浮动总结
① 父级没高度。
② 子盒子浮动了。
③ 影响下面布局了，我们就应该清除浮动了。

![image-20200417134252458](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200417134253.png)