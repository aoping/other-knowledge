## 任务自动化

### gulp
### grunt


## 编译工具
### babel
### webpack webpack-stream



## i18n
有两种方案：
1.动态加载(vue-i18n)， 缺点需要把框架打包进去，优点可以动态切换，且只生成一份代码
2.静态直出(webpack i18n插件可以生成不同语言版本的js)，缺点生成多份代码，优点没有框架，代码精简



## webpack
### 构建速度
    devtool
    module.noParse
    resolve.modules

### 生成分析报告
http://webpack.github.io/analyse
```
webpack --profile --json > stats.json
```