---
title: android 面试题集
description: 记录常见android面试题目
author: cotes
date: 2024-03-29 09:48:00 +0800
categories: [面试, android]
tags: [android 面试]
render_with_liquid: false
---
# java 基础
## 1、http与https有什么区别
- https协议需要到ca申请证书，一般免费证书较少，因而需要一定费用。
- http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl加密传输协议。
- http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。
- http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。

## 2、equals,==有什么区别
- ==：用于基本数据类型的比较，判断引用是否指向堆内存的同一块地址
- equals：用于判断两个变量是否是对同一个对象的引用，即堆中的内容是否相同

## 3、双委派机制
当某个类加载器需要加载某个.class文件时，它首先把这个任务委托给他的上级类加载器，递归这个操作，如果上级的类加载器没有加载，自己才会去加载这个类
好处：
- 避免类的重复加载
- 保护程序安全，防止核心API被随意篡改

## 4、ArrayList和HashMap 区别
- ArrayList：底层数据结构是Object数组，查询快，增删慢，线程不安全
- HashMap：数组+链表+红黑树

## 5、抽象类和接口，有什么区别
- 相同点：都不能被实例化
- 不同点： 1、接口实现implements，抽象类用extents，可以实现多个接口，但是只能继承一个类
- 2、关键字不一样，抽象类用abstract修饰，接口用interface

## 6、反射三种方式
- Class clz = Class.forName("com.entity.Book");
- Class clz = Book.class;
- Book book = new Book();  Class clz = book.getClass(); 

## 7、sleep 和 wait 区别
-  sleep：当前线程停止执行，让出cpu给其他的线程。但是不会释放对象锁资源以及监控的状态，当指定的时间到了之后又会自动恢复运行状态。
-  wait：让线程放弃当前的对象的锁，notify才能唤醒

# Android 

## 1、造成ANR的原因及解决办法
- 1、主线程阻塞或主线程数据读取。解决办法：使用子线程处理耗时任务或者阻塞任务
- 2、CPU满负荷，I/O阻塞。解决办法：文件读写或者数据库操作放在子线程。
- 3、内存不足。解决办法：优化内存，防止内存泄漏。
- 4、各大组件ANR。解决办法：各大组件的生命周期也应避免耗时操作

## 2、进程间通信方式
- aidl broadcast socket ContentProvider

## 3、intentService
- 初见intentService是在2016年看google 文档的android performance tips 里面说建议使用它，因为他可以shut down it self
- 源码分析

## 4、android 事件传递

## 5、handler 机制

## 6、mvp mvvm
- mvp  ： model 数据处理， p 逻辑处理， v  视图。简要一点mvp是面向接口编程，每层都有对应都接口（该接口代表该层都行为），p层持有
view 和model 层都接口进行逻辑处理
- mvvm ： 当前android 用databind 和viewModel 分层来进做mvvm。vm 和mvp都p 相似，因为用了databind和livedata 所以数据变化直接响应到了ui。更简洁

## 7、TextSurface和SurfaceView 区别
