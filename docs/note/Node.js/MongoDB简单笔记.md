<!--
 * @Descripttion: 
 * @version: 
 * @Author: qiaoyurensheng@163.com
 * @Date: 2020-06-15 00:28:55
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-06-15 00:29:14
--> 
### 1. MongoDB 数据库的相关概念

在一个数据库软件中可以包含多个数据仓库，在每个数据仓库中可以包含多个数据集合，每个数据集合中可以包含多条文档（具体的数据）。

| **术语**   | **解释说明**                                             |
| ---------- | -------------------------------------------------------- |
| database   | 数据库，mongoDB数据库软件中可以建立多个数据库            |
| collection | 集合，一组数据的集合，可以理解为JavaScript中的数组       |
| document   | 文档，一条具体的数据，可以理解为JavaScript中的对象       |
| field      | 字段，文档中的属性名称，可以理解为JavaScript中的对象属性 |

#### 1.1 MongoDB 第三方包 mongoose
> 使用Node.js操作MongoDB数据库需要依赖Node.js第三方包mongoose
> 使用npm install mongoose命令下载

#### 1.2 MongoDB 的启动与关闭
> - 在命令行工具中运行net start mongoDB即可启动MongoDB，否则MongoDB将无法连接。
> - 在命令行工具中运行 net stop mongoDB 停止MongoDB

#### 1.3 MongoDB 的链接
> 使用mongoose提供的connect方法即可连接数据库。
```javascript
mongoose.connect('mongodb://localhost/playground')
     .then(() => console.log('数据库连接成功'))
     .catch(err => console.log('数据库连接失败', err));
```


    { useNewUrlParser: true, useUnifiedTopology: true }
#### 1.4 创建数据库
> 在MongoDB中不需要显式创建数据库，如果正在使用的数据库不存在，MongoDB会自动创建。


### 2.MongoDB 增删改查
#### 2.1 创建集合

创建集合分为两步，一是**对集合设定规则**，二是**创建集合**，创建mongoose.Schema构造函数的实例即可创建集合。
```javascript
// 设定集合规则
 const courseSchema = new mongoose.Schema({
     name: String,
     author: String,
     isPublished: Boolean
 });
  // 创建集合并应用规则(集合名称，应用的规则),返回的是构造函数
 const Course = mongoose.model('Course', courseSchema); // courses
```

#### 2.2 创建文档
##### 第一种方法

创建文档实际上就是向集合中插入数据。
分为两步：
- 1.创建集合实例。
- 2调用实例对象下的save方法将数据保存到数据库中。

```javascript
// 创建集合的实例
 const course = new Course({
     name: 'Node.js course',
     author: '黑马讲师',
     tags: ['node', 'backend'],
     isPublished: true
 });
  // 将数据保存到数据库中
 course.save();
```
##### 第二种方法
```javascript
//通过回调函数接收返回数据
Course.create({name: 'JavaScript基础', author: '黑马讲师', isPublish: true}, (err, result) => { 
     //  错误对象
    console.log(err)
     //  当前插入的文档
    console.log(result)
});
```

```javascript
//通过 Promise 对象接收返回数据
Course.create({name: 'JavaScript基础', author: '黑马讲师', isPublish: true})
      .then(result => console.log(result))
      .catch(err => console.log(err))

```

#### 2.3 mongoDB数据库导入数据
- mongoimport –d 数据库名称 –c 集合名称 --file 要导入的数据文件  
- 找到mongodb数据库的安装目录，将安装目录下的bin目录放置在环境变量中。

#### 2.4 查询文档


> find
```javascript
//  根据条件查找文档（条件为空则查找所有文档）
Course.find().then(result => console.log(result))
```
```javascript
// 返回文档集合(数组)
[{
    _id: 5c0917ed37ec9b03c07cf95f,
    name: 'node.js基础',
    author: '黑马讲师‘
},{
     _id: 5c09dea28acfb814980ff827,
     name: 'Javascript',
     author: '黑马讲师‘
}]
```
> findOne

```javascript
//  根据条件查找文档
Course.findOne({name: 'node.js基础'}).then(result => console.log(result))
```
```javascript
// 返回文档(对象)
 {
    _id: 5c0917ed37ec9b03c07cf95f,
    name: 'node.js基础',
    author: '黑马讲师‘
}
```

> 匹配查询

需要先补齐 集合规则 与 集合 才能进行查询
```javascript
const userSchema = new mongoose.Schema({
    name: String,
    age: String,
    email: String,
    password: String,
    hobbies: [String]
})


const User = mongoose.model('User', userSchema);
```

