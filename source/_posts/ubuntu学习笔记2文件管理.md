---

title: ubuntu常用命令
date: 2020-09-16 14:42:17
categories: 
- linux
- ubuntu
- 文件管理
---




# 一、 文件管理

虚拟终端：try1-tty7  ctrl+alt+f1 f2

## 1.1 常见文件格式扩展名

Linux 中一个文件是否能被执行，和后缀名没有太大的关系，主要和文件的属性有关。了解Linux 文件的后缀名还是有必要的，特别是自己创建一些文件，最好加后缀名，这样做的目的是为了应用方便。使用file 命令查看该文件的类型。
```
au：音频文件
gif：GIF 图像文件
html/.htm：HTML 文件
jpg：JPEG 图像文件
pdf：PDF 文档
png：PNG 图像文件
txt：纯ASCII 文本文件
wav：音频文件
XPm：图像文件
conf：配置文件，有时也使用.cfg
lock：锁文件，用来判定程序或设备是否正在被使用

c：C 程序语言的源码文件
cpp：C++ 程序语言的源码文件
h：C 或C++ 程序语言的头文件
o：程序的对象文件
pl：Perl 脚本
py：Python 脚本
so：库文件
sh：Shell 脚本
```

## 1.2 Linux 文件类型
Linux 下的文件可以分为4 种不同的类型：普通文件、目录文件、链接文件、特殊文件。

▶ 1、普通文件 (-) ：最常用的一种文件，其特点是不包含文件系统的结构信息。如，图形文件，文本文件、Shell 脚本、二进制可执行程序、各种类型数据文件。这些文件一般是用一些相关的应用程序创建，比如图像工具、文件工具、归档工具等。
▶ 2、目录文件(d) ：用于存放文件名及其相关信息的文件。是内核组织文件系统的基本节点。目录文件下面可以包含下一级目录或者普通文件。Linux 下的目录文件和其他os 中的“目录”概念不同，它是linux 文件中的一种。
▶ 3、链接文件(l) ：一种特殊的文件，实际上指向一个真实存在的文件连接，类似于windows 下的“快捷方式”，直接访问、不占用磁盘空间。
▶ 4、特殊文件
(1) 块设备文件(b) : 数据的读写以块为单位，比如硬盘，光驱等设备。目前在最新的Linux 发行版本中，一般不用自己来创建设备文件，因为这些文件是和内核相关联的。
(2) 字符设备文件(c) ：串行接口的设备
(3) 套接字文件(s) ：套接字文件是一个用户不可见的，高度简化的，用于汇集网络套接字的内存文件。
(4) 管道文件(p) ：用于不同进程间的信息传递。一个进程将需要传递的信息或数据写入管道的一端，另一个进程则从管道另一端取得数据或信息。

## 1.3 Linux文件系统

文件和目录的访问权限
▶ 文件权限类型
read (r): 查看文件内容
write (w): 修改文件
execute (x): 如同命令一样执行文件
▶ 目录权限类型
read (r): 列出目录内容
write (w): 在目录中增删文件
execute (x): 访问目录中的文件
▶ 权限分组
文件拥有者(user)
文件拥有者所在用户组中的其它成员(group)
所有其它用户(other)



![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929230844.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929230912.png)

## 1.4 Linux 文件系统目录结构

FHS:文件系统层次化标准



▶ /: Linux 文件系统的入口，也是处于最高一级的目录。不要把根目录划分的过大。
▶ /bin: 放置一些系统的必备执行档，例如:cat、cp、chmod、df、dmesg（用于显示开机信息）、gzip、kill、ls、mkdir、more、mount、rm、su、tar 等。
▶ /usr/bin: 主要放置一些应用软件工具的必备执行档，例如c++、g++、gcc、chdrv、diff、dig、du、eject、elm、free、gnome*、zip、htpasswd、kfm、ktop、last、less、locale、m4、make、man、mcopy、ncftp、newaliases、nslookup passwd、quota、smb*、wget 等。



▶ /boot: Linux 的内核及引导系统程序所需要的文件，系统Kernel 的配置文件，启动管理程序GRUB 的目录，vmlinuz是在启动过程中最重要的一个文件，因为这个文件就是实际系统所使用的kernel。
▶ /dev: 设备文件存储目录，比如声卡、磁盘...
▶ **/etc**: 统配置文件的所在地，一些服务器的配置文件也在这里；比如用户帐号及密码配置文件。
▶ **/home**: 一般情况下，除root 外的普通用户主目录默认存放目录。



