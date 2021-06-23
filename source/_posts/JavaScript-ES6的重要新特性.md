---
title: JavaScript ES6的重要新特性
tags:
  - JavaScript
  - ES6
categories:
  - 前端
abbrlink: 4c1b6471
top_img: https://cdn.jsdelivr.net/gh/b1acksoil/blog-cdn/img/article/4c1b6471/top_img.png
date: 2021-06-24 01:31:07
---

> ECMAScript 6（简称ES6）是于2015年6月正式发布的JavaScript语言的标准，正式名为ECMAScript 2015（ES2015）。它的目标是使得JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

ES6对JavaScript做了大量改造，增加了许多实用的新特性，大幅提高了灵活性和应用性。

# let 和 const
## var的变量提升问题
在ES6以前，变量的声明一般只有一种方法：`var` 。
但`var`存在着“变量提升”的问题。举个例子：
```javascript
var msg = 'hello'

function say() {
  console.log(msg)
  var msg = 'world'
  console.log(msg)
}

say()
```
按正常思维来说，控制台会先输出`hello`，再输出`world`。但实际的输出却是：
```plaintext
undefined
world
```
这是因为使用`var`定义变量时，变量的声明会被单独提前到函数的顶端，而初始化则留在原位。所以上面的代码等价于：
```javascript
var msg = 'hello'

function say() {
  var msg           // 重新声明变量msg
  console.log(msg)  // undefined
  msg = 'world'
  console.log(msg)
}

say()
```

## 使用 let 定义局部变量
ES6中，`let`的出现很好的解决了上面的问题。  
`let`定义的是局部变量，仅在当前代码块（即最近的一对大括号）有效。举个例子：
```javascript
for (let i=0; i<5; i++) {
  console.log(i)
}
console.log(i)
```
输出如下：
```javascript
0
1
2
3
4
Uncaught ReferenceError: i is not defined
```
可以看出，`let`就是弥补了缺陷的`var`。官方也推荐尽量使用`let`而不是`var`。

## 使用 const 定义常量
`const`定义的变量与`let`一样都是局部变量，但`const`定义的是不能修改的常量。
```javascript
const num = 123
num = 456    // Uncaught TypeError: invalid assignment to const 'num'
```
但若`const`定义的变量是一个对象，其值还是可以被修改的：
```javascript
const obj = {
  key: 'damedane'
}

obj.key = 'dameyo'    // 不报错
obj = {
  key: 'dameyo'       // 报错
}
```
`const`定义变量时必须初始化：
```javascript
const a    // Uncaught SyntaxError: missing = in const declaration
```

# 箭头函数
## 基础写法
在ES6以前，定义函数需要使用`function`关键字：
```javascript
var func = function (a, b) {
  return a + b
}
```
ES6中新增了一种简写定义函数的方式，称为箭头函数：
```javascript
var func = (a, b) => {
  return a + b
}
```
如果函数内只包含`return`语句，还可以缩写为
```javascript
var func = (a, b) => a + b
```
如果返回值为一个对象，那这样的写法是错误的：
```javascript
let errfunc = (v) => { key: v }   // SyntaxError
```
因为这样的写法和函数体冲突了，所以要写成这样的形式：
```javascript
let okfunc = (v) => ({ key: v })
```

关于参数有几个需要注意的点：  
当只有一个参数时，括号可写可不写
```javascript
let squ = n => n**2
// 等同于
let squ = (n) => n**2
```
当没有参数，或有两个及以上个参数时，括号不能少
```javascript
let say = () => {
  console.log('hello')

let mul = (a, b) => a * b
```

## this指向问题
在使用`function`关键字定义函数时，`this`指向的是调用该函数的那个对象：
```javascript
let obj = {
  a: 10,
  add: function () {
    let func = function () {
      return this.a + 15
    }
    return func
  }
}

console.log(obj.add()())    // NaN
```
这里由于JavaScript的this指向错误，导致`this`指向`window`对象，所以`this.a`的值为`undefined`，故而输出为`NaN`。

而使用箭头函数就不会出现这个问题：
```javascript
let obj = {
  a: 10,
  add: function () {
    let func = () => this.a + 15
    return func
  }
}

console.log(obj.add()())   // 25
```
---
# 未完待更...
