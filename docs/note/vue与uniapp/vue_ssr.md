## vue ssr 实战

#### SSR 概念 （server side render）

Vue.js 是构建客户端应用程序的框架。默认情况下，可以在浏览器中输出 Vue 组件，进行生成 DOM 和操作 DOM。然而，也可以将同一个组件渲染为服务器端的 HTML 字符串，将它们直接发送到浏览器，最后将这些静态标记"激活"为客户端上完全可交互的应用程序。



>    传统web渲染技术：asp.net php jsp

![image-20200503233936790](https://gitee.com//qiaoyukeji/markdown_tupian/raw/master/markdown/20200503233938.png)

>    SSR：

![image-20200503234609398](https://gitee.com//qiaoyukeji/markdown_tupian/raw/master/markdown/20200503234610.png)

## 实现vue ssr 的具体过程

#### 创建vue cli 3

```
vue create ssr
```

#### 安装依赖

渲染器 `vue-server-renderer`

`nodejs` 服务器 `express`	

```
npm i vue-server-renderer express -D
```



#### 编写服务端启动脚本

```js
const express = require("express")
const Vue = require("vue")

//创建express 和 vue 实例
const app = express()
//创建渲染器
const renderer = require('vue-server-renderer').createRenderer()

//用渲染器渲染page 可以得到 html 内容
const page = new Vue({
    template: '<div>hello ,vue ssr</div>'
})

app.get("/", async (req, res) => {
    try {
        //用渲染器渲染page 可以得到 html 内容
        const html = await renderer.renderToString(page)
        console.log(html);
        res.send(html)
    } catch (error) {
        res.status(500).send("服务器内部错误")
    }

})

app.listen(3000, () => {
    console.log("server is running...");

})
```

---



### vue-router	

```
npm install vue-router --save
```

**配置**

-   创建./src/router/index.js
-   创建Index.vue、Detail.vue，更新App.vue

```js
//	router/index.js
import Vue from 'vue'
import Router from "vue-router";
import Index from "../components/Index";
import Detail from "../components/Detail";

Vue.use(Router)

//这里为什么不导出一个router 实例 ？
//因为：将来每次用户请求都需要用户实例
export default function createRouter(){
    return new Router({
        mode: 'history',
        routes: [
            {
                path: '/',
                component: Index
            },
            {
                path: '/detail',
                component: Detail
            }
        ]
    })
}
```

```vue
//	App.vue
<template>
  <div id="app">
    <nav>
      <router-link to="/">首页</router-link>
      <router-link to="/detail">详情页</router-link>
    </nav>
    <router-view></router-view>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>

```

### 构建

#### 构建流程

![image-20200504132616680](https://gitee.com//qiaoyukeji/markdown_tupian/raw/master/markdown/20200504132627.png)

####  代码结构

![image-20200504132645686](https://gitee.com//qiaoyukeji/markdown_tupian/raw/master/markdown/20200504132648.png)



#### 入口 ：app.js

```
//	app.js
// 创建vue实例
import Vue from "vue";
import App from "./App";
import createRouter from "./router";

//这里为什么使用工厂函数 ？
//因为：将来每次用户请求都需要用户实例
export default function createApp() {
    const router = new createRouter()
    const app = new Vue({
        router,
        render: h => h(App)
    })
    return { app, router }
}
```

####  服务端入口

entry-server.js

```js
//  渲染首屏
import createApp from "./app";


// context 是什么 ？
export default context => {
    return new Promise((resolve, reject) => {
        const { app, router } = createApp();
        //进入首屏去
        router.push(context.url)

        router.onReady(() => {
            resolve(app)
        },reject)
    })
}
```

####  客户端入口

entry-client.js

```js
//挂载、激活app
import createApp from "./app";

const { app, router } = createApp()

router.onReady(() => {
    app.$mount('#app')
})
```

