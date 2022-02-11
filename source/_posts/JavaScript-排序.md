---
title: JavaScript 排序
top: false
cover: false
toc: true
mathjax: true
abbrlink: 666a6660
date: 2022-02-11 17:41:42
password:
summary:
tags:
  - JavaScript
categories:
  - 前端
---

## js中排序的几种方法

### 1.sort()方法

 注：sort() 方法用于对数组的元素进行排序,并返回数组。默认排序顺序是根据字符串Unicode码点。

 > 语法：array.sort(fun)；参数fun可选。规定排序顺序。必须是函数。
注：如果调用该方法时没有使用参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。
如果想按照其他规则进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：
若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
若 a 等于b，则返回 0。
若 a 大于 b，则返回一个大于 0 的值。
简单点就是：比较函数两个参数a和b，返回a-b 升序，返回b-a 降序
注：原数组发生改变

例：

1. 不传参数，将不会按照数值大小排序，按照字符编码的顺序进行排序；

```js
 var arr = ['General','Tom','Bob','John','Army'];
  var resArr = arr.sort();
  console.log(resArr);//输出   ["Army", "Bob", "General", "John", "Tom"]
  
  var arr2 = [30,10,111,35,1899,50,45];
  var resArr2 = arr2.sort();
  console.log(resArr2);//输出   [10, 111, 1899, 30, 35, 45, 50]
```

2. 传入参数，实现升序，降序；

```js
 var arr3 = [30,10,111,35,1899,50,45];
  arr3.sort(function(a,b){
   return a - b;
  })
  console.log(arr3);//输出  [10, 30, 35, 45, 50, 111, 1899]
  
  var arr4 = [30,10,111,35,1899,50,45];
  arr4.sort(function(a,b){
   return b - a;
  })
  console.log(arr4);//输出 [1899, 111, 50, 45, 35, 30, 10]
```

3. 根据数组中的对象的某个属性值排序；

```js
  var arr5 = [{id:10},{id:5},{id:6},{id:9},{id:2},{id:3}];
  arr5.sort(function(a,b){
   return a.id - b.id
  })
  console.log(arr5);
  //输出新的排序
  //  {id: 2}
  //  {id: 3}
  //  {id: 5}
  //  {id: 6}
  //  {id: 9}
  //  {id: 10}
```

4. 根据数组中的对象的多个属性值排序，多条件排序；

```js
 var arr6 = [{id:10,age:2},{id:5,age:4},{id:6,age:10},{id:9,age:6},{id:2,age:8},{id:10,age:9}];
  arr6.sort(function(a,b){
   if(a.id === b.id){//如果id相同，按照age的降序
    return b.age - a.age
   }else{
    return a.id - b.id
   }
  })
  console.log(arr6);
  //输出新的排序
  //  {id: 2, age: 8}
  //  {id: 5, age: 4}
  //  {id: 6, age: 10}
  //  {id: 9, age: 6}
  //  {id: 10, age: 9}
  //  {id: 10, age: 2}

```

5. 根据指定布尔值属性排序

原理：
```js
true - false  //-1
true = true   //0
false = false //0
false = true  //1
```

代码实现：
```js
array = [
    { name: 'service1', isFree: true },
    { name: 'service2', isFree: false },
    { name: 'service3', isFree: true },
    { name: 'service4', isFree: false }
]
array.sort((a, b) => a.isFree - b.isFree)
//打印结果：
[
    { name: "service2", isFree: false },
    { name: "service4", isFree: false },
    { name: "service1", isFree: true },
    { name: "service3", isFree: true }
]
```

### 2.reverse()方法

```js
var ar1=[2,4,6,8,1,3]
ar1.reverse()//此方法为倒序，也就是反过来。并不会进行大小排序
console.log(ar1)//[3, 1, 8, 6, 4, 2]
```

### 3.冒泡排序

