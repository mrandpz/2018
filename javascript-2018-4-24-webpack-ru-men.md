1.browser-sync 省时同步的调试工具 -- [http://www.browsersync.cn/](http://www.browsersync.cn/)

2.

* commonjs  nodejs 
* amd  require.js
* cmd seajs

3.Browserify  可以让你使用类似于 node 的 require\(\) 的方式来组织浏览器端的 Javascript 代码，通过预编译

让前端 Javascript 可以直接使用 Node NPM 安装的一些库

4.打包less  lessc 文件目录  打包成.css

lessc index.less index.css

lessc index.less index.css --clean-css="advanced" 压缩

```
@import 某某文件
@import 某某文件
@import 某某文件
```

5.压缩js m就是把变量各种简单字母， o则是压缩

```
uglifyjs index.js -m(混淆) -o(压缩) index.min.js
```

6.tinify 压缩图片，其实就是tinypng 官网注册一个账号使用命令,转换成base64，这些都可以用nodejs写成批量处理

一、认识webpack

* 全局化安装webpack  npm install webpack -g
* npm init -y
* cnpm install --save-dev webpack  安装本地webpack依赖
* 简单输出 webpack 某个文件 输出到某个文件

二、开始建立webpack

* 建立一个 文件名 webpack.config.js

```
var webpack = require('webpack')
module.exports = {
    entry: __dirname + '/src/js/index.js',  // 进口文件
    output:{
        path:__dirname + '/assets/js', // 输出文件
        filename: 'index.js',
        publicPath:'/temp/'   // 内存空间
    },
    devServer:{
        contentBase:'./',
        host:'localhost', //自己的ip地址
        port:'3333',
        color:true
    },
    module:{
        loaders:[
            {
                test:/\.css$/,
                loader:'style-loader!css-loader',
                include: '需要处理的文件',
                exclude: '忽略的文件'
            },
            {
                test:'/\.json$/',
                loader:'json'
            },
            {
                test:/\.js$/,
                exclude:/node_modules/,
                loader:'babel',
                query:{
                    presets:['es2015','react']
                }
            }
        ]
    },
    plugins:[
        new webpack.HotModuleReplacementPlugin()
    ]
}

输入命令：webpack
```

* npm install webpack-dev-server --save-dev   安装本地服务
* npm install jquery --save  安装依赖库

* 执行命令  webpack-dev-server  启动本地服务

* 1、webpack-dev-server ---iFrame  2、webpack-dev-server ---inline 全部  3、webpack-dev-server ---inline --hot 局部刷新，有加hot的话要声明一个插件 new webpack.HotModuleReplacementPlugin\(\)  正常cli都会有自己的热插拔插件

* 加 less-loader  cnpm install less-loader less --save  需要加的loader可以去github看

* 加json babel

* npm start  改成 webpack-dev-server ---inline --hot

* npm install --save-dev babel-core babel-loader babel-preset-es2015 babel-preset-react

* css 分离 安装  extract-text-webpack-plugin  引入



