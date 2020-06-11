### VUE

[来自CSDN](https://blog.csdn.net/qq_44317018/article/details/104146747)

*   [什么是Vue](#Vue_1)
*   [如何使用Vue](#Vue_19)
*   [MVVM设计模式](#MVVM_132)
*   [绑定语法: 同模板字符串中的${}](#__183)
*   [指令(directive)](#directive_225)

*   [v-bind](#vbind_229)
*   [v-show](#vshow_276)
*   [v-if](#vif_342)
*   [高频笔试题(手写) 观察者模式](#__429)
*   [v-for](#vfor_477)
*   [splice](#splice_575)
*   [:key="i"](#keyi_586)
*   [绑定HTML片段内容](#HTML_598)
*   [v-html](#vhtml_599)
*   [防止用户短暂看到{{}}](#_625)
*   [v-cloak](#vcloak_628)
*   [v-text](#vtext_667)
*   [事件绑定](#_693)
*   [vue中如何获得事件对象 (vue中如何获得鼠标位置)](#vue_vue_747)
*   [$event](#event_791)
*   [v-once](#vonce_837)
*   [v-pre](#vpre_857)
*   [双向绑定](#_860)
*   [v-model](#vmodel_866)

*   [监控函数 watch](#_watch_992)
*   [绑定样式](#_1007)

*   [绑定内联样式](#_1008)
*   [绑定class](#class_1114)

*   [自定义指令](#_1365)
*   [计算属性](#_1420)
*   [过滤器](#_1494)
*   [axios](#axios_1638)
*   [组件](#_1713)
*   [组件化开发](#_1792)

*   [定义子组件](#_1808)
*   [组件间传递数据](#_1907)

*   [SPA: Single Page Application](#SPA_Single_Page_Application_1967)
*   [VUE脚手架](#VUE_2133)

*   [安装生成脚手架代码的工具 vue create](#_vue_create_2139)
*   [运行 npm run serve](#_npm_run_serve_2196)
*   [为脚手架添加axios模块](#axios_2208)
*   [脚手架项目结构](#_2221)
*   [脚手架和SPA应用代码的结构](#SPA_2278)
*   [es6模块化开发在脚手架中的应用](#es6_2284)
*   [用VUE脚手架项目开发](#VUE_2297)

*   [组件的生命周期](#_2371)
*   [总结](#_2404)

##### 什么是Vue

1.  什么是: 基于MVVM设计模式的渐进式的纯前端js框架  
    (1). MVVM?  
    (2). 渐进式: 不要求整个项目都用vue做，可以轻松和别的技术混搭，且会多少就可以先用多少！  
    (3). 纯前端js框架: 与nodejs无关！单靠浏览器就可运行！  
    (4). 框架:  
    a. 原生js: 不需要下载，浏览器就自带的ES+DOM+BOM  
    1). 优点: 万能！  
    2). 缺点: 繁琐！  
    b. jQuery函数库: 基于原生js，重新封装的一批函数的集合。简化了传统DOM每一步操作！  
    1). 优点: 简单！  
    2). 缺点: 没有简化开发的步骤！依然包含大量重复的编码！  
    c. 框架: 已经包含核心功能的半成品项目！  
    1). 优点: 根本上简化了开发流程，几乎避免了重复编码  
    2). 缺点: 需要转变观念，和做事方法！很难适应！
2.  为什么: 便于大项目的开发，避免重复代码，提高开发效率
3.  何时: 凡是以数据为主(增删改查)的项目，都可用vue开发！

##### 如何使用Vue

1.  下载:  
    (1). 下载vue.js文件，引入普通网页中使用:  
    `<script src="js/vue.js">` —— 初学者  
    版本: 2.6  
    开发版: 未压缩版: 包括完备的注释，代码格式和见名知义的变量名，同时带有非常人性化的错误提示。  
    生产版: 压缩版: 去掉了注释，代码格式，极简化了变量名，同时删除了错误提示！  
    (2). 使用脚手架代码: —— 公司中  
    版本: 3或4
2.  我的第一个vue功能: 示例：单击按钮改变数量:  
    jQuery版本：
```
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="js/jquery-1.11.3.js"></script>
    </head>
    <body>
    <button id="btnMinus">-</button><span >0</span><button id="btnAdd">+</button>
    <script>

    //DOM4步
    //1. 查找出发事件的元素
    //本例中: 先点击+按钮
    $("#btnAdd")
    //2. 绑定事件处理函数
    .click(function(){
      //3. 查找要修改的元素
      //本例中查找当前按钮兄弟中的span元素
      var $span=$(this).siblings("span")
      //4. 修改元素
      //获取span的内容，转为整数
      var n=parseInt($span.html());
      //n+1
      n++;
      //再放回去
      $span.html(n);
    })
    
    //1. 查找出发事件的元素
    //本例中: 先点击+按钮
    $("#btnMinus")
    //2. 绑定事件处理函数
    .click(function(){
      //3. 查找要修改的元素
      //本例中查找当前按钮兄弟中的span元素
      var $span=$(this).siblings("span")
      //4. 修改元素
      //获取span的内容，转为整数
      var n=parseInt($span.html());
      //只有n>0时，才能-1
      n>0&&(n--);
      //再放回去
      $span.html(n);
    })
    </script>
    </body>
```

Vue版本:
```
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <!--0. 先引入vue.js-->
    <script src="js/vue.js"></script>
    </head>
    <body>
    <!--1. 做界面: 
      1.1 要求:只能有一个唯一的父元素
      1.2 用{{变量}}语法在HTML中标记出可能变化的位置——类似于模板字符串中的${变量}
      本例中: 只有span的内容可能会变
      1.3 用@事件名="处理函数名",为元素绑定事件
    -->
    <div id="app">
      <button @click="minus">-</button>
      <span>{{n}}</span>
      <button @click="add">+</button>
    </div>
    <script>
    //2. 定义一个对象，其中保存页面上所需的所有变量
    //data中的变量名应该和html中的{{}}里的变量名保持一致
    //通常HTML中有几个{{变量}}，data中就要有几个属性支持页面上的变量
    //本例中: HTML中只需要一个变量n
    //一个功能的所有变量都要写在data对象内！
    var data={ n:0 }
    //3. 创建一个Vue类型的子对象，将数据对象data和页面元素区域div#app绑定起来！
    new Vue({
    //:左边都不能改名
      el:"#app",//找到HTML中id为app的元素区域
      data:data,//将保存数据的data对象包含进new Vue里边来！
          //{ n:0 } 就成了vue的成员
      //所有页面上需要的事件处理函数都要写在methods的成员中:
      methods:{
        //本例中: 页面上需要两个函数: add和minus
        //在事件处理函数中，只需要埋头专心处理数据即可！new Vue()会自动保持变量和页面内容同步！
        //且在methods的方法中，可用this.访问当前对象自己data中的变量
        add:function(){
        //this->当前new Vue()对象！
          this.n++; //this.data.n++
        },
        minus:function(){
          if(this.n>0){
            this.n--;
          }
        }
      }
    })
    </script>
    </body>
```

##### MVVM设计模式

1.  什么是: 对前端三大部分代码的重新划分
2.  旧划分:  
    (1). HTML 专门定义网页内容的语言  
    (2). CSS专门定义网页样式的的语言  
    (3). Js专门操作页面内容和样式，添加交互行为的语言
3.  问题: 因为HTML和CSS很弱！缺少编程语言必须的要素！  
    (1). 没有变量，如果想让内容虽程序自动改变，不可能！  
    (2). 缺少必要的程序结构: 没有分支和循环  
    导致: JS要承担一切操作页面的代码！导致JS代码繁琐，且重复代码极多！
4.  新划分:  
    (1). 界面/视图(View):  
        a. 包括传统的HTML+CSS  
        b. 增强了HTML的功能！  
            1). 比如: HTML中可以写变量！  
            2). HTML中可以写if else if else 也可以写for循环  
      			3). HTML中可以写事件绑定！  
    (2). 模型数据(Model): 页面上所有需要的变量，集中保存在一个对象中！  
    	问题: 模型数据中的变量值，不会自动跑到页面上指定位置的！  
    (3). 视图模型(ViewModel): 用一个对象将视图(View)和模型对象(Model)绑定起来！  
      		 绑定结果: 数据模型中的变量值，可以自动跑到视图中指定位置，无需任何js编码！且模型对象中数据改变，视图中对应位置的变量值跟着自动变化！
5.  MVVM的原理: Vue框架是如何实现MVVM设计模式的  
    (1). new Vue()加载data对象  
    a. 将data对象打散，data内部的属性直接隶属于new Vue()对象  
    b. 将data中每个原始属性隐姓埋名，隐藏  
    c. 为data中每个属性请保镖:  
    1). Data中每个属性都有一对儿get/set方法  
    2). 今后只要想修改data中的变量都会自动触发set()  
    3). 在每个属性的set方法中，都自动植入一个notify()函数调用，只要试图修改data中的属性值时，都会自动调用set(),只要自动调用set()势必会自动notify()发出通知  
    (2). 加载虚拟DOM树:  
    a. 通过el属性值的选择器找到要监控区域的父元素  
    b. 创建虚拟DOM树  
    c. 扫描这个要监控的区域:  
    1). 每发现一个{{变量}}的元素，就将该元素的信息，记录进虚拟DOM树，同时首次用data中同名变量的值，代替页面中{{n}}的位置。  
    2). 每发现一个@事件名="函数名"的元素，就自动变为:  
    On事件名=“new Vue().函数名”  
    (3). 加载methods对象: methods对象中的所有方法，都会被打散，直接隶属于new Vue()和data中被打散的属性平级  
    所以，在methods中的方法中，想操作data中的属性，都可以写为"this.属性名"即可！  
    (4). 当触发事件时，自动调用new Vue()中methods中指定的函数，执行其中this.属性名的修改。修改会自动触发属性的set()方法，自动触发set()内部的notify函数:  
    a. 遍历虚拟DOM树，只找出受影响的个别元素  
    b. 利用虚拟DOM树提前封装好的DOM操作，只修改页面中受影响的个别元素！——效率高！
6.  总结: MVVM的原理/Vue的绑定原理:  
    **访问器属性+观察者模式+虚拟DOM树**
7.  什么是虚拟DOM树:  
    (1). 什么是虚拟DOM树: 仅保存可能发生变化的少量元素的精简版DOM树  
    (2). 优点:  
    a. 小, 遍历快！  
    b. 只更新受影响的元素，效率高！  
    c. 封装了DOM操作，无需我们程序员重复编码！

##### 绑定语法: 同模板字符串中的${}

插值语法: Interpolation

1.  什么是绑定语法: 让HTML中的内容也可随程序中的变量改变而自动改变！——也就是给HTML中添加变量功能
2.  何时: 只要元素的内容中想随变量自动改变
3.  如何: `<元素>xxxx{{变量名}}xxxx</元素>`
4.  原理:  
    (1). 首次加载页面内容时，会用data中同名变量的初始值代替{{变量名}}位置  
    (2). 当data中同名变量在new Vue()中被更改时，自动更新{{变量名}}位置为新值
5.  总结: {{}}中可以放什么，不能放什么  
    (1). 可以放: 变量，表达式，函数调用，创建对象，访问数组元素，三目  
    (2). 不能放: 程序结构(分支和循环)，没有返回值的函数调用
6.  示例: 使用vue在页面上显示不同内容
```
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="js/vue.js"></script>
    </head>
    <body>
    <div id="app">
      <h1>用户名:{{uname}}</h1>
      <h2>性别:{{sex==1?"男":"女"}}</h2>
      <h3>下单时间:{{new Date(orderTime).toLocaleString()}}</h3>
      <h3>小计:¥{{(price*count).toFixed(2)}}</h3>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        uname:"dingding",
        sex:1,
        orderTime:1579507293225,
        price:12.5,
        count:5
        //将来这些值都来自于ajax请求
      }
    })
    </script>
    </body>
```

##### 指令(directive)

1.  什么是: 为HTML元素添加新功能的特殊属性
2.  何时: 只要HTML元素需要某些特殊的功能时，就要使用对应的指令来实现
3.  包括: 13种

###### v-bind

4.  如果元素的属性值希望动态改变:  
    (1). 问题: 不能用{{}}绑定  
    (2). 解决: 应该用v-bind指令：  
    a. 标准写法: <元素 v-bind:属性名=“js表达式”>  
    b. 强调: 一定不要加{{}}，属性名前加v-bind:，=后的"“就扮演了{{}}的角色！{{}}中能写什么，此时”"中就能写什么！  
    c. 简写: 其实v-bind可省略！但是:不能省略！`<元素:属性名="js表达式">`  
    (3). 示例: 根据不同的变量值，动态改变
```
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
    </head>
    <body>
    <div id="app">
    <!--希望img的src属性，随变量PM25的值变化
      如果pm25<100, src变为1.png
      否则如果pm25<200, src变为2.png
      否则如果pm25<300, src变为3.png
      否则src变为4.png-->
    <img :src="pm25<100?'img/1.png':
               pm25<200?'img/2.png':
               pm25<300?'img/3.png':
                        'img/4.png'" >
    <h1>{{pm25<100?'img/1.png':
          pm25<200?'img/2.png':
          pm25<300?'img/3.png':
                   'img/4.png'}}</h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        //本例中: 因为页面上只需要一个变量pm25，所以data中只有一个变量pm25
        pm25:125
      }
    })
    setInterval(function(){
      vm.pm25=Math.random()*400
    },1000)
    </script>
    </body>
```

6.  根据程序中的变量值控制一个元素显示隐藏: 2种办法:

###### v-show

a. 如何: `<元素 v-show="js条件">`  
b. 原理: new Vue()扫描到v-show时，自动执行js条件，如果条件为true，则该元素原样显示。否则如果js条件执行结果为false，则new Vue()自动为当前元素加display:none，隐藏  
c. 示例: 点按钮控制对话框显示和隐藏
```
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
        .alert{
          width:300px;
          height:100px;
          position:fixed;
          padding:10px;
          top:50%;
          left:50%;
          margin-left:-160px;
          margin-top:-60px;
          background-color:#faf
        }
        .alert>span{
          cursor:pointer;
          border:1px solid #fff;
          float:right;
          padding:5px;
        }
      </style>
      <script src="js/vue.js"></script>
    </head>
    <body>
    <div id="app">
      <!--希望单击按钮时，让对话框显示-->
      <button @click="showIt">click me</button>
      <div v-show="show" class="alert">
        <!--希望点x时，关闭对话框-->
        <span @click="close">x</span>
        您的浏览器版本太低，请升级!
      </div>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        //本例中: 因为页面上需要一个bool类型的变量show，控制对话框的显示隐藏
        show:false
      },
      methods:{
        //因为页面上单击按钮需要调用名为showIt的函数，所以
        //showIt:function(){
        showIt(){
          //本例中: 调用showIt为了让对话框显示！
          //所以: 
          this.show=true;
        },
        //因为页面上单击x按钮需要调用名为close的函数，所以
        close(){
          //本例中: 调用close为了关闭对话框
          this.show=false;
        }
      }
    })
    </script>
    </body>
```

###### v-if

a. 也能控制一个元素显示隐藏，上例中v-show可直接换成v-if。  
b. 但是原理不同：v-if在扫描时，如果条件为true，则保留该元素。否则如果条件为false，则删除该元素！  
鄙视: v-show vs v-if  
v-show 采用display:none方式隐藏元素，不改变DOM树，效率高！  
v-if 采用添加删除元素方式控制元素显示隐藏，可能频繁修改DOM树，效率低！  
5\. 控制两个元素二选一显示隐藏:  
(1). <元素1 v-if=“条件”>  
<元素2 v-else>  
(2). 强调:  
a. v-else后不要写条件！(同js程序中的else)  
b. v-if 和 v-else之间必须连着写，不能插入任何其他元素  
(3). 原理: 如果扫描到v-if时，自动执行条件。如果条件为true，则保留v-if元素，删除v-else元素。否则如果条件为false，则删除v-if元素，保留v-else元素  
(4). 示例: 切换登录和注销状态

```
    <div id="app">
    <!--希望如果已经登录，显示第一个div
        如果点注销，希望状态改为未登录-->
    <div v-if="isLogin" id="div1">
      Welcome dingding | <a href="javascript:;" @click="logout">注销</a>
    </div>
    <!--否则如果未登录时，显示第二个div
        如果点登录，则状态改为已登录-->
    <div v-else id="div2">
      <a href="javascript:;" @click="login">登录</a> | <a href="javascript:;">注册</a>
    </div>
    
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        //因为界面上需要一个变量isLogin来表示是否登录
        isLogin:false
      },
      methods:{
        //因为页面上单击登录，需要调用login函数
        login(){
          //点击登录，修改状态为已登录
          this.isLogin=true;
        },
        //因为页面上单击注销，需要调用logout函数
        logout(){
          //点击注销，修改状态为未登录
          this.isLogin=false;
        }
      }
    })
    </script>
```

6.  多个元素多选一显示:  
    (1). <元素1 v-if=“条件1”>  
    <元素2 v-else-if=“条件2”>  
    … …  
    <元素n v-else>  
    (2). 强调:  
    a. v-else后不要写条件！(同js程序中的else)  
    b. v-if和v-else-if 和 v-else之间必须连着写，不能插入任何其他元素  
    (3). 原理: 在new Vue扫描到这里时:  
    a. new Vue()会自动依次计算每个条件。  
    b. 哪个条件为true，就就保留哪个元素，删除其他元素  
    c. 如果所有条件都不满足，只保留v-else元素，删除之前其余元素  
    (4). 示例: 多个表情，多选一显示
```
    <div id="app">
    <!--随变量PM25的值变化，在四个img中选其一显示，删除其他img。
      如果pm25<100, 显示1.png
      否则如果pm25<200, 显示2.png
      否则如果pm25<300, 显示3.png
      否则显示4.png-->
    <img v-if="pm25<100" src="img/1.png">
    <img v-else-if="pm25<200" src="img/2.png">
    <img v-else-if="pm25<300" src="img/3.png">
    <img v-else src="img/4.png">
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        //本例中: 因为页面上只需要一个变量pm25，所以data中只有一个变量pm25
        pm25:125
      }
    })
    setInterval(function(){
      vm.pm25=Math.random()*400
    },1000)
    </script>
```

###### 高频笔试题(手写) 观察者模式

    //观察者（observer）模式: 变量值修改，所有关注的人都能自动得到通知，并收到新值
    //保存数据的对象
    var data={
      n:0, //外人想随时获得的变量，保存着外人关心的一个数据n
      observers:[],//用一个数组保存将来关心这个变量n的所有外人，这些觊觎这个变量n的外人，也称为观察者
      //定义一个函数，专门修改变量n的值
      setN(n) {
        this.n = n
        //任何时候修改了变量n的值，都可以通知所有关注n的外人
        this.notifyAllObservers()
      },
      //定义一个函数，专门将关注变量n的外人(观察者)对象，集中保存在data中的observers数组中，便于集中通知。
      addObs(observer) {
        this.observers.push(observer)
      },
      //定义一个函数，专门用于通知当前data中的observers数组中保存的关心变量n的外人们，n发生改变了
      notifyAllObservers() {
        //遍历observers数组中每个外人对象
        this.observers.forEach(observer => {
          //每遍历一个外人对象，就通知外人，它关心的变量n发生改变了，请及时获取变量n的新值
          observer.getNewN()
        })
      }
    }
    
    //向data的observers数组中添加三个关心变量n的外人(观察者)对象
    for(var i=0;i<3;i++){
      data.addObs({
        //每个外人对象都包括两个属性和一个函数
        name:`obs${i}`, //外人的名字
        look: data, //每个外人都关心data对象中的变量，都紧紧盯着data对象
        //每个外人都准备一个函数，当data中变量改变时，可用于重新获得data对象中n的新值。
        getNewN:function(){
          console.log(`${this.name} known that n is updated to ${this.look.n}`)
        }
      })
    }
    
    // 测试代码
    console.log("data将n改为1时:")
    data.setN(1)
    console.log("data将n改为2时:")
    data.setN(2)
    console.log("data将n改为3时:")
    data.setN(3)


###### v-for

1.  反复生成多个相同结构的HTML元素: v-for  
    (1). `<要反复生成的元素 v-for="(value, i) of 数组">`  
    强调: v-for一定要放在那个要反复生成的元素上，而不是放在父元素上！  
    (2). 原理:  
    a. 当new Vue()扫描到这里时，自动遍历of后的数组中每个元素  
    b. 每遍历一个元素，就创建一个当前HTML 元素的副本  
    c. of前的两个变量:  
    1). `value`会自动获得当前正在遍历的数组元素值  
    2). `i` 会自动获得当前正在遍历的下标位置  
    d. 如果当前元素或子元素中，需要使用当前正在遍历的元素值或下标，可用绑定语法来绑定value和i的值。  
    强调: value和i的使用范围仅限于当前元素及其子元素范围内，不能在当前元素外使用！  
    (3). 示例: 遍历数组元素，反复生成多个相同结构的元素

    <div id="app">
      <ul>
        <!--本例中: 因为要反复生成多个li，所以v-for要写在li上，而不是li的父元素ul上-->
        <li v-for="(value,i) of teachers" :key ="i">
          第{{i+1}}阶段: {{value}}
        </li>
      </ul>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        teachers:["亮亮","然然","东东","涛涛"]
      }
    })
    </script>
    

(4)v-for还可:  
a. 可遍历数字下标的一切: 比如字符串  
b. 可遍历对象中每个属性  
示例: 遍历对象中每个属性，反复生成多个html元素

    <div id="app">
      <!--希望遍历data中一个对象的每个属性，反复生成多个相同结构的HTML元素-->
      <ul>
        <li v-for="(value,key) of ym" :key ="key">{{key}} : {{value}}</li>
      </ul>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        ym:{
          math:89,
          chs:69,
          eng:91
        }
      }
    })
    </script>


c. v-for还会数数: 给v-for一个数字，他可以生成从1开始依次递增的一个序列！  
1).`<要反复生成的元素 v-for="i of 数字">`  
2). 原理: v-for会像人一样，自动从1开始数数，每数一个数，就自动创建当前元素的一个副本。直到数到给定数字结束。  
3). 其中: i会接住每次数的一个数字，可用于当前元素及子元素的绑定中。  
示例: 根据页数，生成指定个数的分页按钮

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
      ul{ list-style:none }
      ul>li{
        float:left; 
        border:1px solid #555;
        width:36px;
        height:36px;
        line-height:36px;
        text-align:center;
      }
      ul>li+li{
        border-left:0
      }
      </style>
      <script src="js/vue.js"></script>
    </head>
    <body>
    <div id="app">
      <ul>
        <li v-for="i of pageCount">{{i}}</li>
      </ul>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        pageCount:3
      }
    })
    </script>
    </body>


###### splice

(5) **坑**: 如果v-for遍历的是数组时，在程序中通过下标修改数组元素值，页面上的HTML元素不会自动更改！  
比如: `this.teachers[0]="燕儿"` 页面上是不会变的！  
因为数组中的数字类型的下标012…无法添加访问器属性，也就不受监控！  
**解决**: 今后，vue中修改数组中的元素值！必须用数组家函数！才能自动更新页面。因为函数都是受监控的。  
比如: `this.teachers.splice(0,1,"燕儿")`  
删除0位置的1个元素，再在0位置放入"燕儿"  
结果: 页面会自动变化！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206101758917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
(6). 其实每次使用v-for时，都要同时绑定:key=“i”

###### :key=“i”

BS: 为什么v-for必须加:key  
答: 因为v-for反复生成的多个元素，除了内容不同之外，从元素属性上来看多个元素毫无差别！每个反复生成的元素都是一样的。所以，如果将来修改了数组中一个元素时，v-for因为无法识别每个HTML元素，所以只能把所有的HTML元素重新生成一遍——效率低！  
如果给每个元素都绑定`:key="i"`属性，则每个HTML元素上都有一个唯一的标识key=“0” key=“1” … 。当将来修改了数组中每个位置的元素时，只需要修改对应key的HTML元素即可，其他HTML元素保持不变！——效率高！  
**总结**: 避免修改数组元素时，重新生成所有HTML元素，而是只更新其中一个HTML元素即可！提高修改效率！  
**如何**:  
1). 当遍历数组时: `<元素 v-for="(val,i) of 数组" :key="i"`  
Key的值依次是0 1 2 3…  
2). 当遍历对象时: `<元素 v-for="(val,key) of 对象" :key="key"`  
Key的值依次是: 属性名1 属性名2 …  
因为一个对象内的属性名肯定不会重复，所以，属性名也可以当做:key唯一标识一个HTML元素

###### 绑定HTML片段内容

###### v-html

(1). 问题: {{}}不能绑定HTML片段内容。  
因为: {{}}本质相当于DOM中的textContent，会将HTML内容原样显示，不会被编译！  
(2). 解决: 今后只要要绑定的变量内容是一段HTML片段时，都用v-html来绑定！  
(3). 如何:`<元素 v-html="包含HTML内容的变量或表达式">`  
(4). 强调:  
a. v-html会将绑定内容中的HTML内容，编译后再显示给人看  
b. v-html也是指令，所以v-html后的""中可以写js表达式，比如字符串拼接！  
c. 用了v-html，就不要再元素开始标签和结束标签直接写内容！因为会被v-html内容替换！  
(5). 示例: 绑定HTML内容

    <div id="app">
      <h1>消息来源:{{html}}</h1>
      <h1 v-html="'消息来源:'+html">
        Welcome
      </h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        html:`<p>来自<a href="javascript:;">&lt;&lt;新华社&gt;&gt;</a>的消息</p>`
      }
    })
    </script>


###### 防止用户短暂看到{{}}

问题: 因为vue代码是放在js文件中，所以，如果网速慢，vue代码暂时没有下载下来时，用户很可能短暂看到页面上的绑定语法，用户体验不好！  
解决: 2个办法:

###### v-cloak

(1). 用v-cloak暂时隐藏带有{{}}内容的元素:  
a. 2步:  
1). 在包含绑定语法{{}}的元素上添加`v-cloak`属性  
2). 在css中手动添加样式: `[v-cloak]{ display:none }`  
b. 原理：  
1). 用属性选择器查找所有带有v-cloak属性的元素，暂时隐藏  
2). 当new Vue()渲染完成时，自动找到所有v-cloak属性，自动移除。  
c. 示例: 使用v-cloak防止用户短暂看到{{}}

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
      [v-cloak]{
        display:none
      }
      </style>
      <script src="js/vue.js"></script>
    </head>
    <body>
    <div id="app">
      <h1 v-cloak>Welcome: {{uname}}</h1>
    </div>
    <script>
    setTimeout(function(){
      var vm=new Vue({
        el:"#app",
        data:{
          uname:"dingding"
        }
      })
    },2000)
    </script>
    </body>


d. 问题: 既要在HTML中写指令，又要手动添加css选择器，步骤繁琐的！

###### v-text

(2). 用v-text代替内容中{{}}语法，来绑定非HTML片段内容:  
a. <元素 v-text=“原{{}}内容”></元素>  
b. 原理:  
1). 因为绑定语法写在了元素的属性里，所以，如果不是vue帮忙，用户无论如何是看不到元素属性中的内容的！  
2). New Vue()读取到v-text时，会解析v-text的内容，替换元素开始标签和结束标签之间的内容  
c. 强调:  
1). 和v-html不同，v-text等效于{{}}等效于DOM中的textContent，所以如果v-text中包含HTML片段，是不会被编译，而是原样显示给人看！  
2). v-text也是指令，所以v-text后的""中也可以写js表达式，比如字符串拼接！  
3). 用了v-text，也不要在元素开始标签和结束标签直接写内容！因为会被v-text内容替换！  
d. 示例: 使用v-text防止用户短暂看到{{}}

    <div id="app">
      <h1 v-text="'Welcome:'+uname"></h1>
    </div>
    <script>
    setTimeout(function(){
      var vm=new Vue({
        el:"#app",
        data:{
          uname:"dingding"
        }
      })
    },2000)
    </script>


###### 事件绑定

(1). 标准写法:  
a. div#app中: <元素 v-on:事件名=“处理函数()”  
b. new Vue()内:  
methods:{  
处理函数(形参变量){  
//可用"this.属性名"方式访问data中的模型变量  
}  
}  
(2). 简写:  
a. v-on: 可用@简写  
<元素 @事件名=“处理函数()”  
b. 如果处理函数不需要传参，()可省略  
<元素 @事件名=“处理函数”  
(3). 示例: 点击按钮，数量增长

    <div id="app">
      <button @click="change(-1)">-</button>
      <span>{{n}}</span>
      <button @click="change(+1)">+</button>
    </div>
    <script>
    var data={ n:0 }
    var vm=new Vue({
      el:"#app",
      data:data,
      methods:{
        //本例中，因为页面上只需要一个change函数，所以methods中只添加一个change函数
        //但是页面上调用change()函数时，传入了一个参数值,所以定义change函数时需要定义一个形参来接住实参值
        change(i){
          //如果i==+1,说明本次想+1
          if(i==+1){
            this.n++;
          }else{//否则如果i!=+1，说明本次想-1
            //只有n>0时，才能-1
            if(this.n>0){
              this.n--;
            }
          }
        }
      }
    });
    </script>


(4). 事件对象:  
a. 回顾: DOM中事件对象总是作为事件处理函数的第一个参数值默认传入:  
元素.on事件名=function(e){  
e->event  
e.stopPropagation()  
e.preventDefault()  
e.target  
e.offsetX e.offsetY  
e.clientX e.clientY  
}

###### vue中如何获得事件对象 (vue中如何获得鼠标位置)

1). 如果事件处理函数不需要传入实参值时，则:  
事件对象也是作为处理函数第一个参数值自动传入，也是在函数定义时，用一个形参e，就可接住——同DOM  
示例: 使用e获得鼠标位置:

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
      div{
        width:300px; height:100px;
        margin:20px;
      }
      #d1{
        background-color:#aaf
      }
      #d2{
        background-color:#ffa
      }
      </style>
      <script src="js/vue.js"></script>
    </head>
    <body>
    <div id="app">
    <div id="d1" @click="doit">d1</div>
    <div id="d2">d2</div>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        
      },
      methods:{
        doit(e){//同DOM的e
          console.log(`点在d1的: x:${e.offsetX},y:${e.offsetY}`);
        }
      }
    })
    </script>
    </body>


