版本1：案例github地址 [https://github.com/mrandpz/reactWithWebpack](https://github.com/mrandpz/reactWithWebpack)

安装所需的依赖包

1.

```
//devDependencies
babel-core
```

babel-core 的作用是把 js 代码分析成 ast ，方便各个插件分析语法进行相应的处理。有些新语法在低版本 js 中是不存在的，如箭头函数，rest 参数，函数默认值等，这种语言层面的不兼容只能通过将代码转为 ast，分析其语法后再转为低版本 js。

2.

`babel-loader`

很少有大型项目仅仅需要 babel，一般都是 babel 配合着 webpack 或 glup 等编译工具一起上的。

```
module: {
  loaders: [{
    loader: 'babel',
    test: /\.jsx?$/,
    include: path.join(__dirname, 'src'),
    query: {
      plugins: ['transform-runtime'],
      presets: [
        ["env", {
          "targets": {
            "chrome": 52
          },
          "modules": false,
          "loose": true
        }],
        'stage-2',
        'react'
      ],
    }
  }]
}
```

需要注意的是，`babel-runtime`虽然没有出现在配置里，但仍然需要安装，因为`transform-runtime`依赖它。

3.`babel-preset-latest`

latest是一个特殊的presets，包括了es2015，es2016，es2017的插件（目前为止，以后有es2018也会包括进去）。即总是包含最新的编译插件。

4.babel-preset-react  编译react

5.babel-preset-stage-n

以下是4 个不同阶段的（打包的）预设：

* `babel-preset-stage-0`

* `babel-preset-stage-1`

* `babel-preset-stage-2`

* `babel-preset-stage-3`

以上每种预设都依赖于紧随的后期阶段预设，数字越小，阶段越靠后，存在依赖关系。也就是说stage-0是包括stage-1的，以此类推。也就是说这些stage包含的特性是比latest更新的特性但还未被写入标准进行发布。

6.babel-plugin-transform-runtime

Babel 几乎可以编译所有时新的 JavaScript 语法，但对于 APIs 来说却并非如此。例如： Promise、Set、Map 等新增对象，Object.assign、Object.entries等静态方法。

为了达成使用这些新API的目的，社区又有2个实现流派：babel-polyfill和babel-runtime+babel-plugin-transform-runtime。

但 babel-runtime 也有问题，第一，很不方便，第二，在代码中中直接引入 helper 函数，意味着不能共享，造成最终打包出来的文件里有很多重复的 helper 代码。所以，babel 又开发了 babel-plugin-transform-runtime，这个模块会将我们的代码重写，如将 Promise 重写成 \_Promise（只是打比方），然后引入\_Promise helper 函数。这样就避免了重复打包代码和手动引入模块的痛苦。

7.babel-plugin-transform-decorators-legacy 装饰器修饰类

8.`babel-runtime`

那什么时候用`babel-polyfill`什么时候用`babel-runtime`呢？如果你不介意污染全局变量（如上面提到的业务代码），放心大胆地用`babel-polyfill`；而如果你在写模块，为了避免污染使用者的环境，没的选，只能用`babel-runtime`+`babel-plugin-transform-runtime`。

9 css-loader

10.

```
file-loader
less-loader
style-loader
url-loader
webpack
webpack-dev-middleware
webpack-hot-middleware
less
koa
koa-router
```

11.

```
//dependencies
prop-types  // react 校验
react
react-dom
```

12. 写完依赖后，试着启动一个服务

```
│  .babelrc                      //babel配置文件
│  package.json
│  README.md
│
├─server                         //存放服务端代码文件
│  │  server.js                  //开启http服务
│  │
│  └─middleware
│          devMiddleware.js      //koa中间件，可以让webpack-dev-middleware配合koa使用
│          hotMiddleware.js      
│
├─src                            //存放前端业务代码文件
│  │  index.js                   //前端页面入口文件
│  │
│  ├─assets                      //前端静态资源目录
│  │      index.html             
│  │
│  └─components                  //存放你的react组件
│          App.js
│          app.less
│
└─webpack                       //存放webpack配置文件
        webpack.config.js
```

13.新建 .babelrc 文件

```
{
	"presets":[
		[
			"laster",
			{
				modules:false
			}
		],
		"stage-0",
		"react"
	],
	"plugins":[
		"transform-time",
		"transform-decorators-legacy"
	]
}
```

14.建立一个server 文件夹，并且建立一个server.js 文件

