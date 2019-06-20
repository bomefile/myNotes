brew update

brew search [software]

brew安装软件后，

1，配置文件在/usr/local/etc中

2，安装文件在/usr/local/Cellar中

3，二进制可执行程序的软连接在/usr/local/bin中

## idea 文件无法创建问题
````
ERROR in ch.qos.logback.core.rolling.RollingFileAppender[FILE] - Failed to create parent directories for [/opt/logs/100003171/apollo-configservice.log]

原因：

权限不够，启动时无法创建存放日志的文件夹。

解决方法：

root权限下手动创建文件并赋权

[root@app204 100003171]# touch apollo-configservice.log

[root@app204 100003171]# chmod 777 apollo-configservice.log

````

# root权限切换

````
sudo su
````
> 然后输入密码，用户名显示sh-3.2#,这里的#代表的含义就是具有root权限 
这时，再输入
````
su -
````
就可以进入root用户

> 那接下来，如果我们要切换至普通用户该怎么做？
````
su - 用户名
````
(-和用户名之间有空格)

# mac root用户方式打开应用

打开终端，输入命令：
````
sudo open -a AppName
```` 
应用的名字可以在输入 sudo open -a 后，在访达里把应用图标拖过去就有了路径名称