```javascript
//  匹配大于 小于
//$gt : >   ,  $lt   :  <
 User.find({age: {$gt: 20, $lt: 50}}).then(result => console.log(result))
```

```javascript
 //  匹配包含 $in
 User.find({hobbies: {$in: ['敲代码']}}).then(result => console.log(result))
```

```javascript
//  选择要查询的字段  
 User.find().select('name email').then(result => console.log(result))
```

```javascript
 // 将数据按照年龄进行排序,（升序）
 User.find().sort('age').then(result => console.log(result))

 // 将数据按照年龄进行排序,（降序）
 User.find().sort('-age').then(result => console.log(result))
```

```javascript
//  skip 跳过多少条数据  limit 限制查询数量
 User.find().skip(2).limit(2).then(result => console.log(result))

```

#### 2.5 删除文档

```javascript
 // 删除单个,返回删除的数据
Course.findOneAndDelete({}).then(result => console.log(result))
 // 删除多个,{}不填默认删除所有
User.deleteMany({}).then(result => console.log(result))
```


#### 2.6 更新文档

```javascript
// 更新单个
User.updateOne({查询条件}, {要修改的值}).then(result => console.log(result))

// 更新多个
User.updateMany({查询条件}, {要更改的值}).then(result => console.log(result))
```


#### 2.6 mongoose 验证
在创建集合**规则**时，可以设置当前字段的验证规则，验证失败就则输入插入失败。
>1. required: true 必传字段  
```javascript
const postSchema = new mongoose.Schema({
    title: {
        type: String,
        // [是否必填，自定义错误信息]
        required: [true, '请传入文章标题']
    }
})
```

>2. minlength：3 字符串最小长度  
>3. maxlength: 20 字符串最大长度  
```javascript
const postSchema = new mongoose.Schema({
    title: {
        type: String,
        required: [true, '请传入文章标题'],
        minlength: 2,
        //[长度，自定义错误信息]
        maxlength: [5,'文章长度不能超过5']
    }
})
```
>4. min: 2 数值最小为2  
>5. max: 100 数值最大为100  
```javascript

const postSchema = new mongoose.Schema({
    title: {
        type: String,
        required: [true, '请传入文章标题'],
        minlength: 2,
        maxlength: 5,
        trim: true
    },
    age: {
        type: Number,
        //也可以自定义错误信息，同上
        min: 18,
        max: 100
    }
})
```
>6. enum: ['html', 'css', 'javascript', 'node.js']  
```javascript
const postSchema = new mongoose.Schema({
    title: {
        type: String,
        required: [true, '请传入文章标题'],
        minlength: 2,
        maxlength: 5,
        trim: true
    },
    age: {
        type: Number,
        min: 18,
        max: 100
    },
    category: {
        type: String,
        //传入值必须为enum中包含的值
        enum: ["Html", "JavaScript", "Node.js"]
    }
})
```
>7. trim: true 去除字符串两边的空格  
>8. validate: 自定义验证器  
```javascript
const postSchema = new mongoose.Schema({
    title: {
        type: String,
        required: [true, '请传入文章标题'],
        minlength: 2,
        maxlength: 5,
        trim: true
    }
    author: {
        type: String,
        validate: {
            validator: (v) => {
                //v表示要验证的值，  返回布尔值,true 验证成功，false  验证失败，
                return v && v.legth > 4
            },
            //自定义错误信息
            message: '传入的值不符合验证规则'
        }
    }
})
```
>9. default: 默认值  
```javascript
const postSchema = new mongoose.Schema({
    title: {
        type: String,
        required: [true, '请传入文章标题'],
        minlength: 2,
        maxlength: 5,
        trim: true
    },
    age: {
        type: Number,
        min: 18,
        max: 100
    },
    publishDate: {
        //类型为日期类型
        type: Date,
        //默认值为当期日期
        default: Date.now
    }
})
```
> 10 . 获取错误信息：error.errors['字段名称'].message
```javascript
Post.create({ title: 'bbb', age: 20, category: "html", author: 'bd' })
    .then(res => {
        console.log(res);
    })
    .catch(error => {
        //获取错误信息对象
        const err = error.errors;
        //循环错误信息对象
        for (var item in err) {
            //打印错误信息
            console.log(err[item].message);
        }
    })
```


#### 2.7 集合关联
通常不同集合的数据之间是有关系的，例如文章信息和用户信息存储在不同集合中，但文章是某个用户发表的，要查询文章的所有信息包括发表用户，就需要用到集合关联。
- 使用id对集合进行关联
- 使用populate方法进行关联集合查询

