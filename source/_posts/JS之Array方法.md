---
title: JS之Array方法
top: false
cover: false
toc: true
mathjax: true
summary: 手敲Array的全部方法
tags:
  - JavaScript
categories:
  - 前端
abbrlink: cc1e3fbf
date: 2020-12-15 10:10:14
password:
---

## Array.from()

### 从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例

#### 返回值

一个新的数组实例。

#### 从 String 生成数组

```js
Array.from('huyi');
// ["h", "u", "y", "i"]
```

#### 从 Set 生成数组

```js
const hy = new Set(['huyi', 'happy', 'top', 'huyi']);
Array.from(hy)
// ["huyi", "happy", "top"]
```

#### 从 Map 生成数组

```js

const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map);
// [[1, 2], [2, 4], [4, 8]]

const mapper = new Map([['1', 'a'], ['2', 'b']]);
Array.from(mapper.values());
// ['a', 'b'];

Array.from(mapper.keys());
// ['1', '2'];

```

#### 在 Array.from 中使用箭头函数

```js

Array.from([1, 2, 3], x => x + x);
// [2, 4, 6]

```

## Array.isArray()

### 用于确定传递的值是否是一个 Array

#### 返回值

如果值是 Array，则为true; 否则为false

```js
// 下面的函数调用都返回 true
Array.isArray([]);
Array.isArray([1]);
Array.isArray(new Array());
Array.isArray(new Array('a', 'b', 'c', 'd'))
// 其实 Array.prototype 也是一个数组。
Array.isArray(Array.prototype);

// 下面的函数调用都返回 false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray(new Uint8Array(32))
Array.isArray({ __proto__: Array.prototype });

```

## Array.of()

### 方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型

#### 返回值

新的 Array 实例。

>Array.of() 和 Array 构造函数之间的区别在于处理整数参数：Array.of(7) 创建一个具有单个元素 7 的数组，而 Array(7) 创建一个长度为7的空数组（注意：这是指一个有7个空位(empty)的数组，而不是由7个undefined组成的数组)

```js
Array.of(7);       // [7]
Array.of(1, 2, 3); // [1, 2, 3]
Array.of(1);         // [1]
Array.of(undefined); // [undefined]

Array(7);          // [ , , , , , , ]
Array(1, 2, 3);    // [1, 2, 3]

```

## Array.concat()

### 用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组

#### 返回值

新的 Array 实例

#### 连接两个数组

```js
var hu = ['a', 'b', 'c'];
var yi = [1, 2, 3];

hu.concat(yi);
// ['a', 'b', 'c', 1, 2, 3]

```

#### 连接三个数组

```js

var hu1 = [1, 2, 3],
    hu2 = [4, 5, 6],
    hu3 = [7, 8, 9];

var huyi = hu1.concat(hu2, hu3);
console.log(huyi);
//  [1, 2, 3, 4, 5, 6, 7, 8, 9]

```

#### 将值连接到数组

```js

var hu = ['a', 'b', 'c'];
var huyi = hu.concat(1, [2, 3]);
console.log(huyi);
// ['a', 'b', 'c', 1, 2, 3]

```

#### 合并嵌套数组

```js
var num1 = [[1]];
var num2 = [2, [3]];
var num3=[5,[6]];

var nums = num1.concat(num2);

console.log(nums);
// [[1], 2, [3]]

var nums2=num1.concat(4,num3);

console.log(nums2)
// [[1], 4, 5,[6]]

num1[0].push(4);

console.log(nums);
// [[1, 4], 2, [3]]

```

## copyWithin()

### 方法浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度

#### 语法

> arr.copyWithin(target[, start[, end]])

#### 参数

**target**  

0 为基底的索引，复制序列到该位置。如果是负数，target 将从末尾开始计算。
如果 target 大于等于 arr.length，将会不发生拷贝。如果 target 在 start 之后，复制的序列将被修改以符合 arr.length。

**start**  

0 为基底的索引，开始复制元素的起始位置。如果是负数，start 将从末尾开始计算。
如果 start 被忽略，copyWithin 将会从0开始复制。

**end**  

0 为基底的索引，开始复制元素的结束位置。copyWithin 将会拷贝到该位置，但不包括 end 这个位置的元素。如果是负数， end 将从末尾开始计算。
如果 end 被忽略，copyWithin 方法将会一直复制至数组结尾（默认为 arr.length）。

#### 返回值

改变后的数组。

#### 描述

参数 target、start 和 end 必须为整数。  

如果 start 为负，则其指定的索引位置等同于 length+start，length 为数组的长度。end 也是如此。  

copyWithin 方法不要求其 this 值必须是一个数组对象；除此之外，copyWithin 是一个可变方法，它可以改变 this 对象本身，并且返回它，而不仅仅是它的拷贝。  

