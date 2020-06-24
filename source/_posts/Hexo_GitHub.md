---
title: Hexo_GitHub
date: 2020-03-18 16:10:03
top: 3
tags: 实用技术
---

本文记录了利用Github搭建hexo博客的步骤。

<!-- more -->

# 1.安装 Node.js

[官方网站](https://nodejs.org/en/ )

一路next

# 2.安装Git

[官方网站](https://git-scm.com/downloads)

一路next

# 3. 配置Git

## （1）注册Github账号

你需要一个GitHub账号，没有的话需要注册一个

[点击这个，或者自己百度注册教程](https://jingyan.baidu.com/article/4ae03de3d6f9c53eff9e6bdd.html)

## （2）设置用户名和用户邮箱

设置用户名，输入：

>  git  config --global  user.name  "你在github上注册的用户名"

设置用户邮箱，输入：

> git  config --global  user.email  "注册时候的邮箱"

## （3）生成SSH key 

新建一个文件夹，比如我这里建了 ==my_hexo_blog==
打开你的文件夹，然后在空白处点鼠标的右键，选择 ==Git Bash Here==

我们以后所有的操作都在这个文件夹里，失败的话可以删掉重来。

> 这个Git Bash Here就相当于Linux中的终端窗口了，以后我们就用这个东东来打开终端。
>
> (不知道为什么我用Git Bash不管用，用cmd可以)

然后输入：

>  ssh-keygen -t rsa -C "you_email@your_email.com"

这个email是你在github上注册的email
默认两次回车（确认路径和密码）
你也可以设置密码，这里两次回车是设置没密码

## （4）把SSH key（公钥）连接到github上

找到这个地址，将id_rsa.pub用记事本打开并复制里面的内容：

 ![](https://img2018.cnblogs.com/blog/1015208/201812/1015208-20181226115814812-1021312262.png)

打开GitHub网站：



![](https://img2018.cnblogs.com/blog/981453/201908/981453-20190813153201526-547325296.png)



# 4.安装hexo

1. 新建一个文件夹，比如我这里建了 ==my_hexo_blog==
   打开你的文件夹，然后在空白处点鼠标的右键，选择 ==Git Bash Here==

   > 这个Git Bash下载下来就相当于Linux中的终端窗口了，以后我们就用这个东东来打开终端。
   >
   > (不知道为什么我用Git Bash不管用，用cmd可以)

2. 检测node 与 npm是否安装成功

   > node -v
   >
   >  npm -v

3. 我们需要先来安装个cnpm提高速度，以后下载什么东西都用cnpm

   > npm install -g cnpm --registry=https://registry.npm.taobao.org

4. 检测cnpm下载成功

   > cnpm
   >
   > cnpm -v

5. 正式安装hexo

   > cnpm install -g hexo-cli

6. 检测hexo 是否安装成功

   > hexo -v

7. 使用hexo搭建博客

   > hexo init # 初始化一个博客

8. 在本地启动查看博客

   > hexo s

# 5. 运行测试



新建一个markdown

> hexo new "我的第一篇博客文章"
>
> 用markdown进行编写

```
hexo clean #用来清理缓存文件
hexo g      #生成文件
hexo  s     #运行本地服务器
hexo  d   #上传到服务器
```
# 6. 将博客部署到GitHub上



新建一个github仓库，用户部署个人博客的github仓库的命名必须符合特定要求才行

> 你的github账号名称.github.io

在==my_hexo_blog==文件夹里面执行下面语句，安装一个部署的插件

> cnpm install --save hexo-deployer-git

配置==my_hexo_blog==里面的_config文件

找到Deployment，修改如下：

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
	type: git
	repo: 从github上复制过来的东西（下图中箭头所指的东西）
	branch: master
```



部署到远端：

> hexo d

常用的命令：

```
hexo new "test" # 新建名为test的md文档
hexo clean #用来清理缓存文件
hexo g      #生成文件
hexo  s     #运行本地服务器
hexo  d   #上传到服务器
```

博客已经搭建完毕，你可以到此结束，也可以继续阅读。



# 7. 备份工作

如图：

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/%E5%AE%9E%E7%94%A8%E6%8A%80%E6%9C%AF/BlogBackup/FirstBlogBackup.png)

接着可以参考这篇文章：

https://heathhou.github.io/2020/06/19/BlogBackup/