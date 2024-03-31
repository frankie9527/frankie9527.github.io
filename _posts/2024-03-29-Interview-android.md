---
title: android 面试题集
description: 记录常见android面试题目
author: cotes
date: 2024-03-29 09:48:00 +0800
categories: [面试, android]
tags: [android 面试]
render_with_liquid: false
---
## 进程间通信方式
- aidl broadcast socket 
## intentService
- 初见intentService是在2016年看google 文档的android performance tips 里面说建议使用它，因为他可以shut down it self
- 源码分析

## android 事件传递

## handler 机制

## mvp mvvm
- mvp  ： model 数据处理， p 逻辑处理， v  视图。简要一点mvp是面向接口编程，每层都有对应都接口（该接口代表该层都行为），p层持有
view 和model 层都接口进行逻辑处理
- mvvm ： 当前android 用databind 和viewModel 分层来进做mvvm。vm 和mvp都p 相似，因为用了databind和livedata 所以数据变化直接响应到了ui。更简洁

## TextSurface和SurfaceView 区别
