/*********************************************************************************/

cat [log] | grep [search] | tail -n 10

ps -ef|grep tomcat

/*******************************************************************************/


解压 tar.gz  

tar -zxvf 文件名


后台执行命令 ：

命令后加 &




查看系统位数：getconf LONG_BIT


jdk卸载

yum -y remove java-*

jkd安装
yum -y install java-1.8.0-openjdk-devel


Q:bash: ./java: /lib/ld-linux.so.2: bad ELF interpreter: 没有那个文件或目录”的问题“，
A:sudo yum install glibc.i686


linux下cp整个文件夹的文件到另一个文件夹
cp -R /home/usera/. /mnt/temp

############################################################
镜像网址
http://mirrors.163.com/
http://mirrors.sohu.com/ 
############################################################
Linux系统下配置yum，nc，telnet
http://www.xmyy.com/plus/view.php?aid=289713

echo "this is test"

shell 脚本
#!/bin/bash

添加执行权限
chmod u+x file

cron 定期脚本


