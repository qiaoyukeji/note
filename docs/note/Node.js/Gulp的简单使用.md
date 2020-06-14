<!--
 * @Descripttion: 
 * @version: 
 * @Author: qiaoyurensheng@163.com
 * @Date: 2020-06-15 00:29:52
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-06-15 00:29:53
--> 
## gulp工作原理

原理：
> 1.Gulp是基于Node.js中的数据流  
> 2.Gulp主要基于使用pipe事件输入及输出  
> 3.插件独立使用  

Gulp的优势
> 1.Gulp是基于代码进行配置  
> 2.Gulp的可读性更高  
> 3.Gulp基于数据流，所以可以操作 pipe() 事件
  
安装步骤
> 1.首先需要拥有 node 环境  
> 2.通过npm install -g gulp 安装全局  
> 3.初始化package.json  
> 4.在项目文件中安装gulp，npm install gulp --save-dev  

> 新建文件gulpfile.js(必须)，填入以下代码  
```javascript
//处理任务(初始化)

var gulp = require("gulp");

// 常用任务
//gulp.task -- 定义任务
//gulp.src-- 找到需要执行任务的文件
//gulp.dest -- 执行任务的文件的去处
//gulp.watch-- 观察文件是否发生变化


//定义任务
//task(任务名,回调函数)
gulp.task("message", function () {
    return console.log("Gulp is runing!");
})


//执行任务 gulp 任务名

//定义默认任务 仅使用gulp即可运行
gulp.task("default", function () {
    return console.log("这是默认任务！");
})
```
具体内容
> 1.拷贝文件  
> 2.压缩图片  
> 3.压缩JS代码  

- 拷贝文件
```javascript
gulp.task("copyHtml", function () {
    //pipe左边的文件输出到pipe的括号里的路径

    gulp.src("./src/*.html")
        //dist()找到具体的路径
        .pipe(gulp.dest('dist'));
});
```


- 图片压缩
```javascript
//安装对应压缩图片的模块 npm i gulp-imagemin
// var imagemin = require("gulp-imagemin");
gulp.task("imageMin", function () {
    // pipe左边的文件输出到pipe的括号里(的路径)
    gulp.src("./src/images/gulp.jpg")
        .pipe(imagemin())
        .pipe(gulp.dest("dist/images"));
});
```

- 压缩js文件
```javascript
//安装对应压缩js的模块 npm install uglify
// var uglify= require("gulp-uglify")
gulp.task("minify", function () {
    gulp.src("./src/js/file1.js")
        .pipe(uglify())
        .pipe(gulp.dest("dist/js"));
});
```
- sass转化为css
```javascript
//安装转化模块 npm install gulp-sass
// var sass = require("gulp-sass");
gulp.task("sass", function () {
    gulp.src("src/sass/style.scss")
        //on处理事件，这里处理error事件
        .pipe(sass()).on("error", sass.logError)
        .pipe(gulp.dest("dist/css"));
});
```

- 代码合并
```javascript
//安装相应合并模块 npm install gulp-concat
// var concat = require("gulp-concat");
gulp.task("scripts", function () {
    gulp.src("src/js/*.js")
        //concat:合并的方法，concat(合并后的名字)
        .pipe(concat("main.js"))
        //代码压缩
        .pipe(uglify())
        //代码输出
        .pipe(gulp.dest("dist/js"));
})
```


- 监听文件是否发生变化
```javascript
//监听文件是否发生变化
gulp.task("watch", function () {
    //gulp3 watch(监听的文件路径，调用的任务名)
    //gulp4 watch(监听的文件路径，回调函数)
    gulp.watch("src/js/*.js", function () {
        gulp.src("src/js/*.js")
            //concat:合并的方法，concat(合并后的名字)
            .pipe(concat("main.js"))
            //代码压缩
            .pipe(uglify())
            //代码输出
            .pipe(gulp.dest("dist/js"));
    });

    gulp.watch("src/iamges/*", function () {
        // pipe左边的文件输出n到pipe的括号里(的路径)
        gulp.src("./src/images/gulp.jpg")
            .pipe(imagemin())
            .pipe(gulp.dest("dist/images"));
    });

    gulp.watch("src/sass/*.scss", function () {
        gulp.src("src/sass/style.scss")
            //on处理事件，这里处理error事件
            .pipe(sass()).on("error", sass.logError)
            .pipe(gulp.dest("dist/css"));
    });

    gulp.watch("src/*.html", function () {
        //pipe左边的文件输出到pipe的括号里的路径

        gulp.src("./src/*.html")
            //dist()找到具体的路径
            .pipe(gulp.dest('dist'));
    });
});
```
- (默认)执行多个任务 
```javascript
//(默认)执行多个任务 
//gulp3
// gulp.task("default", ["message", "copyHtml", "imageMin", "sass", "minify"]);
//gulp4
gulp.task('default', gulp.series(gulp.parallel("message", "copyHtml", "sass", "imageMin", "scripts")));
```