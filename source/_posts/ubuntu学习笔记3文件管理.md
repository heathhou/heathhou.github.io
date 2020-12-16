---
title: Ubuntu学习笔记3文件管理
date: 2020-10-16 15:32:17
tags: [linux,ubuntu,学习笔记]
declare: true
---

<!-- more -->


# 一、 文件管理

虚拟终端：try1-tty7  ctrl+alt+f1 f2

## 1.1 Linux 文件基础知识
▶ 文件管理是学习和使用Linux 的基础，也是Linux 系统管理与维护中最重要的部分之一。在Linux 系统上，任何软件和I/O 设备都被视为文件。Linux 中的文件名最大支持256 个字符，分别可以用A～Z、a～z、0～9 等字符来命名。

▶ 和Windows 不同，Linux 中文件名是区分大小写的，所有的UNIX 系列操作系统都遵循这个规则。在Windows 下，目录结构属于分区；Linux 下分区属于目录结构。Linux 下也没有盘符的概念（如Windows 下的C 盘、D 盘），而只有目录，不同的硬盘分区是被挂载在不同目录下的。

▶ Linux 文件的扩展名: 在windows 操作系统中根据文件的后缀就能判断文件的类型。比如file.txt、file.doc、file.sys、file.mp3、file.exe 等，而在linux 系统中，abc.exe 可以是文本文件，abc.txt 也可以是可执行文件。在Linux 中，带有扩展名的文件，只能代表程序的关联，并不能说明文件的类型，从这方面来说，Linux 的扩展名没有太大的意义。



▶ 压缩和归档文件扩展名及其含义如下。