###### $event

BS: 如果既想传入自定义实参值，又想获得事件对象:  
i. 借助 $ event关键字: vue框架内部内置的专门指向事件对象的关键词。用 $ event等效于用事件对象e  
ii. 调用函数时，可将 $ event和其他实参值一起传入函数中  
iii. 定义函数时，可用普通的形参变量接住 $ event的值。  
iv. 示例: 使用 $event获得鼠标位置并传入自定义实参值

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
      div{
        width:300px; height:100px;
        margin:20px;
      }
      #d1{
        background-color:#aaf
      }
      #d2{
        background-color:#ffa
      }
      </style>
      <script src="js/vue.js"></script>
    </head>
    <body>
    <div id="app">
    <div id="d1" @click="doit('d1',$event)">d1</div>
    <div id="d2" @click="doit('d2',$event)">d2</div>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        
      },
      methods:{
        doit(name,e){//同DOM的e
          console.log(`点在${name}的: x:${e.offsetX},y:${e.offsetY}`);
        }
      }
    })
    </script>
    </body>


###### v-once

仅在首次渲染页面时绑定一次，即使之后模型变量再改变，也不会自动更新页面: `<元素 v-once>`  
示例: 显示时间

    <h1>当前系统时间: {{time}}</h1>
    <!--希望上线时间只在首次打开网页时绑定一次，之后，即使time变量值发生变化，也不会自动更新上线时间-->
    <h1 v-once>上线时间: {{time}}</h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        time:new Date().toLocaleString()
      }
    })
    setInterval(function(){
      vm.time=new Date().toLocaleString()
    },1000)
    </script>