```javascript
// 用户集合
const User = mongoose.model('User', new mongoose.Schema({ name: { type: String } })); 
// 文章集合
const Post = mongoose.model('Post', new mongoose.Schema({
    title: { type: String },
    // 使用ID将文章集合和作者集合进行关联
    author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
}));

//创建用户
// User.create({ name: 'itheima' }).then(res => {
//     console.log(res);
// })

//创建文章
// Post.create({ title: '123', author: '5e8d617a10b7d10cb4fac26f' }).then(res => {
//     console.log(res);
// })

//联合查询
Post.find()
      .populate('author')
      .then((err, result) => console.log(result));

```


##### 一个增删改查的小案例:
```javascript
const http = require('http')
const mongoose = require("mongoose")
const url = require("url")
const querystring = require('querystring')

//数据库连接
mongoose.connect("mongodb://localhost/playground", { useUnifiedTopology: true, useNewUrlParser: true }).then(() => {
    console.log("数据库连接成功");
}).catch(() => {
    console.log("数据库连接失败");
})

//创建用户集合规则
const UserSchema = new mongoose.Schema({
    name: {
        type: String,
        required: true,
        maxlength: 20,
        minlength: 2
    },
    age: {
        type: Number,
        max: 80,
        min: 18
    },
    password: String,
    email: String,
    hobbies: [String]
})
//创建集合 返回集合构造函数
const User = mongoose.model("User", UserSchema)


//创建服务器
const app = http.createServer()

//为服务器对象添加请求事件
app.on("request", async (req, res) => {
    //请求方式
    const method = req.method;
    //请求地址
    const { pathname, query } = url.parse(req.url, true);

    if (method == 'GET') {
        //呈现用户列表页面
        if (pathname == "/list") {
            //查询用户信息
            let users = await User.find();
            console.log(users);
            //html字符串
            let list = `
            <!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<title>用户列表</title>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css">
</head>
<body>
	<div class="container">
		<h6>
			<a href="/add" class="btn btn-primary">添加用户</a>
		</h6>
		<table class="table table-striped table-bordered">
			<tr>
				<td>用户名</td>
				<td>年龄</td>
				<td>爱好</td>
				<td>邮箱</td>
				<td>操作</td>
			</tr>
            
            
            
            `;

            //对数据进行循环
            users.forEach(item => {
                list += `
                <tr>
				<td>${item.name}</td>
				<td>${item.age}</td>
				<td>	
                
                `;

                item.hobbies.forEach(i => {
                    list += `
                    <span>${i}</span>
                    `
                })
                list += `
                </td>
				<td>${item.email}</td>
				<td>
					<a href="/remove?id=${item.id}" class="btn btn-danger btn-xs">删除</a>
					<a href="/modify?id=${item._id}" class="btn btn-success btn-xs">修改</a>
				</td>
			</tr>
                
                `
            })

            list += `
            </table>
	</div>
</body>
</html>
            `
            res.end(list)
        } else if (pathname == '/add') {
            let add = `
            <!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<title>用户列表</title>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css">
</head>
<body>
	<div class="container">
		<h3>添加用户</h3>
		<form method="post" action="/add">
		  <div class="form-group">
		    <label>用户名</label>
		    <input name="name" type="text" class="form-control" placeholder="请填写用户名">
		  </div>
		  <div class="form-group">
		    <label>密码</label>
		    <input name="password" type="password" class="form-control" placeholder="请输入密码">
		  </div>
		  <div class="form-group">
		    <label>年龄</label>
		    <input name="age" type="text" class="form-control" placeholder="请填写邮箱">
		  </div>
		  <div class="form-group">
		    <label>邮箱</label>
		    <input name="email" type="email" class="form-control" placeholder="请填写邮箱">
		  </div>
		  <div class="form-group">
		    <label>请选择爱好</label>
		    <div>
		    	<label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="足球"> 足球
		    	</label>
		    	<label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="篮球"> 篮球
		    	</label>
		    	<label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="橄榄球"> 橄榄球
		    	</label>
		    	<label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="敲代码"> 敲代码
		    	</label>
		    	<label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="抽烟"> 抽烟
		    	</label>
		    	<label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="喝酒"> 喝酒
		    	</label>
		    	<label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="烫头"> 烫头
		    	</label>
		    </div>
		  </div>
		  <button type="submit" class="btn btn-primary">添加用户</button>
		</form>
	</div>
