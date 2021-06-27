---
title: JavaScript ES6的重要新特性 (二) 参数默认值、模板字符串、扩展运算符、对象解构
tags:
  - JavaScript
  - ES6
categories:
  - 前端
abbrlink: 6fff736
top_img: https://cdn.jsdelivr.net/gh/b1acksoil/blog-cdn/img/article/6fff736/top_img.png
cover: https://cdn.jsdelivr.net/gh/b1acksoil/blog-cdn/img/article/6fff736/top_img.png
date: 2021-06-26 22:54:04
---

书接上文。在上一篇ES6特性讲解的文章中讲了一下 let/const 和箭头函数，这一篇就来说说ES6的另外几个重要的特性——函数的参数默认值、模板字符串、扩展运算符和对象、数组解构。

# 函数的参数默认值
ES6以前，对于需要有参数默认值的函数是这样定义的：
```javascript
function say(msg) {
  msg = msg || 'hello'      // 为参数msg设置默认值'hello'
  console.log(msg)
}
```
ES6新定义了一种更优雅的设置参数默认值的方法：
```javascript
function say(msg = 'hello') {      // 设置默认值
  console.log(msg)
}
```

# 模板字符串
以前拼接字符串需要笨拙地使用`+`号：
```javascript
// ES6以前
var year = '2021'
var month = '06'
var day = 26
var showDay = true

var date = year + '-' + month + '-' + (showDay ? day : '')

console.log(date)   // 2021-06-26
```
ES6定义了一种新的字符串拼接方法，可以使用`${变量名或表达式}`的方法来将字符串变量直接嵌入大字符串。大字符串必须以<code>`</code>（Tab上面那个键）号括起来：
```javascript
// ES6
var year = '2021'
var month = '06'
var day = 26
var showDay = true

var date = `${year}-${month}-${showDay ? day : ''}`   // 注意大字符串以 ` 号括起来了

console.log(date)   // 2021-06-26
```

# 扩展运算符
ES6中新增了一种扩展运算符`...`，在对象、数组、函数中被广泛使用。
## 对象中的扩展运算符
假设有这样一个对象：
```javascript
let fooObj = {
  name: 'Eric',
  age: 16
}
```
我们要把它与另一个对象合并，可以这样写：
```javascript
let barObj = {
  ...fooObj,
  hobby: 'gaming'
}
console.log(barObj)    // {name: 'Eric', age: 16, hobby: 'gaming'}
```
由于对象`Object`属于引用数据类型，在合并的时候合并的其实是对象的引用，修改被合并的对象，主对象也会跟着改变：
```javascript
fooObj.age = 18    // 修改被合并的变量
console.log(barObj)    // {name: 'Eric', age: 18, hobby: 'gaming'}
```
## 数组中的扩展运算符
数组中扩展运算符的使用方法与对象中的类似：
```javascript
let fooArr = [1, 2, 3, 4]
let barArr = [5, 6, ...fooArr]
console.log(barArr)    // [5, 6, 1, 2, 3, 4]

// 修改被合并数组的值
fooArr[0] = 100
console.log(barArr)    // [5, 6, 100, 2, 3, 4]
```

## 函数中的扩展运算符
我们可以用扩展运算符来定义无限长度的形参：
```javascript
function add(...num) {
  let sum = 0
  for (let i=0; i<num.length; i++) {
    sum += num[i]
  }
  return sum
}

console.log(add(1, 2, 3, 4))    // 10
```
同时也可以用扩展运算符来将数组中的元素直接全部当作实参传入函数：
```javascript
let args = [2, 4, 6, 8]
console.log(add(...args))    // 20
```
## 高级用法
实际上所有可迭代的对象都可以使用扩展运算符`...`来遍历，并转换为序列。例如：
```javascript
// 字符串
const str = 'a string'
console.log([...str])   // ['a', ' ', 's', 't', 'r', 'i', 'n', 'g']
```


# 对象、数组解构
## 对象解构
假设我们有这样一个对象：
```javascript
const obj = {
  name: 'Jack',
  age: '18',
  hobby: 'coding'
}
```
我们要想取出对象中的值，可以这样写：
```javascript
const name = obj.name
const age = obj.age
const hobby = obj.hobby
```
ES6提供了一种新的写法，效果与上面一样：
```javascript
const { name, age, hobby } = obj
```
### 变量名与键名保持一致
注意取出的变量名要和对象里的键名保持一致，不然会取不到值：
```javascript
const { n, a, h } = obj
console.log(n, a, h)    // undefined undefined undefined
```
### 解构同时重命名
若想解构的同时重命名，可以这样写：
```javascript
const { name:n, age:a, hobby:h } = obj
console.log(n, a, h)    // Jack 18 coding
```

## 数组解构
JavaScript的数组解构十分灵活。与对象结构不同，数组结构用的是中括号`[]`：
```javascript
const arr = ['Max', 20, 'painting']

const [ name, age, hobby ] = arr
console.log(name, age, hobby)    // Max 20 painting
```
### 解构变量个数小于数组元素个数
若解构变量个数小于数组元素个数：
```javascript
const [ n, a ] = arr
console.log(n, a)    // Max 20
```
可以看出只是取不出值而已，并不会报错。
### 解构变量个数大于数组元素个数
再来看看解构变量个数大于数组元素个数：
```javascript
const [ n, a, h, foo ] = arr
console.log(n, a, h, foo)    // Max 20 painting undefined
```
同样不会报错，多出来的值被赋上了`undefined`。  
### 使用丢弃变量解构
有的时候我们不想取出中间的值，就可以这样写：
```javascript
const [ name, , hobby ] = arr    // 使用了丢弃变量
console.log(name, hobby)    // Max painting
```
### 使用扩展运算符解构
可以使用扩展运算符来一次性解构多个元素：
```javascript
const [ name, ...remain ] = arr
console.log(name, remain)    // Max [18, 'painting']
```
像这样使用扩展运算符取到的是一个数组。注意在数组解构中使用扩展运算符时，扩展运算符只能存在一次且只能存在于最后方：
```javascript
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
let [ a, b, c, ...d, e, ...f ] = arr    // Uncaught SyntaxError: Rest element must be last element
```

