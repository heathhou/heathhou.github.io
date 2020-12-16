---
title: Ubuntu学习笔记4磁盘管理
date: 2020-10-21 19:37:17
tags: [linux,ubuntu,学习笔记]
declare: true
---

<!-- more -->

# 一、 存储结构和磁盘划分


▶ Linux 系统中一切都是文件，那么硬件设备肯定也不例外。既然是文件就必须有名称，系统内核的udev 设备管理器会自动把硬件名称规范起来，目的是让运维人员可以通过设备文件的名字猜出设备大致的属性以及分区信息等，对于陌生的设备这点特别的方便，另外udev 服务会一直以守护进程的形式运行并侦听来自内核发出的信号来管理/dev 目录下的设备文件。

▶ 现在的IDE 设备已经很少见，所以一般硬盘设备都会是以“/dev/sd”开头的，而一台主机上可以有多块硬盘，因此系统便会用a-p 来代表16 块不同的硬盘（默认从a 开始分配）。主分区或扩展分区的编号从1 开始至4 结束，逻辑分区编号从5 开始。

▶ 例如：
/dev/sda1
dev: 硬件设备文件所在的目录
hd：表示IDE 设备，sd：表示SCSI 设备
a、b、c⋯：表示硬盘的顺序号
1、2、3⋯：表示分区的顺序号




▶ FHS 文件系统层次结构标准协定（Filesystem HierarchyStandard）是工程师在Linux 系统中存储文件的时候需要遵守的规则，FHS 是根据以往无数Linux 系统用户和开发者的经验而总结出来的，指导用户应该把文件保存到什么位置，以及告诉运维人员应该在何处找到所需的文件。

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/20201021194800.png)

▶ 硬盘设备则是由大量的扇区组成的，其中第一个扇区最重要，它里面保存着主引导记录与分区表信息。单个扇区容量为512bytes 组成，主引导记录需要占用446bytes，分区表的为64bytes，结束符占用2bytes(存放55 AA)，而其中每记录一个分区信息需要16bytes，这最多四个能被写到第一个扇区中的分区信息就叫做主分区。

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/20201021195919.png)


# 二、 查看磁盘或目录的容量


## 2.1 df

df：列出文件系统的整体磁盘使用量；

```
df 参数：
-a：列出所有的文件系统，包括系统特有的/proc 等文件系统
-k：以KB 的容量显示各文件系统
-m：以MB 的容量显示各文件系统
-h：以人们较易阅读的GB,MB,KB 等格式自行显示
-H：以M=1000K 替代M=1024K 的进位方式
-T：连同该分区的文件系统名称（例如ext3）也列出
-i：不用硬盘容量，而以inode 的数量来显示
```

## 2.2 du

du：评估文件系统的磁盘使用量（常用于评估目录所占
容量）

```
du 参数：
-a : 列出所有的文件与目录容量，因为默认仅统计目录下面
的文件量而已；
-h : 以人们较易读的容量格式（G/M）显示；
-s : 列出总量，而不列出每个个别的目录占用了容量；
-S : 不包括子目录下的总计，与-s 有点差别；
-k : 以KB 列出容量显示；
-m : 以MB 列出容量显示。
```

```
sudo du -hs /home/wl
sudo du -sm /var/log* | sort -nr |head
```


# 三、 磁盘的分区和格式化



## 3.1 在虚拟机中增加一块硬盘

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/linux/ubuntu学习笔记3磁盘管理/20201021210848.png)


## 3.2 启动虚拟机，查看磁盘

`ls –l /dev/sd*`

发现新增磁盘sdb

## 3.3 方式1 : 使用fdisk分区

### 3.3.1 对sdb 进行分区

`fdisk /dev/sdb`

### 3.3.2 分区步骤
```
输入：n，表示new 新增
输入分区号：1
输入起始扇区号：回车
输入结束扇区号：+5G

输入：p：查看分区

输入：n，继续新增分区
输入起始扇区号：回车
输入结束扇区号：回车

输入：p: 查看分区
输入：n: 新建分区
输入：d: 删除分区
输入：q: 不保存退出
输入：w: 保存退出

输入n之后：
输入：p: 新增普通分区
输入：e: 新增扩展分区
```

### 3.3.3 查看sdb 磁盘分区情况

`ls –l /dev/sd*`

注意：在没有执行w 命令确认分区之前，可以使用d 命令
删除指定分区。


## 3.4 方式2 : 使用parted分区