</body>
</html>
            `;
            res.end(add);
        } else if (pathname == '/modify') {
            let user = await User.findOne({ _id: query.id });
            let hobbies = ['足球', '篮球', '橄榄球', '敲代码', '抽烟', '喝酒', '烫头'];
            console.log(user);

            let modify = `
            <!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<title>用户列表</title>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css">
</head>
<body>
	<div class="container">
		<h3>修改用户</h3>
		<form method="post" action="/modify?id=${user._id}">
		  <div class="form-group">
		    <label>用户名</label>
		    <input value="${user.name}" name="name" type="text" class="form-control" placeholder="请填写用户名">
		  </div>
		  <div class="form-group">
		    <label>密码</label>
		    <input value="${user.password}" name="password" type="password" class="form-control" placeholder="请输入密码">
		  </div>
		  <div class="form-group">
		    <label>年龄</label>
		    <input value="${user.age}" name="age" type="text" class="form-control" placeholder="请填写邮箱">
		  </div>
		  <div class="form-group">
		    <label>邮箱</label>
		    <input value="${user.email}" name="email" type="email" class="form-control" placeholder="请填写邮箱">
		  </div>
		  <div class="form-group">
		    <label>请选择爱好</label>
		    <div>
		    	<label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="足球"> 足球
                </label>
                `;
            hobbies.forEach(item => {
                let isHobby = user.hobbies.includes(item);
                if (isHobby) {
                    modify += `
                    <label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="${item}" checked> ${item}
                </label>`
                } else {
                    modify += `
                    <label class="checkbox-inline">
		    	  <input name="hobbies" type="checkbox" value="${item}" > ${item}
                </label>`
                }
            })
            modify += `    
		    </div>
		  </div>
		  <button type="submit" class="btn btn-primary">修改用户</button>
		</form>
	</div>
</body>
</html>
            `;
            res.end(modify)

        } else if (pathname == "/remove") {
            // res.end(query.id)
            await User.findOneAndDelete({ _id: query.id });
            res.writeHead(301, {
                Location: "/list"
            })
            res.end()
        }
    } else if (method == "POST") {
        //用户添加功能
        if (pathname == "/add") {
            //接收用户提交的信息
            let formData = '';
            //接收post参数
            req.on("data", param => {
                formData += param;
            })
            //post参数接收完毕
            req.on("end", async () => {
                // console.log(querystring.parse(formData));
                let users = querystring.parse(formData);

                //将用户提交的数据添加到数据库中

                await User.create(users);
                //重定向
                res.writeHead(301, {
                    Location: "/list"
                })
                res.end();
            })
        } else if (pathname == "/modify") {
            //接收用户提交的信息
            let formData = '';
            //接收post参数
            req.on("data", param => {
                formData += param;
            })
            //post参数接收完毕
            req.on("end", async () => {
                // console.log(querystring.parse(formData));
                let users = querystring.parse(formData);

                //将用户提交的数据添加到数据库中

                await User.updateOne({ _id: query.id }, users);
                //重定向
                res.writeHead(301, {
                    Location: "/list"
                })
                res.end();
            })
        }

    }})

//监听端口
app.listen(3000)
```

### 3. 模板引擎
#### 3.1 模板引擎
模板引擎是第三方模块。
让开发者以更加友好的方式拼接字符串，使项目代码更加清晰、更加易于维护。


#### 3.2 art-template 模板引擎

- 1. 在命令行工具中使用 npm install art-template 命令进行下载
- 2. 使用const template = require('art-template')引入模板引擎
- 3. 告诉模板引擎要拼接的数据和模板在哪 const html = template(‘模板路径’, 数据);
- 4. 使用模板语法告诉模板引擎，模板与数据应该如何进行拼接 

#### 3.3  art-template代码示例

```javascript
 // 导入模板引擎模块
 const template = require('art-template');
 // 将特定模板与特定数据进行拼接
 const html = template('./views/index.art',{
    data: {
        name: '张三',
        age: 20
    }
 }); 
```
```javascript
//  views/index.art 文件
 <div>
    <span>{{data.name}}</span>
    <span>{{data.age}}</span>
 </div>
```

### 4. 模板引擎语法

#### 4.1 模板语法
1. art-template同时支持两种模板语法：标准语法和原始语法。  
2. 标准语法可以让模板更容易读写，原始语法具有强大的逻辑处理能力。  

> 标准语法： {{ 数据 }}
原始语法：<%=数据  %>


#### 4.2 输出
将某项数据输出在模板中，标准语法和原始语法如下：

> 标准语法：{{ 数据 }}
原始语法：<%=数据 %>

