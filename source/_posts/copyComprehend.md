---
title: 浅拷贝与深拷贝
date: 2020-12-01 11:54:43
tags:
  - 'Javascript'
categories:
  - 'Javascript'
keywords:
description: '关于浅拷贝与深拷贝自己的理解'
toc: false
---

**首先我们要知道对象和数组属于引用类型,是保存在堆中的,而像 str,num,bool 是存放在栈中的**

1. 直接拷贝

   ```js
   //Arr
   let arr = [1, 2, 3]
   let newArr = arr
   arr[0] = 99
   console.log(arr, newArr) //( [99,2,3],[99,2,3])
   //Obj
   let obj = { name: 'zs', age: 10 }
   let newObj = obj
   obj.age = 99
   console.log(obj, newObj) //( { name: 'zs', age: 99 },{ name: 'zs', age: 99 })
   ```

2. 使用方法进行拷贝

   ```js
   //Arr
   let arr = [1, 2, { name: 'zs' }]
   let newArr = arr.concat() //arr.slice()和[...arr]在这里相同
   arr[0] = 99
   console.log(arr, newArr) //[ 99, 2, { name: 'zs' } ] [ 1, 2, { name: 'zs' } ]
   arr[2].name = 'copy'
   console.log(arr, newArr) //[ 99, 2, { name: 'copy' } ] [ 1, 2, { name: 'copy' } ]
   //Obj
   let obj = { name: 'zs', list: [1, 2, 3] }
   let newObj = { ...obj }
   obj.name = 'copy'
   console.log(obj, newObj) //{ name: 'copy', list: [ 1, 2, 3 ] } { name: 'zs', list: [ 1, 2, 3 ] }
   obj.list[2] = 99
   console.log(obj, newObj) //{ name: 'copy', list: [ 1, 2, 99 ] } { name: 'zs', list: [ 1, 2, 99 ] }
   ```

3. 使用 JSON 方法来进行拷贝

   ```js
   //Arr
   let arr = [1, 2, { id: 11 }]
   let newArr = JSON.parse(JSON.stringify(arr))
   arr[2].id = 999
   console.log(arr, newArr) //[ 1, 2, { id: 999 } ] [ 1, 2, { id: 11 } ]
   //Obj
   let obj = { name: 'zs', list: [1, 2, 3] }
   let newObj = JSON.parse(JSON.stringify(obj))
   obj.list[0] = 999
   console.log(obj, newObj) //{ name: 'zs', list: [ 999, 2, 3 ] } { name: 'zs', list: [ 1, 2, 3 ] }
   ```

---

## 由此我们可以得出

1. 直接的引用数组或者对象变量,因为会指向同一个堆,所以改变任何一个变量的值,都会改变指向这个堆的其余变量的值
2. 使用方法,像`concat/slice/...`等来进行拷贝,所拷贝的对象中,应该只存在简单类型,如果其中包含对象或者数组,其中的对象和数组又会指向另外的堆,所以改变其中的数组或者对象,也会改变其他指向此堆的变量的值
3. 使用`JSON.parse(JSON.stringify(xx)`来进行拷贝,可以做到真正的深拷贝,修改戏中的值,并不会污染其他变量(不涉及之中函数的考究)