###### v-pre

防止元素内容中的{{}}被vue编译，让内容中的{{}}原样显示！  
<元素 v-pre> xxx{{xx}}xxx </元素>

###### 双向绑定

1.  单向绑定: 只能将data中的变量值，自动同步更新到HTML页面中。但是，页面上的修改，无法自动更新回data的变量中。(前面的11种都是)  
    (data —> div#app 但是 div#app -x-> data)
2.  双向绑定: 既能将data中的变量值，自动同步更新到HTML页面中。又能将页面上的修改自动更新回data的变量中。  
    (data <===> div#app)
3.  何时使用双向绑定: 只有绑定表单元素时，才有必要用双向绑定！因为只有表单元素，用户才能在页面上修改的它的内容。

###### v-model

4.  如何: 每种表单元素绑定的原理不同:  
    1). 文本框/文本域: **绑定的是value属性**  
    a. `<input v-model:value="变量"/>` / `<textarea v-model:value="变量"></textarea>`  
    b. 原理: new Vue()扫描到这里时，自动为当前元素绑定事件，比如，如果`<input type="text" v-model:value="变量">`，就会翻译为: οninput=“vm.变量=当前文本框的新value”。  
    c. 示例: 点按钮，按回车，在文本框中输入内容，都可获得文本框中输入的关键词，执行搜索操作。

    <div id="app">
      <!--在文本框上按回车可以查找-->
      <input type="text" v-model:value="keywords" @keyup="myKeyUp">
      <!--点击按钮可以查找-->
      <button @click="search">百度一下</button>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        keywords:"macbook i5"
      },
      methods:{
        search(){
          console.log(`查找 ${this.keywords} 相关的内容...`)
        },
           // $event
           //   ↓
        myKeyUp(e){
          //只有按回车才查找
          if(e.keyCode==13){
            //调用旁边的search()函数
            this.search();
          }
        }
      },
      //想变量keywords只要被更改，就重新执行一次搜索
      watch:{
        keywords(){
          console.log("自动调用一次watch中的keywords函数...")
          this.search();
        }
      }//进入new Vue()中的一切data:{}, methods:{}, watch:{}都会被打散，最终都直接隶属于new VUe()对象，都是平级的，所以可以this.方式，互访。
    })
    </script>
    

(2). 单选按钮: **绑定的是checked属性**  
a. `<input type="radio" name="sex" value="1" v-model:checked="变量">`男  
`<input type="radio" name="sex" value="0" v-model:checked="变量">`女  
b. 原理:  
(1). 从data->input: 用checked绑定的变量的值和当前radio的value做比较。如果checked绑定的值和value值相等，则当前radio选中。否则不选中。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200203105700372.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
(2). 切换选中一个radio后，用当前选中的radio的value值代替checked属性绑定的data中的变量值。导致，页面中其它关注这个变量的位置都自动发生改变。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020020310572173.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
示例: 选择性别

    <div id="app">
    <label><input type="radio" name="sex" value="1" v-model:checked="sex">男</label>
    <label><input type="radio" name="sex" value="0" v-model:checked="sex">女</label>
    <h1>sex:{{sex}}</h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        sex:1
      }
    })
    </script>


