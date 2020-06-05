---
title: Array方法总结
date: 2020-05-25 15:44:48
tags:
  - 'Javascript'
categories:
  - 'Javascript'
keywords:
description: 'Array方法总结'
---

## `Array.from()` 转换为数组

**方法从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例。**

```js
//对象的话需要有length属性，并且键应该为数字或者str的数字
let obj = { 0: 'AA', 1: 'BB', length: 2 }
let arr1 = Array.from(obj) //arr1 = ['AA','BB']
let str = 'array'
let arr2 = Array.from(str) //arr2 = ['a','r','r','a','y']
let setObj = new Set([1, 2, 3, 4, 5])
//其中第二个参数类似map的执行回调函数
let arr3 = Array.from(setObj, (item) => {
  return item + 1
}) //arr2 = [ 2, 3, 4, 5, 6 ]
```

---

## `Array.isArray()` 判断是否为数组

**用于确定传递的值是否是一个 Array。**

```js
Array.isArray([1, 2, 3]) // true
Array.isArray({ foo: 123 }) // false
Array.isArray('foobar') // false
Array.isArray(undefined)
```

---

## `Array.of()` 创建数组

**方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。**

**`Array.of()` 和 `Array` 构造函数之间的区别在于处理整数参数：`Array.of(7)` 创建一个具有单个元素 7 的数组，而 `Array(7)` 创建一个长度为 7 的空数组（注意：这是指一个有 7 个空位(empty)的数组，而不是由 7 个 undefined 组成的数组）。**

```js
Array.of(7) // [7]
Array.of(1, 2, 3) // [1, 2, 3]
Array(7) // [ , , , , , , ]
Array(1, 2, 3) // [1, 2, 3]
```

---

## `concat()` 合并数组

**该方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。**

```js
let arr1 = [1, 2, 3]
let arr2 = [4, 5, 6]
let arr3 = [7, 8, 9]
let arrM = arr1.concat(arr2, arr3) //[ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

---

## `includes()` 判断数组有无此值

**该方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回 false。**

```js
arr.includes('要查询的值', '从数组N索引起查找')
let arr = [1, 2, 3, 4, 5, '6']
console.log(arr.includes(3)) //true
console.log(arr.includes(1, 3)) //false
console.log(arr.includes(3, -3)) //false
console.log(arr.includes(3, -4)) //true
console.log(arr.includes(6)) //false
```

---

## `indexOf()` 查询给定值在数组的索引

**该方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。**

```js
arr.indexOf('要查询的值', '从数组N索引起查找')

