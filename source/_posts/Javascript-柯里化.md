---
title: Javascript 柯里化
date: 2020-11-20 16:22:36
tags:
  - Javascript
  - 柯里化
  - Currying
category: Javascript
author: Xavier
summary: 柯里化为实现多参函数提供了一个递归降解的实现思路——把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数，在某些编程语言中（如 Haskell），是通过柯里化技术支持多参函数这一语言特性的。所以柯里化原本是一门编译原理层面的技术，用途是实现多参函数。
---

# JavaScript 柯里化

> 在《Mostly adequate guide》一书中，这样总结了柯里化: ——只传递给函数一部分参数来调用它，让它返回一个函数去处理剩下的参数。

## 在 JavaScript 中实现柯里化

我们先写一个实现加法的函数 add

```javascript
function add (x, y) {
  return x + y
}
```

现在我们直接实现一个被柯里化的 add 函数，该函数名为 curriedAdd，则根据上面的定义，curriedAdd 需要满足以下条件：

```javascript
curriedAdd(1)(3) === 4

// true

var increment = curriedAdd(1)

increment(2) === 3

// true

var addTen = curriedAdd(10)

addTen(2) === 12

// true

```

满足以上条件的 curriedAdd 的函数可以用以下代码段实现：

```javascript
function curriedAdd (x) {
  return function add (y) {
    return x + y
  }
}
```

当然以上实现是有一些问题的：它并不通用，并且我们并不想通过重新编码函数本身的方式来实现 Currying 化。

但是这个 curriedAdd 的实现表明了实现 Currying 的一个基础 —— Currying 延迟求值的特性需要用到 JavaScript 中的作用域——说得更通俗一些，我们需要使用作用域来保存上一次传进来的参数。

对 curriedAdd 进行抽象，可能会得到如下函数 currying ：

```javascript
function currying (fn, ...args1) {

    return function (...args2) {

        return fn(...args1, ...args2)

    }
}
var increment = currying(add, 1)

increment(2) === 3

// true

var addTen = currying(add, 10)

addTen(2) === 12

// true
```