▶ /root: Linux 超级权限用户root 的主目录。
▶ /sbin: 大多是涉及系统管理的命令的存放，是超级权限用户root 的可执行命令存放地，普通用户无权限执行这个目录下的命令，这个目录和/usr/sbin; /usr/X11R6/sbin或/usr/local/sbin 目录是相似的；凡是目录sbin 中包含的都是root 权限才能执行的。
▶ **/tmp**: 临时文件目录，有时用户运行程序的时候，会产生临时文件。/tmp 就用来存放临时文件的。/var/tmp 目录和这个目录相似。



▶ /proc: 操作系统运行时，进程（正在运行中的程序）信息及内核信息（比如cpu、硬盘分区、内存信息等）存放在这里。（伪文件系统，自动装载内核的映象，可以获取系统的信息。）
这个目录在磁盘上其实是不存在的。
▶ /sys: 系统设备信息的虚拟目录，Sysfs 的根目录下包含了七个目录：block, bus, class, devices, firmware, ,module 和power(这些目录随内核的不同而有所不同 )
▶ /var: 这个目录的内容是经常变动的，存放被系统更改过的数据。
▶ /lib: 启动时所用到的库文件都放在这个目录下，那些非启动用的库文件放在/usr/lib 下。内核模块放在/lib/modules 下。
▶ **/lost+found**: 当系统意外崩溃或机器意外关机，产生一些文件碎片放在这里。当系统启动的过程中fsck 工具会检查这里，并修复已经损坏的文件系统。



▶ /media: 即插即用型存储设备的挂载点自动在这个目录下创建，如USB 盘系统自动挂载后，会在这个目录下产生一个目录；CDROM/DVD 自动挂载后，也会在这个目录中创建一个目录，类似cdrom 的目录。（挂载点目录，一般是光盘）
▶ **/mnt**: 这个目录下面放着一些用来安装其他设备的子目录。（挂载点目录）
▶ /opt: 表示的是可选择的意思，有些软件包也会被安装在这里，也就是自定义软件包。
▶ /srv: 主要用来存储本机或本服务器提供的服务或数据。（用户主动生产的数据、对外提供服务）
▶ /cdrom: 光驱。



▶ /usr: Unix Software Resource 的缩写，也就是Unix 操作系统软件资源所放置的目录，而不是用户的数据；所有系统默认的软件都会放置到/usr 目录下，系统安装完毕后，这个目录会占用最多的硬盘容量。

```
/bin 存放二进制可执行文件
/include 存放C，C++ 的头文件
/lib 存放启动时不需要的库文件
/local 存放本地计算机所需要的文件
/sbin 存放绝大部分的系统程序
/share 存放各种共享文件
/src 存放程序的源代码
```









# 二、常用命令

## 2.1 文件与目录基本操作

掌握基本的文件与目录操作命令。
▶ 定位文件与目录命令: 
> cd pwd find locate
> 

▶ 浏览文件命令:
> ls head tail cat more less
> 

▶ 目录操作命令:
> mkdir rmdir
> 

▶ 文件操作命令:
> touch rm cp mv ln tar gzip gunzip whereis
> 

whatis
▶ 文件压缩和解压缩:
> tar gzip
> 


## 2.2 Linux命令格式说明

> command [-options] [parameters]

1. [-options] 命令选项，-开始，多个选项可用一个-连起来
   如ls -l -a 与ls -la 相同
   
2. 单字符选项前使用一个减号-，单词（多字符）选项前使用两个减号- -
   如
   
   ```
   ls - -help
   ```
   
   
   
3. parameters：参数是可选的或必须的

4. 所有的命令从标准输入接受输入，输出结果显示在标准输出

▶ TAB，将命令补充完整
▶ 上下箭头键, 使用历史记录功能

## 2.3 定位文件和目录


1. pwd  ： 显示用户所在的位置。

2. cd : 用来改变工作目录。
```
在使用cd 进入某个目录时，用户必须具有对该目录的读权限。
(1) 改变当前所处的目录，如果用户当前处于/root 目录，要
进入/etc 目录。
root@Ubuntu:～# cd /etc
root@Ubuntu: /etc # pwd
/etc
(2) 返回上级目录。
root@Ubuntu:～# cd ..
root@Ubuntu:/# pwd
/
(3) 回到用户主目录。
root@Ubuntu:/# cd
root@Ubuntu:～# pwd
/root
(4) cd - 返回进入此目录之前所在目录
```

## 2.4 find使用命令详解

find : 在硬盘上查找文件。
find 是Linux 功能最为强大，使用也是较为复杂的命令。