let arr = [1, 2, 3, 4, 5, '6', 3]
//返回为搜索值第一次出现的索引值
console.log(arr.indexOf(3)) //2
console.log(arr.indexOf(1, 3)) //-1
console.log(arr.indexOf(3, -4)) //6
console.log(arr.indexOf(3, -5)) //2
console.log(arr.indexOf(6)) //-1
```

---

## `lastIndexOf()` 倒查给定值在数组的索引

**该方法在数组中的最后一个的索引，如果不存在则返回 -1。从数组的后面向前查找，从 fromIndex 处开始。**

```js
arr.indexOf('要查询的值', '从数组N索引起逆向查询')
let arr = [3, 2, 8, 2, 3]
console.log(arr.lastIndexOf(3)) //4
console.log(arr.lastIndexOf(1)) //-1
console.log(arr.lastIndexOf(2, 1)) //1
console.log(arr.lastIndexOf(2, -1)) //3
console.log(arr.lastIndexOf(6)) //-1
```

---

## `slice()` 截取数组

**该方法返回一个新的数组对象，这一对象是一个由 begin 和 end 决定的原数组的浅拷贝（包括 begin，不包括 end）。原始数组不会被改变。**

```js
arr.slice('要从数组的N索引开始截取(包含)', '截止的索引位置(不包括)')
let arr1 = [0, 1, 2, 3, 4, 5] //[ 0, 1, 2, 3, 4, 5 ]
let arr2 = arr1.slice(3, 5) //[ 3, 4 ]
let arr3 = arr1.slice(4) //[ 4, 5 ]
let arr4 = arr1.slice(-4) //[ 2, 3, 4, 5 ]
```

---

## splice() 增删改数组

**该方法通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容。此方法会改变原数组。**

```js
arr.splice('所要操作的起始索引,要删除以后元素的个数,要添加到数组的内容')
let arr1 = [0, 4]
arr1.splice(1, 0, 1, 2, 3)
console.log(arr1) //[ 0, 1, 2, 3, 4 ]
let arr2 = [0, 1, 1, 1, 2, 3]
arr2.splice(1, 2)
console.log(arr2) //[0, 1, 2, 3]
let arr3 = [0, 1, 2, 3, 3, 3, 7]
arr3.splice(3, 2, 4, 5, 6)
console.log(arr3) //[ 0, 1, 2, 4, 5, 6, 3, 7 ]
let arr4 = [0, 1, 4]
arr4.splice(2, 0, 2, 3)
console.log(arr4) //[ 0, 1, 2, 3, 4 ]
```

---

## `join()` 转字符串

**该方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。如果数组只有一个项目，那么将返回该项目而不使用分隔符。**

```js
arr.join('用以要分割的东西')
let arr = ['A', 'B', 'C', 'D']
console.log(arr.join()) //A,B,C,D
console.log(arr.join('')) //ABCD
console.log(arr.join('-')) //A-B-C-D
console.log(arr.join('?')) //A?B?C?D
```

---

## `pop()` 删数组最后元素

**该方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。**

```js
let arr = [1, 2, 3]
arr.pop()
console.log(arr) //[1,2]
```

---

## `push()` 数组尾部添加

**该方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。**

```js
let arr = [1, 2, 3]
arr.push(4, 5, 6)
console.log(arr) //[ 1, 2, 3, 4, 5, 6 ]
```

---

## `shift()` 删数组第一元素

**方法从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。**

```js
let arr1 = [1, 2, 3]
let arr2 = ['a', 'b', 'c']
arr1.shift()
arr2.shift()
console.log(arr1, arr2) //[ 2, 3 ] [ 'b', 'c' ]
```

---

## `unshift()` 数组开头 添加

**方法将一个或多个元素添加到数组的开头，并返回该数组的新长度(该方法修改原有数组)。**

```js
let arr = [4, 5, 6]
arr.unshift(0, 1, 2, 3)
console.log(arr) //[ 0, 1, 2, 3, 4, 5, 6 ]
```

---

## `reverse()` 翻转数组

**该方法将数组中元素的位置颠倒，并返回该数组。数组的第一个元素会变成最后一个，数组的最后一个元素变成第一个。该方法会改变原数组。**

```js
let arr1 = [1, 2, 3, 4]
let arr2 = ['a', 'b', 'c', 'd']
arr1.reverse()
arr2.reverse()
console.log(arr1, arr2) //[ 4, 3, 2, 1 ] [ 'd', 'c', 'b', 'a' ]
```

---

## `fill()` 填充数组

**该方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。**

```js
arr
  .fill(
    '要填充的值',
    '要被填充的起始位置(默认为0)',
    '要被填充的截止位置(默认为arr.length)'
  )
  [(1, 2, 3)].fill(4) // [4, 4, 4]
;[1, 2, 3].fill(4, 1) // [1, 4, 4]
;[1, 2, 3].fill(4, 1, 2) // [1, 4, 3]
;[1, 2, 3].fill(4, 1, 1) // [1, 2, 3]
;[1, 2, 3].fill(4, 3, 3) // [1, 2, 3]
;[1, 2, 3].fill(4, -3, -2) // [4, 2, 3]
;[1, 2, 3].fill(4, NaN, NaN) // [1, 2, 3]
;[1, 2, 3].fill(4, 3, 5) // [1, 2, 3]
```

---

## `copyWithin()` 复制数组自身一部分

**该方法浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度。**

```js
copyWithin(
  '复制序列到该位置的索引',
  '复制数组的起始索引处(默认为0)',
  '复制数组的结束索引处'
) //其中参数为负数的话，为倒序索引
  [(0, 1, 2, 3, 4, 5)].copyWithin(0, 2) //[ 2, 3, 4, 5, 4, 5 ]
  [(0, 1, 2, 3, 4, 5)].copyWithin(0, 2, 3) //[ 2, 1, 2, 3, 4, 5 ]
  [(0, 1, 2, 3, 4, 5)].copyWithin(0, -2) //[ 4, 5, 2, 3, 4, 5 ]
  [(0, 1, 2, 3, 4, 5)].copyWithin(0, -2, -1) //[ 4, 1, 2, 3, 4, 5 ]
  [(0, 1, 2, 3, 4, 5)].copyWithin(-2) //[ 0, 1, 2, 3, 0, 1 ]
