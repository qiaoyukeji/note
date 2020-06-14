<!--
 * @Descripttion: 
 * @version: 
 * @Author: qiaoyurensheng@163.com
 * @Date: 2020-06-15 00:58:33
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-06-15 00:59:32
--> 
## axios:功能强大的网络请求库（黑马程序员）

### 1.基础参数
axios 可用 async/await 修饰
```javascript
//引入axios
<script src="https://cdn.bootcss.com/axios/0.19.2/axios.min.js"></script> 

//then回调函数：第一个在请求响应完成时触发，第二个在请求失败时触发
//get(地址?查询字符串)
axios.get(地址?key=value&key2=value2).then(function(response){},function(err){})
//get(地址，{params:{key:value, key2:value2}})
//axios.get(地址,{
//    params:{
//        key:value,
//        key2:value2
//    }
//}).then(function(response){},function(err){})


//delect 与 get 类似

//post(地址，参数对象)
axios.post(地址，{key:value,key2:value2}).then(function(response){},function(err){})
//var params=new URLSearchParams();
//params.append("key","value");
//params.append("key2","value2");
//axios.post(地址,params).then(function(response){},function(err){})



//put 与 post 类似


```
```
axios 的响应结果
data : 实际响应回来的数据
header : 响应头信息
status : 响应状态码
statusText : 响应状态信息
```

> #### axios全局配置
>> axios.default.timeout=3000;  //设置超时时间
>> axios.default.baseURL='http://localhost:3000/api';  //设置默认地址
>> axios.default.header["token"]="qwerasdf123";  //设置请求头token 

### 2.axios 拦截器
应用场景：  
- 1：每个请求都带上的参数，比如token，时间戳等。  
- 2：对返回的状态进行判断，比如token是否过期

> 请求拦截器
```javascript
// 请求拦截器
axios.interceptors.request.use(
  config => {
    // 每次发送请求之前判断vuex中是否存在token
    // 如果存在，则统一在http请求的header都加上token，这样后台根据token判断你的登录情况
    // 即使本地存在token，也有可能token是过期的，所以在响应拦截器中要对返回状态进行判断
    const token = window.localStorage.getItem("token");
    token && (config.headers.Authorization = token);
    return config;
  },
  error => {
    return Promise.error(error);
  }
);
```

> 响应拦截器
```javascript
//响应拦截器
axios.interceptors.response.use(
  response => {
    // 如果返回的状态码为200，说明接口请求成功，可以正常拿到数据
    // 否则的话抛出错误
    if (response.status === 200) {
      return Promise.resolve(response);
    } else {
      return Promise.reject(response);
    }
  },
  // 服务器状态码不是2开头的的情况
  // 这里可以跟你们的后台开发人员协商好统一的错误状态码
  // 然后根据返回的状态码进行一些操作，例如登录过期提示，错误提示等等
  // 下面列举几个常见的操作，其他需求可自行扩展
  error => {
    if (error.response.status) {
      switch (error.response.status) {
        // 401: 未登录
        // 未登录则跳转登录页面，并携带当前页面的路径
        // 在登录成功后返回当前页面，这一步需要在登录页操作。
        case 401:
          vant.Toast.fail("身份验证失败，请关闭重新进入。");
          break;

        // 403 token过期
        // 登录过期对用户进行提示
        // 清除本地token和清空vuex中token对象
        // 跳转登录页面
        case 403:
          vant.Toast.fail("登录过期，请关闭重新进入。");
          // 清除token
          break;

        // 404请求不存在
        case 404:
          vant.Toast.fail("您访问的网页不存在。");
          break;
        // 其他错误，直接抛出错误提示
        default:
          vant.Toast.fail(error.response.data.message);
      }
      return Promise.reject(error.response);
    }
  }
);
```

### 3.测试接口（可自行使用其他接口）
> 随机获取笑话的接口
- 请求地址：https://autumnfish.cn/api/joke/list
- 请求方法：get
- 请求参数：num
  
| 参数名 | 参数说明 | 备注       |
| ------ | -------- | ---------- |
| num    | 笑话条数 | 类型为数字 |

> 用户注册的接口
- 请求地址：https://autumnfish.cn/api/user/reg
- 请求方法：post
- 请求参数：username
  
| 参数名   | 参数说明 | 备注     |
| -------- | -------- | -------- |
| username | 用户名   | 不能为空 |


### 4.具体小案例

```html
    <input type="button" value="get请求" class="get">
    <input type="button" value="post请求" class="post">
    <!-- 引入axios -->
    <script src="https://cdn.bootcss.com/axios/0.19.2/axios.min.js"></script>

    <script>
        //get点击事件
        document.querySelector(".get").onclick = function () {
            axios.get("https://autumnfish.cn/api/joke/list?num=3").then(function (response) {
                console.log(response);
            }, function (err) {
                console.log("错误：" + err);
            })
        };

        // post点击事件
        document.querySelector(".post").onclick = function () {
            axios.post("https://autumnfish.cn/api/user/reg", { username: "jack" }).then(function (response) {
                console.log(response);
            }, function (err) {
                console.log("错误：" + err);
            })
        }
    </script>
```

### 5.axios + vue
> 注意： axios 中的 this 已经改变，无法拿到 data 中的数据，故使用 that
```javascript
<div id="app">
        <input @click="getJoke" type="button" value="获取笑话">
        <p>{{ joke }}</p>
    </div>


    <script src="https://cdn.bootcss.com/axios/0.19.2/axios.min.js"></script>
    <script src="https://cdn.bootcss.com/vue/2.6.11/vue.min.js"></script>
    <script>
        var app = new Vue({
            el: "#app",
            data: {
                joke: "一个笑话"
            },
            methods: {
                getJoke: function () {
                    // console.log(this.joke);
                    var that = this;
                    axios.get("https://autumnfish.cn/api/joke").then(function (response) {
                        // console.log(response.data);
                        //axios中的this已经改变，无法拿到data中的数据，故使用that
                        // console.log(this.joke);
                        that.joke = response.data;
                    }, function (err) {
                        console.log("错误：" + err);
                    })
                }
            }
        })
    </script>
```