```
find 命令格式：fing [<path>][option]
```

```
path : 要查找的目录路径
option : 常用的选项

-name file 查找名为filename的文件
-perm 按执行权限进行查找
-user username 按文件属性进行查找
-group groupname 按组进程查找
-mtime -n +n 按文件更改时间来查找文件 -n 指n天以内，+n 指n天以前
-atime -n +n 按文件访问时间来查找文件 -n 指n天以内，+n 指n天以前
-ctime -n +n 按文件创建时间来查找文件 -n 指n天以内，+n 指n天以前
-nogroup 查无有效属性的文件，即文件的属性在/etc/passwd中不存在
-type b/d/c/p/l/f 查是块设备、目录、字符设备、管道、符号链接、普通文件
-size n[c] 查长度为n块[或n字节]的文件
-prune 忽略某个目录
```


​    
### 2.4.1 按照名字进行查找

```
find -name file
```

 查找名为filename的文件。
​  

```
(1) 从根目录开始查找文件名为passwd 的文件
find / -name passwd
find / -name passwd 2>/dev/null
(2) 在/etc 中查找文件init
find /etc -name init
find /etc/ -name init 2>/dev/null
(3) 在/etc/中查找文件xxx，不区分大小写
find /etc -iname xxx
(4) 查找文件名包含init 的文件
find /etc –name *init*
find /etc –name init??? 可能会查找到initabc initxyz
(5) 在当前目录和子目录中，查找大写字母开头的txt 文件
find . -name ’[A-Z]*.txt’ -print
```




### 2.4.2 按目录查找

(1) 在/etc 及其子目录中，查找host 开头的文件
> find /etc -name ’host*’ -print
> 

(2) 在当前目录除abc 之外的子目录内搜索txt 文件　　
> find . -path ”./abc” -a -prune -o -name ”*.txt” -print
> 

解释：如果目录/abc 存在（即-a 左边为真），则求-prune 的值，
-prune 返回真，‘与’逻辑表达式为真（即-path ’./abc’-a -prune 为真），
find 命令将在除这个目录以外的目录下查找txt 后缀文件并打印出来；
如果目录abc 不存在（即-a 左边为假），则不求值-prune ，
‘与’逻辑表达式为假，则在当前目录下查找所有txt 后缀文件。
因为使用了-prune 参数，所以末尾需要使用-print 参数。
-a 是条件与，-o 是条件或，所以-o 前面的满足之后，后面的就不会再执行。
-path xxx -prune：表示忽略某个目录-a 也可以不写。



### 2.4.3 按权限查找

```
-perm 按执行权限进行查找

(1) 在当前目录及子目录中，查找属主具有读写执行，其他
具有读执行权限的文件　　
find . -perm 755 -print
(2) 查找用户有写权限或者组用户有写权限的文件或目录
find ./ -perm /220
find ./ -perm /u+w,g+w
find ./ -perm /u=w,g=w
```




### 2.4.4 按类型查找　（b/d/c/p/l/f ）


    在当前目录及子目录中，查找符号链接文件
    find . -type l -print
    find /etc -name init* -a –type f
    find /etc -name init* -a -type d


### 2.4.5 按属主及属组查找

    -nogroup 查无有效属组的文件，即文件的属组在/etc/groups 中不存在
    -nouser 查无有效属主的文件，即文件的属主在/etc/passwd 中不存在
    
    (1) 查找属主是www 的文件　　
    find / -user www -type f -print 　　
    (2) 查找属主被删除的文件
    find / -nouser -type f -print
    (3) 查找属组mysql 的文件
    find / -group mysql -type f -print
    (4) 查找用户组被删掉的文件
    find / -nogroup -type f -print

### 2.4.6 按时间查找


    (1)atime [+-] 时间: 按照文件访问时间搜索
    (2)-mtime [+-] 时间: 按照文改时间搜索（修改文件的内容）
    (3)-ctime [+-] 时间: 按照文件修改时间搜索（修改文件的时间）
    +-时间的含义:
    ”-5” 指的是5 天内修改的文件，”5” 指的是前5～6 天那一天修改的文件，”+5” 指的是6 天前修改的文件。
    
    (1) 查找2 天内被更改过的文件
    find . -mtime -2 -type f -print 　
    (2) 查找2 天前被更改过的文件
    find . -mtime +2 -type f -print 　
    (3) 查找一天内被访问的文件
    find . -atime -1 -type f -print
    (4) 查找一天前被访问的文件
    find . -atime +1 -type f -print 　　
    (5) 查找一天内状态被改变的文件
    find . -ctime -1 -type f -print 　
    (6) 查找一天前状态被改变的文件
    find . -ctime +1 -type f -print
    
    find 不仅可以按照atime、mtime、ctime 来查找文件的时间，也可以按照amin、mmin 和cmin 来查找文件的时间，区别只是所有time 选项的默认单位是天，而min 选项的默认单位是分钟。
    查找10 分钟以前状态被改变的文件。
    find . -cmin +10 -type f -print