Linux 中一个文件是否能被执行，和后缀名没有太大的关系，主要和文件的属性有关。了解Linux 文件的后缀名还是有必要的，特别是自己创建一些文件，最好加后缀名，这样做的
目的是为了应用方便。使用file 命令查看该文件的类型。
```
gz：使用gzip 压缩的文件
bz2：使用bzip2 压缩的文件
tar：使用tar 压缩的文件，又称tar 文件
tbz：使用tar 和bzip 压缩的文件
tgz：使用tar 和gzip 压缩的文件
zip：使用zip 压缩的文件，Linux 下使用gzip 命令压缩的文
件

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

▶ 在linux 中，目录也是一种文件。系统在建立每一个目录时，都会自动生成两个目录文件，一个是“.”，代表目录本身，另一个是“..”，代表目录的父目录。对于根目录而言，由于不存在父目录，所以“.”和“..”都代表其自身。


## 1.4 Linux 目录常见概念
▶ 1、路径，是指从树型目录中的某个目录层次到某个文件的一条道路。
绝对路径：从“根”开始的路径。
相对路径：从用户工作目录开始的路径。
▶ 2、根目录
Linux 的根目录（/）是Linux 系统中最特殊目录。
根目录是所有目录的起点，操作系统本身的驻留程序存放在以根目录开始的专用目录中。
▶ 用户家目录是系统管理员增加用户时建立起来的（以后也可以根据实际情况改变），每个用户都有自己的家目录，不同用户的家目录一般互不相同。用户登录到系统中时，其工作目录便是该用户的家目录，一般情况下，与用户的登录名相同，位于/home 下，但是root 用户比较特殊，其主目录为/root。用户可以通过一个～符号来引用自己的家目录。
▶ cd ～可以进入用户自己的家目录
▶ echo $HOME：显示用户家目录路径

## 1.5 Linux 文件系统目录结构

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

## 1.6 文件与目录基本操作

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
> touch rm cp mv ln tar gzip gunzip whereis whatis
> 


▶ 文件压缩和解压缩:
> tar gzip
> 

# 二、 Linux 命令格式说明 


> command [-options] [parameters]

1. [-options] 命令选项，-开始，多个选项可用一个-连起来
   如ls -l -a 与ls -la 相同
   
2. 单字符选项前使用一个减号-，单词（多字符）选项前使用两个减号- -
   如
   
```
ls --help
```

   

3. parameters：参数是可选的或必须的

4. 所有的命令从标准输入接受输入，输出结果显示在标准输出

▶ TAB，将命令补充完整
▶ 上下箭头键, 使用历史记录功能



# 三、 定位文件和目录

## 3.1 pwd
pwd  ： 显示用户所在的位置。

## 3.2 cd
cd : 用来改变工作目录。
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

## 3.3 find使用命令详解

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
### 3.3.1 按照名字进行查找

```
find -name file
```

查找名为filename的文件。

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




### 3.3.2 按目录查找

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



### 3.3.3 按权限查找

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




### 3.3.4 按类型查找　（b/d/c/p/l/f ）
```
在当前目录及子目录中，查找符号链接文件
find . -type l -print
find /etc -name init* -a –type f
find /etc -name init* -a -type d
```

### 3.3.5 按属主及属组查找

```
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
```

### 3.3.6 按时间查找

```
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
```

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu学习笔记/20200930192231.png)

### 3.3.7 按文件新旧查找

```
(1) 查找比abc.txt 新的文件
find . -newer ”abc.txt” -type f -print
(2) 查找比abc.txt 旧的文件
find . ! -newer ”abc.txt” -type f -print
(3) 查找比abc.txt 新，比bcd.txt 旧的文件
find . -newer ’abc.txt’ ! -newer ’bcd.txt’ -type f -print
```



### 3.3.8 按大小查找

```
(1) 查找超过1M 的文件
find / -size +1M -type f -print 　　
(2) 查找等于600 字节的文件
find . -size 600c -print
(3) 查找小于32k 的文件
find . -size -32k -print
(4) 查找当前目录下大于80M 小于100M 的文件
find . -size +80M -a -size -100M -type f -print
```

### 3.3.9 -inum 根据i 节点查找

```
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
```

### 3.3.10 对搜索结果执行操作-exec 命令{} \;

```
花括号代表前面find 查找出来的文件名，
exec 解释：-exec 参数后面跟的是command 命令，它的终止是以“；”为结束标志的，所以这句命令后面的分号是不可缺少的，考虑到各个系统中分号会有不同的意义，所以前面加反斜杠。
(1) 在/etc 下查找init 开头的所有文件，并显示详细信息
find /etc -name init* -a -type f -exec ls –l {} \;
(2) 在/home 下查找用户为wl 的文件，逐个询问删除。删除操作需要谨慎，可以使用–ok，而不是-exec
find /home -user wl -ok rm {} \;
-ok：出现详细信息，并询问是否需要查看。回答y，则可以继续下一个信息
(3) 查找aa.txt 并备份为aa.txt.bak
find . -name ’aa.txt’ -exec cp {} {}.bak \;
```

## 3.4 locate

同find 命令相比较，locate 命令是从linux 文件数据库（/var/lib/mlocate/mlocate.db）中查找，而不是每次搜索文件系统。因为是从数据库中查找，locate 的速度远远快于find 命令。但是，使用locate 命令查找的结果仅仅是在当前数据库，结果可能会没有find 准确。
```
如果没有mlocate.db，则使用:
(1)sudo apt-get install mlocate

(2)sudo updatedb
系统就会创建mlocate.db

(3) 查找和android 相关的所有文件，并且只显示前5 个
locate android -n 5

