---
title: BlogBackup
date: 2020-06-19 16:53:34
tags: 实用技术
categories: 博客
---

本文章的目的：万一写的博客丢失了，或者换电脑了，应该如何恢复我的博客。

<!-- more -->

# 前提：

已经使用GitHun搭建好了hexo博客

# 1. 搭建流程

2. 在仓库heathhou.github.io里创建两个分支:master和hexosource。master用于存储静态网页，hexosource用于备份本地博客的内容。如图：

   ![](https://cdn.jsdelivr.net/gh/heathhou/image_store/实用技术/BlogBackup/20200619170552.png)

3. 设置hexosource为默认分支(注意这个分支保存的是网站源文件，并不是生成后上传github上用于显示的)

   ![](https://cdn.jsdelivr.net/gh/heathhou/image_store/实用技术/BlogBackup/20200619171146.png)

4. 新建一个文件夹，用来下载此项目。万一博客文件丢失或者换电脑，好恢复博客。我新建的文件夹是**my_hexo_blog_git**

5. 使用git在**my_hexo_blog_git**文件夹内执行下面的命令，将此项目下载到**my_hexo_blog_git**这个文件夹内。

   > git clone git@github.com:heathhou/heathhou.github.io.git

6. 修改_config.yml中的deploy参数，将本地博客迁移到github上(一般下载下来就是对的)。

   ![](https://cdn.jsdelivr.net/gh/heathhou/image_store/实用技术/BlogBackup/20200619172431.png)

7. 终端进入heathhou.github.io目录，执行这条语句

   > npm install hexo-deployer-git --save

8. 搭建完成



# 2. 日常操作

1. 用markdown写文章，保存到/source/_posts目录下。一顿操作猛如虎。

   ```
   hexo new "test1"
   hexo clean
   hexo g
   hexo s
   hexo d
   ```

   

2. 备份本地hexo博客

   ```
   git config core.autocrlf false (出现下面错误的话在执行这条语句)
   git add .
   git commit -m "恢复blog"
   git push origin hexosource
   ```

   

如果出现如下错误：

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/实用技术/BlogBackup/20200619173235.png)

就先执行下条语句：

   > git config core.autocrlf false



# 3.恢复头像图片

1. 新建一个文件夹，我这里是**my_hexo_image_store**

2. 进入**my_hexo_image_store**文件夹

3. 使用git执行下面的命令来下载文件

   > git clone -b blog_assets git@github.com:heathhou/image_store.git

4. 将下载的文件复制到**my_hexo_blog_git\heathhou.github.io\themes\yilia\source**里面去

5. 删除**my_hexo_image_store**文件夹

6. hexo一顿操作
