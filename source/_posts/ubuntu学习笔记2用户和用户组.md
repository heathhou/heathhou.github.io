---

title: ubuntu学习笔记2用户和用户组
date: 2020-09-16 14:42:17
categories: 
- linux
- ubuntu
- 学习笔记
---

<!-- more -->

# 一、常用命令

1. tail -n 5 /etc/group	查看最后5个用户组
2. tail -n 5 /etc/passwd	查看最后5个用户
3. id user1 查看user1的uid与组与附加组
4. su - stu2 : 进入stu2的身份
5. sudo passwd stu2 : 为用户stu2创建密码
6. openssl passwd : 产生密码(加盐，重复，效果也不一样)
7. echo -n 34 ： 回音，会返回34
8. echo -n 34 |openssl passwd -1 -stdin 产生密码（密码是34）(-1 代表加密方式)(加盐，重复，效果也不一样)
9. sudo useradd -N -g sudo -m -p 'echo -n hadoop|openssl passwd -1 -stdin' hadoop
10. 批量加入用户和密码：
11. sudo newusers < createUser.user  ： 重定向输入，将createUser.user输入到newusers



# 二、 用户和用户组

1. 在Linux 中，每个用户必须有一个主组。当创建账号时，系统会自动创建一个同名组作为该账户的主组。用户必须属于一个且只有一个主组。用户可以属于零个或者多个附加组。

2. 每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同Linux 系统对用户组的规定有所不同，如Linux 下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建。用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对/etc/group 文件的更新。

## 2.1 文件

在Linux 中，万物皆文件，所以用户与组也以配置文件的形式保存在系统中，以下为用户和组的主要配置文件详解：
```
/etc/passwd：用户及其属性信息(名称、UID、主组ID 等）
/etc/group：组及其属性信息
/etc/shadow：用户密码及其相关属性
/etc/gshadow：组密码及其相关属性
```

### 2.1.1 passwd

 用户账号文件。

该文件用于用户登录时校验用户的登录名、加密的口令数据项、用户ID(UID)、默认的用户分组ID(GID)、GECOS 字段、用户登录子目录。
1. 该文件的每一行保存一个用户的资料，以及登录后使用的shell; 而用户资料的每一个数据项之间采用冒号分隔。
2. 
```
 wl:x:1000:1000:wanglei„,:/home/wanglei:/bin/bash
```
3. ![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929220028.png)
▶ 1、登录名唯一性，它的长度一般不超过32 个字符，它们可以包括冒号和换行之外的任何字符。登录名要区分大小写。放在etc/passwd 文件的开头部分的用户是系统定义的虚拟用户bin、daemon。

▶ 2、加密的口令当编辑/etc/passwd 文件来创建一个新账号时，在加密口令字段的位置用x 代替。表示是一个经过加密处理的口令，加密后的密码放置在/etc/shadow 文件中，且该文件只能被root 组的账号访问。如果该字段显示“*”则表示对应账号停用。

▶ 3、UID 每个账号唯一的识别号，最大值为65535。UID 在500 之前的账号是提供系统服务使用的，管理员新增的第一个普通用的UID 为500，然后依次是501、502⋯以此类推。

▶ 4、GID 组账号的唯一的识别号。用户组的信息被存放在/etc/group 文件中，root 组的GID 为0。管理员创建的第一个组的GID 为500，然后依次是501、502⋯以此类推。

▶ 5、GECOS 字段通常用来定义每个用户的个人信息。

▶ 6、用户的登录子目录用户登录后直接进入的目录，在默认的状态下，每个用户都有一个主目录。root 用户的主目录为/root，管理员创建的用户的主目录通常为/home/< 用户名>，如tom 用户主目录为/home/tom。

▶ 7、登录shell 用户登楼后运行的shell，此处出现的是默认的shell，大多数情况下是/bin/bash。如果用户只是系统通过该用户账号获取系统的某种服务，而不希望该用户能够登录Linux 工作站，可以将此登录shell 修改为/bin/false、/bin/true、/dev/null 和/sbin/nologin 等其中之一。

``查看/etc/passwd 的内容:cat /etc/passwd``

### 2.1.2 shadow

保存用户账号的密码。

每行记录了一个合法用户账号的数据。

▶ 在Linux 系统中通常使用影子口令机制（Shadow Password），用户的身份信息被存放在/etc/passwd 文件中，用户的口令信息加密后保存在另一个文件/etc/shadow 中，并只设置root 账号的可读属性，因而大大提高了系统的安全性能。

▶ Linux/Unix 采用了“shadow 文件”机制，将加密的口令转移到/etc/shadow 文件里，该文件为root 超级用户可读，同时/etc/passwd 文件的密文域显示一个x，从而最大限度地减少了密文泄漏的机会。

▶ 加密后的密码可以分为三段来看，被$ 分割。其中第一段就是表明散列算法的类型，第二段是系统为们密码添加的盐值(salt), 最后第三段才是映射完的散列值。

▶ 其中6 代表的是采用SHA-512 算法进行加密的。1 代表的是MD5 算法，5 代表的是SHA-256 算法等。
▶ sudo passwd root
Enter new UNIX password: (设置root 密码)
Retype new UNIX password: (重复密码)

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929220347.png)