(4) 查找apt.conf 文件
locate apt.conf
```
# 四、 浏览文件和目录

## 4.1 ls 

浏览文件和目录。
显示用户当前或指定目录的内容

### 4.1.1 简介

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

### 4.1.2 选项

```
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
```

## 4.2 head

用来查看文件的开头部分。
按照默认设置，只能阅读文件的前十行。

Head –n 可以查看前n 行。
查看文件/etc/profile 前五行:

```
head -5 etc/profile
```



## 4.3 tail

查看文件结尾部分
缺省状态tail 命令查看文件结尾十行，与head 命令相反。
这有助于查看日志文件的最后十行，阅读重要的系统消息；
还可以使用tail 来观察日志文件被更新的过程。
即时观察/var/log/messages 的变化:

```
tail -f /var/log/messages
```



## 4.4 cat

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

## 4.5 more

more 命令是一般用于要显示的内容会超过一个画面长度的情况。为了避免画面显示时瞬间就闪过去，用户可以使用more 命令，让画面在显示满一页时暂停，此时可按空格健继续显示下一个画面，按b 键就会往回（back）一页显示或按Q 键停止显示。



```
(1) 显示/etc/profile 文本文件的内容
more /etc/profile屏幕在显示满一屏时暂停，此时可按空格健继续显示下一屏。
(2) 当用ls 命令查看文件列表时，如果文件太多，则可配合more 命令使用
ls -al | more
```

# 五、 搜索文件内容

## 5.1 grep

搜索文件内容可以使用Global Regular Expression Print （grep）命令。

```
grep [options] [pattern] [file]
```



### 5.1.1 选项:options


![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu学习笔记/20201003172900.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu学习笔记/20201003172919.png)

### 5.1.2 模式:pattern

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

### 5.1.3 举例

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


## 5.2 awk

awk 是一个强大的文本分析工具，相对于grep 的查找，sed 的编辑，awk 在其对数据分析并生成报告时，显得尤为强大。简单来说awk 就是把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理。

### 5.2.1 简介

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



### 5.2.3 举例

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

# 六、 硬连接和软连接文件

## 6.1 硬连接文件

硬链接是通过索引节点进行的链接。在Linux 中，多个文件指向同一个索引节点是允许的，像这样的链接就是硬链接。硬链接只能在同一文件系统中的文件之间进行链接，不能对目录进行创建。如果删除硬链接对应的源文件，则硬链接文件仍然存在，而且保存了原有的内容，这样可以起到防止因为误操作而错误删除文件的作用。由于硬链接是有着相同inode 号仅文件名不同的文件，因此，删除一个硬链接文件并不影响其他有相同inode 号的文件。

硬链接可由命令link 或ln 创建。
link oldfile newfile
ln oldfile newfile

## 6.2 软连接文件

软链接（也叫符号链接）与硬链接不同，文件用户数据块中存放的内容是另一文件的路径名的指向。软链接就是一个普通文件，只是数据块内容有点特殊。软链接可对文件或目录创建。
▶ 主要应用于两个方面：
▶ 一方面，方便管理，例如可以把一个复杂路径下的文件链接到一个简单路径下方便用户访问；
▶ 另一方面，解决文件系统磁盘空间不足的情况。
例如某个文件文件系统空间已经用完了，但是现在必须在该文件系统下创建一个新的目录并存储大量的文件，那么可以把另一个剩余空间较多的文件系统中的目录链接到该文件系统中，这样就可以很好的解决空间不足问题。注意：删除软链接并不影响被指向的文件，但若被指向的原文件被删除，则相关软连接就变成了死链接

## 6.3 实验举例

touch f1 # 创建一个测试文件f1
ln f1 f2 # 创建f1 的一个硬连接文件f2
ln -s f1 f3 # 创建f1 的一个符号连接文件f3
ls -li # -i 参数显示文件的inode 节点信息
Figure 5: 软链接和硬链接文件
从上面的结果中可以看出，硬连接文件f2 与原文件f1 的
inode 节点相同，然而符号连接文件的inode 节点不同

# 七、 操作文件和目录

## 7.1 cp

复制文件或目录。

### 7.1.1 语法

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

### 7.1.2 举例



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

### 7.1.3 注意

1. ln -s 创建软链接时，用绝对路径，而不是相对路径。否则会因为找不到原文件而报错，呈现红色！
2. 创建软连接之后，若删除了原文件，查看链接文件，也会出现同样错误！
3. cp 复制链接文件，不加参数d，是复制的是源文件，加参数d，则复制的是链接文件。

## 7.2 touch

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






## 7.3 mv

移动文件, 可以将文件及目录移到另一目录下，或更改文件及目录的名称。

```
1. 将test 文件移动上层目录。
mv test ../

