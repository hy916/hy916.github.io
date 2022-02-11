---
title: js变量转换为数值
top: false
cover: false
toc: true
mathjax: true
tags:
  - JavaScript
categories:
  - 前端
abbrlink: eff85764
date: 2020-11-20 11:31:00
password:
summary:
---

这三种 JavaScript 方法可用于将变量转换为数字：


1. Number() 方法
2. parseInt() 方法
3. parseFloat() 方法
这些方法并非数字方法，而是全局 JavaScript 方法

## 全局方法

JavaScript 全局方法可用于所有 JavaScript 数据类型。  
这些是在处理数字时最相关的方法：

| 方法           |     描述   |
|:---|:---|
| Number()      |        返回数字，由其参数转换而来。|
| parseFloat()  |      解析其参数并返回浮点数。|
| parseInt()    |      解析其参数并返回整数。|

## Number() 方法

Number() 可用于把 JavaScript 变量转换为数值

## 用于日期的 Number() 方法

Number() 还可以把日期转换为数字

## parseInt() 方法

parseInt() 解析一段字符串并返回数值。允许空格。只返回首个数字
如果无法转换为数值，则返回 NaN (Not a Number)

## parseFloat() 方法

parseFloat() 解析一段字符串并返回数值。允许空格。只返回首个数字
如果无法转换为数值，则返回 NaN (Not a Number)。

## 数值属性

  |   属性         |      描述    |
  |:------|:-------|
|  MAX_VALUE     |      返回 JavaScript 中可能的最大数。|
|  MIN_VALUE         |      返回 JavaScript 中可能的最小数。|
|  NEGATIVE_INFINITY    |       表示负的无穷大（溢出返回）。|
|  NaN                 |      表示非数字值（"Not-a-Number"）。|
|  POSITIVE_INFINITY      |         表示无穷大（溢出返回）。|

## JavaScript MIN_VALUE 和 MAX_VALUE

* MAX_VALUE 返回 JavaScript 中可能的最大数字。
* MIN_VALUE 返回 JavaScript 中可能的最小数字。

## JavaScript NaN - 非数字

NaN 属于 JavaScript 保留字，指示数字并非合法的数字。   
尝试使用非数字字符串进行算术运算将导致 NaN（非数字）：

```js

var x = 100 / "Apple";  // x 将是 NaN (Not a Number)
```

## 数字属性不可用于变量

* 数字属性属于名为 number 的 JavaScript 数字对象包装器。   
* 这些属性只能作为 Number.MAX_VALUE 访问。   
* 使用 myNumber.MAX_VALUE，其中 myNumber 是变量、表达式或值，将返回 undefined   

## JavaScript 数组

* JavaScript 数组用于在单一变量中存储多个值。
* 数组是一种特殊的变量，它能够一次存放一个以上的值。
* 数组可以用一个单一的名称存放很多值，并且还可以通过引用索引号来访问这些值。

## 访问数组元素

* 我们通过引用索引号（下标号）来引用某个数组元素。
* 这条语句访问 cars 中的首个元素的值
* [0] 是数组中的第一个元素。[1] 是第二个。数组索引从 0 开始。

```js
var cars = ["Saab", "Volvo", "BMW"];
document.getElementById("demo").innerHTML = cars[0]; 
```

## 改变数组元素

这条语句修改了 cars 中第一个元素的值：

```js
var cars = ["Saab", "Volvo", "BMW"];
cars[0] = "Opel";
document.getElementById("demo").innerHTML = cars[0];
```

## 访问完整数组

通过 JavaScript，可通过引用数组名来访问完整数组：

```js
var cars = ["Saab", "Volvo", "BMW"];
document.getElementById("demo").innerHTML = cars; 
```

## 数组是对象

* 数组是一种特殊类型的对象。在 JavaScript 中对数组使用 typeof 运算符会返回 "object"。  
* 但是，JavaScript 数组最好以数组来描述。  
* 数组使用数字来访问其“元素”。  

## 数组元素可以是对象

