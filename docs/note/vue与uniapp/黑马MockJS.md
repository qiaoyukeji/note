### 1.安装Moke

可在vue图形化界面里安装

### 2.导入Mock
在vue项目src目录中新建mock>index.js,然后在main.js中导入
```javascript
// mock>index.js
//导入模拟数据mock包
import Mock from 'mockjs'

//通过Mock.mock() 来模拟API接口
Mock.mock('/api/goodslist', 'get', {
    status: 200,
    message: '获取商品成功',
    data: [1, 2, 3, 4]
})


```

    import './mock/index'   //main.js中导入mock
```vue
// App.vue
<template>
  <div id="app">
    学习mock
    <button @click="getGoodsList">获取商品列表</button>
  </div>
</template>

<script>
export default {
  methods: {
    async getGoodsList() {
      const { data: res } = await this.$http.get("/api/goodslist");
      console.log(res);
    }
  }
};
</script>

<style>
</style>
```


```javascript
Mock.mock('/api/goodslist', 'get', {
    status: 200,
    message: '获取商品成功',
    // 5-10表示随即生成5-10个data   
    'data|5-10': [{
        // @increment生成一个全局的自增整数
        id: '@increment',
        // @cword 随机生成一个汉字，@cword(2,8) 随机生成2~8个汉字
        name: "@cword(2,8)",
        //@natural(a,b)随即生成一个a~b之间自然数
        price: '@natural(2,10)',
        count: '@natural(100,999)',
        // @dataImage 随即生成一个图片
        img: '@dataImage(78x78)'
    }]
})
```