​    

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu学习笔记/20200930192231.png)

### 2.4.7 按文件新旧查找

~~~
(1) 查找比abc.txt 新的文件
find . -newer ”abc.txt” -type f -print
(2) 查找比abc.txt 旧的文件
find . ! -newer ”abc.txt” -type f -print
(3) 查找比abc.txt 新，比bcd.txt 旧的文件
find . -newer ’abc.txt’ ! -newer ’bcd.txt’ -type f -print
~~~



### 2.4.8 按大小查找

~~~
(1) 查找超过1M 的文件
find / -size +1M -type f -print 　　
(2) 查找等于600 字节的文件
find . -size 600c -print
(3) 查找小于32k 的文件
find . -size -32k -print
(4) 查找当前目录下大于80M 小于100M 的文件
find . -size +80M -a -size -100M -type f -print
~~~

### 2.4.9 inum 根据i 节点查找

~~~
可以根据文件的inode 节点值，删除该文件。有些文件很特殊，用rm 难以直接删除时，可以使用该方式。
touch “this is test”
rm this is test
rm: 无法删除“this”: 没有那个文件或目录
rm: 无法删除“is”: 没有那个文件或目录
rm: 无法删除“test”: 没有那个文件或目录
可以使用rm “this is test”
或者:
(1) 使用ls -i
278653 this is test
(2) find . -inum 278653 -exec rm {} \;
~~~

### 2.4.10 对搜索结果执行操作-exec 命令{} \;

~~~
花括号代表前面find 查找出来的文件名，
exec 解释：-exec 参数后面跟的是command 命令，它的终止是以“；”为结束标志的，所以这句命令后面的分号是不可缺少的，考虑到各个系统中分号会有不同的意义，所以前面加反斜杠。
(1) 在/etc 下查找init 开头的所有文件，并显示详细信息
find /etc -name init* -a -type f -exec ls –l {} \;
(2) 在/home 下查找用户为wl 的文件，逐个询问删除。删除操作需要谨慎，可以使用–ok，而不是-exec
find /home -user wl -ok rm {} \;
-ok：出现详细信息，并询问是否需要查看。回答y，则可以继续下一个信息
(3) 查找aa.txt 并备份为aa.txt.bak
find . -name ’aa.txt’ -exec cp {} {}.bak \;
~~~

## 2.5 locate

同find 命令相比较，locate 命令是从linux 文件数据库（/var/lib/mlocate/mlocate.db）中查找，而不是每次搜索文件系统。因为是从数据库中查找，locate 的速度远远快于find 命令。但是，使用locate 命令查找的结果仅仅是在当前数据库，结果可能会没有find 准确。

如果没有mlocate.db，则使用:
(1)sudo apt-get install mlocate

(2)sudo updatedb
系统就会创建mlocate.db

(3) 查找和android 相关的所有文件，并且只显示前5 个
locate android -n 5

(4) 查找apt.conf 文件
locate apt.conf

## 2.6 ls 

浏览文件和目录。


显示用户当前或指定目录的内容

### 2.6.1 简介

```
ls 命令可以使用通配符*、？、[abc] [^abc]。这样可以使用户很方便地查找特定形式的文件和目录。如果不指定目录，将显示当前目录的内容。

(1) 输出根目录下文件或目录的详细信息。
root@Ubuntu:～# ls –l ：以长格式显示文件的详细信息
[文件属性][inode 数][拥有者][所有者组][大小] [建立日期] [文件/目录名]


总用量84
drwxr-xr-x 2 root root 4096 6 月3 10:02 bin
drwxr-xr-x 3 root root 4096 9 月29 08:35 boot
drwxr-xr-x 20 root root 3280 9 月29 08:34 dev
drwxr-xr-x 140 root root 12288 9 月29 13:55 etc
drwxr-xr-x 3 root root 4096 3 月25 2019 home
```

### 2.6.2 选项

