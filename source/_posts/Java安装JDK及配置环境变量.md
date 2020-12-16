---
title: Java安装JDK及配置环境变量
date: 2020-10-17 22:29:06
tags: [java]
declare: true
---

<!-- more -->

# 一、 注册并登陆oracle账号

打开 https://www.oracle.com/

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/1.png)


注册与登录都是傻瓜式操作，这里就不说明了。

# 二、 下载jdk（jdk中包含了jre）

## 2.1 第一种操作：

打开 https://www.oracle.com/

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/2.png)



![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/3.png)

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/4.png)


![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/5.png)


选择jdk版本，这里以jdk8为例。

### 2.1.1 不想下载以前的版本的话

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/6.png)



### 2.2.2 想下载以前的版本，把网页拉到最下面

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/7.png)


选择想要下载的版本

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/8.png)


进行a或b之后. 根据自己的操作系统选择版本，这里以windows64位为例

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/9.png)

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/10.png)



如果认为以上操作麻烦，可以看这里：

## 2.2第二种操作：

百度网盘链接：
链接：https://pan.baidu.com/s/1lkkAyca30WzyX6b2PZk_pA 

提取码：k8ri 

如果新版本jdk在电脑上安装步骤中无法安装，建议使用8u202及以后较低版本

# 三、安装jdk

找到下载好的jdk,双击打开

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/11.png)


![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/12.png)

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/13.png)

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/14.png)


**注意，记住这里的安装路径。**

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/15.png)

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/16.png)



等待安装完成。

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/17.png)

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/18.png)




# 四、配置环境

右键我的电脑—属性

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/19.png)


## 4.1 新建 JAVA_HOME 变量

找到jdk的安装路径：

![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/20.png)


![](https://cdn.jsdelivr.net/gh/heathhou/image_store/分类/Java/安装JDK及配置环境变量/21.png)


## 4.2 查找 CLASSPATH 变量

若没有的话，需新建（1.5之后不用再设置CLASSPATH了，但个人强烈建议继续设置以保证向下兼用问题）

复制：
`.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`

注意：最前面有个小点


![](https://gitee.com/heathhou/image_store/raw/master/分类/Java/安装JDK及配置环境变量/22.png)


## 4.3 配置PATH的变量

(这里以win7为例，win10就是把每一项分开了，比win7界面好看点)

复制：`%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`


![](https://gitee.com/heathhou/image_store/raw/master/分类/Java/安装JDK及配置环境变量/23.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/Java/安装JDK及配置环境变量/24.png)




# 五、检查环境变量是否配置成功
按下win + r

输入cmd,按下回车

分别输入:

`java`

`javac`

或者：

`java -version`

`javac -version`

没有报错说明配置成功。

![](https://gitee.com/heathhou/image_store/raw/master/分类/Java/安装JDK及配置环境变量/25.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/Java/安装JDK及配置环境变量/26.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/Java/安装JDK及配置环境变量/27.png)

![](https://gitee.com/heathhou/image_store/raw/master/分类/Java/安装JDK及配置环境变量/28.png)



# 六、 结束

初学阶段不介意使用IDE，建议使用记事本编写Java代码。

现在可以show your code 了。