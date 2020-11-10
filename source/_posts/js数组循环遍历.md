---
title: js数组循环遍历方法
top: true
cover: false
toc: true
mathjax: true
abbrlink: 42099
date: 2020-10-21 11:09:05
password:
summary: 记录一些js遍历数组及过滤数组的常用方法
tags:  
- Es6
- Array
- JS
categories: 
- 前端
--- 
## for:循环代码块一定的次数

 for 循环的语法：for (语句 1; 语句 2; 语句 3){  语句 4:   被执行的代码块 }
 语句 1 （代码块）开始前执行;语句 2 定义运行循环（代码块）的条件;语句 3 在循环（代码块）已被执行之后执行
执行顺序是：语句 1，语句 2， 语句 4，语句 3
应用最为普遍的循环写法，性能好，可读性好。

```js
var a = [1, 2, 3, 45, 6];
for (var j = 0; j < a.length; j++) {
  console.log(a[j])
}// 1, 2, 3, 45, 6
```

## 升级版for

优点：性能比普通for循环好，省去了每次对于数组长度的判断。
缺点：对于长度可能会产生变动的数组，这种方法不适用，可能会导致有的值没被遍历到等错误。

```js
var a = [1, 2, 3, 45, 6];
var len = a.length;
for (var j = 0; j < len; j++) {
  console.log(a[j])
}
// 1, 2, 3, 45, 6
```

## forEach() 方法用于调用数组的每个元素，并将元素传递给回调函数

语法：array.forEach(function(currentValue, index, arr), thisValue) currentValue 必须 当前元素值 ；index 可选 当前元素的索引值 ；arr 可选 当前元素属于的数组对象。 
优点：提供的三个参数可以很大程度上减少代码长度，可读性好。
缺点：无法遍历对象， 在IE9以上才能使用，而且无法使用 break，continue 跳出循环，使用 return 是跳过本次循环。
forEach循环数组而已。foreach函数无法用break跳出

```js
var b = [1, 2, 3, 45, 6];
b.forEach(val => {
  console.log(val)
})
// [1, 2, 3, 45, 6]
```

## each() 方法主要用于DOM遍历，each() 方法规定为每个匹配元素规定运行的函数。通过它，你可以遍历对象、数组的属性值并进行处理

语法：$(selector).each(function(index,element));index - 选择器的 index 位置，element - 当前的元素（也可使用 "this" 选择器）.
 优点：既可以遍历数组，也可以遍历对象，jQuery对于方法进行了改进，一些语句可以跳出循环：
 return false：将停止循环 (就像在普通的循环中使用 ‘break’)。
 return true：跳至下一个循环(就像在普通的循环中使用’continue’)。

```js
var d = [1, 2, 3, 45, 6];
$(d).each((k, v) => { consoel.log(k, v) })
```

## map():对数组中的每一个元素进行操作

语法：function(currentValue,index,arr) currentValue 必须 当前元素值 ；index 可选 当前元素的索引值 ；arr 可选 当前元素属于的数组对象,
map()方法返回一个新数组，数组中的元素为原始数组元素调用函数处理的后值。 map()方法按照原始数组元素顺序依次处理元素.
优缺点和forEach相似，IE9+才能使用，如果想在低版本IE运行，可以在原型里添加方法
 需要注意的是map方法返回的是一个新的数组，不会改变之前的数组， 而且break，continue等语句失效，无法提前跳出循环，而且map方法是可以使用return语句的

```js
var e = [1, 2, 3, 45, 6];
e.map((a, g) => { console.log(a, g) })
//1 0
//2 1
//3 2
//45 3
//6 4
```

## for in:一般用来遍历对象的每一个属性。每次都将属性名作为字符串保存在变量里,但是它也可以遍历数组

  语法：for (variable in object ) {…statement}
 variable是一个变量名，数组的一个元素或者是对象的一个属性
 object是一个对象名，或者是计算结果为对象的表达式。
 statement通常是一个原始语句或者语句块，由它构成循环的主体。

```js
var f = { a: 1, b: 2, c: 3 };
for (var aa in f) {
  console.log(aa, f[aa])
}
//a 1
//b 2
//c 3
```

```js
var c = [1, 2, 3, 45, 6];
for (var aa in c) {
  console.log(c[aa])
}
//1, 2, 3, 45, 6
```

 for of 读取键值（适合处理数组),而for ... in  用于对象或基础的可访问属性的遍历，适合处理对象
 优点：简洁，可以使用break、continue、return等语句，可以遍历数组、对象、DOM节点数组、Set对象等等
 缺点：属于ES6的语法内容，使用时应注意兼容性。

```js
const t = [1, 2, 3, 45, 6];
for (aa of t) {
  console.log(aa)
}
//1, 2, 3, 45, 6
```

## filter:过滤数组。返回值为true的元素组成新数组

语法：function(currentValue,index,arr) currentValue 必须 当前元素值 ；index 可选 当前元素的索引值 ；arr 可选 当前元素属于的数组对象。
filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

```js
var g = [1, 2, 3, 45, 6];
var g1 = g.filter(a => a >= 4)
console.log(g1)
//[ 45, 6 ]
```

## reduce:进行累加或者累积操作。,该方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值

语法:array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
 total必需。初始值, 或者计算结束后的返回值。currentValue必需。当前元素；currentIndex可选。当前元素的索引；arr可选。当前元素所属的数组对象。

```js
var h = [1, 2, 3, 45, 6];
var h1 = h.reduce((a, b) => a - b)
console.log(h1)
//-55
```

## some:检查数组中是否有元素满足条件。某一元素为true，则为true，否则返回false(一个满足条件即可)

```js
var i = [1, 2, 3, 45, 6];
var i1 = i.some(item => item > 2)
console.log(i1)
//true
```

## every() - 检查数组中是否所有元素都满足条件。某一个为false，则返回false，否则返回true(都必须满足条件)

```js
var j = [1, 2, 3, 45, 6];
var j1 = j.every(item => item > 2)
console.log(j1)
//false
```