(3). 双向绑定select元素: 因为改变select的选中项，改变的是中整个select的value值，所以应该绑定select元素的value  
a.

    <select v-model:value="变量">
    		<option value="值1">文本1</option>
    		<option value="值2">文本2</option>
    		... ...


b. 原理:  
1). 从data->select:用value绑定变量值，和每个option的value做比较，哪个option的value等于变量值，就选中哪个option![在这里插入图片描述](https://img-blog.csdnimg.cn/20200203111243520.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
2). 切换select中的选中项: 用新选中的option的value值替换select的value绑定的data中的变量值。导致所有关系这个变量的其它位置自动变化。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200203111301921.png)  
c. 示例: 选择订单状态:

    <div id="app">
    <select v-model:value="orderStatus">
      <option value="0">未付款</option>
      <option value="10">已付款</option>
      <option value="20">已发货</option>
      <option value="30">已签收</option>
    </select>
    <h1>orderStatus:{{orderStatus}}</h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        //0:未付款  10:已付款  20:已发货 30:已签收
        orderStatus:10
      }
    })
    </script>


(4). 双向绑定一个checkbox的情况: 因为选中或取消选中checkbox改变的它的checked属性，所有v-model应该绑定checked属性。且绑定的变量应该是bool类型  
a. `<input type="checkbox" v-model:checked="变量">`  
b. 原理:  
1). 从data->input checkbox: 根据变量是true还是false，设置当前checkbox是否选中  
2). 当切换checkbox的选中状态后，就用新的checked属性值(true或false)，更新到绑定的data中的变量中  
c. 示例: 同意，启用表单元素，不同意，则禁用表单元素  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200203111621961.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200203111639452.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)

    <div id="app">
      <input type="text" placeholder="请输入用户名" :disabled="!isAgree"><br/>
      <input type="password" placeholder="请输入密码" :disabled="!isAgree"><br/>
      <label><input type="checkbox" v-model:checked="isAgree">同意</label></br>
      <button :disabled="!isAgree">注册</button>
      <h1>isAgree:{{isAgree}}</h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        isAgree:false //表示不同意
      }
    })
    </script>


(5). 简写: 其实以上所有v-model后的":属性名"都可省略！v-model可自动根据所在的元素不同，选择对应的的元素自动绑定。

##### 监控函数 watch

(1). 双向绑定过程中只要希望变量值一发生变化，就自动执行一项操作，可用watch，添加监控函数。  
(2). new Vue({  
el:"#app",  
data:{ 变量: 值, … },  
methods:{  
函数(){ … }  
},  
watch:{ //监视  
要监视的变量(){ //只要data中的变量被修改，watch中与变量同名的监视函数，就会被自动执行！  
… …  
}  
}  
})  
(3). 强调: watch中的函数名必须和要监视的变量同名！

##### 绑定样式

###### 绑定内联样式

(1). 不好的做法: 将元素的整个style属性当做一个字符串来绑定  
<元素 style=“固定不变的css属性” :style=“变量”>  
data:{  
变量:“可能变化的css属性” //比如: “top:50px; left:100px”  
}  
缺点: 不便于修改其中某一个css属性。  
(2). 好的做法: 将元素的style属性当做一个对象来绑定:  
优点: 便于修改单个css属性  
a. 只创建一个变量，但是变量值以对象方式保存多个css属性  
<元素 style=“固定不变的css属性” :style=“变量”>  
data:{  
变量:{  
Css属性: 值,  
… : …  
}  
//自动翻译为: 一个字符串: “css属性:值; css属性:值; …”  
}  
:style动态绑定的变量中的css属性，经过编译为字符串后，自动和不带:的固定不变的style中的css属性最终合并为一个style属性。  
示例: 用键盘上下左右方向键控制一个小方块的移动:

    <div id="app">
      <div id="pop" style="position:fixed; width:100px; height:100px; background-color:pink" :style="popStyle"></div>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        popStyle:{
          top:"0px",
          left:"0px"
        }
        //自动翻译为: popStyle:"top:0px; left:0px"
      }
    })
    window.onkeydown=function(e){
      //左: 37  上: 38  右: 39  下: 40
      if(e.keyCode==39){//右
        var left=parseInt(vm.popStyle.left);
        left+=20;
        vm.popStyle.left=left+"px";
      }else if(e.keyCode==40){//下
        var top=parseInt(vm.popStyle.top);
        top+=20;
        vm.popStyle.top=top+"px";
      }
    }
    
    </script>


b. 为每个动态变化的css属性都创建一个变量（创建多个变量）,绑定时，"“中使用匿名对象:style=”{css属性: 变量1, css属性:变量2 }"  
<元素 style=“固定不变的css属性” :style="{css属性1: 变量1, css属性2: 变量2 , …}">  
data:{  
变量1: 值1,  
变量2: 值2  
}  
结果: :style="{css属性1: 变量1, css属性2: 变量2 , …}"，会被自动翻译为:  
style=“css属性1:变量1的值; css属性2: 变量2的值”，再和其他写死的不带:的style合并  
示例: 用键盘上下左右方向键控制一个小方块的移动:

    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
    </head>
    <body>
    <div id="app">
      <div id="pop" style="position:fixed; width:100px; height:100px; background-color:pink" :style="{top, left}"></div>
      <!--自动翻译为: top:0px; left:0px;-->
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        top:"0px",
        left:"0px"
      }
    });
    window.onkeydown=function(e){
      //左: 37  上: 38  右: 39  下: 40
      if(e.keyCode==39){//右
        var left=parseInt(vm.left);
        left+=20;
        vm.left=left+"px";
      }else if(e.keyCode==40){//下
        var top=parseInt(vm.top);
        top+=20;
        vm.top=top+"px";
      }else if(e.keyCode==38){//上
        var top=parseInt(vm.top);
        top-=20;
        vm.top=top+"px";
      }else if(e.keyCode==37){//左
        var left=parseInt(vm.left);
        left-=20;
        vm.left=left+"px";
      }
    }
    </script>
    </body>
    </html>


###### 绑定class

(1). style绑定内联样式的问题: 多数样式的修改，都是同时修改多个css属性，如果用style绑定，每个css属性都要写出来，代码繁琐！  
(2). 解决: 将来只要批量修改一个元素的多个css属性，应该用class方式，代替style方式  
(3). 如何:  
a. 不好的做法: class属性也可以作为一整条字符串绑定，但是问题依然是不便于只修改其中一个class。  
b. 好的做法，将class作为一个对象绑定：  
1). 只声明一个变量，但是变量值是一个对象，其中包含多个class名  
i. <元素 class=“固定不变的class” :class=“变量”  
ii. data:{  
变量: { class1 : true或false, class2: true或false }  
}  
iii. 结果: 编译时，仅将变量对象中值为true的class，编译进最终的class中，值为false的class，不包含在最终的正式class字符串中。且动态绑定的:class会和不带:绑定的固定不变的class，合并为一个class！  
iv. 示例: 验证手机号格式:

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <style>
        /* 定义提示框的基础样式 */
        .msg{
          display:inline-block;
          width:160px;
          height:25px;
          border:1px solid #555;
          text-align:center;
          line-height:25px;
        }
        /* 定义提示框在验证通过时的样式 */
        .success{
          border:1px solid green;
          background-color:lightgreen;
          color:green
        }
        /* 定义提示框在验证失败时的样式 */
        .fail{
          border:1px solid red;
          background-color:pink;
          color:red
        }
      </style>
    </head>
    <body>
    <div id="app">
      <!-- 因为要获得用户输入的手机号进行验证，所有必须用双向绑定 -->
      <input type="text" v-model="phone">
      <!-- 因为提示框的样式可能在success和fail之间来回切换，所以动态绑定span的部分class 
          又因为提示框的内容也可能随验证结果而动态变化，所以也要绑定一个变量msg-->
      <span class="msg" :class="msgClass">{{msg}}</span>
      <!--界面中共需要三个变量-->
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        //因为页面中需要三个变量，所以data中就要有三个变量
        phone:"", //实时接用户在文本框中输入的手机号
        msg:"", //根据验证结果的对错，绑定提示信息的内容
        //根据验证结果的对错，动态在success和fail两个class之间来回切换。
        msgClass:{
          success:false,
          fail:false
        }
      },
      watch:{
        //因为用户一边输入，vue就一边验证，所以必须用watch随时监控用于的输入变化。
        phone(){
          //定义正则验证phone的内容
          var reg=/^1[3-9]\d{9}$/;
          //如果用正则验证phone的内容通过
          if(reg.test(this.phone)==true){
            //就修改msgClass应用成功的样式，不应用失败的样式
            this.msgClass={
              success:true,
              fail:false
            }
            //修改span的提示信息内容
            this.msg="手机号格式正确！"
          }else{//否则如果验证失败
            //就修改msgClass应用失败的样式，不应用成功的样式
            this.msgClass={
              success:false,
              fail:true
            }
            //修改span的提示信息内容
            this.msg="手机号格式正确！"
          }
        }
      }
    })
    </script>
    </body>


2). 为每个class都声明一个变量，在绑定时，可用{}对象语法绑定:  
i. <元素 class=“固定不变的class” :class="{class1: 变量1, class2: 变量2, …}"  
ii. data:{  
变量1: true或false,  
变量2: true或false  
}  
iii. 结果: 编译时，仅将:class="{}"中值为true的class，编译进最终的class中，值为false的class，不包含在最终的正式class字符串中。且动态绑定的:class会和不带:绑定的固定不变的class，合并为一个class！  
iv. 示例: 验证手机号格式:

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <style>
        /* 定义提示框的基础样式 */
        .msg{
          display:inline-block;
          width:160px;
          height:25px;
          border:1px solid #555;
          text-align:center;
          line-height:25px;
        }
        /* 定义提示框在验证通过时的样式 */
        .success{
          border:1px solid green;
          background-color:lightgreen;
          color:green
        }
        /* 定义提示框在验证失败时的样式 */
        .fail{
          border:1px solid red;
          background-color:pink;
          color:red
        }
      </style>
    </head>
    <body>
    <div id="app">
      <!-- 因为要获得用户输入的手机号进行验证，所有必须用双向绑定 -->
      <input type="text" v-model="phone">
      <!-- 因为提示框的样式可能在success和fail之间来回切换，所以动态绑定span的部分class 
          又因为提示框的内容也可能随验证结果而动态变化，所以也要绑定一个变量msg-->
      <!--                       class名  变量-->
      <!-- <span class="msg" :class="{success:success, fail:fail}">{{msg}}</span> -->
      <!--结果: 哪个class名后的变量值为true，才会进入最终的class字符串中。变量值为false的class，不会出现在最终的class字符串中-->
      <span class="msg" :class="{success, fail}">{{msg}}</span>
      <!--界面中共需要四个变量-->
      <!--但是，两个class和错误提示三个变量的值，都和验证结果这一个数据有关！所有，其实只用一个变量就可控制三个值的变化-->
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        //因为页面中需要三个变量，所以data中就要有三个变量
        phone:"", //实时接用户在文本框中输入的手机号
        msg:"", //根据验证结果的对错，绑定提示信息的内容
        //根据验证结果的对错，动态在success和fail两个class之间来回切换。
        success:false,
        fail:false
      },
      watch:{
        //因为用户一边输入，vue就一边验证，所以必须用watch随时监控用于的输入变化。
        phone(){
          //定义正则验证phone的内容
          var reg=/^1[3-9]\d{9}$/;
          //如果用正则验证phone的内容通过
          if(reg.test(this.phone)==true){
            //就修改msgClass应用成功的样式，不应用失败的样式
            this.success=true;
            this.fail=false
            //修改span的提示信息内容
            this.msg="手机号格式正确！"
          }else{//否则如果验证失败
            //就修改msgClass应用失败的样式，不应用成功的样式
            this.success=false;
            this.fail=true
            //修改span的提示信息内容
            this.msg="手机号格式正确！"
          }
        }
      }
    })
    </script>
    </body>