~~~
(1)ls: 显示当前或指定目录的内容
(2)ls -a 列出当前目录下所有文件（包括隐含文件）
(3)ls -la 列出目录下所有文件或目录的详细信息
(4)ls -R 列出包括子目录下的所有文件R 表示递归显示
(5)ls -h 以人类可以阅读的形式列出human-readable
(6)ls -t 按照修改时间排序，最近的排在最前面
(7)ls -F 在不同文件(夹) 结尾，输出不同字符
            1:  /: 目录
            2: @：符号链接文件
            3: *：可执行文件
            4: |：管道文件
            5: =：socket 文件
            6: 普通文件没有符号
(8)ls -d 只显示目录本身，不展开目录
(9)ls -S 以文件大小排序，默认从大到小
(10)ls -r：逆序排序r:reverse
(11)ls -X 按扩展名的首字母排序
例：ls -Slhr: 以文件大小排序，以K M G 为单位，逆序显示详情
~~~

## 2.7 head

用来查看文件的开头部分。
按照默认设置，只能阅读文件的前十行。

Head –n 可以查看前n 行。
查看文件/etc/profile 前五行:

```
head -5 etc/profile
```



## 2.8 tail

查看文件结尾部分
缺省状态tail 命令查看文件结尾十行，与head 命令相反。
这有助于查看日志文件的最后十行，阅读重要的系统消息；
还可以使用tail 来观察日志文件被更新的过程。
即时观察/var/log/messages 的变化:

```
tail -f /var/log/messages
```



## 2.9 cat

合并文件或者显示文件的内容。

cat 是“concatenate”的缩写，即合并文件。该命令可以显示文件的内容，或者是将多个文件合并成一个文件。

```
(1) 使用cat 阅读短文
cat /etc/profile
(2) 建立两个文件并重定向到file1 与file2重定向标准输出，使用“>”符号。把“>”符号放在cat 命令之后（或在任何写入标准输出的工具程序和应用程序之后），会把它的输出重定向到跟在符号之后的文件中。

”>”:覆盖，”»”: 追加。

cat > file1 回车
hello 按ctrl+d 结束输入

cat > file2 回车
great 按ctrl+d 结束输入

tac:concatenate and print files in reverse，将文件全部内容从尾到头反向连续输出到标准输出(屏幕) 上，tac 是cat 的反写，功能与cat 命令刚好相反。
```

## 2.10 more

more 命令是一般用于要显示的内容会超过一个画面长度的情况。为了避免画面显示时瞬间就闪过去，用户可以使用more 命令，让画面在显示满一页时暂停，此时可按空格健继续显示下一个画面，按b 键就会往回（back）一页显示或按Q 键停止显示。



```
(1) 显示/etc/profile 文本文件的内容
more /etc/profile屏幕在显示满一屏时暂停，此时可按空格健继续显示下一屏。
(2) 当用ls 命令查看文件列表时，如果文件太多，则可配合more 命令使用
ls -al | more
```



## 2.11 grep

搜索文件内容可以使用Global Regular Expression Print （grep）命令。

```
grep [options] [pattern] [file]
```



### 2.11.1 选项:options


![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu学习笔记/20201003172900.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu学习笔记/20201003172919.png)

### 2.11.2 模式:pattern

```
(1) 直接输入要匹配的字符串，如要匹配hello.c 文件中
printf 的个数：grep -c “printf” hello.c

(2) 使用基本正则表达式

^ 锚定行的开始。如’^grep’ 匹配所有以grep 开头的行。

. 匹配一个非换行符的字符。如:'gr.p' 匹配gr 后接一个任意字符，然后是p。

* 匹配零个或多个先前字符。如: '*grep' 匹配所有一个或多个空格后紧跟grep 的行。

.* 一起用代表任意字符。

[abc] 匹配一个指定范围内的字符。表示匹配一个字符，这个字符必须是abc 中的一个。如’[Gg]rep’ 匹配Grep 和grep。

[^] 匹配一个不在指定范围内的字符。如[^123] 匹配一个字符，这个字符是除了1、2、3 以外的所有字符。

\(..\) 标记匹配字符，如’\(love\)’，love 被标记为1。

\< 锚定单词的开始，如:’\<grep’ 匹配包含以grep 开头的单词的行。

\> 锚定单词的结束，如’grep\>’ 匹配包含以grep 结尾的单词的行。

x\{m\} 重复字符x，m 次，如：‘o\{5\}’ 匹配包含5 个o的行。

x\{m,\} 重复字符x, 至少m 次，如：’o\{5,\}’ 匹配至少有5 个o 的行。

x\{m,n\} 重复字符x，至少m 次，不多于n 次，如：
’o\{5,10\}’ 匹配5–10 个o 的行。

\w 匹配文字和数字字符，也就是[A-Za-z0-9]。

\W \w 的反置形式，匹配一个或多个非单词字符，如点号句号等。

\b 单词锁定符，如: ’\bgrep\b’ 只匹配grep。

```

