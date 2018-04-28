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
* 四个核心概念： 1 入口\(entry\) 2输出\(output\) 3 loader 4 插件\(plugins\)

1.entry 的最可扩展配置   插件`CommonsChunkPlugin`

```
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
```

二、开始建立webpack

* 建立一个 文件名 webpack.config.js

```
var webpack = require('webpack')
module.exports = {
    mode: 'production',  // 环境变量
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
    watch:true, // 监控文件变化
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

```
const ExtractTextPlugin = require("extract-text-webpack-plugin");
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: "style-loader",
          use: "css-loader"
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin("styles.css"),
  ]
}
use:指需要什么样的loader去编译文件,这里由于源文件是.css所以选择css-loader
fallback:编译后用什么loader来提取css文件
publicfile:用来覆盖项目路径,生成该css文件的文件路径


改变css输出路径
var extractCSS = new ExtractTextPlugin('../css/[name].css')
{
        test: /\.css$/,
        use: extractCSS.extract({
          fallback: "style-loader",
          use: "css-loader"
        })
      }
      plugins: [
    new extractCSS ("styles.css"),
  ]
```

* `test`  
  属性，用于标识出应该被对应的 loader 进行转换的某个或某些文件

  `use`  
  属性，表示进行转换时，应该使用哪个 loader。

* watch:true 对编辑代码进行监听刷新

* html-webpack-plugin  生成html文件，有设置标题，类似ejs语法等参数

```
{
  entry: 'index.js',
  output: {
    path: __dirname + '/dist',
    filename: 'index_bundle.js'
  },
  plugins: [
    new HtmlWebpackPlugin(), // Generates default index.html
    new HtmlWebpackPlugin({  // Also generate a test.html
      filename: 'test.html',
      template: 'src/assets/test.html'
    })
  ]
}
```

* js压缩  uglifyjs-webpack-plugin 参数很多[https://www.npmjs.com/package/uglifyjs-webpack-plugin](https://www.npmjs.com/package/uglifyjs-webpack-plugin)

```
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')

module.exports = {
  plugins: [
    new UglifyJsPlugin({
      配置参数
    })
  ]
}

new webpack.optimize.UglifyJsPlugin({
  配置参数
})
```

* 公共js处理 类似于jquery等,加入这个处理后就能够

```
entry中引入jquery
entry:{
    app:'普通js',
    v:[jquery] //表示从依赖包中加载
}
在plugin中
plugins:[
    new webpack.ProvidePlugin({
        $:'jquery'  
    })
    new webpack.optimize.commonsChunkPlugin('v':'lib/jquery.min.js')
]

// 引用cdn方式

extrenals:{
    jquery:;'cdn' 
}
```

* 有很多入口的时候 output 参数要注意

```
entry:{
    app:'普通js',
    more:[__dirname+'路径/a.js','路径/b.js'],
    v:[jquery] //表示从依赖包中加载
}
output:{
    filename:'js/[name].js'
},
在plugin中
plugins:[
    new webpack.ProvidePlugin({
        $:'jquery'  
    })
    new webpack.optimize.commonsChunkPlugin({
        names:['a','b']
    })
]
```

* 图片怎么打包 url-loader file-loader

```
module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192
            }

          }
        ]
        //另一种参数写法
        use: 'url-loader?limit=1024&name=[path][name].[ext]&outputPath=img/&publicPath=output/', 
      }
    ]
  }
```

name表示输出的文件名规则，如果不添加这个参数，输出的就是默认值：文件哈希。加上\[path\]表示输出文件的相对路径与当前文件相对路径相同，加上\[name\].\[ext\]则表示输出文件的名字和扩展名与当前相同。加上\[path\]这个参数后，打包后文件中引用文件的路径也会加上这个相对路径。

utputPath表示输出文件路径前缀。图片经过url-loader打包都会打包到指定的输出文件夹下。但是我们可以指定图片在输出文件夹下的路径。比如outputPath=img/，图片被打包时，就会在输出文件夹下新建（如果没有）一个名为img的文件夹，把图片放到里面。

publicPath表示打包文件中引用文件的路径前缀，如果你的图片存放在CDN上，那么你上线时可以加上这个参数，值为CDN地址，这样就可以让项目上线后的资源引用路径指向CDN了。

* resolve
* ```
  resolve:{
      root:'d:/js/' // cdn路径也可以
      extensions:['','js'],
      alias:{
          appAdd:'add.js' // 别名
      }
  }
  ```

* html里面的img也需要进行处理，file-loader没处理到

```
{
  test: /\.html$/,
  loader: "html-loader"
}
```