iv. 示例: 优化: 尽量减少vue中data中的变量，便于维护。

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <style>
        /* 定义提示框的基础样式 */
        .msg{
          display:inline-block;
          width:160px;
          height:25px;
          border:1px solid #555;
          text-align:center;
          line-height:25px;
        }
        /* 定义提示框在验证通过时的样式 */
        .success{
          border:1px solid green;
          background-color:lightgreen;
          color:green
        }
        /* 定义提示框在验证失败时的样式 */
        .fail{
          border:1px solid red;
          background-color:pink;
          color:red
        }
      </style>
    </head>
    <body>
    <div id="app">
      <!-- 因为要获得用户输入的手机号进行验证，所有必须用双向绑定 -->
      <input type="text" v-model="phone">
      <!-- 因为提示框的样式可能在success和fail之间来回切换，所以动态绑定span的部分class 
          又因为提示框的内容也可能随验证结果而动态变化，所以也要绑定一个变量msg-->
      <!--                       class名  变量-->
      <!-- <span class="msg" :class="{success:success, fail:fail}">{{msg}}</span> -->
      <!--结果: 哪个class名后的变量值为true，才会进入最终的class字符串中。变量值为false的class，不会出现在最终的class字符串中-->
      <!-- <span class="msg" :class="{success:isRight, fail:isRight==false}">{{isRight==true?"手机号可用":"手机号格式错误！"}}</span> -->
      <span class="msg" :class="isRight==true?'success':'fail'">{{isRight==true?"手机号可用":"手机号格式错误！"}}</span>
      <!--界面中共需要四个变量-->
      <!--但是，两个class和错误提示三个变量的值，都和验证结果这一个数据有关！所有，其实只用一个变量就可控制三个值的变化-->
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        //因为页面中需要三个变量，所以data中就要有三个变量
        phone:"", //实时接用户在文本框中输入的手机号
        isRight:false
      },
      watch:{
        //因为用户一边输入，vue就一边验证，所以必须用watch随时监控用于的输入变化。
        phone(){
          //定义正则验证phone的内容
          var reg=/^1[3-9]\d{9}$/;
          //将验证结果保存到变量isRight中，依次牵连着三个位置发生变化！
          this.isRight=reg.test(this.phone);
        }
      }
    })
    </script>
    </body>


##### 自定义指令

1.  向Vue大家庭中添加自定义指令:  
    Vue.directive(“指令名”, { //向Vue大家庭中添加一个新的指令，并制定指令名  
    //回调函数: 当渲染后的元素被插入到DOM树上之后，自动执行该回调函数  
    inserted(当前指令所在的DOM元素对象){  
    //对当前指令所在的DOM元素对象，执行DOM操作  
    //在这里对当前DOM元素执行的DOM操作，会自动应用到页面上  
    }  
    })  
    强调: 添加自定义指令时，指令名一定不要带v-前缀！比如，想添加一个让元素自动获得焦点的自定义指令，可命名为"focus"
    
2.  使用自定义指令: 只要在想应用对应效果的元素上，添加"v-指令名"属性即可。  
    强调: 虽然定义指令时，指令名没有加v-前缀，但是使用指令时，必须加v-前缀
    
3.  原理:  
    (1). Vue.directive(“指令名”,{  
    inserted(domElem){  
    对domElem执行原生DOM操作  
    }  
    })  
    向Vue大家庭中添加一个新的自定义指令，关联一个处理函数  
    (2). new Vue()时，会扫描`<div id="app">`下的所有内容。  
    (3). 每扫描到一个v-开头的指令属性，就会回Vue大家庭中找是否有对应的指令。如果有对应的指令，就调用指令关联的处理函数，对指令所在的元素执行原生DOM操作。
    
4.  示例: 让文本框自动获得焦点:
  

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <script>
        Vue.directive("focus",{
          inserted(domElem){
            //让当前元素自动获得焦点
            domElem.focus();
            //      DOM原生
          }
        })
      </script>
    </head>
    <body>
    <div id="app">
      <input type="text" v-focus><button>百度一下</button>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
    
      }
    })
    </script>
    </body>
    

强调: new Vue()起到最重要的扫描HTML内容的作用，只有new Vue()才认识v-开头的指令，所有，即使data中没有值，只要用到了Vue相关的功能，new Vue()都不能省略！

##### 计算属性

1.  什么是: 程序中没有保存该属性的属性值，每次绑定属性时，都需要根据其他属性的值动态计算获得该属性的属性值。
2.  为什么: 有些值，总是可以根据其他属性值的变化，动态计算获得。这样的值，就没必要在程序中再保存一份。因为就算保存了，这个属性所依赖的其他属性值一旦发生变化，这个属性的属性值连带也要改变。
3.  何时: 今后，只要一个属性的值可以根据其他属性计算出来，都没必要保存！
4.  如何:  
    (1). 定义计算属性:  
```vue
    new Vue({  
    el:"#app",  
    data:{  
    页面所需的变量  
    },  
    methods:{  
    自定义函数或事件处理函数  
    },  
    watch:{  
    监视某个变量的监视函数  
    },  
    computed:{  
    属性名(){  
    return 根据其他属性值计算后获得的计算结果  
    }  
    }  
    }) 
```
(2). 使用计算属性:             计算属性，虽然本质是一个函数，但是在HTML中绑定语法中使用时，不要加()!
5.  结果：  
    (1). 只要计算属性所依赖的另一个属性值发生改变，同样会通知计算属性重新计算新的属性值。  
    (2). 计算属性计算出的结果，会被Vue缓存起来，反复使用，避免重复计算。即使反复使用多次，也只在首次计算一次。
6.  鄙视: methods vs computed  
    (1). 用法:  
    a. methods必须加()  
    b. computed 不用加()  
    (2). 反复使用:  
    a. methods中的方法，每调用一次，就会重新执行一次，执行结果，不会被vue缓存起来。  
    b. computed中的计算属性，只在第一次使用时计算一次，然后，结算结果，就会被Vue缓存起来，即使在别的地方反复使用这个计算属性，也不会重复计算，而是直接从缓存中获取值。但是，当所依赖的其他属性值发生变化时，计算才被迫重新计算一次。
7.  如何选择methods和computed:  
    (1). 如果这次使用时，更关心函数的执行结果数据时，首选计算属性  
    (2). 如果这次使用时，更关心函数执行操作的过程，结果数据无所谓，甚至函数没有返回值，则首选methods中的方法。
8.  示例: 使用计算属性绑定购物车总价:
```
    <div id="app">
      <h3>总计: ¥{{total.toFixed(2)}}</h3>
      <ul>
        <li v-for="(item,i) of cart" :key="i">
          {{item.pid}} | {{item.pname}} | ¥{{item.price.toFixed(2)}} | {{item.count}} —— 小计：¥{{(item.price*item.count).toFixed(2)}}
        </li>
      </ul>
      <h3>总计: ¥{{total.toFixed(2)}}</h3>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        cart:[
          {pid:1, pname:"华为",price:4455, count:2},
          {pid:2, pname:"小米",price:3455, count:1},
          {pid:3, pname:"OPPO",price:3356, count:3},
        ]
      },
      methods:{ //叫方法，所以用法同方法的用法——必须加()
        
      },
      computed:{ //叫属性，所以用法同属性的用法——不加()
        total(){
          console.log("调用了一次total()");
          var sum=0;
          for(var p of this.cart){
            sum+=p.price*p.count;
          }
          return sum;
        }
      }
    })
    </script>
```

##### 过滤器

1.  什么是: 专门对变量的原始值进行加工后，再显示的特殊函数
  
2.  为什么: 个别变量的原始值不能直接给人看！  
    比如: 性别 0和1 日期的毫秒数
    
3.  何时: 如果一个变量的值不能直接给人看时，必须经过加工，才能给人看时
  
4.  如何:  
    (1). 向Vue大家庭中添加过滤器函数  
    Vue.filter(“过滤器名字”, function(oldVal){ //接受一个变量的原始值  
    return 根据oldVal的不同，动态返回的新值  
    })  
    (2). 在绑定语法中使用过滤器函数：  
    {{变量 | 过滤器名 }}
    
5.  结果:  
    (1). 变量的原始值不会立刻显示出来，而是先交给|后的过滤器函数  
    (2). 再将过滤器处理后的返回值，返回出来，显示在元素内容中
    
6.  原理:  
    (1). Vue.filter(“过滤器名”, function(oldVal){ return 新值 })  
    定义一个过滤器函数，加入到Vue大家庭中备用  
    (2). 当new Vue()扫描到{{}}中的|时，会回Vue大家庭中查找相应名称的过滤器函数。  
    (3). 只要找到，就先将|前的变量原始值，交给过滤器函数的oldVal参数，经过过滤器函数的加工，返回新值。显示到当前绑定语法的位置。
    
7.  示例: 过滤性别的1和0为男和女
  

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <script>
        //sexFilter=function(){ ... }
        Vue.filter("sexFilter",function(oldVal){
          //性别接住的旧值可能是1或0
          return oldVal==1?"男":"女"
        })
      </script>
    </head>
    <body>
    <div id="app">
      <h1>性别: {{sex | sexFilter}}</h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        sex:1
      }
    })
    </script>
    </body>
    
8.  过滤器可以加参数:  
    (1). 定义过滤器时:  
    Vue.filter(“过滤器名”,function(oldVal, 自定义形参, …){  
    Return 新值  
    })  
    (2). 使用过滤器时:  
    {{变量 | 过滤器名(自定义实参, …) }}  
    (3). 示例: 根据参数值返回不同语言的性别
```
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <script>
        //sexFilter=function(){ ... }
        Vue.filter("sexFilter",function(oldVal,language){
          //性别接住的旧值可能是1或0
          //language参数可能接住cn或en,其中，默认是cn
          if(language=="en"){
            return oldVal==1?"Male":"Female"
          }else{
            return oldVal==1?"男":"女"
          }
        })
      </script>
    </head>
    <body>
    <div id="app">
      <h1>性别: {{sex | sexFilter}}</h1>
      <h1>性别: {{sex | sexFilter("en")}}</h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        sex:1
      }
    })
    </script>
```

9.  过滤器可以连用:  
    (1). 绑定语法中: {{变量 | 过滤器1 |过滤器2 | … }}  
    (2). 强调:  
    a. 后一个过滤器2，进入的旧值，已经不是变量的原始值了，而是前一个过滤器加工后的中间值。  
    b. 只有最后一个过滤器的返回值，才会显示到页面上。如果希望前几个过滤器的返回值也能一起显示到页面上，只能在最后一个过滤器中将新值拼接到上一步过滤器传入的旧值上。  
    (3). 示例：为性别再额外添加图标
```
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <script>
        //定义一个新的过滤器专门为性别添加图标
        Vue.filter("sexIcon",function(oldVal){
          //oldVal可能有六种：1  0  男  女   Male   Female
          if(oldVal==1||oldVal==0){
            return oldVal==1?"♂":"♀";
          }else{
            return oldVal=="男"||oldVal=="Male"?oldVal+"♂":oldVal+"♀";
          }
        });
        //sexFilter=function(){ ... }
        Vue.filter("sexFilter",function(oldVal,language){
          //性别接住的旧值可能是1或0
          //language参数可能接住cn或en,其中，默认是cn
          if(language=="en"){
            return oldVal==1?"Male":"Female"
          }else{
            return oldVal==1?"男":"女"
          }
        })
      </script>
    </head>
    <body>
    <div id="app">
      <h1>性别: {{sex | sexFilter | sexIcon }}</h1>
      <h1>性别: {{sex | sexFilter("en") | sexIcon }}</h1>
      <h1>性别: {{sex | sexIcon }}</h1>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        sex:1
      }
    })
    </script>
    </body>
    
```
##### axios

