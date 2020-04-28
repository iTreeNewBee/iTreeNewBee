---
layout: post
title:  "java常见异常"
date:   2019-11-12 13:01:03
categories: java
tags: java 
excerpt: 常见异常记录
---
* content
{:toc}  

Throwable 类是所有异常和错误的超类，下面有 Error 和 Exception 两个子类分别表示错误和异常。其中异常类 Exception 又分为运行时异常和非运行时异常，这两种异常有很大的区别，也称为不检查异常（Unchecked Exception）和检查异常（Checked Exception）
1.NullPointerException
空指针异常，操作一个null对象的方法或属性会抛出这个异常。
2.OutofMemoryError
内存出现异常，不是程序控制的，指要分配的对象的内存超出了当前最大的堆内存，需要调整堆内存大小及优化程序。
3.IOException
IO，即input,output，在读写磁盘文件、网络内容时候发生的异常，这种异常是受检查异常，需要手工捕获。
4.FileNotFoundException
文件找不到异常，如果文件不存在抛出此异常。是IOException的子类，同样是受检查异常，需要手工捕获。
5.ClassNotFoundException
类找不到异常。加载类的时候抛出，即在类路径下不能加载指定的类。受检查异常，需要进行手工捕获。
6.ClassCastException
类转换异常，将一个不是该类的实例转换成这个类就会抛出。例如将一个数字强制转换成字符串就会报这个异常。（运行时异常，不需要手工捕获）
7.NoSuchMethodException
没有这个方法异常，一般发生在反射调用方法时。受检查异常，需要手工捕获。
8.IndexOutOfBoundsException
索引越界异常，当操作一个字符串或者数组的时候经常遇到的异常。（运行时异常）
9.ArithmeticException
算术异常，发生在数字的算术运算时的异常，如一个数字除以0.
10.SQLException
SQL异常，发生在操作数据库时的异常。
11.EOFException
文件结束异常
12.IllegalArgumentException
方法接收到非法参数抛出此异常