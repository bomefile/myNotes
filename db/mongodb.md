
https://www.cnblogs.com/weixuqin/p/7258000.html

````
brew search mongodb
````
查看更低版本的MongoDB，然后安装更低版本的MongoDB。
````
brew install mongodb@3.4
````
启动MongoDB服务：
````
brew services start mongodb@3.4
````
关闭MongoDB服务：

````
brew services stop mongodb@3.4
````
进入MongoDB图形化界面：

````
mongo
````
查看homebrew安装的服务情况：

brew services list