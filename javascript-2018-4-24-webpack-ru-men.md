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

7.

