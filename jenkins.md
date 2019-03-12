1：安装虚拟机 完整教程

https://www.cnblogs.com/shuoer/p/9471839.html，里面不需要安装Tomcat，其他都有步骤

2：安装镜像，我选择的是有图形界面的Ubuntu，直接去官网找镜像文件，傻瓜式安装

3：Jenkins需要安装java环境，找到一个友好的教程  https://blog.csdn.net/williamyi96/article/details/78268595

4：查看密码 cat /var/lib/jenkins/secrets/initialAdminPassword

5： 修改端口号  sudo vim /etc/default/jenkins 

xiaomengzhi whoami

6: 主机访问虚拟机的Jenkins： ifconfig查找ip。主机访问即可

7：线上的项目也要开始玩了