* JavaScript 变量可以是对象。数组是特殊类型的对象。
* 正因如此，您可以在相同数组中存放不同类型的变量。
* 您可以在数组保存对象。您可以在数组中保存函数。你甚至可以在数组中保存数组
  
## length 属性

* length 属性返回数组的长度（数组元素的数目）。
* length 属性始终大于最高数组索引（下标）。

```js
* 访问第一个数组元素
fruits = ["Banana", "Orange", "Apple", "Mango"];
var first = fruits[0];
```

```js

* 访问最后一个数组元素
fruits = ["Banana", "Orange", "Apple", "Mango"];
var last = fruits[fruits.length - 1];
```

## 遍历数组元素

* 遍历数组的最安全方法是使用 "for" 循环：

```js
var fruits, text, fLen, i;

fruits = ["Banana", "Orange", "Apple", "Mango"];
fLen = fruits.length;
text = "<ul>";
for (i = 0; i < fLen; i++) {
     text += "<li>" + fruits[i] + "</li>";
}
```

您也可以使用 Array.foreach() 函数：

```js
var fruits, text;
fruits = ["Banana", "Orange", "Apple", "Mango"];

text = "<ul>";
fruits.forEach(myFunction);
text += "</ul>";

function myFunction(value) {
  text += "<li>" + value + "</li>";
}
```

## 添加数组元素

1. 向数组添加新元素的最佳方法是使用 push() 方法
2. length 属性向数组添加新元素

3. **添加最高索引的元素可在数组中创建未定义的“洞”**

## 关联数组

* 很多编程元素支持命名索引的数组。  
* 具有命名索引的数组被称为关联数组（或散列）。  
* JavaScript 不支持命名索引的数组。  
* 在 JavaScript 中，数组只能使用数字索引。  

## 数组和对象的区别

* 在 JavaScript 中，**数组使用数字索引**。
* 在 JavaScript 中，**对象使用命名索引**。
* 数组是特殊类型的对象，具有数字索引。

## 何时使用数组，何时使用对象

* JavaScript 不支持关联数组
* 如果希望元素名为字符串（文本）则应该使用对象。
* 如果希望元素名为数字则应该使用数组。

## 避免 new Array()

* 没有必要使用 JavaScript 的内建数组构造器 new Array()。
* **请使用 [] 取而代之！**  
下面两条不同的语句创建了名为 points 的新的空数组：

```js

var points = new Array();         // 差
var points = [];                  // 优
```

下面两条不同的语句创建包含六个数字的新数组：   

```js
var points = new Array(40, 100, 1, 5, 25, 10); // 差
var points = [40, 100, 1, 5, 25, 10];          // 优
```

new 关键词只会使代码复杂化。它还会产生某些不可预期的结果

```js
var points = new Array(40, 100);  // 创建包含两个元素的数组（40 和 100）
```

假如删除其中一个元素会怎么样？

```js
var points = new Array(40);       // 创建包含 40 个未定义元素的数组！！！
```

## 如何识别数组

常见的问题是：我如何知晓某个变量是否是数组？  
问题在于 JavaScript 运算符 typeof 返回 "object"：

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];

typeof fruits;             // 返回 object
```

typeof 运算符返回 "object"，因为 JavaScript 数组属于对象。

解决方案 1：
为了解决这个问题，ECMAScript 5 定义了新方法 Array.isArray()：

```js
Array.isArray(fruits);     // 返回 true
```

此方案的问题在于 ECMAScript 5 不支持老的浏览器。

解决方案 2：
创建您自己的 isArray() 函数以解决此问题：

```js
function isArray(x) {
    return x.constructor.toString().indexOf("Array") > -1;
}
```

假如参数为数组，则上面的函数始终返回 true。

或者更准确的解释是：假如对象原型包含单词 "Array" 则返回 true。

解决方案 3：
假如对象由给定的构造器创建，则 instanceof 运算符返回 true：

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];

fruits instanceof Array     // 返回 true
```
