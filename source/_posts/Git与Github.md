---
title: Git与Github
date: 2020-03-18 16:10:03
tags: 实用技术
---

本文记录了Git与Github相关的一些操作
<!-- more -->

# Git具体命令

1. 安装Git
2. 在命令行输入 git 用来检测 Git 是否安装成功
3. git init  初始化 git 仓库
4. git add  提交到缓存区
   - git add 1.txt 将1.txt提交到缓存区
5. git commit 提交到工作区
   - git commit -m "first commit"  commit 是提交的意思，-m 代表是提交信息，进行提交
6. git remote add origin git@github.com:heathhou/gitdemo.git 
   - origin 在以后就可以代表  git@github.com:heathhou/gitdemo.git 
7. git push origin master 提交到远程仓库
8. git status   查看状态
9. git reset xxx 回滚版本
   - git reset --mixed xxx （默认）归档区 和 缓冲区
   - git reset --hard xxx 归档区 缓冲区 和 工作区
   - git reset --soft xxx 归档区
   - xxx --> 操作所对应的哈希值
10. git log  查看所有产生的 commit 记录
11. git reflog 查看提交的操作
12. git revert xxx 撤销某次提交的操作
    - xxx --> 操作所对应的哈希值
13. git add & git commit
14. git branch  查看分支
    - git branch  -v  （默认）查看有哪些分支
    - git branch a  创建a分支
15. git checkout 切换分支   
    - git checkout a  切换到 a 分支上
    - git checkout -b a  先新建再切换，未免有点麻烦，可以一步到位的
16. git merge xxx 合并分支
    - git merge b1 将b1分支合并到当前分支
    - xxx --> 某一分支
17. git branch -d  删除分支
18. git branch -D  强制删除分支
19. git tag  贴标签
20. git pull  （将本地更新到远程仓库一致）拉取远程仓库最新的版本并将远端同名分支合并到本地分支
21. git fetch 获取远端的更新





# 向Github提交代码

1. SSH
   - Linux 与 Mac 都是默认安装了 SSH ，而 Windows 系统安装了 Git Bash 应该也是带了 SSH
     的。大家可以在终端（win下在 Git Bash 里）输入 ssh查看是否安装了ssh.
   
2. 生成SSH key
   
   > ssh-keygen -t rsa -C "you_email@your_email.com"
   
     这个email是几在github上注册的email
     默认两次回车（确认路径和密码）
     你也可以设置密码，这里两次回车是设置没密码
   