```js
//每轮依次比较相邻两个数的大小，后面比前面小则交换
var b=0//设置用来调换位置的值
var a=[1,9,33,2,5,34,23,98,14]//冒泡排序
for(var i=0;i<a.length;i++){
    for(var j=0;j<a.length;j++){
        if(a[j]>a[j+1]){
            b=a[j]
            a[j]=a[j+1]
            a[j+1]=b
        }
    }
}
console.log(a)//[1, 2, 5, 9, 14, 23, 33, 34, 98]

```

### 4.选择排序

```js
//选择排序/打擂台法：
//规律：通过比较首先选出最小的数放在第一个位置上，然后在其余的数中选出次小数放在第二个位置上,依此类推,直到所有的数成为有序序列。
var arr = [9, 8, 7, 6, 5, 4];
//用选择排序的方法从小到大排列数组元素。

//比较的轮数
for(var i = 0; i < arr.length - 1; i++){
//每轮比较的次数
　　for(var j = i + 1; j < arr.length; j++){
　　　　if(arr[i] > arr[j]){
　　　　　　var tmp = arr[i];
　　　　　　arr[i] = arr[j];
　　　　　　arr[j] = tmp;
　　　　}
　　}
}

alert(arr);//4,5,6,7,8,9
```

### 5.快速排序

先从数列中取出一个数作为基准数

分区过程，将比这个数大的数全放到它的右边，小于或等于它的数全放到它的左边

再对左右区间重复第二步，直到各区间只有一个数

```js
function quickSort(arr, i, j) {
  if(i < j) {
    let left = i;
    let right = j;
    let mid = Math.floor((left+right)/2);
    let temp = arr[left];
    arr[left] = arr[mid];
    arr[mid] = temp;
    let pivot = arr[left];
    while(i < j) {
      while(arr[j] >= pivot && i < j) {  // 从后往前找比基准小的数
        j--;
      }
      if(i < j) {
        arr[i++] = arr[j];
      }
      while(arr[i] <= pivot && i < j) {  // 从前往后找比基准大的数
        i++;
      }
      if(i < j) {
        arr[j--] = arr[i];
      }
    }
    arr[i] = pivot;
    quickSort(arr, left, i-1);
    quickSort(arr, i+1, right);
    return arr;
  }
}
```

### 6.二分查找排序

二分法排序的原理，算法思想简单描述：
在插入第i个元素时，对前面的0～i-1元素进行折半，先跟他们中间的那个元素比，如果小，则对前半再进行折半，否则对后半进行半，直到left>right，然后再把第i个元素前1位与目标位置之间的所有元素后移，再把第i个元素放在目标位置上。

二分法排序最重要的一个步骤就是查找要插入元素的位置，也就是要在哪一个位置上放我们要准备排序的这个元素。
当我们查找到位置以后就很好说了，和插入排序一样，将这个位置以后的所有元素都向后移动一位。这样就实现了二分法排序。

然后是怎么查找着一个位置呢，就是不断的比较已排序的序列中的中间元素和要排序元素，如果大于的话，说明这个要排序的元素在已排序序列中点之前的序列。

```js
var erfen = function (val, arr) {
        if (arr.length < 1||val<arr[0]||val>arr[arr.length-1]) { 
          return false; 
        }//如果这个数字没在其中直接返回false
        else if (val == arr[0]||val==arr[arr.length-1]) {
            return true;
        }//如果找到了就返回true
        else if (arr.length == 1) {
            return false;
        }//如果不能再缩小了而且没查到返回false
        var res = [];
        var base = Math.floor(arr.length / 2);
        if (val > arr[base]) {
           res = arr.splice(base + 1, arr.length - 1);
        }//如果大于中间的从右边开始找
       else if (val = arr[base]) {
            return true;
        }//恰巧等于中间的就返回true
        else {
           res = arr.splic(0, base - 1);
        }//如果小于中间的就从右边找
        return erfen(val,res);//递归
    };

```