1.  什么是axios: 基于Promise的专门发送ajax请求的函数库
2.  为什么: 总结发送ajax请求:  
    (1). xhr4步/6步  
    (2). 自己封装函数，考虑不全面  
    (3). jQuery中 $ .ajax: 问题，在vue中几乎不再使用DOM操作，几乎不用jQuery了。如果单是为了引入$.ajax函数而引入整个jQuery库，有点儿小题大做。  
    (4). Vue官方提供了一套发送ajax请求的组件: vue-resource，后来，Vue发现哪个框架都有自己的发送ajax请求就得函数，而且都大同小异，所以，Vue认为自己没有必要再重新开放按一套ajax函数库，所以vue-resource已经不再维护。  
    (5). Vue官方帮我们选了一个时髦好用的ajax函数库: axios，所以将来在框架中发送ajax请求，几乎都用axios。
3.  何时: 只要在Vue框架中，发送ajax请求服务器端数据，都用axios
4.  如何:  
(1). 准备: 在项目中引入axios.js，才能引入axios函数库  
`<script src="js/axios.js">` 引入的顺序和vue.js无关  
(2). 设置所有服务器端接口的公共域名部分  
axios.defaults.baseURL=“服务器端域名地址部分”  
(3). 发送get请求:  
axios.get(“url”,{ //向服务器端接口地址url发送get请求  
params:{ //携带参数  
参数1: 值1,  
… : …  
}  
//自动翻译为"?参数1=值1&参数2=值2&…"  
//}).then(function(result){  
}).then(res\=>{  
res.data才是服务器端返回的结果  
})  
(4). 发送post请求:  
axios.post(“url”, “变量1=值1&变量2=值2&…”)  
.then(res=>{  
res.data时服务器端返回的结果  
})  
(5). 示例: 使用axios向新浪云上的接口地址发送get和post请求，传参，并接受响应结果
```
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/axios.min.js">
        //axios={ 
        //  get(){ ... },
        //  post(){ ... }
        //}
      </script>
      <script src="js/qs.min.js">
        //专门就将对象语法转为查询字符串语法
        //{ uname:"dingding", upwd:"123456"}
        // ↓ Qs.stringify(对象) 
        //"uname=dingding&upwd=123456"
      </script>
    </head>
    <body>
      <script>
      //先定义所有接口统一的服务器端域名部分
      axios.defaults.baseURL="http://xzserver.applinzi.com"
      //向服务器端请求学子商城首页商品数组，包含6个商品对象的信息
      axios.get("/index")
          .then(res=>{
            console.log(res.data);
          })
      //想获取5号商品的详细信息: 要求: 携带一个lid参数，值为要查询的商品编号
      axios.get("/details",{
        params:{lid:5}
      }).then(res=>{
        console.log(res.data) //返回5号商品的详细信息
      })
      //用用户名dingding，密码123456，调用登录接口
      axios.post("/users/signin",
        //"uname=dingding&upwd=123456"
        Qs.stringify({ uname:"dingding", upwd:"123456"})
      ).then(res=>{
        console.log(res.data);
      })
      </script>
    </body>
```

##### 组件

1.  什么是: 页面中拥有专属的HTML、CSS、js和数据的可重用的独立功能区域
  
2.  为什么: 1. 重用！2. 便于大项目的分工协作！3. 松耦合！
  
3.  何时: 只要页面中出现一个功能，可能被反复使用，或需要多人分工协作时，都用组件。
  
4.  如何创建一个组件:  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206103955549.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
    强调: 因为HTML标签名不区分大小写，所组件名如果包含多个单词，绝对不能用驼峰命名！必须用-分割多个单词。  
    比如: myCounter，错的。因为myCounter可能被转换为全大写或全消息的标签名，使用时会有歧义。  
    my-counter，对的。不会被转换。
    
5.  如何使用组件: Vue中的组件本质就是一个可重用的自定义HTML标签而已  
    在页面中<组件名></组件名>
    
6.  原理:  
    (1). Vue.component(“my-counter”,{})其实是向当前页面的Vue大家庭中添加一个Vue组件对象。  
    (2). new Vue()在页面中扫描到一个自定义标签时，就会回vue的大家庭中查找是否有同名的组件  
    (3). 如果找到这个组件，就先复制组件的模板中的HTML片段，代替页面中自定义标签所在位置。  
    (4). 为本次组件的使用，临时调用一次data()函数，返回一个本次组件使用专属的数据对象。  
    (5). 创建组件对象，监控当前组件的小区域。  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206104247372.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
    new Vue() vs 组件  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206104324712.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)
    
7.  示例: 定义修改数量的组件，并重用  
    (1). 1\_my-counter.js
 ```   

    Vue.component("my-counter",{
      //大多数属性同new Vue()
      //1. 定义可反复使用的组件的HTML片段模板
      template:`<div>
        <button @click="change(-1)">-</button>
        <span>{{count}}</span>
        <button @click="change(+1)">+</button>
      </div>`,
      //2. 定义data()函数，可返回一个新的数据对象
      data(){
        return {//相当于以前new Vue()中的data{}
          //因为组件模板中需要一个变量count
          count:0
        }
      },
      //3. 之后的内容和new Vue()中就完全一样了
      methods:{
        change(i){
          this.count+=i;
          this.count<0&&(this.count=0)
        }
      }
    })
 ```

(2). 1\_component.html
```
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <script src="1_my-counter.js">
        //Vue.component("my-counter",{ ... })
      </script>
    </head>
    <body>
    <div id="app">
      <my-counter></my-counter>
      <my-counter></my-counter>
      <my-counter></my-counter>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        
      }
    })
    </script>
    </body>
    
```
8.  其实，当组件的template模板被替换到页面上之后，new Vue()是不放心的。万一这次新加载的组件内容中又包含内嵌的不认识的标签和指令属性怎么办？  
    所以，new Vue()会重新扫描本次替换上来的模板HTML片段的内容。如果又包含不认识的指令，就再次去Vue家庭中查找指令。如果又遇到不认识的标签就再次去Vue大家庭中查找组件

##### 组件化开发

1.  什么是: 今后一个网页都是由组件拼接而成
  
2.  为什么: 1. 重用！2. 便于大项目的分工协作！3. 松耦合！
  
3.  何时: 今后几乎所有的项目都是组件化开发完成的
  
4.  如何:  
    (1). 拿到一个网页后，先划分网页中的组件共有多个少，以及包含关系是什么  
    (2). 创建多个组件js文件，每个组件js文件中都创建一个组件对象  
    (3). 父组件中可用子组件标签，在父组件内部插入子组件  
    (4). 所有组件的js文件，应该都引入new Vue()所在的网页中
    
5.  原理:  
    (1). 网页中new Vue()扫描到`<div id="app">`下不认识的标签，就回Vue大家庭中查找是否包含该组件定义  
    (2). 如果找到该组件定义，则用组件的template，替换页面中组件标签所在的位置  
    (3). new Vue()绝不是只扫描一次，而是每替换一次组件的模板片段，就重新扫描新加入的模板片段中，是否又包含更子级的不认识的标签。  
    (4). 只要扫描到不认识的标签，就会继续回Vue大家庭中，查找是否包含该组件定义。然后用组件的模板片段，代替刚才组件中不认识的标签出现的位置。依次类推，直到所有标签new Vue()都认识，也就是所有标签都变成浏览器原生HTML的标签后，new Vue()才停止扫描。  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206104549703.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)
    

###### 定义子组件

(1). 什么是子组件: 规定只能在一个指定的父组件内使用的组件  
(2). 为什么: 因为有些组件，必须只能用在指定的父组件内，才有意义。如果离开指定父组件，毫无意义，甚至会出错。  
(3). 何时: 今后，只要一个组件规定只能在某个父组件内使用时，都用子组件  
(4). 根组件、全局组件、子组件：  
a. 根组件： new Vue() ——监控整个页面，负责扫描和绑定页面中所有内容。一个页面中只有一个根组件  
b. 全局组件: Vue.component() —— 可用在任何位置！没有限制！  
c. 子组件: 仅限于在某个指定父元素内才能使用的组件对象。一旦出了这个规定的父组件，使用子组件就会报错。  
(5). 如何使用子组件:  
a. 创建子组件对象: 2个特点:  
1). 不要用Vue.component()创建，而只要创建一个普通的js对象即可！  
2). 虽然是普通的js对象，但是对象中的内容要和Vue.component()中的内容格式相同。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020020610483059.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
7\. 示例: 使用组件拼接todo案例的HTML界面（暂时不含功能和数据）  
(1). 2\_todo.js
```
    Vue.component("todo",{
      template:`<div>
        <h1>待办事项列表</h1>
        <todo-add></todo-add>
        <todo-list></todo-list>
      </div>`,
      components:{//规定todoAdd和todoList两组件只能在当前父组件todo内使用
        todoAdd, todoList
    //vue会自动将驼峰命名的组件对象名，翻译为-分割
    //     ↓         ↓
    //<todo-add> <todo-list>
      }//表示今后todoAdd和todoList只能在todo内使用
    })
```

(2). 2\_todo-add.js
```
    //定义子组件不要用Vue.component()，只能创建普通对象，且对象名必须用驼峰命名
    var todoAdd={
      template:`<div>
        <input type="text"/>
        <button>+</button>
      </div>`
    } 
```

(3). 2\_todo-list.js
```
    var todoList={ 
      template:`<ul>
        <todo-item></todo-item>
        <todo-item></todo-item>
        <todo-item></todo-item>
      </ul>`,
      components:{ //规定todoItem组件只能在当前父组件todoList内使用
        todoItem 
      }
    }
```

(4). 2\_todo-item.js
```
    //对象的变量名，必须使用驼峰命名
    //且，对象的变量名，将来会被自动翻译为子组件的标签名。
    var todoItem={//{}内保持组件的内容格式不变。
      template:`<li>
        1 - 吃饭 <a href="javascript:;">x</a>
      </li>`
    }
```

(5). 2\_todo.html
```
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <!--子组件一定要在父组件之前引入！-->
      <script src="2_todo-add.js">
        //Vue.component("todo-add",{ ... })
      </script>
      <script src="2_todo-item.js">
        //Vue.component("todo-item",{ ... })
      </script>
      <script src="2_todo-list.js">
        //Vue.component("todo-list",{ ... })
      </script>
      <script src="2_todo.js">
        //Vue.component("todo",{ ... })
      </script>
    </head>
    <body>
    <div id="app">
      <todo></todo>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        
      }
    })
    </script>
    </body>
    
```
###### 组件间传递数据

(1). 父给子:  
a. 问题: Vue中父组件data中的数据成员，子组件不能直接使用！因为Vue中每个组件的data数据都是自己专属的！所以必须父组件主动传给子组件才能用:  
b. 第一步: 父组件中: 在子组件的开始标签上用:将自己data中的变量绑定给子组件的一个自定义属相上  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206112618374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
c. 第二步: 子组件用props属性，从父组件绑定的自定义属性中取出父组件给的值。子组件用props属性取出的父组件给的值，使用方法和子组件自己的data中的变量用法完全一样：即可用于绑定语法，又可在js程序中用this.访问。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206112715613.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206112731904.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
d. 升级: 为todo案例添加数据绑定(暂时不实现删除和添加操作)  
1). 2\_todo.js
```
    Vue.component("todo",{
      template:`<div>
        <h1>待办事项列表</h1>
        <todo-add></todo-add>
        <!--爹todo，通过:绑定语法，将自己data中的变量tasks，赋值给子组件todo-list的自定义属性tasks中-->
        <todo-list :tasks="tasks"></todo-list>
      </div>`,
      data(){
        return {
          tasks:["吃饭","睡觉","打亮亮","学习"]
        }
      },
      components:{
        todoAdd, todoList
    //vue会自动将驼峰命名的组件对象名，翻译为-分割
    //     ↓         ↓
    //<todo-add> <todo-list>
      }//表示今后todoAdd和todoList只能在todo内使用
    })
```