2. 将profile 改名为profile.back。
mv profile profile1.back
```



## 7.4 rm

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



## 7.5 mkdir

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



## 7.6 rmdir

删除目录。与创建目录类似，加上-p 参数表示如果删除一个目录后，其父目录为空，则将其父目录一同删除。

```
1. 删除目录 dir1
rmdir dir1

2. 删除当前目录下的book/Linux 子目录，如果book 目录为空，也删除该目录。
rmdir –p book/Linux
book 目录不为空则保留。
```



## 7.7 umask

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



# 八、 文件权限管理

## 8.1 chgrp

chgrp 改变文件或目录的所属组。

```
语法：chgrp [选项] [组] [文件]

必要参数:
-c 当发生改变时输出调试信息
-f 不显示错误信息
-R 处理指定目录以及其子目录下的所有文件，递归
-v 运行时显示详细的处理信息
–dereference 作用于符号链接的指向，而不是符号链接本身
–no-dereference 作用于符号链接本身

选择参数:
–reference=<文件或者目录>
–help 显示帮助信息
–version 显示版本信息
```



```
例1 改变文件的群组属性并显示过程
chgrp -v root file1.tar
将file1.tar 文件由wl 组改变为root

例2 根据指定文件改变文件的组属性
chgrp - - reference = file1.tar file2.tar
改变file2.tar 的组属性，使之与file1.tar 的组属性相同

例3 递归改变多个文件的组属性
chgrp -R wanglei myfile
```



## 8.2 chown 
指定文件或目录的所有者，还可以修改文件所属组。

```
语法：chown [选项] [用户] [: 群组] [文件或目录]

参数：
-c 显示更改的部分
-f 忽略错误信息
-R 处理指定目录以及其子目录下的所有文件，递归
-v 显示处理过程
-reference=< 文件或目录> 指定某文件或目录作为参考，
把操作的目录或文件设置成参考对象相同的所有者和组
```



```
例1 更改所属用户
chown wanglei /tmp/test.tmp

例2 更改所属组
chgrp wanglei /tmp/test.tmp 或chown :wanglei
/tmp/test.tmp

例3 一次性更改用户和用户组
chown wanglei:wanglei /tmp/test.tmp

例4 更改目录及子目录的所有者、所属组
chown -R wanglei:teac /tmp/mylog
```



## 8.3 chmod 

改变文件或目录的访问权限。

```
语法：chmod [OPTION]... MODE[,MODE]... FILE...

mode : 权限设定字串，格式如下:

ugoa...[[+-=][rwxX]...][,...]
u 表示该文件的拥有者，g 表示与该文件的拥有者属于同一个群体(group) 者，o 表示其他以外的人，a 表示这三者皆是。
+ 表示增加权限、- 表示取消权限、= 表示唯一设定权限。
r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该文件是个子目录或者该文件已经被设定过为可执行。
```



```
例1 将文件file1.txt 设为所有人皆可读取
chmod ugo+r file1.txt 或者chmod a+r file1.txt

例2 将文件file1.txt 与file2.txt 设为: 该文件拥有者，与其所属同一个群体者可写入，但其他以外的人则不可写入
chmod ug+w,o-w file1.txt file2.txt

例3 将ex1.py 设定为只有该文件拥有者可以执行
chmod u+x ex1.py

例4 将目前目录下的所有文件与子目录皆设为任何人可读取
chmod -R a+r *
```



```
chmod 也可以用数字来表示权限
语法为：chmod abc file

其中a,b,c 各为一个数字，分别表示User、Group、及Other的权限
r, 读取权限，数字代号为“4”即“100”
w, 写入权限，数字代号为“2”即“010”
x, 执行或切换权限，数字代号为“1”即“001”
-, 不具任何权限，数字代号为“0”即“000”