### 2.11.3 举例

1、在某个文件里搜索error 字符串

> grep “error”log.txt
> grep -i “ErroR”log.txt -i 忽略大小写
> 

2、grep 使用- -color=auto 将关键字部分使用颜色高亮显示。如果每次使用grep 都得要自行加上- -color=auto 比较麻烦，可以在~/.bashrc 内加上：alias grep=’grep - -color=auto’

> source  ̃/.bashrc 命令立即生效。
> 

3、在passwd 中找带有sh 的行，并且显示行号。
> grep –n ‘sh’/etc/passwd
> 

4、在passwd 中找带有bash 的行，-o 标识只显示命中的字符串only
> grep –o ‘bash’/etc/passwd

5、在passwd 中反向查找。不含有bash 的行
> grep -v ‘bash’/etc/passwd
> 

6、查找命中行的内容，以及上面两行内容。
> grep -B2 –n ‘wl’/etc/passwd
> 

7、查找命中行的内容，以及下面两行内容。
> grep -A2 -n ‘wl’/etc/passwd
> 

8、查找命中行的内容，以及上下各两行内容。
> grep -C2 -n ‘wl’/etc/passwd
> A:after , B:before , C: after and before
> 


9、匹配数字0-9
> grep ‘[0-9]’/etc/passwd
> 

10、在某个配置文件中查找# 开头的注释行
> grep ‘^#’/etc/profile
> 

11、查找以h 结尾的行
> grep -n ‘h$’/etc/passwd
> 

12、查看文件时，去除所有的空行和以“#”开头的行。
> grep -v ‘^$’/etc/profile | grep –v ‘^#’
> 


13、查找字母o 出现两次的内容
> grep ’o\{2\}’ /etc/passwd
> 

14、在当前目录搜索带’user’ 行的文件
> grep ‘user’*
> 


## 2.12 awk

awk 是一个强大的文本分析工具，相对于grep 的查找，sed 的编
辑，awk 在其对数据分析并生成报告时，显得尤为强大。简单来
说awk 就是把文件逐行的读入，以空格为默认分隔符将每行切
片，切开的部分再进行各种分析处理。

### 2.12.1 简介

▶ 语法：

> awk ’pattern + action’ filenames
> 

pattern: 正则表达式，用//括起来
action: 找到匹配内容时，所执行的一系列命令
▶ awk 其实是一门编程语言，它支持条件判断、数组、循环等
功能。所以，我们也可以把awk 理解成一个脚本语言解释
器。
▶ grep 、sed、awk 被称为linux 中的” 三剑客”:
grep 更适合单纯的查找或匹配文本；
sed 更适合编辑匹配到的文本；
awk 更适合格式化文本，对文本进行较复杂格式处理。 



### 2.12.2 举例

```
-F 指定分隔符, 默认为空格；
$0 表示整个当前行；
$1 表示每行第一个字段；
NR 表示每行的记录号；\t 为制表符；\n 为换行符；

[例1] 搜索/etc/passwd/中含有root 关键字的行
awk ’/root/’ /etc/passwd
或awk ’/root/{print}’ /etc/passwd
或awk ’/root/{print $0}’ /etc/passwd

[例2] 搜索/etc/passwd 有root 关键字的所有行，并显示对应的shell
awk -F: ’/root/{print $1,$7}’ /etc/passwd

[例3] 显示当前目录下所有的目录文件，过滤掉其他文件
ls -lF | awk ’/^d/’

```

## 2.13 硬连接和软连接文件

### 2.13.1 硬连接文件

硬链接是通过索引节点进行的链接。在Linux 中，多个文件指向同一个索引节点是允许的，像这样的链接就是硬链接。硬链接只能在同一文件系统中的文件之间进行链接，不能对目录进行创建。如果删除硬链接对应的源文件，则硬链接文件仍然存在，而且保存了原有的内容，这样可以起到防止因为误操作而错误删除文件的作用。由于硬链接是有着相同inode 号仅文件名不同的文件，因此，删除一个硬链接文件并不影响其他有相同inode 号的文件。

硬链接可由命令link 或ln 创建。
link oldfile newfile
ln oldfile newfile

### 2.13.2 软连接文件