2). 2\_todo-list.js
```
    var todoList={
      template:`<ul>
        <!--比如: 名为tasks兜里的爹的tasks数组照样可用于当前子组件中v-for遍历-->
         <!--如果当前todoList的子组件todoItem中继续需要todoList中的数据，也可通过:绑定语法，由当前组件放入子组件上的自定义属性中。可以放进多个自定义属性中，像多个口袋一样-->
        <!--比如：todo-item子组件主要当前组件遍历出的任务名task和任务序号i，所以在todo-item上添加两个自定义属性，绑定task和i变量的值-->
        <todo-item v-for="(task,i) of tasks" :task="task" :i="i" :key="i"></todo-item>
      </ul>`,
      //孩子todoList组件，从爹给的名为tasks的兜里掏出爹给的tasks数组，就像使用自己的tasks数组一样使用。
      props:["tasks"],
      components:{ 
        todoItem 
      }
    }
```

3). 2\_todo-item.js
```
    //对象的变量名，必须使用驼峰命名
    //且，对象的变量名，将来会被自动翻译为子组件的标签名。
    var todoItem={//{}内保持组件的内容格式不变。
      template:`<li>
        <!--从爹给的口袋里获得的数据，可在孩子里用于绑定语法中，就像用自己data中的数据一样方便-->
        {{i+1}} - {{task}} <a href="javascript:;">x</a>
      </li>`,
      //孩子todoItem组件，可从爹给的两个口袋task和i中取出爹给的两个值:任务名和任务序号。
      props:[ "task", "i" ]
    }
```

##### SPA: Single Page Application

1.  什么是: 整个应用程序只有一个完整的HTML页面，其它所谓的页面，其实都是组件而已。所谓的切换页面或跳转页面，其实都是在一个页面内，切换不同的组件而已。
2.  何时: 几乎移动端的项目都用单页面应用
3.  为什么:  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206113436376.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)
4.  如何:  
    (1). 只创建一个唯一完整的HTML页面，包含new Vue()  
    (2). 创建其他"页面"对应的组件文件  
    强调: 在SPA应用当中，所谓的"页面"，其实都是包含页面片段内容的子组件  
    (3). 创建路由对象，包含路由字典:  
    a. 路由器对象: 随时监控地址栏变化，并能根据路由字典中规定，查找对应组件，替换唯一完整的HTML页面中指定区域 的对象。  
    b. 路由字典: 包含所有相对路径及其对应的组件对象名的数组  
    c. 路由器中必须包含路由字典才能正常工作  
    d. 如何:  
    1). 引入`<script src="js/vue-router.js">`  
    2). 创建路由器对象和路由字典
```
    var router=new VueRouter({
      			routes:[
        				{path:"/", component: Index},
        				{path:"/details", component: Details},
        				{path:"/products", component: Products},
        				{path:"*", component: NotFound }
      			]
    		})
    
```
(4). 将之前所有组件对象，路由字典对象都引入唯一完整的HTML页面中  
a. 引入顺序: vue-router.js， 子组件，父组件，路由器对象  
b. 在`<div id="app">`中添加`<router-view></router-view>`为将要到来的页面组件片段占位。  
c. 在new Vue()中引入router对象  
(5). 如果包含全局组件，比如页头:  
a. 先创建页头组件js: my-header.js  
Vue.component(“my-header”,{ … })  
b. 再将全局组件引入唯一完成的HTML页面中`<script src="my-header.js">`  
c. 最后，在`<div id="app">`中，`<router-view>`外部，添加全局组件标签

    <div id="app">
    		<my-header></my-header>
    		<router-view></router-view>
    	</div>


d. 结果: 将来切换页面组件时，仅替换router-view部分。Router-view外部的部分保持不变，页头就出现在每个页面的顶部，成了多个页面共有的部分了。  
5\. 路由跳转:  
(1).HTML中写死的:  
a. 不要用`<a href="xxx">`  
b. 必须用`<router-link to="/相对路径">文本</router-link>`  
(2). Js中跳转: `this.$router.push("/相对路径")`  
6\. 路由传参:  
(1). 在路由字典中配置路由对象，允许传参
```
    var router=new VueRouter({
    	routes:[
    		...
    		{path:"/details/:lid", component: Details, props:true}
    	]                参数名               将参数lid的值直接变成props中的属性
    	结果: 从此，想进入/details，必须带参数值！不带参数值不让进！
    })
    
```
(2)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200206114414926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
7\. 示例: 实现单页面应用  
(1). 3\_SPA.html
```
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <script src="js/vue.js"></script>
      <script src="js/vue-router.js"></script>
      <script src="3_index.js"></script>
      <script src="3_details.js"></script>
      <script src="3_products.js"></script>
      <script src="3_not_found.js"></script>
      <script src="3_router.js">
        //var router=new VueRouter({ ... })
      </script>
      <script src="3_my_header.js"></script>
    </head>
    <body>
    <div id="app">
      <my-header></my-header>
      <router-view></router-view>
    </div>
    <script>
    var vm=new Vue({
      el:"#app",
      data:{
        
      },
      //router:router
      router
    })
    </script>
    </body>
    </html>
```

(2). 3\_index.js
```
    var Index={
      template:`<div style="background-color:#C8BFE7">
        <h1>这里是首页</h1>
        <button @click="goToDetails">查看1号商品的详情</button><br/>
        <router-link to="/details/2">查看2号商品的详情</router-link>
      </div>`,
      methods:{
        goToDetails(){
          this.$router.push("/details/1")
        }
      }
    }
    
```
(3). 3\_details.js
```
    var Details={
      template:`<div style="background-color:#FF7F27">
        <h1>这里是详情页</h1>
        <h2>显示{{lid}}号商品的详细信息...</h2>
        <button @click="back">返回首页</button>
      </div>`,
      props:[ "lid" ],
      methods:{
        back(){
          this.$router.push("/")
        }
      }
    }
    
```
(4) 3\_products.js
```
    var Products={
      template:`<div style="background-color:#B5E61D">
        <h1>这里是商品列表页</h1>
      </div>`
    }
    
```
(5). 3\_not\_found.js
```
    var NotFound={
      template:`<h1 style="color:red">您访问的页面不存在！<br>404:Not Found</h1>`
    }
```

(6). 3\_router.js
```
    var router=new VueRouter({
      routes:[
        {path:"/", component: Index},
        {path:"/details/:lid", component: Details,props:true},
        {path:"/products", component: Products},
        {path:"*", component: NotFound }
      ]
    })
    
```
(7) 3\_my\_header.js
```
    Vue.component("my-header",{
      template:`<div>
        <h1>这里是页头</h1>
        <ul>
          <li><router-link to="/">首页</router-link></li>
          <li><router-link to="/products">商品列表页面</router-link></li>
        </ul>
      </div>`
    })
    
```
##### VUE脚手架

1.  什么是: 已经包含核心功能的半成品项目
2.  为什么:  
    (1). 简单: 已经包含了核心功能，避免了大量重复编码  
    (2). 规范: 文件夹结构和文件夹名，文件名都已标准化，降低了不同项目之间的差异。
3.  何时: 今后几乎所有前端项目的开发都是用脚手架完成的。

###### 安装生成脚手架代码的工具 vue create

4.  如何:  
    (1). 安装生成脚手架代码的工具: `npm i -g @vue/cli`  
    安装之后: 输入`vue -V` , 看到版本号就算成功  
    (2). 用生成脚手架代码的工具为本次项目创建一套脚手架代码结构:  
    a. 在想要生成项目的目录，地址栏里写cmd，打开命令行  
    b. 在命令行中输入`vue create xzvue`  
    c. `Your connection to the default npm registry seems to be slow.`  
    你现在的链接是链接到默认的国外的npm仓库，看起来有些慢  
    `Use https://registry.npm.taobao.org for faster installation?` (Y/n)  
    是否使用国内的淘宝镜像来更快速安装 **输入Y按回车**  
    d. `? Please pick a preset:` 请选择一个预置的设置  
    `default (babel, eslint)` //使用默认设置  
    `>` `Manually select features` //手动选择功能  
    按方向键下，选第二个，手动选择功能，按**回车**  
    e. `? Check the features needed for your project: (Press <space> to select, <a> to toggle all`  
    选择你的项目需要的功能（按空格选中或取消选中，按a全选所有）  
    , `<i>to invert selection)`  
    (`*`) Babel 将浏览器不认识的ES6甚至更高版本的js代码，翻译为ES5版本的js  
    ( ) TypeScript  
    ( ) Progressive Web App (PWA) Support  
    (`*`) Router VUE中实现单页面应用的核心——路由器组件  
    (`*`) Vuex 管理共享状态  
    ( ) CSS Pre-processors  
    `>` ( ) Linter / Formatter Linter 是代码质量检查工具，会将格式不规范也报错！一定不要选择  
    ( ) Unit Testing  
    ( ) E2E Testing  
    按方向键上下移动，移动到想要选中的功能上，按空格键**选中Babel、Router、Vuex，取消选中Linter**  
    f. `Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n)` **输入n 按回车**  
    是否使用history模式作为路由器的标识（生产环境中需要配置首页重定向才能使用）  
    Vue-router默认采用#/相对路径 方式实现客户端路由地址:  
    比如: http://localhost:5500/index.html#/  
    http://localhost:5500/index.html#/details/2  
    history模式:  
    http://localhost:5500/  
    http://localhost:5500/details/2  
    默认浏览器会将所有地址栏中的地址发给服务器端请求资源，只要#地址留在客户端，不发给服务器。  
    但是，http://localhost:5500/details/2 我们本来想在客户端路由切换页面组件，但是浏览器也会发送给服务器端查找，因为服务器端没有这个资源，所以，很可能报错！  
    所以，将来，要么就用默认#/相对路径方式，要么可用histroy,必须同时请服务器端修改配置！  
    g. `Where do you prefer placing config for Babel, ESLint, etc.? (Use arrow keys)`  
    你想把本次的配置保存在哪个位置？（用方向键选择）  
    `In dedicated config files` //把每种组件的配置，放在各自单独的配置文件中  
    `> In package.json` //将所有配置集中放在一个package.json文件中  
    按方向键下，**选in package.json，按回车**  
    h. `Save this as a preset for future projects? (y/N)`  
    是否保存这次的配置为将来项目的预定义配置  
    **输入N，按回车**  
    i. 看到结果: 说明用脚手架工具生成项目源代码结构成功  
    …  
    Successfully created project xzvue.  
    👉 Get started with the following commands:  
    `$` cd xzvue  
    `$` npm run serve
    
    j. 在windows资源管理器中，进入当前文件夹，就看到为这次项目生成的半成品项目源代码文件夹xzvue。  
    k. 每做一个新项目，这套a-h的步骤都要重新操作一遍。  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200217155458727.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)
    

###### 运行 npm run serve

l. 其实刚创建完的脚手架项目源代码包含示例网页:  
用vscode打开刚创建的脚手架项目文件夹  
右键点击项目中的package.json文件，选在终端/命令行中打开  
在弹出的命令行窗口中，输入`npm run serve`  
Npm run serve: 做了两件事:  
编译脚手架项目代码为浏览器认识的ES5代码  
同时启动简易开发服务器运行网站中网页  
打开浏览器，在地址栏中输入: `http://localhost:8080`，可看到示例网页  
或在命令行窗口中，按ctrl点连接地址: http://localhost:8080，也可查看示例网页  
强调: 从此live server 退出历史舞台！不再使用live server运行！**所有vue项目都用npm run serve运行**  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200217161655522.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)