rwx 属性则4+2+1=7;rw-属性则4+2=6;-x 属性则0+0+1=1
chmod a=rwx file 和chmod 777 file 效果相同
chmod ug=rwx,o=x file 和chmod 771 file 效果相同
```



## 8.4 chattr & lsattr

有时候发现用root 权限都不能修改某个文件，大部分原因是曾经用chattr 命令锁定了该文件。

chattr：锁定文件。

lsattr：查看chattr给某些文件锁定的mode。

```
chattr 命令的用法：
chattr [ -RV ] [ -v version ] [ (+ / -)mode ] files⋯

R: 递归处理
V：显示处理过程

mode(参数):
a：(常用)即Append Only，系统只允许在这个文件之后追加数据，不允许任何进程覆盖或截断这个文件。如果目录具有这个属性，系统将只允许在这个目录下建立和修改文件，而不允许删除任何文件。
i：(常用)即Immutable，系统不允许对这个文件进行任何的修改。

A：即Atime，告诉系统不要修改对这个文件的最后访问时间。
S：即Sync，一旦应用程序对这个文件执行了写操作，使系统立刻把修改的结果写到磁盘。
b：不更新文件或目录的最后存取时间。
c：将文件或目录压缩后存放。
d：当dump 程序执行时，该文件或目录不会被dump 备份。
D: 检查压缩文件中的错误。
s：彻底删除文件，不可恢复，因为是从磁盘上删除，然后用0 填充文件所在区域。
u：当一个应用程序请求删除这个文件，系统会保留其数据块以便以后能够恢复删除这个文件，用来防止意外删除文件或目录。
t: 文件系统支持尾部合并（tail-merging）。
X：可以直接访问压缩文件的内容。
```

```
举例：
1、用chattr 命令防止系统中某个关键文件被修改：
chattr +i /etc/resolv.conf
然后用mv /etc/resolv.conf 等命令操作于该文件，都是得到Operation not permitted 的结果。vim 编辑该文件时会提示W10: Warning: Changing a readonly file 错误。
要想修改此文件就要把i 属性去掉：chattr -i /etc/resolv.conf

lsattr /etc/resolv.conf
会显示如下属性
—-i——– /etc/resolv.conf

2、让某个文件只能往里面追加数据，但不能删除，适用于各种日志文件：
chattr +a /var/log/messages
```

# 九、 管理用户账号

## 9.1 setuid & setgid

 setuid 是一种文件的拥有者具备的特殊属性，它使得被设置了setuid 位的程序无论被哪个用户启动，都会自动具有文件拥有者的权限。

setgid 与setuid 类似，只是setgid 是文件归属的组具备的特殊属性，具有setgid 的可执行文件运行时，自动获取文件对应的组权限，因为组权限不像用户权限那样精确，所以使用setgid 的程序很少。

```
▶ 用户存储用户信息的/etc/passwd 文件只有超级用户才能进行修改，而用于存储用户口令的文件/etc/shadow 甚至只有超级用户才可以访问。只有在普通用户执行passwd 命令的时候，能够读取和修改/etc/passwd 和/etc/shadow 文件，才能使普通用户修改自己的口令。为了解决在用户修改口令时，文件系统存取权限矛盾，Linux 给/usr/sbin/passwd 命令设置了setuid 属性。
▶ setuid 是一种文件的拥有者具备的特殊属性，它使得被设置了setuid 位的程序无论被哪个用户启动，都会自动具有文件拥有者的权限。在Linux 中典型拥有setuid 属性的文件就是/usr/bin/passwd 程序。通常setuid 属性只会设置在可执行的文件上，因为尽管理论上可以给不可执行的文件加上setuid 属性，但是这样做通常是没有意义的。
▶ 文件属性中的s 占据的位即为setuid 位，“s”代表对应的文件被设置了setuid 属性，因为passwd 程序的拥有者是超级用户root，因此passwd 程序执行的时候就自动获取了超级用户的权限，所以无论是哪个用户执行了passwd 程序都可以修改系统的口令文件。
```

```
【setuid】的使用
▶ 要给一个文件加上setuid 属性，可以使用如下的命令：
chmod u+s <文件名> 或chmod 4xxx <文件名>