copyWithin 就像 C 和 C++ 的 memcpy 函数一样，且它是用来移动 Array 或者 TypedArray 数据的一个高性能的方法。复制以及粘贴序列这两者是为一体的操作;即使复制和粘贴区域重叠，粘贴的序列也会有拷贝来的值。  

copyWithin 函数被设计为通用式的，其不要求其 this 值必须是一个数组对象。  

copyWithin 是一个可变方法，它不会改变 this 的长度 length，但是会改变 this 本身的内容，且需要时会创建新的属性。  


```js

[1, 2, 3, 4, 5].copyWithin(-2)
// [1, 2, 3, 1, 2]

[1, 2, 3, 4, 5].copyWithin(0, 3)
// [4, 5, 3, 4, 5]

[1, 2, 3, 4, 5].copyWithin(0, 3, 4)
// [4, 2, 3, 4, 5]

[1, 2, 3, 4, 5].copyWithin(-2, -3, -1)
// [1, 2, 3, 3, 4]


const array1 = ['a', 'b', 'c', 'd', 'e'];

// 将索引第3处的元素复制到索引第0处
console.log(array1.copyWithin(0, 3, 4));
// ["d", "b", "c", "d", "e"]

// 将索引3中的所有元素复制到索引1末尾
console.log(array1.copyWithin(1, 3));
// ["d", "d", "e", "d", "e"]

```

>第一遍看,虽然抄写下来，但是无法理解😅此方法

## entries()

### 返回一个新的Array Iterator对象，该对象包含数组中每个索引的键/值对

```js

const array1 = ['a', 'b', 'c'];

const iterator1 = array1.entries();

console.log(iterator1);
// expected output: Array [0, "a"]

console.log(iterator1.next().value);
// expected output: Array [1, "b"]

```

#### 返回值

一个新的 Array 迭代器对象。**Array Iterator是对象**，它的原型`（__proto__:Array Iterator）`上有一个next方法，可用用于遍历迭代器取得原数组的`[key,value]`

#### Array Iterator

```js
var arr = ["a", "b", "c"];
var iterator = arr.entries();
console.log(iterator);

//Array Iterator是对象

/*Array Iterator {}
         __proto__:Array Iterator
         next:ƒ next()
         Symbol(Symbol.toStringTag):"Array Iterator"
         __proto__:Object
*/
```

#### iterator.next()

```js
var arr = ["a", "b", "c"];
var iterator = arr.entries();
console.log(iterator.next());

/*{value: Array(2), done: false}
          done:false
          value:(2) [0, "a"]
           __proto__: Object
*/
// iterator.next()返回一个对象，对于有元素的数组，
// 是next{ value: Array(2), done: false }；
// next.done 用于指示迭代器是否完成：在每次迭代时进行更新而且都是false，
// 直到迭代器结束done才是true。
// next.value是一个["key","value"]的数组，是返回的迭代器中的元素值。

```

#### iterator.next方法运行

```js

var arr = ["a", "b", "c"];
var iter = arr.entries();
var a = [];

// for(var i=0; i< arr.length; i++){   // 实际使用的是这个
for(var i=0; i< arr.length+1; i++){    // 注意，是length+1，比数组的长度大
    var tem = iter.next();             // 每次迭代时更新next
    console.log(tem.done);             // 这里可以看到更新后的done都是false
    if(tem.done !== true){             // 遍历迭代器结束done才是true
        console.log(tem.value);
        a[i]=tem.value;
    }
}

console.log(a);                         // 遍历完毕，输出next.value的数组

// false
// Array [0, "a"]
// Array [1, "b"]
// false
// Array [2, "c"]
// true
// Array [Array [0, "a"], Array [1, "b"], Array [2, "c"]]
```

#### 二维数组按行排序

```js
function sortArr(arr) {
    var goNext = true;
    var entries = arr.entries();
    while (goNext) {
        var result = entries.next();
        if (result.done !== true) {
            result.value[1].sort((a, b) => a - b);
            goNext = true;
        } else {
            goNext = false;
        }
    }
    return arr;
}

var arr = [[1,34],[456,2,3,44,234],[4567,1,4,5,6],[34,78,23,1]];
sortArr(arr);

// (4) [Array(2), Array(5), Array(5), Array(4)]
// 0: (2) [1, 34]
// 1: (5) [2, 3, 44, 234, 456]
// 2: (5) [1, 4, 5, 6, 4567]
// 3: (4) [1, 23, 34, 78]
// length: 4
// __proto__: Array(0)
```

#### 使用for…of 循环

```js
var arr = ["a", "b", "c"];
var iterator = arr.entries();
// undefined

for (let e of iterator) {
    console.log(e);
}

// [0, "a"]
// [1, "b"]
// [2, "c"]
```

## every()

### 测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值

>**注意**：若收到一个空数组，此方法在一切情况下都会返回 true。