3. GitHub上添加SSH key

   找到这个地址，将id_rsa.pub用记事本打开并复制里面的内容：

    ![](https://img2018.cnblogs.com/blog/1015208/201812/1015208-20181226115814812-1021312262.png)

   打开GitHub网站：

   

   ![](https://img2018.cnblogs.com/blog/981453/201908/981453-20190813153201526-547325296.png)

   

4. Push&Pull
   - git push origin master  把本地代码推到远程 master 分支
   - git pull origin master  把远程最新的代码更新到本地
   - 一般我们在 push 之前都会先 pull ，这样不容易冲突。

5. 提交代码

   - Clone自己的项目  ,例如输入：

   > git clone git@github.com:stormzhang/test.git  

   这样就把 test 项目 clone 到了本地，你可以把 clone 命令理解为高级点的复制，这个时候该项目本身就已经是一个git 仓库了，不需要执行 git init 进行初始化，而且甚至都已经关联好了远程仓库，我们只需要在这个 test 目录下任意修改或者添加文件，然后进行 commit ，之后就可以执行：

   >  git push origin master  

   进行代码提交

   - 假设我们本地有个 test2 的项目，我们需要的是在 GitHub 上建一个 test 的项目，然后把本地
     test2 上的所有代码 commit 记录提交到 GitHub 上的 test 项目。

     - 在 GitHub 上建一个 test 项目
     
     - 把本地 test2 项目与 GitHub 上的 test 项目进行关联，切换到 test2 目录，执行如下命
       令：
     
       - > git remote add origin git@github.com:stormzhang/test.git
         >

   什么意思呢？就是添加一个远程仓库，他的地址是 git@github.com:stormzhang/test.git ，
   而 origin 是给这个项目的远程仓库起的名字，是的，名字你可以随便取，只不过大家公认的只有一个远程仓库时名字就是 origin ，为什么要给远程仓库取名字？因为我们可能一个项目有多个远程仓库？比如 GitHub 一个，比如公司一个，这样的话提交到不同的远程仓库就需要
   指定不同的仓库名字了。
        

- 查看我们当前项目有哪些远程仓库可以执行如下命令：

> git remote -v

- 接下来，我们本地的仓库就可以向远程仓库进行代码提交了：

> git push origin master 

- 友情提醒，在提交代码之前先要设置下自己的用户名与邮箱，这些信息会出现在所有
的 commit 记录里，执行以下代码就可以设置：

> git config —global user.name "stormzhang"
> git config —global user.email "stormzhang.dev@gmail.com" 



# Git 进阶

1. 用户名和邮箱

   - >git config --global user.name "ZhugeBorrowedSword"
      >git config --global user.email "bhcbfx@163.com"
      
      以上进行了全局配置，当然有些时候我们的某一个项目想要用特定的邮箱，这个时候只需切
      换到你的项目，以上代码把 --global 参数去除，再重新执行一遍就ok了。
   
2. alias  起别名

   - > git config --global alias.co checkout # 别名
     > git config --global alias.ci commit
     > git config --global alias.st status
     > git config --global alias.br branch 
   - > git commit    git ci
     > git checkout    git co
     > git branch    git br
     > git status    git st
     
   - 当然以上别名不是固定的，你完全可以根据自己的习惯去定制，除此之外还可以设置组合，比如：
   
     > git config --global alias.psm 'push origin master'
     > git config --global alias.plm 'pull origin master'
     >
     > git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
   
3. 其他配置

   - > git config --global color.ui true # 开启颜色
     >
     > git config --global core.quotepath false # 设置显示中文文件名

4. diff

   - > diff命令算是很常用的，使用场景是我们经常在做代码改动，但是有的时候2天前的代码了，做了哪些改动都忘记了，在提交之前需要确认下，这个时候就可以用diff来查看你到底做了哪些改动

5. checkout

   - 切换分支
   - 切换tag
   - 撤销

6. stash

   设想一个场景，假设我们正在一个新的分支做新的功能，这个时候突然有一个紧急的bug需要
修复，而且修复完之后需要立即发布。当然你说我先把刚写的一点代码进行提交不就行了
   么？这样理论上当然是ok的，但是这会产品垃圾commit，原则上我们每次的commit都要有实
际的意义，你的代码只是刚写了一半，还没有什么实际的意义是不建议就这样commit的，那
   么有没有一种比较好的办法，可以让我暂时切到别的分支，修复完bug再切回来，而且代码也
能保留的呢？
   
   这个时候 stash 命令就大有用处了，前提是我们的代码没有进行 commit ，哪怕你执行了
   add 也没关系，我们先执行
   
   > git stash 
   
   命令，什么意思呢？意思就是把当前分支所有没有 commit 的代码先暂存起来，这个时候你再
   执行 git status 你会发现当前分支很干净，几乎看不到任何改动，你的代码改动也看不见
   了，但其实是暂存起来了。执行
   
   > git stash list
   
   你会发现此时暂存区已经有了一条记录。
   这个时候你可以切换会其他分支，赶紧把bug修复好，然后发布。之后一切都解决了，你再切
   换回来继续做你之前没做完的功能，但是之前的代码怎么还原呢？
   
   > git stash apply
   
   你会发现你之前的代码全部又回来了，就好像一切都没发生过一样，紧接着你最好需要把暂
   存区的这次 stash 记录删除，执行：
   
   > git stash drop
   
   就把最近一条的 stash 记录删除了，是不是很方便？其实还有更方便的，你可以使用：
   
   > git stash pop
   
   来代替 apply 命令，pop 跟 apply 的唯一区别就是 pop 不但会帮你把代码还原，还自动帮你
   把这条 stash 记录删除，省的自己再 drop 一次了，为了验证你可以紧接着执行 git stash
   list 命令来确认是不是已经没有记录了。
   最后还有一个命令介绍下：
   
   > git stash clear
   
   就是清空所有暂存区的记录，drop 是只删除一条，当然后面可以跟 stash_id 参数来删除指
   定的某条记录，不跟参数就是删除最近的，而 clear 是清空。
   
   
   
7. merge & rebase
   我们知道 merge 分支是合并的意思，我们在一个 featureA 分支开发完了一个功能，这个时候需要合并到主分支 master 上去，我们只需要进行如下操作：
   
   - > git checkout master
      > git rebase featureA
   
   rebase 跟 merge 的区别你们可以理解成有两个书架，你需要把两个书架的书整理到一起
   去，第一种做法是 merge ，比较粗鲁暴力，就直接腾出一块地方把另一个书架的书全部放进
   去，虽然暴力，但是这种做法你可以知道哪些书是来自另一个书架的；第二种做法就是
   rebase ，他会把两个书架的书先进行比较，按照购书的时间来给他重新排序，然后重新放置
   好，这样做的好处就是合并之后的书架看起来很有逻辑，但是你很难清晰的知道哪些书来自
   哪个书架的。
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ​		

