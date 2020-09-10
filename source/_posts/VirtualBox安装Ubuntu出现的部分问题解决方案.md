---
title: VirtualBox安装Ubuntu出现的部分问题解决方案
date: 2020-09-10 19:20:13
tags: 实用技术
categories: linux
---

# 一、自己需要配置ubuntu的步骤

1. 设置共享粘贴板与拖放为双向
2. 修改内存为2048MB
3. 修改处理器数量为2
4. 存储选择iso文件
5. 网络选择网络地址NAT
6. 选择共享文件夹
7. 进行安装


# 二、在注册处，键盘无法使用

## 问题描述：

输入姓名，密码，点击无法输入。如图：

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/20200910192412.png)

## 解决方案：

1. 强制退出安装。
2. 选定你的ubuntu，选择设置
3. 选择系统
4. 将系统 --> 主板 --> 内存大小 设置为2048MB
5. 将系统 --> 处理器 --> 处理器数量 设置为2。
6. 点击OK.

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/20200910193007.png)

7. 重新进行安装操作。



# 三、安装完成后出现一串英文

## 问题描述：

Please remove the installation medio , then reboot.

## 解决方案：

1. 选择设备
2. 选择分配光驱
3. 如果有iso文件前面有对号，选择移除虚拟盘,知道没有对号出现
4. 按下Enter键

![](https://gitee.com/heathhou/image_store/raw/master/分类/linux/ubuntu/20200910203541.png)

