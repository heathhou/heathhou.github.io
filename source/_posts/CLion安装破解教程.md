---
title: CLion安装破解教程
date: 2020-10-09 10:46:48
tags: [软件教程,c,c++,c/c++]
declare: true
---

 2019年版本CLion安装破解教程。

 JetBrains 全家桶 2019 年版本，破解步骤都类似。

 想看2020版本的可以查看这篇文章：

 https://www.cnblogs.com/heathhou/p/14017570.html
 

<!-- more -->

# 一、下载安装包

## 1.1 方式1 百度网盘链接

链接：https://pan.baidu.com/s/1_bynfoV85BhZr_p86Gm6Uw 

提取码：sl8x

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009133351.png)

## 1.2 方式2 官网下载


https://www.jetbrains.com/clion/download/#section=windows


# 二、将下载的两个文件进行解压

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009110342.png)

# 三、安装CLion

1. 进入JetBrains CLion v2019.3.4 Winx64文件夹，双击打开JetBrains CLion v2019.3.4 Winx64.exe文件。

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009105435.png)

2. 跟着图片走

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009105513.png)



![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009105642.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009110105.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009110120.png)

3. 等待安装过程。

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009110233.png)

4. 跟着图片走

如下图所选的话电脑会重启。

 ![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009110700.png)

不想现在重启电脑的话就选择下面的“I want to manually reboot later.”，然后点击finsh。

5. 关闭CLion.

# 四、打开CLion软件

1. 打开CLion软件。

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009111818.png)

2. 跟着图片走

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009111935.png)


![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009112035.png)


![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009112055.png)


![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009112118.png)


![](https://gitee.com/heathhou/image_store/raw/master/分类/c/Clion/image-20201009113503823.png)


![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009120428.png)


3. 关闭CLion。

# 五、破解CLion

1. 将第二步解压的jetbrains-agent文件夹里面的文件jetbrains-agent.jar复制到IDE安装路径⽬录下。

 ![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009122352.png)

2. 启动CLion。

3. 跟着图片走 

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009120617.png)

4. 在打开的vmoptions编辑窗⼝末⾏添加：

`-javaagent:/absolute/path/to/jetbrains-agent.jar`

一定要自己确认好路径，填错会导致IDE打不开！！！最好使用绝对路径。

⼀个vmoptions内只能有⼀个 -javaagent 参数。

如果你是⽆外⽹环境，在javaagent路径后加 =offline ，
如： 

`-javaagent:/absolute/path/to/jetbrains-agent.jar=offline`

示例:

mac: `-javaagent:/Users/neo/jetbrains-agent.jar`

linux: `-javaagent:/home/neo/jetbrains-agent.jar`

windows: `-javaagent:C:\Users\neo\jetbrains-agent.jar`

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009122708.png)

5. 重启CLion。

6. 点击确定

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009123403.png)

如果要屏蔽此窗口，只需按照上面写的来做就可以了。第二步解压的jetbrains-agent文件夹里面的important.txt文件复制到jetbrains-agent.jar所在的文件夹中。

7. 跟着图片走

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009121322.png)

8. 选择Activation code⽅式离线激活，将 ACTIVATION_CODE.txt 内的内容复制到空白框里。

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009123810.png)

9. 破解完毕。

10. 重启CLion，正常运行。



# 六、安装MinGW

## 6.1 方式1

1. 打开网址：

https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/

2. 不要点击绿色的按钮，一直向下滑动，找到压缩包，点击下载既可。

如下图：
![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009125204.png)


3. 此时会提示你下载，点击确定下载。

4. 等待下载完成。

5. 将下载的压缩包解压，记住存放解压文件的路径。

如下图：

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009131612.png)

## 6.2 方式2

将一开始从百度网盘里面下载的mingw64文件进行解压。记住存放解压文件的路径。

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009131612.png)

# 七、 配置CLion

1. 新建一个工程。点击New Projet

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009132121.png)



2. 跟着图片走

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009132225.png)


![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009132251.png)


![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009132603.png)


3. 选择File-Settings-Build-Toolchains

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/CLion/20201009132711.png)

4. CLion会自动填写信息，等待几秒钟。!

![](https://gitee.com/heathhou/image_store/raw/master/分类/c/Clion/20201120202118.png)

5. 再次回到第四步。

6. 如果第4步没有自动输入，尝试在Environment中输入之前MinGW解压文件的路径，再次观察是否自动输入。如果还没有自动输入，那就尝试手动输入，看接下来的步骤。

7. Make：

   ```
   #解压文件路径# + \bin\mingw32-make.exe
   ```

    C Compiler：

   ```
   #解压文件路径# + \bin\gcc.exe
   ```

    C++ Compiler：

   ```
   #解压文件路径# + \bin\g++.exe
   ```

    Debugger：

   ```
   #解压文件路径# + \bin\gdb.exe
   ```

    最后点击OK即可。

8. 至此，全部结束。

   