▶ 在/etc/shadow 文件中有9 个字段，每个字段使用“:”分隔。
▶ username：passwd：lastchg: min: max: warn: inactive:
expire:flag

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929220430.png)


![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929220450.png)

▶ 将原本/etc/passwd 文件中的密码移至/etc/shadow 文件中，而shadow 文件只允许管理员root 账户读取，可以提高系统的安全性。而且其中的密码是采用MD5 算法加密的，root账户也无法直接获得口令的内容，但是root 账户可以变更用户密码或停用每个账户。

▶ 可记录密码变更的时间。

▶ 可以设置密码使用的时间，以避免用户的密码变更过于频繁。

▶ 可以使用/etc/login.defs 文件来设置密码的安全性原则，例如密码的最小长度或密码最短的使用时间等。

### 2.1.3 group



### 2.1.4 gshadow



## 2.2 常用命令



### 2.2.1 groupadd

添加用户组。


   ```
-g 指定组ID号
-r 建立系统组账号，即组ID低于GID_MIN
-G 指定附加组
-o 允许设置相同组id的群组，不必唯一
-f 强制执行，创建相同id的组
   ```

1. sudo groupadd -g 2020 mygroup 	新建用户组（指定gid）
2. sudo groupadd testgroup	新建用户组(没有指定gid) 会自动根据上一次组的编号加1
3. sudo groupadd -r group1	新建系统组账号  -r : 用来建立系统工作组，-r 创建的GID 会比定义在系统文件上/etc/login.defs 中的GID_MIN 小。
4. tail -n 5 /etc/group	查看最后5个用户组
5. tail -n 5 /etc/passwd	查看最后5个用户

### 2.2.2 groupdel

groupdel 命令用于删除指定的工作组，命令要修改的系统文件包括/ect/group 和/ect/gshadow。若该组中包括某些用户，则必须先删除这些用户后，方能删除组。

1. sudo groupdel 组名
2. sudo groupdel group1    删除组group1（不能有用户）

### 2.2.3 groupmod

1. groupmod 命令更改群组识别码或名称。
2. groupmod –n 新组名旧组名。
3. groupmod -g 新gid 旧gid。
4. groupmod -go gid 新组名。
   例：sudo groupmod -go 8888 group3，将组group3 的gid 限
   制为8888，而8888 已经存在，并且8888 是另外一个组的
   gid 编号。此时，两个组共用同一个gid 编号。

```
-g 指定GID
-n 修改用户组名
-o 与groupadd相同，重复使用群组识别码
-p 为组设置密码
-R 修改根目录
```



### 2.2.4 groups

groups 用户名 ： 显示用户所属的用户组

### 2.2.5 newgrp

newgrp 组名 ： 切换用户所在用户组，登入另一个群组。使用newgrp 指令切换群组，必须是该群组的用户，否则将无法登入指定的群组。

### 2.2.6 gpasswd

用来管理组。

gpasswd 命令是Linux 下工作组文件/etc/group和/etc/gshadow 的管理工具，用于指定要管理的工作组。

```
-a : 添加用户到组
-d : 从组删除用户
-A：指定管理员
-M：指定组成员和-A 的用途差不多；
-r：删除密码；
-R：限制用户登入组，只有组中的成员才可以用newgrp 加入该组。
```

1. gpasswd -d stu2 student 将用户stu2 从student 组删除
2. gpasswd –a stu2 student 将用户stu2 添加到student 组
3. gpasswd -A stu2 student : 指定stu2为组student的管理员
4. su - stu2 : 进入stu2的身份
5. gpasswd -a stu3 student : 在stu2用户下使用此命令，将stu3加入studnet组，不需要root权限。

### 2.2.7 adduser

创建新用户。一问一答式。

### 2.2.8 useradd

创建新用户。

useradd 命令的使用格式:useradd [参数] 新建用户账号

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929220648.png)

```
-b, --base-dir BASE_DIR       新账户的主目录的基目录
-c, --comment COMMENT         新账户的 GECOS 字段
-d, --home-dir HOME_DIR       新账户的主目录
-D, --defaults                显示或更改默认的 useradd 配置
-e, --expiredate EXPIRE_DATE  新账户的过期日期
-f, --inactive INACTIVE       新账户的密码不活动期
-g, --gid GROUP               新账户主组的名称或 ID
-G, --groups GROUPS           新账户的附加组列表
-h, --help                    显示此帮助信息并退出
-k, --skel SKEL_DIR           使用此目录作为骨架目录
-K, --key KEY=VALUE           不使用 /etc/login.defs 中的默认值
-l, --no-log-init             不要将此用户添加到最近登录和登录失败数据库
-m, --create-home             创建用户的主目录
-M, --no-create-home          不创建用户的主目录
-N, --no-user-group           不创建同名的组
-o, --non-unique              允许使用重复的 UID 创建用户
-p, --password PASSWORD       加密后的新账户密码
-r, --system                  创建一个系统账户
-R, --root CHROOT_DIR         chroot 到的目录
-s, --shell SHELL             新账户的登录 shell
-u, --uid UID                 新账户的用户 ID
-U, --user-group              创建与用户同名的组
-Z, --selinux-user SEUSER     为 SELinux 用户映射使用指定 SEUSER
	--extrausers              Use the extra users database

```

