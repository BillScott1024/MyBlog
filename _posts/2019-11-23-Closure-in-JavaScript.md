---
layout: post
title: JavaScript深入浅出之理解闭包
date: 2019-11-23
tags: JavaScript
music-id: 829845
---

*  目录
{:toc}

-------

![](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/img/d3254348-13a1-4d50-af7d-393051ee62c2.jpg)

-------
# 前言

> 函数与对其状态即词法环境（lexical environment）的引用共同构成闭包（closure）。也就是说，闭包
> 可以让你从内部函数访问外部函数作用域。在JavaScript，函数在每次创建时生成闭包。
> --- MDN Web docs

# 什么是“闭包”
在MDN JavaScript官方文档上对**“闭包”**的描述是：函数与其状态即词法环境的引用，共同构成**闭包**。用更通俗的话来讲就是：闭包就是能够读取其他函数内部变量的函数。简单来说，闭包是一种函数，一种定义在函数内部的函数。本质上，闭包就是将函数内部和外部连接在一起的一座桥梁。
例子🌰：


```js
function func1(){
    var number = 999;
    function func2(){
        console.log(number);
    }
    return func2();
}

var result = func1();
result();               // "999"
var function(){
}

```

其中 func2函数，就是闭包。

# 闭包的作用

1. 在外部能够读取函数内部的变量。
2. 使变量的值一直存在于内存当中。
3. 使用闭包模拟私有方法。

示例代码：


```js
function func1(){
    var number = 999;
    addFunc = function(){
        number += 1;
    }
    
    function func2(){
        console.log(number);
    }
    return func2;
}

var result = func1();
result();       // "999"
addFunc();
result();       //"1000"
```

# 闭包会产生的问题（注意事项）
1. 由于闭包会使得函数中的变量都被保存在内存之中，即使函数已经执行完毕，这些局部变量也不会被垃圾回收器自动回收，有某些环境下容易导致内存泄漏。正确做法是，在退出函数之前，将不使用的变量都删除清空。
2. 闭包会改变函数的值，而不只是改变函数变量的一个副本。
3. 循环闭包问题。











# 引用
本文参考：

> [学习Javascript闭包（Closure）](https://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)
> [闭包](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)
> [用9种办法解决 JS 闭包经典面试题](https://segmentfault.com/a/1190000003818163)