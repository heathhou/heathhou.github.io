---
title: Java与C的易混淆区别
date: 2020-12-16 18:47:01
tags: [java,c]
declare: true
---

本文记录了个人java与c易混淆的一些东西。

<!-- more -->

# switch 支持的数据类型

C：

> short int long char (unsigned,signed)

```c
switch（expression）
    case 1 : statement1;break;
    case 2 : statement2;break;
    case 3 : statement3;break;
    default: statement4;break;
```

expression结果必须是<u>***整型值***</u>（包括char），case<u>***标签***</u>必须是整数类型（包括char）的常量或整形常量表达式，不能用变量来用做case的标签。

java: 

>  byte  short  int char  枚举   String
>  

其中String(jdk1.7）以后才支持

expression本质上是支持***<u>int</u>***类型， byte  short  char  都默认转换成int，String根据哈希值，归跟到底还是int型。

expression与case是String或者不是String要一致。



# 数据类型的精确性

C语言的数据类型比较

```c
printf("%f",0.01 + 0.09);
```

> 输出结果为：0.100000

Java的基本数据类型不是很精确：

```java
System.out.println(0.01 + 0.09);
```

> 输出结果为：0.09999999999999999

要想在java中也使用精确的数据，可以使用BigDecimal类。