```

---

## `flat()` 解套多维数组

**该方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回**

```js
arr.flat('提取嵌套数组结构深度(默认为1)')
let arr = [1, 2, [3, [4, [5]]], [6]]
console.log(arr.flat()) // [1, 2, 3, [4,5], 6]
console.log(arr.flat(2)) //[1, 2, 3, 4, [5], 6]
console.log(arr.flat(Infinity)) //[1, 2, 3, 4, 5, 6]
```

---

## `reduce()` 累加器

**该方法对数组中的每个元素执行一个由您提供的 reducer 函数(升序执行)，将其结果汇总为单个返回值。**

```js
arr.reduce('回调函数(
  "累加器",
  "轮训的当前值",
  "轮询当前值的索引",
  "被指向的arr")')
let arr = [1, 2, 3, 4, 5]
let sum = arr.reduce((sum, item, idx, arr) => {
  return (sum += item)
})
console.log(sum) // 15
```

---

## `forEach()` 单纯的循环数组

**该方法对数组的每个元素执行一次给定的函数。**

```js
arr.forEach('回调函数(
  "轮询的当前值",
  "轮询的当前索引值",
  "被指向的arr"
)')
let arr = [1, 2, 3]
arr.forEach((item, idx, arr) => {
  console.log(item) //1    2    3
})
```

---

## `map()` 循环数组，进行操作

**方法创建一个新数组，其结果是该数组中的每个元素都调用一次提供的函数后的返回值。**

```js
arr.map('回调函数(当前值,当前值的索引,调用的数组){}')
let arr1 = [1, 2, 3, 4, 5]
let arr2 = arr1.map((item, idx, arr) => {
  return item + 1
})
console.log(arr1, arr2) //[ 1, 2, 3, 4, 5 ] [ 2, 3, 4, 5, 6 ]
```

---

## `every()` 循环数组，返回布尔

**该方法测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔**

```js
arr.every('回调函数(当前值,当前值的索引,调用every的数组){}')
let arr = [1, 2, 3, 4, 5]
let flag = arr.every((item, idx, arr) => {
  //所有item都小于5才会输出true，如果有一项大于5的值，则立即停止循环并返回false
  return item < 5 //false
})
```

---

## `some()` 循环数组，返回布尔

**方法测试数组中是不是至少有 1 个元素通过了被提供的函数测试。它返回一个布尔**

```js
arr.some('回调函数(当前值,当前值的索引,调用some的数组){}')
let arr = [1, 2, 3]
let flag = arr.some((item, idx, arr) => {
  //轮训数组,数组中但凡有一个符合条件的item,就跳出循环并返回true;否则返回false
  return item >= 3 //true
})
console.log(flag)
```

---

## `filter()` 过滤数组

**该方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。**

```js
arr.filter('回调函数(
  "轮询的当前值",
  "轮询的当前索引值",
  "被指向的arr"
)')
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
let arr2 = arr.filter((item, idx, arr) => {
  return item > 5
})
console.log(arr, arr2) //[ 1, 2, 3, 4, 5, 6, 7, 8, 9 ] [ 6, 7, 8, 9 ]
```

---

## `sort()` 排序数组

**该方法用原地算法对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的 UTF-16 代码单元值序列时构建的**

```js
arr1.sort("回调函数('第一个用于比较的元素','第二个用于比较的元素')")
let arr1 = [5, 1, 8, 2, 4]
let arr2 = [5, 1, 8, 2, 4]
// 可以写成arr1.sort(),方法默认为从小到大排序
arr1.sort((a, b) => {
  return a - b
})
//  从大到小排序
arr2.sort((a, b) => {
  return b - a
})
console.log(arr1, arr2)
```

---

## `find()` 查找数组第一次出现的值

**改方法返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。**

```js
arr.find('回调函数(
  "轮询的当前值",
  "轮询的当前索引值",
  "被指向的arr"
)')
let arr = [1, 2, 3, 4, 5]
let num = arr.find((item, idx, arr) => {
  return item > 3
})
console.log(num) //4
```

---

## `findIndex()` 查找数组第一次值的索引

**该方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。**

```js
arr.findIndex('回调函数(
  "轮询的当前值",
  "轮询的当前索引值",
  "被指向的arr"
)')
let arr = [1, 2, 3, 4, 5]
let idx = arr.find((item, idx, arr) => {
  return item > 3
})
console.log(idx) //3
```

---