软链接（也叫符号链接）与硬链接不同，文件用户数据块中存放的内容是另一文件的路径名的指向。软链接就是一个普通文件，只是数据块内容有点特殊。软链接可对文件或目录创建。
▶ 主要应用于两个方面：
▶ 一方面，方便管理，例如可以把一个复杂路径下的文件链接到一个简单路径下方便用户访问；
▶ 另一方面，解决文件系统磁盘空间不足的情况。
例如某个文件文件系统空间已经用完了，但是现在必须在该文件系统下创建一个新的目录并存储大量的文件，那么可以把另一个剩余空间较多的文件系统中的目录链接到该文件系统中，这样就可以很好的解决空间不足问题。注意：删除软链接并不影响被指向的文件，但若被指向的原文件被删除，则相关软连接就变成了死链接

### 2.13.3 实验举例

touch f1 # 创建一个测试文件f1
ln f1 f2 # 创建f1 的一个硬连接文件f2
ln -s f1 f3 # 创建f1 的一个符号连接文件f3
ls -li # -i 参数显示文件的inode 节点信息
Figure 5: 软链接和硬链接文件
从上面的结果中可以看出，硬连接文件f2 与原文件f1 的
inode 节点相同，然而符号连接文件的inode 节点不同

## 2.14 cp

复制文件或目录。

### 2.14.1 语法

```
cp [选项] 源文件目标文件
选项：
-a：相当于-d、-p、-r 选项的集合；
-d：如果源文件为软链接（对硬链接无效），则复制出的目标文件也为软链接；
-i：询问，如果目标文件已经存在，则会询问是否覆盖；
-l：把目标文件建立为源文件的硬链接文件，而不是复制源文件；
-s：把目标文件建立为源文件的软链接文件，而不是复制源文件；
-p：复制后目标文件保留源文件的属性（包括所有者、所属组、权限和时间）；
-r：递归复制，用于复制目录；
-u：若目标文件比源文件有差异，则使用该选项可以更新目标文件，此选项可用于对文件的升级和备用
```

### 2.14.2 举例



(1) 复制文件/etc/profile 到当前目录。
> cp /etc/profile .

(2) 复制/etc/apt 目录下所有的内容，包括所有子目录到当
前目录。
> cp –R /etc/apt .

(3) 使用通配符复制etc 目录下mail 开头的所有文件到当前目录。
> cp /etc/mail* .