###### 为脚手架添加axios模块

① 在脚手架生成的项目文件夹内，比如: 这里是xzvue文件夹内  
在地址栏输入cmd，打开命令行  
② 本地安装axios模块:  
`npm i -save axios`  
③ 在脚手架项目源代码的src/main.js中，new Vue()前引入axios模块  
`import axios from "axios"` //node\_modules中安装的模块，引入时都不用加路径  
④设置axios对象的基础路径属性:  
`axios.defaults.baseURL="http://服务器端域名"`  
比如: 学子商城项目中: axios.dafaults.baseURL=“http://xzserver.applinzi.com”  
⑤ 将axios对象放入Vue的原型对象中  
`Vue.prototype.axios=axios;`  
⑥结果: 因为所有组件对象都是Vue类型的子对象，所以在所有组件内，任何位置都可用this.axios.get()和this.axios.post()访问Vue.prototype中的axios对象里的函数。

###### 脚手架项目结构

(1). .git文件夹(隐藏): 本地git仓库文件夹 配置Git仓库忽略的一些文件(不会上传)  
(2). node\_modules文件夹: 保存脚手架项目运行的依赖包。  
(3). public文件夹:  
a. 保存着整个单页面应用唯一完整的index.html文件  
b. 将来还可能保存所有页面都需要的公共的css文件和js文件，比如:  
bootstrap.css , jquery.js , bootstrap.js  
1). 可在public文件夹下新建css和js文件夹  
2). 将所有页面都需要共用的第三方的css和js保存进去  
3). 在唯一完整的index.html，顶部引入所有页面所需的第三方的css和js  
c. 将来网页中用的所有图片，也都应该保存在public下！  
所以，拷贝旧项目中的img文件夹到public下  
(4). src文件夹: 放所有我们自己编写的HTML，css和js  
a. 根组件: 原SPA中唯一完整的页面的HTML和new Vue()不再放在一个.html文件里，而是分为两个文件了:  
1). App.vue 只放根组件`<div id="app">`的HTML内容和根组件的css样式  
2). main.js中放根组件`new Vue({})` 以及对new Vue()的配置  
3). 结果: 运行时，App.vue中的`<div id="app">`和main.js中new Vue()会重新被编译回唯一完整的index.html页面内。  
b. **多个页面组件**:  
1). 所有页面组件都要放在src/views/文件夹下  
2). 每个页面组件都是一个`.vue`文件  
3). 每个`.vue`文件中都包含三部分:

①

    <template>
    	编写当前页面组件的HTML片段
    </template>


②

    <script>//原页面组件对象中所有js内容，不再含template属性
    {
    	data(){  return { ... }  },
    	... 
    }
     </script>


③

    <style>
     当前页面所需的css样式，注意组件间样式冲突(这个组件下的子元素统一样式类名开头)
    </style>


c. 路由器对象: src/router/index.js  
同SPA中的路由器对象几乎完全一样

    new VueRouter({
    	routers:[
    		{path:"/",component:Index},
    		{path:"/details/:lid",component:Details, props:true},
    		...
    		{path:"*", component: NotFound }
    	]
    })


说明: router对象已经在main.js中被加入到new Vue()里了.  
d. components文件夹: 集中保存所有全局组件对象文件和子组件的文件。

###### 脚手架和SPA应用代码的结构

7.  其实: 脚手架代码的结构和SPA应用代码的结构本质是相同的。用已知释新知。  
    (1). 回顾: SPA代码结构:  
    ![s](https://img-blog.csdnimg.cn/20200207093150724.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
    (2). 脚手架代码结构: 其实就是SPA的代码结构  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200207093228218.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)

###### es6模块化开发在脚手架中的应用

(1). 旧SPA应用中的引入问题: 所有组件对象都要先集中引入到Index.html中，再以全局对象方式使用。如果单看某一个组件对象文件，根本看不出依赖关系。——不直观  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200207093331403.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)  
(2). 每个.vue文件和.js文件，默认都是一个模块对象  
(3). 每个模块对象都可向外抛出自己内部的成员，供外部访问  
export default {  
要抛出的组件对象的内容  
}  
(4). 一个模块想使用另一个模块的内容时，无需经过第三方，即可直接找到模块文件引入其中的内容。  
import 变量名 from “目标文件的相对路径”  
(5). 结果: 就可把目标文件中抛出的内容，引入自己文件内，像使用自己的变量和对象一样，使用其他文件模块中的内容。——减少中间商赚差价！  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200207093353240.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0MzE3MDE4,size_16,color_FFFFFF,t_70)

###### 用VUE脚手架项目开发

1.  在public/文件夹中添加网站所需的img文件夹和所有页面共用的第三方css和js，并且在唯一完整的index.html页面中，`<head></head>`中引入第三方的css和js
2.  在src/views/文件夹下，创建多个页面组件，将来程序中有几个页面，就创建几个.vue文件  
    每个页面.vue文件内都包含三部分内容:  
    ①`<template>`中包含这个页面的HTML片段：  
    eg:学子商城项目中: 回到旧jQuery项目中，找到对应的页面.html文件，复制其中的`<main>`部分代码到，Vue脚手架项目中的页面.vue中的`<template>`内  
    ② `<style>`中包含这个页面的css代码:  
    eg:学子商城项目中: 回到旧jQuery项目中，找到对应的页面.css文件，复制其中所有css代码到，Vue脚手架项目中的页面.vue中的`<style>`内
3.  在路由器对象中，添加每个页面的路由地址  
    在src/router/index.js中:  
    ① 先引入所有页面的组件对象:  
    import 页面名 from “页面组件的相对路径”  
    …  
    ② 再修改routes数组中的路由字典条目:  
    `{path:"/路径名", component: 页面名}`
4.  全局组件:  
    ① 在src/components/文件下  
    新建一个普通的组件.vue文件，同样包含三部分  
    `<template>`内包含组件的HTML片段  
    `<script>`内包含组件的vue js代码  
    `<style>`内包含组件的css代码  
    ② 在main.js中，在new Vue()前  
    a. 找到全局组件文件所在的位置，将全局组件的内容以模块对象方式引入到main.js中备用  
    import 组件名 from “./components/组件名.vue”  
    比如: 想引入页头组件:  
    import MyHeader from “./components/MyHeader”  
    b. 将引入的组件对象，变成一个真正的全局组件！  
    Vue.component(“标签名”, 组件名)  
    比如: 想将引入的页头组件对象，变成真正的全局组件  
    Vue.component(“my-header”,MyHeader);  
    c. 结果: 将来在任何页面或组件的任何位置都可通过`<my-header></my-header>`来引入全局组件。  
    比如: 想给将来所有页面上方都加页头: 在App.vue中

    <div id="app">
       <my-header></my-header>
       <router-view/>
    </div>
    

5.  子组件:

① 在src/components/文件夹下新建 子组件.vue文件  
在子组件.vue文件中编写这个子组件的内容  
比如: src/components/Carousel.vue

    <template>
    		<script>
    		<style>


② 在父组件的`<script>`中用import引入子组件对象

    <script>
       import 组件名 from "子组件路径"
       比如: import Carsouel from "../components/ Carsouel "


③ 在父组件的`<script>`中的export default 中

    export default {
    		... ...
    		components:{
    			组件名
    		比如: Carsouel
    		}
    	}


④ 结果: 在当前组件或页面内，就可用`<carsouel></carsouel>`来引入子组件

6.  所有页面都需要的css代码写在App.vue中的`<style>`中
7.  使用axios动态获取数据:  
    (1). 在用脚手架工具生成完项目源代码后，就要为项目添加axios模块(见脚手架安装和配置部分)  
    (2). 在当前组件的生命周期钩子函数中的created()函数内，或mounted()函数内都可发送axios请求。  
    (3). 在axios.get().then(res=>{})会调函数中，将服务器返回的数据(res.data)，分门别类的赋值给data中的变量  
    (4). 在页面/组件的`<template>`中，找到需要这些变量的位置，使用前面提到的绑定语法，绑定数据到页面指定位置

##### 组件的生命周期

①生命周期: 一个组件的加载过程  
② 回顾: 网页加载过程: 也有生命周期  
先加载HTML和JS，当HTML和JS加载完成后，提前触发DOMContentLoaded事件，  
所以，我们可以在DOMContentLoaded中编写发送ajax请求的代码。这样，只要页面加载到这个阶段，事件触发，就会自动向服务器发送请求。  
然后，当所有网页内容加载完，还会触发一个事件: window.onload。凡是写在window.onload事件中的代码，都会在整个页面加载完自动触发执行。  
③ 问题：组件不是页面，无法触发页面的加载完成事件，但是，我们也想在组件加载完自动发送ajax请求！  
④ 解决: 其实组件加载过程，也有生命周期的阶段，每个阶段也能自动触发一个回调函数。但是因为这个回调函数不是网页标准的事件，所以这种特殊的回调函数，称为生命周期中的钩子函数  
⑤ BS 列举: Vue组件加载过程共分四个阶段，每个阶段前后，都会自动触发一个钩子函数。共8个钩子函数:  
1.0 `beforeCreate(){ ... }`  
**1**. 创建(create)阶段: 创建vue对象，并创建vue中的data对象(只有data对象才能更新页面,只要是data创建完都可以写axios)  
1.1 `created(){ ... axios.get() ... }`  
2.0 `beforeMount(){ ... }`  
**2**. 挂载(mount)阶段: 扫描网页内容，建立虚拟DOM树，并首次更新页面中的内容  
2.1 `mounted(){ ... axios.get() ... }`  
\*\*\*\*\*\*\*\*\*\*\*\*\*\* 首次加载过程到此结束\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
3.0 `beforeUpdate(){ ... }`  
**3**. 更新(update)阶段: 当组件的data中的变量被修改时，自动触发该阶段  
3.1 `updated(){ ... }`  
4.0 `beforeDestroy(){ ... }`  
**4**. 销毁(destroy)阶段: 主动调用专门的函数销毁一个组件时才自动触发该阶段  
4.1 `destroyed(){ ... }`  
⑥ BS: 父组件和子组件生命周期函数的执行顺序:  
父组件beforeCreate()  
父组件created()  
父组件 beforeMount()  
父组件扫描页面内容时，发现不认识的子组件标签，开始进入子组件的加载过程  
子组件beforeCreate()  
子组件created()  
子组件 beforeMount()  
子附件 mounted()  
父组件才继续先后扫描后续内容  
父组件的mounted()

##### 总结

1.  元素内容需要动态改变: `{{变量或js表达式}}`
2.  元素属性值需要动态改变: `:属性名="变量或js表达式"`
3.  控制一个元素显示隐藏: 首选 v-show=“条件”
4.  控制两个元素二选一显示:  
    <元素1 v-if=“条件”>  
    <元素2 v-else>
5.  控制多个元素多选一显示:  
    <元素1 v-if=“条件1”>  
    <元素2 v-else-if=“条件2”>  
    … …  
    <元素n v-else>
6.  反复生成多个相同结构的HTML元素时:  
    <元素 v-for="(value,i) of 数组/字符串/对象/数字" :key=“i”>
7.  绑定HTML片段内容:  
    <元素 v-html=“包含HTML内容的变量或表达式”></元素>
8.  防止用户短暂看到{{}}语法:  
    (1). `<style>[v-cloak]{display:none}</style>`  
    <元素 v-cloak>  
    (2). <元素 v-text=“包含{{}}的js表达式”></元素>
9.  绑定事件: <元素 @事件名=“处理函数(参数值,$event)”
10.  只在首次加载页面时绑定一次: v-once
11.  阻止内容中的{{}}被vue编译: v-pre
12.  只要绑定表单元素的值，都用双向绑定v-model  
    <表单元素 v-model=“变量”>