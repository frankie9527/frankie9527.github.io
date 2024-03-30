---
title: android kotlin 笔记
description: 记录kotlin 一些问题
author: cotes
date: 2024-03-29 09:48:00 +0800
categories: [面试, android]
tags: [android 面试]
render_with_liquid: false
---
### let
- The context object is available as an argument (it).
- The return value is the lambda result

'let' can be used to invoke one or more functions on results of call chains. For example, the following code prints the results of two operations on a collection:

```
val numbers = mutableListOf("one", "two", "three", "four", "five")
numbers.map { it.length }.filter { it > 3 }.let { 
    println(it)
    // and more function calls if needed
} 
```
[let doc](https://kotlinlang.org/docs/scope-functions.html#let)

### with
- The context object is available as a receiver (this).
- The return value is the lambda result
### run
- The context object is available as a receiver (this).
- The return value is the lambda result.

run does the same as with but it is implemented as an extension function. So like let, you can call it on the context object using dot notation.

run is useful when your lambda both initializes objects and computes the return value.

### apply