1. sudo useradd -m -d /home/test  -G student,sudo -c "hello" -s "/bin/bash" -e "2025-1-1"  stu2 

   建立stu2 账号，其主目录为/home/stu2、归属于student组、账号信息为general user、用户shell 为/bin/bash、账号有效期到2025 年12 月1 日。

2. sudo passwd stu2 : 为用户stu2创建密码

3. openssl passwd : 产生密码(加盐，重复，效果也不一样)

4. echo -n 34 ： 回音，会返回34

5. echo -n 34 |openssl passwd -1 -stdin 产生密码（密码是34）(-1 代表加密方式)(加盐，重复，效果也不一样)

6. sudo useradd -N -g sudo -m -p 'echo -n hadoop|openssl passwd -1 -stdin' hadoop

   创建用户hadoop，设置密码为hadoop，同时加入sudo主组，同步创建家目录。要求创建用户的同时设立密码。

7. 批量加入用户和密码：

- 新建createUser.user，

  ![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929221711.png)

- sudo newusers < createUser.user 

- 创建密码文件myPasswd.pwd

  ![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929221723.png)

- sudo chpasswd < myPasswd.pwd

- 注：linux 中，文件后缀名不重要。养成文件加后缀名的习
  惯，可以更好地让使用者区分文件类型。

### 2.2.9 userdel 

userdel  用户名 ： 删除用户

userdel -r 用户名 ： 删除用户的同时，将用户家目录和邮件池一并删除

### 2.2.10 passwd

passwd 用户名 ： 修改用户名密码的信息 

passwd 命令后面不接任何参数或用户名，则表示修改当前用户的密码。

```
-l 锁定指定的账户
-u 解锁被指定的账户
-a	报告所有账户的密码状态
-aS 用户名 ： 查看用户密码信息
```
![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929222156.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/ubuntu常用命令/20200929222118.png)


### 2.2.11 openssl passwd

```
-salt
```

Linux 系统中，用户可以利用openssl passwd 手动生成一个密码作为用户账号的密码。openssl passwd 用来计算密码hash 值。
▶ 语法格式：openssl passwd [option] passwd
▶ -1: 用MD5 加密算法
▶ -salt: 加盐，不使用随机产生的salt。-salt 不需要交互确认，
取盐的前两位，若盐相同，则加密密码相同。
▶ openssl passwd
▶ password:
▶ verifying -password:
▶ 生成：tTGWmli4MjAhM(每次都不一样)
▶ sudo usermod -p tTGWmli4MjAhM xx 用户名

▶ openssl passwd 12345
▶ openssl passwd 12345
▶ 没有使用参数，则表示使用默认的-crypt 加密。每次加密结
果均不同。
▶ openssl passwd -salt ’thisispasswd’ 123456
▶ openssl passwd -salt ’thisispasswd’ 123456
▶ salt:thisispasswd 要加密的密码：123456 则上面两条命令结
果相同。（只取盐值的前两位）

### 2.2.12 su & su - 

```
su
su - 
su 和su –命令不同之处在于，su -切换到对应的用户时会将当前的工作目录自动转换到切换后的用户的主目录。
```

### 2.2.13 id

id 用户名 

查看用户和用户组的信息

### 2.2.14 finger

finger 用户名

查看用户信息

### 2.2.15 w&who&whoami

▶ w: 显示所有登录用户，在干什么
▶ who: 显示登录用户
▶ whoami: 显示当前用户名称

### 2.2.16 usermod

```
usermod –L 用户名（同passwd –l 用户名锁定用户）
usermod –U 用户名（同passwd –u 用户名解除锁定）
usermod –l 新用户名 旧用户名
usermod –md home 目录用户名(修改用户home)

usermod -G 组名用户名(将用户加入附加组中，该附加组会成为唯一的附加组，之前该用户所加入的其他附加组全部清空)

usermod –a –G 附加组1，附加组2⋯ 用户（把用户加入多个附加组中，不会清空之前加入的附加组）

gpasswd -a 用户组名（将用户加入到组中）
gpasswd –d 用户组名(将用户student 从stu2 组中移除)

usermod -c ” 用户说明” 用户名
usermod -u 新uid 用户名（修改用户id）
usermod –g 新gid 组名（修改用户组，新组id 要存在）
usermod –e 2030-12-12 用户名(指定账号过期时间)
usermod -f 0 用户名（指定账号密码过期多少天后，禁用该账号，0 表示密码刚过期就禁用帐号）
```



### 2.2.17 gpasswd&usermod

1. gpasswd -a

   - 每次只能为用户增加一个附加组，会保留原有的附加组。

2. gpasswd -d

   - 将用户从一个指定的附加组中删除。

3. usermod -aG

   - 为用户指定若干个附加组，会保留原有的附加组。

4. usermod -G

   - 为用户指定一个附加组，同时会自动清除原有的所有的附加组。