▶ 其中，u+s 表示给文件的拥有者添加setuid 属性，其属性字为4000，xxx 代表文件原来的存取属性。setgid 与setuid 类似，只是setgid 是文件归属的组具备的特殊属性，具有setgid 的可执行文件运行时，自动获取文件对应的组权限，因为组权限不像用户权限那样精确，所以使用setgid 的程序很少。

【setgid】的使用
▶ 要给某个文件添加setgid 属性，可以命令：
▶ chmod g+s < 文件名> 或chmod 2xxx < 文件名>
其中，g+s 表示给文件的归属组添加setgid 属性，其属性字为2000，xxx 代表文件原来的存取属性。

▶ setuid 和setgid 属性都是对正常的Linux 安全机制开的后门，原则上，只有在明确的非用不可的功能中才使用它们。特别是，具有超级用户权限的setuid 属性的应用程序经常是系统遭受攻击的目标。慎用。
```


# 十、 备份和恢复

## 10.1 dump

备份分区、文件或目录。

```
dump 命令格式如下：
dump [选项] 备份之后的文件名原文件或目录

选项：
-level：就是我们说的0～9 共10 个备份级别；
-f 文件名：指定备份之后的文件名；
-u：备份成功之后，把备份时间记录在/etc/dumpdates 文件中；
-v：显示备份过程中更多的输出信息；
-j：调用bzlib 库压缩备份文件，其实就是把备份文件压缩为.bz2 格式，默认压缩等级是2；
-W：显示允许被dump 的分区的备份等级及备份时间；
```

```
dump -0uj -f /root/boot.bak.bz2 /boot/
# 备份命令。先执行一次完全备份, 并压缩和更新备份时间
DUMP: Date of this level 0 dump: Wed Jun 5 03:08:22 2013
# 备份的级别和时间
DUMP: Dumping /dev/sdal (/boot) to /root/boot.bak.bz2
# 备份源和目标
DUMP: Label: none
# 分区没有卷标
DUMP: Writing 10 Kilobyte records
DUMP: Compressing output at compression level 2 (bzlib)
```

▶ 查看备份时间文件

> cat /etc/dumpdates

> /dev/sdal 0 Wed Sep 26 18:08:22 2020 +0800


`# 备份的分区备份级别备份曰期`

▶ 如果/boot 分区的内容发生了变化，则可以使用1 级别进行增量备份。当然，如果数据会继续发生变化，则可以继续使用2～9 级别增量备份。
> dump -1uj -f /root/boot.bak1.bz2 /boot/

▶ 如果备份的是整个分区，那么是可以使用“dump -W”命令来查询分区的备份时间及备份级别的。不过要注意，如果备份时没有使用“-u”选项，那么“dump -W”命令是不会记录备份的时间和级别的。

▶ dump 命令可以非常方便地实现增量备份，但如果实现差异备份时，先使用0 级别完全备份一次，以后的每次备份都使用1 级别进行备份。

▶ 备份文件或目录
dump 命令也可以文件或目录，不过，只要不是备份分区，就只能使用0 级别进行完全备份，而不再支持增量备份。同时，不能使用“-u”选项更新分区的备份时间，当然也不能使用“dump -W”命令查询到文件或目录的备份。
> dump -0j -f /root/etc.dump.bz2 /etc/

▶ 使用增量备份命令
> dump -1j -f /root/etc.dump1.bz2 /etc/

> DUMP：Only level 0 dumps are allowed on a subdirectory

> DUMP：The ENTIRE dump is aborted.

`# 备份失败，目录备份只能使用0 级别`

## 10.2 restor

还原dump 操作备份下的文件、目录或分区

dd 命令：数据备份，并在备份过程中进行格式转换

restore 命令：还原dump 操作备份下的文件、目录或分区

