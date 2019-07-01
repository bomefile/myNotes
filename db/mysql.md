
macOS brew 安装mysql

- 卸载
````
brew remove mysql
````

- 清除

````
brew cleanup
````

- 删除data文件

````
rm -rf /usr/local/var/mysql/
````
- 安装最新版本
````
brew install mysql

````
- 初始化

````
/usr/local/Cellar/mysql/8.0.16/bin/mysql_secure_installation
````