(4）cp 复制软连接文件
a、创建当前目录下user.txt 的软连接文件至/tmp/下，命名mylink。
> ln –s ~/user.txt /tmp/mylink

b、复制/tmp/mylink 至~/下，命名为mylink2
> cp /tmp/mylink ./mylink2

c、cat 查看mylink2 内容
> cat ./mylink2

(5）cp 复制软连接文件，加参数-d
a、创建当前目录下user.txt 的软连接文件至/tmp/下，命名mylink。
> ln –s ~ /user.txt /tmp/mylink

b、复制/tmp/mylink 至~/下，命名为mylink3
> cp -d /tmp/mylink ̃/mylink3

c、ls 查看文件，cat 查看mylink3 内容
> ls –l
> cat ./mylink3

### 2.14.3 注意

1. ln -s 创建软链接时，用绝对路径，而不是相对路径。否则会因为找不到原文件而报错，呈现红色！
2. 创建软连接之后，若删除了原文件，查看链接文件，也会出现同样错误！
3. cp 复制链接文件，不加参数d，是复制的是源文件，加参数d，则复制的是链接文件。

## 2.15 touch

1. 使用ls 命令会发现，每个文件在linux 下面都会记录许多的时间参数。有三个主要的变动时间：
- modified time(mtime)，当文件的“内容数据”更改时，就会更新这个时间。比如，使用vi 修改文件。
- change time(ctime)，当文件的“状态”改变时，就会更新这个时间。比如，权限和属性被更改。
- access time(atime)，当文件的“内容被使用”时，就会更新这个时间。比如，cat xxx。cat、less、more 等对文件只读，不修改文件内容，只会触发修改atime 的值。

2. stat xxx 可以观察一个文件的详情。

3. touch 生成一个空文件或修改文件的存取/修改的时间记录值。
   (1) 将当前目录下的文件时间修改为系统的当前时间。
   touch *
   (2）新建文件
   root@Ubuntu: #touch test
   若文件存在，则修改为系统的当前时间；若文件不存在，则生成一个为当前时间的空文件。
   (3) 将test 文件的日期改为20180710。

   > touch –d 20180710 test
   > ls
   > -rw-r–r– 1 wl wl 0 2018-07-10 00:00 test
   > 注意：文件的最后修改时间离现在不到6 个月的就会只显示月/日/小时/分钟，否在就会显示月/日/年
   
> 还可以使用：
   >
   > touch -d “2 days ago”testfile1 “10 years ago”touch -d “next thursday”testfile2 “next year”
   





## 2.16 mv

移动文件, 可以将文件及目录移到另一目录下，或更改文件及目录的名称。

```
1. 将test 文件移动上层目录。
mv test ../

2. 将profile 改名为profile.back。
mv profile profile1.back
```



## 2.17 rm

rm 删除文件和目录。

```
1. 删除文件主目录下file1 文件。
rm profile

2. 删除文件主目录下file2 文件时给以提示。
rm –i file2rm

3. 递归删除目录。
rm -r apt

4. 强制递归删除目录。
rm –rf /temp
不给提示直接删除temp 目录下的文件与te
```



## 2.18 mkdir

创建目录。

```
1. 在当前目录下建立新目录dir1。
mkdir dir1

2. 若当前目录下无book 目录，在当前目录创建book/Linux 子目录。
mkdir book/Linux

mkdir: 无法创建目录‘book/Linux’: No such file or directory

一次创建多层目录要加-p 参数 :
mkdir –p /book/Linux
```



## 2.19 redir

删除目录。与创建目录类似，加上-p 参数表示如果删除一个目录后，其父目录为空，则将其父目录一同删除。

```
1. 删除目录 dir1
rmdir dir1

2. 删除当前目录下的book/Linux 子目录，如果book 目录为空，也删除该目录。
rmdir –p book/Linux
book 目录不为空则保留。
```



## 2.20 umask

▶ 什么是umask
当用户登录系统之后创建一个文件是会有一个默认权限的，这个权限是怎么来的呢？umask 用于设置用户创建文件或者目录的默认权限，umask 设置的是权限的“补码”。一般在/etc/profile 或和/etc/bashrc 中设置umask。
▶ umask 作用
umask 值用于设置用户在创建文件时的默认权限，当我们在系统中创建目录或文件时，目录或文件所具有的默认权限就是由umask 值决定的。对于root 用户，系统默认的umask值是0022；对于普通用户，系统默认的umask 值是0002。执行umask 命令可以查看当前用户的umask 值。

▶ umask 值一共有4 组数字，其中第1 组数字用于定义特殊权限，一般不予考虑，与一般权限有关的是后3 组数字。默认情况下，对于目录，用户所能拥有的最大权限是777；对于文件，用户所能拥有的最大权限是目录的最大权限去掉执行权限，即666。因为x 执行权限对于目录是必须的，没有执行权限就无法进入目录，而对于文件则不必默认赋予x 执行权限。
▶ 对于root 用户，他的umask 值是022。当root 用户创建目录时，默认的权限就是用最大权限777 去掉相应位置的umask 值权限，即对于所有者不必去掉任何权限，对于所属组要去掉w 权限，对于其他用户也要去掉w 权限，所以目录的默认权限就是755；当root 用户创建文件时，默认的权限则是用最大权限666 去掉相应位置的umask 值，即文件的默认权限是644。

```
root : 	文件： 666 - 022 = 644 rw-r--r--
		目录： 777 - 022 = 755 rwxr-xr-x
user : 	文件：	666 - 002 = 664 rw-rw-r--
		目录：	777 - 002 = 775 rwxrwxr-x
```

▶ 对于目录，直接使用777-umask 即可，得到最终结果。
▶ 对于文件，先使用666-umask。　　
▶ 注意，如果对应位上为偶数：最终权限就是这个偶数值，如果上面的对应位上有奇数，就对应位+1。得到奇数，说明umask 有奇数，+1 变成偶数，表示去掉可执行权限，系统会最大程度保证安全性（尽可能不为文件赋予可执行权限）。

▶ 如何修改umask 值？
直接使用umask 命令只能临时修改umask 值，系统重启之后umask 将还原成默认值。如果要永久修改umask 值，需要修改/etc/profile 文件或是修改/etc/bashrc 文件，例如要将默认umask 值设置为027，那么可以在文件中增加一行“umask 027”。

▶ /etc/profile 和/etc/bashrc 都可以用于设置用户登录系统时自动执行某些操作，他们的区别是/etc/profile 只在用户第一次登录时被执行，而/etc/bashrc 则在用户每次登录加载Bash Shell 时都会被执行。因而，如果是修改/etc/profile 文件，将只对新创建的用户生效；而如果是修改/etc/bashrc文件，则对所有用户都生效。