# 第七章、Linux 文件与目录管理

## 命令档名的搜寻
- which (寻找『运行档』)
````
[root@www ~]# which [-a] command
选项或参数：
-a ：将所有由 PATH 目录中可以找到的命令均列出，而不止第一个被找到的命令名称

范例一：分别用root与一般帐号搜寻 ifconfig 这个命令的完整档名
[root@www ~]# which ifconfig
/sbin/ifconfig            <==用 root 可以找到正确的运行档名喔！
[root@www ~]# su - vbird <==切换身份成为 vbird 去！
[vbird@www ~]$ which ifconfig
/usr/bin/which: no ifconfig in (/usr/kerberos/bin:/usr/local/bin:/bin:/usr/bin
:/home/vbird/bin)         <==见鬼了！竟然一般身份帐号找不到！
# 因为 which 是根据使用者所配置的 PATH 变量内的目录去搜寻可运行档的！所以，
# 不同的 PATH 配置内容所找到的命令当然不一样啦！因为 /sbin 不在 vbird 的 
# PATH 中，找不到也是理所当然的啊！了乎？
[vbird@www ~]$ exit      <==记得将身份切换回原本的 root

范例二：用 which 去找出 which 的档名为何？
[root@www ~]# which which
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot '
        /usr/bin/which
# 竟然会有两个 which ，其中一个是 alias 这玩意儿呢！那是啥？
# 那就是所谓的『命令别名』，意思是输入 which 会等於后面接的那串命令啦！
# 更多的数据我们会在 bash 章节中再来谈的！

范例三：请找出 cd 这个命令的完整档名
[root@www ~]# which cd
/usr/bin/which: no cd in (/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin
:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin)
# 瞎密？怎么可能没有 cd ，我明明就能够用 root 运行 cd 的啊！
````

## 文件档名的搜寻

- whereis (寻找特定文件)

````
[root@www ~]# whereis [-bmsu] 文件或目录名
选项与参数：
-b    :只找 binary 格式的文件
-m    :只找在说明档 manual 路径下的文件
-s    :只找 source 来源文件
-u    :搜寻不在上述三个项目当中的其他特殊文件

范例一：请用不同的身份找出 ifconfig 这个档名
[root@www ~]# whereis ifconfig 
ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz
[root@www ~]# su - vbird        <==切换身份成为 vbird
[vbird@www ~]$ whereis ifconfig <==找到同样的结果喔！
ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz
[vbird@www ~]$ exit              <==回归身份成为 root 去！
# 注意看，明明 which 一般使用者找不到的 ifconfig 却可以让 whereis 找到！
# 这是因为系统真的有 ifconfig 这个『文件』，但是使用者的 PATH 并没有加入 /sbin
# 所以，未来你找不到某些命令时，先用文件搜寻命令找找看再说！

范例二：只找出跟 passwd 有关的『说明文件』档名(man page)
[root@www ~]# whereis -m passwd
passwd: /usr/share/man/man1/passwd.1.gz /usr/share/man/man5/passwd.5.gz
````

- locate
````
[root@www ~]# locate [-ir] keyword
选项与参数：
-i  ：忽略大小写的差异；
-r  ：后面可接正规表示法的显示方式

范例一：找出系统中所有与 passwd 相关的档名
[root@www ~]# locate passwd
/etc/passwd
/etc/passwd-
/etc/news/passwd.nntp
/etc/pam.d/passwd
````

- find
````
[root@www ~]# find [PATH] [option] [action]
选项与参数：
1. 与时间有关的选项：共有 -atime, -ctime 与 -mtime ，以 -mtime 说明
   -mtime  n ：n 为数字，意义为在 n 天之前的『一天之内』被更动过内容的文件；
   -mtime +n ：列出在 n 天之前(不含 n 天本身)被更动过内容的文件档名；
   -mtime -n ：列出在 n 天之内(含 n 天本身)被更动过内容的文件档名。
   -newer file ：file 为一个存在的文件，列出比 file 还要新的文件档名

范例一：将过去系统上面 24 小时内有更动过内容 (mtime) 的文件列出
[root@www ~]# find / -mtime 0
# 那个 0 是重点！0 代表目前的时间，所以，从现在开始到 24 小时前，
# 有变动过内容的文件都会被列出来！那如果是三天前的 24 小时内？
# find / -mtime 3 有变动过的文件都被列出的意思！

范例二：寻找 /etc 底下的文件，如果文件日期比 /etc/passwd 新就列出
[root@www ~]# find /etc -newer /etc/passwd
# -newer 用在分辨两个文件之间的新旧关系是很有用的！
````

# 第八章、Linux磁盘与文件系统管理

- FAT
- NTFS

索引式文件系统(indexed allocation)

![索引式文件系统](http://cn.linux.vbird.org/linux_basic/0230filesystem_files/filesystem-1.jpg)

![FAT文件系统](http://cn.linux.vbird.org/linux_basic/0230filesystem_files/filesystem-2.jpg)

