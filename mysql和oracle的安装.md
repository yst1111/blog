## Mysql

进入mysql官网

![image-20220619111835911](mysql和oracle的安装.assets/image-20220619111835911.png)

选择Downloads

![image-20220619111938569](mysql和oracle的安装.assets/image-20220619111938569.png)

选择社区版

![image-20220619112839819](mysql和oracle的安装.assets/image-20220619112839819.png)

选择windows版

![image-20220619112919219](mysql和oracle的安装.assets/image-20220619112919219.png)

选择版本下载

![image-20220619112958810](mysql和oracle的安装.assets/image-20220619112958810.png)

解压，然后运行这个![image-20220619113150425](mysql和oracle的安装.assets/image-20220619113150425.png)

得到下载界面

Mysql Workbench是操作界面，可以不选，直接使用Navicat

![image-20220619113413881](mysql和oracle的安装.assets/image-20220619113413881.png)



下载完成之后

可以在下载界面查看下载位置，因为这个位置有可能下载C盘的用户下面，难以寻找

![image-20220619113839709](mysql和oracle的安装.assets/image-20220619113839709.png)

给bin目录加环境变量

![image-20220619114029917](mysql和oracle的安装.assets/image-20220619114029917.png)

可以黑窗测试

mysql -h localhost -uroot -p

![image-20220619114148556](mysql和oracle的安装.assets/image-20220619114148556.png)

说明服务已经启动

可以去看一下，设置一下自启动，以后每次开机都**自启动**

![image-20220619114413883](mysql和oracle的安装.assets/image-20220619114413883.png)

打开Mysql Workbench，测试一下

![image-20220619114520435](mysql和oracle的安装.assets/image-20220619114520435.png)



![image-20220619114607851](mysql和oracle的安装.assets/image-20220619114607851.png)



## Oracle

oracle一般不建议安装在windows上，因为耗资源

安装oracle一般3个部分，databases，client客户端，plsql操作页面

![image-20220619114908785](mysql和oracle的安装.assets/image-20220619114908785.png)

这个product文件夹里存着连接信息

![image-20220619115055535](mysql和oracle的安装.assets/image-20220619115055535.png)

可以和Idea进行对照

![image-20220619115159932](mysql和oracle的安装.assets/image-20220619115159932.png)

![image-20220619115553144](mysql和oracle的安装.assets/image-20220619115553144.png)

![image-20220619115758496](mysql和oracle的安装.assets/image-20220619115758496.png)

![image-20220619115829447](mysql和oracle的安装.assets/image-20220619115829447.png)

![image-20220619115913454](mysql和oracle的安装.assets/image-20220619115913454.png)



PLSQL有时抽风

idea能连，但plsql连不上

win + R 调出界面 cmd

采用 ctrl + shift + 回车 （以管理员身份） 连接oracle ：sqlplus system/system

![image-20220619125522260](mysql和oracle的安装.assets/image-20220619125522260.png)



用户名输入：system 密码输入 root

再连plsql，可以了