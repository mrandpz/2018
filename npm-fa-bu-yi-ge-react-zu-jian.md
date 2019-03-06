1：npm init 生成一个package.json

```
{
  "name": "babaloveyou",  #发布到npm仓库的包名 供别人下载 npm i babaloveyou
  "version": "1.0.0",     #版本号，每次 npm publish 的时候必须修改
  "description": "",
  "main": "./dist/bunlde.js", #别人引用的入口
  "scripts": {
    "build": "webpack"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/core": "^7.0.0",
    "@babel/preset-env": "^7.0.0",
    "@babel/preset-react": "^7.0.0",
    "babel-loader": "^8.0.2",
    "css-loader": "^1.0.0",
    "style-loader": "^0.23.0",
    "webpack": "^4.17.2",
    "webpack-cli": "^3.1.0"
  },
  "dependencies": {
    "antd": "^3.9.1",
    "react": "^16.4.2",
    "react-dom": "^16.4.2"
  }
}
```

2：安装本地依赖包

```
cnpm i webpack webpack-cli @babel/core @babel/preset-env @babel/preset-react babel-loader css-loader style-loader -D
```

3：安装依赖包

```
cnpm i react-dom react-dom antd -S
```

4：创建.babelrc 文件，版本8.0.2 最好根据官网配置 [https://babeljs.io/docs/en/babel-preset-react](https://babeljs.io/docs/en/babel-preset-react "babel官方文档")

```
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

5：创建webpack.config.js

```
const path = require('path');

module.exports = {
  mode: 'development',  // 开发环境
  entry: './src/index.js',   // 打包的入口文件
  output: {
    filename: 'index.js',  // 打包后的文件名
    path: path.resolve(__dirname, 'dist'),
    libraryTarget: 'umd' // 打包后的文件兼容 common.js 和 cmd
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

6：创建src文件夹，在src文件夹下创建index.js 文件

```
import Hello from './Hello';

export default Hello;
```

如果有多个组件文件

```
import React from 'react';
import RCmp from './app';
import Button from './button';
import Photo from './photo';
import './app.scss';
RCmp.Button = Button;
RCmp.Photo = Photo;
export default RCmp;
export {
  Button,
  Photo,
  RCmp,
}
```

7：hello.js

```
import React, { Component } from 'react';
import PropTypes from 'prop-types';

import './Hello.css';

class Hello extends Component {
  render () {
    return (
      <h3>Hello</h3>
    );
  }
}


export default Hello;
```

8：执行npm run build 生成 bundle.js文件

9：因为npm link执行会有莫名其妙的报错忽略

然后在对应项目执行 npm link  babaloveyou

或者可以选择用 yarn link

成功提示

    yarn link v1.5.1
    success Registered "babaloveyou".
    info You can now run `yarn link "babaloveyou"` in the projects where you want to use this module and it will be used instead.
    Done in 0.14s.

10：用 creat-react-app创建一个测试项目，yarn start。执行yarn link "babaloveyou"  即可链接到该模块，即可像正常方式引入改模块，调试完成之后publish

# part2

因为我们在特定的环境下处理代码，不可能把所有的包都打包进去，比如react.js 就不应该被打包进去

加上webpack的externals参数

```
externals: {
    'react': 'React',
    'React': 'React',
    'ReactDOM': 'ReactDOM',
    'react-dom': 'ReactDOM',
    'antd': 'antd',
},
```