restore 命令是dump 命令的配套命令，dump 命令是用来备份分区和数据的，而restore 命令是用来恢复数据的。
```
restore命令的格式如下：
restore [模式选项] [选项]

restore 命令常用的模式有以下4 种，这4 种模式不能混用：

-C：比较备份数据和实际数据的变化。如果实际数据中的现有数据发生了变化，那么这个选项能够检测到这个变化。但是如果实际数据中新增了数据，这个选项是不能检测到变化。
-i：进入交互模式，手工选择需要恢复的文件；
-t：查看模式，用于查看备份文件中拥有哪些数据；
-r：还原模式，用于数据还原；
```
# 十一、 文件压缩与解压缩

## 11.1 zip&unzip 

dd 命令：数据备份，并在备份过程中进行格式转换
zip 与 unzip: 压缩与解压

```
zip 与 unzip
(1)压缩单个文件
a. 到临时目录下进行操作，cd /tmp

b. 生成10M 大小的空洞文件test.tmp
dd if=/dev/zero of=./test.tmp count=1 bs=10M

c. 可以循环复制10 次test.tmp，分别生成为
test1.tmp,test2.tmp ...
for i in ‘seq 1 10‘;do cp test.tmp test$i.tmp;done;

d.zip test test.tmp
执行zip 压缩后，发现，出现test.zip 文件。

(2) 压缩多个文件和目录到一个压缩文件中
zip -r myzip test.tmp test1.tmp test2.tmp

(3) 解压缩myzip 文件到当前目录
unzip myzip
```

## 11.2 gzip

使用gzip 来压缩文件，使用gunzip 来解压缩文件，gzip 其压缩命令与解压缩命令gunzip 实际上是同一个程序，文件的大小和参数完全一样，只是命令的名称不同。文件会被压缩，并被保存为filename.gz。当解压缩时，filename.gz 会被删除，同时filename 被还原。
对比zip，gzip 有以下特点：

(1)zip 命令具有将许多文件与目录压缩成一个文件的功能，
但gzip 却不能；
(2) 用gzip 命令压缩后源文件会被删除。

```
(1) 压缩单个文件。
cp /etc/man.config .
gzip man.config
使用ls -l 查看结果时，man.config 消失，多了一个
man.config.gz 文件。

(2) 压缩多个文件。
touch a b
gzip a b
ls -l
对比发现gzip 可以一次压缩许多文件，但不可以压缩目录，
也不可以将许多文件与目录压缩成一个文件
```

## 11.3 tar

tar 是Linux 常用的归档命令，更多是用于硬盘数据备份。
tar 可以对文件和目录进行打包。

利用tar，用户可以对某一特定文件进行归档（一般用作备份文件），也可以在包中改变文件，或者向包中加入新的文件。

归档不同于压缩。归档文件是一个文件和目录的集合，而这个集合被贮存在一个文件中。归档文件没有经过压缩，它所使用的磁盘空间是其中所有文件和目录的总和。压缩文件也是一个文件和目录的集合，且这个集合也被贮存在一个文件中，但是，它的贮存方式使其所占用的磁盘空间比其中所有文件和目录的总和要少。归档文件不是压缩文件，但是压缩文件可以是归档文件。

```
格式：tar [选项] [文件目录列表]
功能：对文件目录进行打包备份
选项：
-c 建立新的归档文件
-r 向归档文件末尾追加文件
-x 从归档文件中解出文件
-O 将文件解开到标准输出
-v 处理过程中输出相关信息
-f 对普通文件操作
-z 调用gzip 来压缩归档文件，与-x 联用时调用gzip 完成解
压缩
-Z 调用compress 来压缩归档文件，与-x 联用时调用
compress 完成解压缩
```

```
tar 示例
（1）将/home 目录下所有文件打包成test.tar。
tar -cvf test.tar /home/* 注意扩展名.tar 需自行加上。
（2）将所有文件打包成test1.tar, 再用gzip 命令压缩：
tar -zcvf test1.tar.gz /tmp/*
（3）查看test.tar 文件中包括了哪些文件
tar -tf test.tar
（4）将text1.tar 解压缩
tar -xvf test.tar
（5）将text1.tar.gz 解压缩
tar -zxvf test.tar
```