### 3.4.1 使用parted 进行分区
```
1、parted 支持用户在大于2TB 的硬盘上创建硬盘分区，但fdisk 命令不支持。
2、parted 支持更多的分区表类型，包括GPT （全局唯一标识分区表）。
3、允许用户调整分区大小。
注：parted 是一个操作硬盘分区的程序。它支持多种分区表类型，包括MS-DOS 和GPT。它允许用户创建、删除、调整、缩减、移动和复制分区，以及重新组织硬盘的使用，复制数据到新的硬盘上。
```

```
1、新增一块10G 大小虚拟硬盘。
2、sudo parted –l
查看所有可用硬盘的名字、储存空间型号、扇区大小、硬盘标志以及分区信息。
```

▶ parted 有两种方法创建分区，一种是交互式方法，另一种是命令。


### 3.4.2 交互式方法分区

分区前，应该先设置磁盘标签。

在磁盘sdb 上，创建一个5G 大小的分区
```
sudo parted /dev/sdb    // 对sdb进行分区
mklabel gpt             //使用gpt分区方式
unit GB                 //划分单位

mkpart                  //进行分区

primary                 //名称
ext4                    //格式化类型
0GB                     //开始位置
5GB                     //结束位置
print                   //打印输出
```

▶ 使用parted 删除分区：rm 分区编号

### 3.4.3 命令方式分区

`sudo parted /dev/sdc mkpart primary ext4 5GB 10GB`

### 3.4.4 查看分区结果

`sudo parted -l`


## 3.5 格式化磁盘分区

在新增分区上，创建文件系统，方可使用磁盘分区。


`sudo mkfs.ext4 /dev/sdb1`

或

`sudo mkfs -t ext4 /dev/sdb2`

## 3.6 挂载分区mount

```
cd /mnt
sudo mkdir sdb1
sudo mkdir sdb2
sudo mount /dev/sdb1 /mnt/sdb1
sudo mount /dev/sdb2 /mnt/sdb2
```


# 四、 mount&umount

mount&umount: 挂载和卸载磁盘

## 4.1 挂载、卸载磁盘普通使用

```
挂载磁盘分区： mount
cd /mnt
sudo mkdir sdb1
sudo mkdir sdb2
sudo mount /dev/sdb1 /mnt/sdb1
sudo mount /dev/sdb2 /mnt/sdb2

解除挂载分区： umount
sudo umount /mnt/sdb1
```
## 4.2 卸载磁盘


### 4.2.1 更改挂载分区权限

新挂载分区，权限为：755。

更改分区权限:

`sudo chmod 777 /mnt/sdb1` 


或者更改分区属主属组为当前使用者：

`sudo chown wl:wl /mnt/sdb1 `



### 4.2.2 解除挂载

使用umount 命令：

`sudo umount /mnt/sdb1`



### 4.2.3 修改 /etc/fstab 配置文件

mount 挂载在重启服务器后会失效，所以，若要长久生效，必须修改/etc/fstab 配置文件。

使用下面的命令编辑 /etc/fstab：
`sudo vi /etc/fstab`

在文件最后增加如下两行，wq 保存退出即可
```
/dev/sdb1 /mnt/sdb1 ext4 defaults 0 0
/dev/sdb2 /mnt/sdb2 ext4 defaults 0 0
```

### 4.2.4 卸载磁盘

```
1、df –h 查看磁盘
2、sudo umount /dev/sdb1
3、命令仅为本次生效，重启发现磁盘重新挂载
4、修改/etc/fstab 文件即可
5、手动增加swap 空间

6. fdisk /dev/sdb  --> d
7. parted /dev/sdc --> rm
```

# 五、 手动增加swap 空间

swap 分区，即交换区。当系统的物理内存不够用的时候，就需要将物理内存中的一部分空间释放出来，以供当前运行的程序使用，那些被释放的空间可能来自一些很长时间没有什么操作的程序，这些被释放的空间被临时保存到swap 空间中，等到程序要运行时，再从swap 中恢复保存的数据到内存中。这样，系统总是在物理内存不够时，才进行swap交换。

通常情况下，swap 空间应大于或等于物理内存的大小，最小不应小于64M，通常swap 空间的大小应是物理内存的2-2.5 倍，swap 的调整对Linux 服务器，特别是Web 服务器的性能至关重要，通过调整swap，有时可以越过系统性能瓶颈，节省系统升级费用。


▶ 1、查看已有swap 空间

▶ 2、新增swap 分区空间

使用dd 创建swapfile，bs 单位bytes，也可以手动指定单位为M 或者G，count 为计数，例子为增加100M*2=200M空间。

`dd if=/dev/zero of=/tmp/swapfile bs=100M count=2`

▶ 3、格式化为swap 格式

`mkswap –f /tmp/swapfile`

▶ 4、启用该虚拟磁盘

