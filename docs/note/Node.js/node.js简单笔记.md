<!--
 * @Descripttion: 
 * @version: 
 * @Author: qiaoyurensheng@163.com
 * @Date: 2020-06-15 00:27:49
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-06-15 00:44:18
--> 
### 一、文件系统

#### 文件读取与写入

```javascript
// 1.引入文件系统模块
const fs = require('fs');
// 2.通过对象调用方法
//同步读取文件（文件名，文件编码）
var readme = fs.readFileSync("readme.txt", "utf8");
console.log(readme);
//同步写入文件(文件名，写入内容)
fs.writeFileSync("writeme.txt", readme);
//异步读取文件（文件名，文件编码，回调函数（错误信息，读取内容））
fs.readFile("readme.txt", "utf8", function (err, data) {
     if (err) throw err;
     console.log(data);
 })
 //异步写入文件
 fs.readFile("write.txt","utf8",function(err,data){
     //异步写入文件(文件名，写入内容)
     fs.writeFile("write.txt",data);
 })
```

#### 创建和删除文件
```javascript
//1.引入文件系统模块
var fs = require('fs');

//2.使用模块对象调用方法
//异步删除文件
fs.unlink("writeme.txt", function (err) {
    if (err) throw err;
    console.log("文件删除成功");
});

//3.创建/删除文件夹
//同步创建文件夹
 fs.mkdirSync("stuff");
//同步删除文件夹
fs.rmdirSync("stuff");

//异步创建文件夹
fs.mkdir("stuff", function (err) {
    if (err) throw err;
    console.log("文件夹创建成功！")

})
//异步删除文件夹
fs.rmdir("stuff", function (err) {
    if (err) throw err;
    console.log("文件夹删除成功！")
})

```

### 二、服务器与客户端

```javascript
//通过http模块，创建本地服务器
//引入http模块
var http = require('http');

//创建本地服务器
var server = http.createServer(function (req, res) {
    console.log("服务器：" + req.url);
    //数据头
    res.writeHead(200, { "Content-type": "text/plain" });
    res.end("Server is working ...");
});

//服务对象监听服务器地址以及端口号
server.listen(8888, "127.0.0.1");
console.log("服务器正在运行。。。");
```

### 三、数据流与管道
#### 读写数据流
```javascript
//数据流

var fs = require('fs');
//读数据流

var myReadStream = fs.createReadStream(__dirname + '/readme.txt', "utf8");

//写入文件流
var myWriteStream = fs.createWriteStream(__dirname + '/writeme2.txt')

//管道可以实现数据转移
myReadStream.pipe(myWriteStream);

// console.log(myReadStream)
// myReadStream.on('data', function (chunk) {
//     console.log('=========================一部分数据======================');
//     //写入数据
//     myWriteStream.write(chunk);
// });
```
```javascript
//在浏览器中访问数据流读取的数据（通过管道pipe）
var http = require('http');
var fs = require('fs');

var server = http.createServer(function (req, res) {
    res.writeHead(200, { "Content-type": "text/plain" });
    var myReadStream = fs.createReadStream(__dirname + '/readme.txt', "utf8");
    myReadStream.pipe(res);

});
server.listen(3000, "127.0.0.1");
console.log("server is runing...");
```


### 四、Node读取HTML和JSON数据
#### 读取html

```javascript
var http = require('http');
var fs = require('fs');

//搭建服务器
//req->request:请求，res->respond:回应（响应）
var server = http.createServer(function (req, res) {
    //文件头需要改为html类型
    res.writeHead(200, { "Content-type": "text/html" });
    var myReadStream = fs.createReadStream(__dirname + '/index.html', "utf8");
    //管道可以实现数据转移
    myReadStream.pipe(res);

});
//监听IP+端口
server.listen(3000, "127.0.0.1");
console.log("server is runing...");
```
#### 读取json

```javascript
var http = require('http');
var fs = require('fs');

//搭建服务器
//req->request:请求，res->respond:回应（响应）
var server = http.createServer(function (req, res) {
    //文件头可以改为json类型
    res.writeHead(200, { "Content-type": "application/json" });
    var myReadStream = fs.createReadStream(__dirname + '/person.json', "utf8");
    //管道可以实现数据转移
    myReadStream.pipe(res);

});
//监听IP+端口
server.listen(3000, "127.0.0.1");
console.log("server is runing...");
```

### 五、路由

```javascript

//搭建服务器
//req->request:请求，res->respond:回应（响应）
var server = http.createServer(function (req, res) {
    //判断用户将要访问的地址（路由）
    if (req.url == '/home' || req.url == '/') {
        res.writeHead(200, { "Content-type": "text/html" });
        //将文件读取流中读取到的文件通过管道（pipe）发送到页面中
        fs.createReadStream(__dirname + '/index.html', "utf8").pipe(res);
    } else if (req.url == "/contact") {
        res.writeHead(200, { "Content-type": "text/html" });
        fs.createReadStream(__dirname + '/contact.html', "utf8").pipe(res);
    } else if (req.url == "/api/docs") {
        var data = [{ name: "herry", age: 43 }, { name: "bucky", age: 12 }];
        res.writeHead(200, { "Content-type": "application/json" });
        //将data值转化为json字符串
        res.end(JSON.stringify(data));
    }

});
server.listen(3000, "127.0.0.1");
console.log("server is runing...");

```

### 六、Express模板

>send是express的方法，end是原生的方法，而且使用了end也可以返回数据

```javascript
//引入express框架

var express = require('express');

//实例化express对象
var app = express()

//通过对象调用方法
//根据用户请求的地址返回相应的数据信息，get(路径，函数)
app.get('/', function (req, res) {
    console.log(req.url);
    //发送到浏览器的信息
    res.send("this is home page!")
})

app.get("/contact", function (req, res) {
    console.log(req.url);
    res.send("thid id contact page！")

})

//路由参数
app.get("/profile/:id", function (req, res) {
    //params可以获取路由的参数
    res.send("路径参数为：" + req.params.id)
})


//监听服务器端口号
app.listen(8888);
```


- #### EJS模板引擎

```javascript
//引入express框架

var express = require('express');

//实例化express对象
var app = express()

//配置视图引擎
app.set('view engine', 'ejs');

//通过对象调用方法
//根据用户请求的地址返回相应的数据信息，get(路径，函数)
// app.get('/', function (req, res) {
//     console.log(req.url);
//     //发送到浏览器的信息
//     res.sendFile(__dirname + "/index.html");
// })

// app.get("/contact", function (req, res) {
//     console.log(req.url);
//     res.sendFile(__dirname + '/contact.html');

// })

//路由参数
app.get("/profile/:id", function (req, res) {
    //使用render(文件名，传入参数)，访问.ejs文件，只需给出文件名，无需后缀名（提前创建了一个views>profile.ejs）
    res.render('profile', { name: 'EJS' });
})

app.listen(8888);

```

```javascript

//路由参数
app.get("/profile/:id", function (req, res) {
    var data = [{ age: 29, name: "herry" }, { age: 33, name: "bob" }];
    //render(文件名，传入参数)，访问.ejs文件，只需给出文件名，无需后缀名
    res.render('profile', { websiteName: req.params.id, data: data });
})
//  views>profile.ejs中部分代码
 <h1>Welcome to <%= websiteName  %></h1>
    <!-- <p><strong>Age:</strong><%=  data.age %></p>
    <p><strong>name:</strong><%=  data.name %></p> -->

    <ul>
        <% data.forEach(function(item){%>
        <li><%= item.age %></li>
        <li><%= item.name %></li>
        <% }) %>
    </ul>
监听服务器端口号
```