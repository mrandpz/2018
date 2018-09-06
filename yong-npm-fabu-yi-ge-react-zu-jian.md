基础知识：npm yarn webpack

封装组件的前提：尽量不包括业务逻辑，如必要，则尽量少。不然会变得难以维护

编辑器：vscode

首先，选择一个目录 mkdir babaloveyou;

进入到目录：cd babaloveyou



```
npm init #创建package.json得到
{
  "name": "babaloveyou",    #这个组件的名称，也就是到时候发布到npm仓库的时候提供给别人npm i babalove
  "version": "1.0.0",       #发布到npm仓库的版本号，初始版本1.0.0，每次npm publish 的时候版本号都必须改变
  "description": "",        #对这个npm包的描述
  "main": "index.js",       #别人引用这个包的入口位置，一般修改为 ./lib/index.js 或者 ./dist/index.js 具体看webpack打包后主入口的位置
  "scripts": {
    "build": "webpack"
  },
  "author": "",
  "license": "ISC"
}

```

安装本地依赖包

```
cnpm i webpack webpack-cli @babel/core @babel/preset-env @babel/preset-react babel-loader css-loader style-loader -D
```

安装依赖包

```
cnpm i react react-dom antd -S
```

配置 .babel  因为版本更新，所以最好还是去官网看文档配置 [https://babeljs.io/docs/en/babel-preset-react](https://babeljs.io/docs/en/babel-preset-react)

```
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

配置webpack.config.js  

```
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
    libraryTarget: 'umd'   // 兼容common.js 和 cmd模式
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: 'babel-loader',
        exclude: /node_modules/
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      }
    ]
  },
};
```



