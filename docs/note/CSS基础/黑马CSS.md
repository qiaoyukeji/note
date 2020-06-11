页面布局要学习三大核心, 盒子模型, 浮动 和 定位。

学习好盒子模型能非常好的帮助我们布局页面

## 1.盒子模型

### 1.1 看透网页布局的本质

网页布局过程：

1. 先准备好相关的网页元素，网页元素基本都是盒子 Box 。

2. 利用 CSS 设置好盒子样式，然后摆放到相应位置。

3. 往盒子里面装内容

.

网页布局的核心本质： **就是利用 CSS 摆盒子**

### 1.2 盒子模型（Box Model）组成

所谓盒子模型：就是把HTML页面中的布局元素看作是一个矩形的盒子，也就是一个盛装内容的容器。

CSS 盒子模型本质上是一个盒子，封装周围的HTML 元素，它包括：边框、外边距、内边距、和实际内容

![image-20200416210314854](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416210324.png)

![image-20200416210416513](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416210417.png)

### 1.3 边框（border）

CSS 边框属性允许你指定一个元素边框的样式和颜色。

边框样式border-style 可以设置如下值：

- none：没有边框即忽略所有边框的宽度（默认值）

- solid：边框为单实线(最为常用的)

- dashed：边框为虚线

- dotted：边框为点线

![image-20200416222130353](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416222132.png)

![image-20200416222144284](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200416222145.png)