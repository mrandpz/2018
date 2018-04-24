npm =&gt; Node Package Manager 包管理工具  账号xiaomengzhi1992

核心项目的核心代码整成npm包

切换nodejs的版本 nvm

npm install xxx 安装

npm unstall xxx 卸载

1.如何发布自己的一个包

* npm adduser 注册账号\(已注册忽略\)
* npm login 登陆
* npm whoami  检查是否登陆
* 建立package，npm init 输入包名，也就是发布上去别人要下载的包名等一些东西
* 写下index.js 
* npm publish 发布 =》 此时需要点开注册的邮箱去做校验，才能发布，如果你以后修改了代码，然后想要同步到 npm 上的话请修改 package.json 中的 version 然后再次 publish，更新的版本上传的版本要大于上次
* nrm 切换npm源的工具 nrm ls 显示出所有的源 nvm use切换源
* 想撤销发布的包，npm unpublish 包名 --force
* 发布版本  npm version 0.1.2  patch代表补丁2   minor代表小修小改1  major代表大版本0，最后publish发布到远端，查看远端版本npm view xiaomengzhi1992 versions
* npm update xiaomengzhi --save 更新模块
* 清楚缓存  npm cache clean --force
* 更新模块 npm install xiaomengzhi1992 --save
* 