```
  <!-- 标准语法 -->
 <h2>{{value}}</h2>
 <h2>{{a ? b : c}}</h2>
 <h2>{{a + b}}</h2>

  <!-- 原始语法 -->
 <h2><%= value %></h2>
 <h2><%= a ? b : c %></h2>
 <h2><%= a + b %></h2>
```

#### 4.3 原文输出
如果数据中携带HTML标签，默认模板引擎不会解析标签，会将其转义后输出。
- 标准语法：{{@ 数据 }}
- 原始语法：<%-数据 %>
```javascript
 <!-- 标准语法 -->
 <h2>{{@ value }}</h2>
 <!-- 原始语法 -->
 <h2><%- value %></h2>
```

#### 4.4 条件判断
```javascript
 <!-- 标准语法 --> 
 {{if 条件}} ... {{/if}}
 {{if v1}} ... {{else if v2}} ... {{/if}}

 <!-- 原始语法 -->
 <% if (value) { %> 
    ... 
 <% } %>

 <% if (v1) { %>
    ...
 <% } else if (v2) { %>
    ...
 <% } %>
```

#### 4.5 循环语法
- 标准语法：{{each 数据}} {{/each}}
- 原始语法：<% for() { %> <% } %>
```javascript
 <!-- 标准语法 -->
 {{each target}}
     {{$index}} {{$value}}
 {{/each}}
  <!-- 原始语法 -->
 <% for(var i = 0; i < target.length; i++){ %>
     <%= i %> <%= target[i] %>
 <% } %>
```
#### 4.6 子模板
使用子模板可以将网站公共区块(头部、底部)抽离到单独的文件中。
- 标准语法：{{include '模板'}}
- 原始语法：<%include('模板') %>
```javascript
  <!-- 标准语法 -->
 {{include './header.art'}}
  <!-- 原始语法 -->
 <% include('./header.art') %>
```

#### 4.7 模板继承

使用模板继承可以将网站HTML骨架抽离到单独的文件中，其他页面模板可以继承骨架文件。

```html
//Html骨架模板  layout.art
 <!doctype html>
 <html>
     <head>
         <meta charset="utf-8">
         <title>HTML骨架模板</title>
         {{block 'head'}}{{/block}}
     </head>
     <body>
         {{block 'content'}}{{/block}}
     </body>
 </html>
```
```html
 <!--index.art 首页模板-->
 <!-- 继承骨架模板 -->
 {{extend './layout.art'}}
 {{block 'head'}} <link rel="stylesheet" href="custom.css"> {{/block}}
 {{block 'content'}} <p>This is just an awesome page.</p> {{/block}}
```

### 5 . 案例

#### 5.1 案例介绍 – 学生档案管理

目标：模板引擎应用，强化node.js项目制作流程。

知识点：http请求响应、数据库、模板引擎、静态资源访问。

<img src="https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200410163744.png" alt="image-20200410163741420" style="zoom: 67%;" />![image-20200410163752537](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200410163755.png)

#### 5.2 制作流程

1. 建立项目文件夹并生成项目描述文件
2.  创建网站服务器实现客户端和服务器端通信
3. 连接数据库并根据需求设计学员信息表
4. 创建路由并实现页面模板呈递
5. 实现静态资源访问
6. 实现学生信息添加功能
7. 实现学生信息展示功能

#### 5.3 第三方模块 router

功能：实现路由
使用步骤：

- 获取路由对象

- 调用路由对象提供的方法创建路由

- 启用路由，使路由生效

  ```js
  const getRouter = require('router')
  const router = getRouter();
  router.get('/add', (req, res) => {
      res.end('Hello World!')
  }) 
  server.on('request', (req, res) => {
      router(req, res)
  })
  
  ```

  


#### 5.4 第三方模块 serve-static

  功能：实现静态资源访问服务
  步骤：

  - 引入serve-static模块获取创建静态资源服务功能的方法
  - 调用方法创建静态资源服务并指定静态资源服务目录
  - 启用静态资源服务功能

```js
const serveStatic = require('serve-static')
const serve = serveStatic('public')
server.on('request', () => { 
    serve(req, res)
})
server.listen(3000)

```



#### 5.5 添加学生信息功能步骤分析

1. 在模板的表单中指定请求地址与请求方式
2. 为每一个表单项添加name属性
3. 添加实现学生信息功能路由
4. 接收客户端传递过来的学生信息
5. 将学生信息添加到数据库中
6. 将页面重定向到学生信息列表页面





#### 5.6 学生信息列表页面分析

1. 从数据库中将所有的学生信息查询出来
2. 通过模板引擎将学生信息和HTML模板进行拼接
3. 将拼接好的HTML模板响应给客户端