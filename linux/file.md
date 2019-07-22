# 文件内容查阅

## cat
````
[root@www ~]# cat [-AbEnTv]
选项与参数：
-A  ：相当於 -vET 的整合选项，可列出一些特殊字符而不是空白而已；
-b  ：列出行号，仅针对非空白行做行号显示，空白行不标行号！
-E  ：将结尾的断行字节 $ 显示出来；
-n  ：列印出行号，连同空白行也会有行号，与 -b 的选项不同；
-T  ：将 [tab] 按键以 ^I 显示出来；
-v  ：列出一些看不出来的特殊字符

范例一：检阅 /etc/issue 这个文件的内容
[root@www ~]# cat /etc/issue
CentOS release 5.3 (Final)
Kernel \r on an \m

范例二：承上题，如果还要加印行号呢？
[root@www ~]# cat -n /etc/issue
     1  CentOS release 5.3 (Final)
     2  Kernel \r on an \m
     3
# 看到了吧！可以印出行号呢！这对於大文件要找某个特定的行时，有点用处！
# 如果不想要编排空白行的行号，可以使用『cat -b /etc/issue』，自己测试看看：

范例三：将 /etc/xinetd.conf 的内容完整的显示出来(包含特殊字节)
[root@www ~]# cat -A /etc/xinetd.conf
#$
....(中间省略)....
$
defaults$
{$
# The next two items are intended to be a quick access place to$
....(中间省略)....
^Ilog_type^I= SYSLOG daemon info $
^Ilog_on_failure^I= HOST$
^Ilog_on_success^I= PID HOST DURATION EXIT$
....(中间省略)....
includedir /etc/xinetd.d$
 $
# 上面的结果限於篇幅，鸟哥删除掉很多数据了。另外，输出的结果并不会有特殊字体，
# 鸟哥上面的特殊字体是要让您发现差异点在哪里就是了。基本上，在一般的环境中，
# 使用 [tab] 与空白键的效果差不多，都是一堆空白啊！我们无法知道两者的差别。
# 此时使用 cat -A 就能够发现那些空白的地方是啥鬼东西了！[tab]会以 ^I 表示，
# 断行字节则是以 $ 表示，所以你可以发现每一行后面都是 $ 啊！不过断行字节
# 在Windows/Linux则不太相同，Windows的断行字节是 ^M$ 罗。
# 这部分我们会在第十章 vim 软件的介绍时，再次的说明到喔！
````

## more

more (一页一页翻动)
````
[root@www ~]# more /etc/man.config
#
# Generated automatically from man.conf.in by the
# configure script.
#
# man.conf from man-1.6d
....(中间省略)....
--More--(28%)  <== 重点在这一行喔！你的光标也会在这里等待你的命令
仔细的给他看到上面的范例，如果 more 后面接的文件内容行数大於萤幕输出的行数时， 就会出现类似上面的图示。重点在最后一行，最后一行会显示出目前显示的百分比， 而且还可以在最后一行输入一些有用的命令喔！在 more 这个程序的运行过程中，你有几个按键可以按的：

空白键 (space)：代表向下翻一页；
Enter         ：代表向下翻『一行』；
/字串         ：代表在这个显示的内容当中，向下搜寻『字串』这个关键字；
:f            ：立刻显示出档名以及目前显示的行数；
q             ：代表立刻离开 more ，不再显示该文件内容。
b 或 [ctrl]-b ：代表往回翻页，不过这动作只对文件有用，对管线无用
````

## less (一页一页翻动)
````
[root@www ~]# less /etc/man.config
#
# Generated automatically from man.conf.in by the
# configure script.
#
# man.conf from man-1.6d
....(中间省略)....
:   <== 这里可以等待你输入命
````

````
空白键    ：向下翻动一页；
[pagedown]：向下翻动一页；
[pageup]  ：向上翻动一页；
/字串     ：向下搜寻『字串』的功能；
?字串     ：向上搜寻『字串』的功能；
n         ：重复前一个搜寻 (与 / 或 ? 有关！)
N         ：反向的重复前一个搜寻 (与 / 或 ? 有关！)
q         ：离开 less 这个程序；
````

