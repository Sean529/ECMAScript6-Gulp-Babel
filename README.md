# ECMAScript6-Gulp-Babel
学习ECMAScript6，使用Gulp自动化构建工具执行Babel预编译。

## 目录结构

```
┌ ES6               // 开发目录
├── dist
│ └── index.js      // 编译后文件
├── node_modules    // 依赖
├── src
│ └── es6.js        // ES6语法
├── gulpfile.js     // Gulp主文件
├── index.html      // 入口文件 
└── package.json    // 项目依赖
```

## 安装依赖

``` bash
# 初始化创建 package
npm init -y

# 第一次需要全局安装 gulp
npm install -g gulp

# 安装 gulp
npm install --save-dev gulp

# 安装 gulp-babel
npm --save-dev gulp-babel

# 安装 gulp-load-plugins
npm --save-dev gulp-load-plugins

# 安装 babel-cli babel-preset-es2015
npm install --save-dev babel-cli babel-preset-es2015

# 安装 browser-sync 浏览器同步
npm install --save-dev browser-sync
```

## 配置

1. 创建 src 文件夹 
2. 创建 index.js 文件 （ES6）
3. 创建 index.html 文件 引入 index.js （编译后的js）
```
<script src = "dist/index.js"></script>
```
4. 创建 gulpfile.js文件
```
var gulp = require('gulp')

// lodin plugins
var $ = require('gulp-load-plugins')()

// 浏览器同步
var browserSync = require('browser-sync').create()

// ES6
gulp.task('es6', function () {
    return gulp.src('src/*.js')
        .pipe($.babel({
            presets: ['es2015']
        }))
        .pipe(gulp.dest('dist/')) // 编译ES6
        .pipe(browserSync.stream())
})

// 监控文件修改
gulp.task('serve', ['es6'], function () {
    browserSync.init({
        server: './'
    })
    gulp.watch(['src/index.js'], ['es6'] // 执行es6
    gulp.watch("*.html").on('change', browserSync.reload) // 会在编译完es6后，更新页面
})

gulp.task('default', ['serve']) // 定义默认任务
```

## 启动

``` bash
# dist 目录中生成编译后的js文件
gulp
```

## 预览

![Image text](https://raw.githubusercontent.com/XieShangZheng/img-folder/master/clipboard.png)