`sudo swapon /tmp/swapfile`

▶ 5、实现开机自动挂载交换文件

`vi /etc/fstab`

增加条目/tmp/swapfile swap swap defaults 0 0

▶ 6、卸载swap 空间，删除文件

(1) swapoff 卸载增加的swap

`swapoff /tmp/swapfile`

(2) 删除文件

`rm /tmp/newdisk`


# 六、 磁盘配额

## 6.1 基础知识
▶ 当Linux 根分区的磁盘空间耗尽时，Linux 系统将无法再建立新的文件（包括程序运行的临时文件），从而出现服务程序崩溃、系统无法启动等故障现象。为了避免在服务器中出现类似的磁盘空间不足的问题，可以设置启用磁盘配额功能，对用户在指定文件系统（分区）中使用的磁盘空间、文件数量进行设置，以防止个别用户恶意或无意间占用大量磁盘空间，从而保持系统存储空间的稳定性和持续可用性。

▶ 设置用户和组配额的分配量对磁盘配额的限制一般是从一个用户占用磁盘大小和所有文件的数量两个方面来进行的。设置磁盘配额时，“某用户在系统中共计只能使用50MB 磁盘空间”，这样的限制要求是无法实现的，只能设置“某用户在/home 分区能使用30MB，在/backup 分区能使用20MB”。

▶ 磁盘配额的设置单位是分区，针对分区启用配额限制功能后才可以对用户设置，而不理会用户文件放在该文件系统中的哪个目录中，其他系统，如Unix、Windows，原理与Linux相同。

▶ 在具体操作之前，先了解一下磁盘配额的两个基本概念：软限制和硬限制。

▶ 硬限制：一个用户可拥有的磁盘空间或文件的绝对数量，绝对不允许超过这个限制。

▶ 软限制：一个用户在一定时间范围内（默认为一周，可以使用命令“edquota –t”重新设置，时间单位可以为天、小时、分钟、秒）超过其限制的额度，在不超出硬限制的范围内可以继续使用空间，系统会发出警告（警告信息设置文件为“/etc/warnquota.conf”），但如果用户达到时间期限仍未释放空间到限制的额度下，系统将不再允许该用户使用更多的空间。

## 6.2 设置磁盘配额的步骤：

### 6.2.1 大致步骤
1、查看内核是否支持配额quota；

2、安装磁盘配额工具;

3、激活分区的配额功能;

4、建立配额数据库;

5、启动分区磁盘配额功能;

6、设置用户和组磁盘配额；

7、设置宽限期。

### 6.2.2 具体步骤
1、ubuntu 系统默认没有安装quota 命令，需要自行安装。

`sudo apt-get install quota`

2、指定空闲的磁盘、阵列或者lvm，激活空间的配额功能

(1) 在虚拟机中加入一块磁盘

(2) 格式化后，挂载

(3) 查看df -h

(4) 使用mount –o 命令加入参数后，重新挂载

A、临时生效:

`sudo mount –o remount,usrquota,grpquota /mnt/sdb1`

B、永久生效

sudo vi /etc/fstab 在文件系统中加入quota 支持，在文件最后一行加入：

`/dev/sdb1 /mnt/sdb1 ext4 defaults,usrquota,grpquota 0 0`

重启服务：

`sudo /etc/init.d/quota start`

(5) 创建配额文件系统

`sudo quotackeck –cvug /mnt/sdb1`

c: 创建v：显示详细信息

u：检查用户磁盘配额信息

g：检查群组磁盘配额信息

(6) 查看磁盘sdb1 配额情况

`mount|grep sdb1`

(7) quota 服务开启与关闭

i、开启:`sudo quotaon -vug /mnt/sdb1`

ii、关闭:`sudo quotaoff -vug /mnt/sdb1`

(8) 创建用户和用户组

`sudo groupadd groupd`

`sudo useradd -g group1 user1`

(9) 指定用户或用户组配额

`sudo edquota -u user1`

设置软限制为10M，硬限制为20M，硬限制要大于软限制

(10) 设置组配额

`sudo edquota -g group1`

(11) 查看用户和组配额

`sudo quota -uvs user1`

`sudo quota -gvs group1`

(12) 更改/mnt/sdb1 挂载点的所有者和所属组

(13) 切换至user1，切换到/mnt/sdb1 目录下

(14) 使用dd 命令，创建一个12M 大小的空洞文件

`dd if=/dev/zero of=test bs=12M count=1`

(15) 查看用户配额，发现用户超过软限制，配额计时器开始计时。当计时器过期时，如果用户的使用配额一直在软限制以上，则会将软限制强制作为硬限制。

# 七、 阵列管理
