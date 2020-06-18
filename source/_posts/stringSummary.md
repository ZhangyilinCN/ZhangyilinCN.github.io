---
title: String方法总结
date: 2020-06-08 16:49:22
tags:
  - 'Javascript'
categories:
  - 'Javascript'
keywords:
description: 'String方法总结'
---

## `charAt()` 返回指定位 str

**该方法从一个字符串中返回指定的字符。**

```js
let str = 'ABCD'
console.log(str.charAt(2)) //C
```

---

## `concat()` 拼接多个 str

**该方法将一个或多个字符串与原字符串连接合并，形成一个新的字符串并返回。**

```js
//此方法性能不如+、+=
let str1 = 'AB'
let str2 = 'CD'
let str3 = 'EF'
let str4 = str1.concat(str2, str3)
console.log(str4) //ABCDEF
```

---

## `endsWith()` 检索 str 末尾

**该方法用来判断当前字符串是否是以另外一个给定的子字符串“结尾”的，根据判断结果返回 true 或 false。**

```js
str.endsWith('要搜索的Str', '所有str的多少位(默认为整个str的长度)')
let str1 = 'aaa'
let str2 = 'asiud iis ksdkas  hgdfg aaa'
console.log(str2.endsWith(str1)) //true
console.log(str2.endsWith(str1, 10)) //false
```

---

## `includes()` 检索 str 返回布尔

**该方法用于判断一个字符串是否包含在另一个字符串中，根据情况返回 true 或 false。**

```js
str.includes('要搜索的str', '从第几位索引开始')
let str1 = 'aaa'
let str2 = 'as aaa hg'
console.log(str2.includes(str1)) //true
console.log(str2.includes(str1, 5)) //false
```

---

## `indexOf()` 检索 str 返回布

**方法返回调用它的 String 对象中第一次出现的指定值的索引，从 fromIndex 处进行搜索。如果未找到该值，则返回 -1。**

```js
str.indexOf('要搜索的str', '从第几位索引开始')
let str1 = 'aaa'
let str2 = 'as aaa hg'
console.log(str2.indexOf(str1)) //3
console.log(str2.indexOf(str1, 5)) //-1
```

---

## `lastIndexOf()` 逆向检索 str 返回布

**该方法返回调用 String 对象的指定值最后一次出现的索引，在一个字符串中的指定位置 fromIndex 处从后向前搜索。如果没找到这个特定值则返回-1 。**

```js
str.indexOf('要搜索的str', '从结尾的第几位索引开始')
let str1 = 'aa'
let str2 = 'bb aa cc aa'
console.log(str2.lastIndexOf(str1)) //9
console.log(str2.lastIndexOf(str1, 3)) //3
```

---

## `padEnd()` 末尾补位 str

**该方法会用一个字符串填充当前字符串（如果需要的话则重复填充），返回填充后达到指定长度的字符串。从当前字符串的末尾（右侧）开始填充。**

```js
str.padEnd('限定的长度', '补位的str')
let str1 = '0123'
let str2 = str1.padEnd(7, 'AB') // '0123ABA'
let str3 = str1.padEnd(1, 'AB') // '0123'
```

---

## `padStart()` 开头补位 str

**该方法用另一个字符串填充当前字符串(重复，如果需要的话)，以便产生的字符串达到给定的长度。填充从当前字符串的开始(左侧)应用的。**

```js
str.padStart('限定的长度', '补位的str')
let str1 = '0123'
let str2 = str1.padStart(7, 'AB') // 'ABA0123'
let str3 = str1.padStart(1, 'AB') // '0123'
```

---

## `repeat()` 重复 str

**构造并返回一个新字符串，该字符串包含被连接在一起的指定数量的字符串的副本。**

```js
str.repeat('num')
let str = 'abc'
console.log(str.repeat(3)) //abcabcabc
console.log(str.repeat(1.5)) //abc
```

---

## `replace()` 正则查询替换

**该方法返回一个由替换值（replacement）替换一些或所有匹配的模式（pattern）后的新字符串。模式可以是一个字符串或者一个正则表达式，替换值可以是一个字符串或者一个每次匹配都要调用的回调函数。**

```js
str.replace('正则', '替换项')
let str1 = 'abcd11abcd'
let str2 = str1.replace(/abcd/, 'ABCD') //ABCD11abcd
let str3 = str1.replace(/abcd/g, 'ABCD') //ABCD11ABCD
```

---

## `slice()` 截取 str 得到新 str

**该方法提取某个字符串的一部分，并返回一个新的字符串，且不会改动原字符串。**

```js
str.slice('起始索引', '结束索引')
let str1 = 'abcdefg'
let str2 = str1.slice(0, 2) //ab
let str3 = str1.slice(0, -1) //abcdef
let str4 = str1.slice(0, -3) //abcd
let str5 = str1.slice(-4) //defg
```

---

## `substring()` 截取 str 得到新 str

**方法返回一个字符串在开始索引到结束索引之间的一个子集, 或从开始索引直到字符串的末尾的一个子集。**

```js
str.substring('起始索引', '结束索引')
//如果起始索引大于结束索引,则起始索引变为结束,结束的变为其实,进行截取
//如果参数中出现小于0的参数,怎当做0处理
let str = '01234567'
console.log(str.substring(0, 3)) //012
console.log(str.substring(4, 2)) //23
console.log(str.substring(-4, 2)) //01
```

---

## `split()` str 转化 arr

**方法使用指定的分隔符字符串将一个 String 对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置。**

```js
str.split('作为被分割的指引str', '分割后数组最大长度')
let str = 'asdqswezsxc'
let arr1 = str.split() // [ 'asdqswezsxc' ]
let arr2 = str.split('') // [ 'a', 's', 'd', 'q', 's', 'w', 'e', 'z', 's', 'x', 'c' ]
let arr3 = str.split('-') //['asdqswezsxc']
let arr4 = str.split('e') //[ 'asdqsw', 'zsxc' ]
let arr5 = str.split('', 2) //[ 'a', 's' ]
```

---

## `startsWith()` 判断 str 开头

**该方法用来判断当前字符串是否以另外一个给定的子字符串开头，并根据判断结果返回 true 或 false。**

```js
let str = 'aabbccd'
console.log(str.startsWith('a')) //true
console.log(str.startsWith('aa')) //true
console.log(str.startsWith('aaa')) //false
```

---

## toLocaleLowerCase() 把 str 变为小写

**方法根据任何指定区域语言环境设置的大小写映射，返回调用字符串被转换为小写的格式。**

```js
let str = 'ABCD'
console.log(str.toLocaleLowerCase()) //abcd
```

---

## toLowerCase() 把 str 变为小写

**会将调用该方法的字符串值转为小写形式，并返回。**

```js
let str = 'ABCD'
console.log(str.toLowerCase()) //abcd
```

---

## toLocaleUpperCase() 把 str 变为大写

**方法根据本地主机语言环境把字符串转换为大写格式，并返回转换后的字符串。**

```js
let str = 'abcd'
console.log(str.toLocaleUpperCase()) //ABCD
```

---

## toUpperCase() 把 str 变为大写

**方法将调用该方法的字符串转为大写形式并返回（如果调用该方法的值不是字符串类型会被强制转换）。**

```js
let str = 'abcd'
console.log(str.toUpperCase()) //ABCD
```

---

## `toString()` 转为 str

**该方法返回指定对象的字符串形式。**

```js
let num = 123
let str = num.toString()
console.log(num, typeof num) //123 'number'
console.log(str, typeof str) //123 string
```

---

## `trim()` 去除 str 的两端空白字符

**方法会从一个字符串的两端删除空白字符。在这个上下文中的空白字符是所有的空白字符 (space, tab, no-break space 等) 以及所有行终止符字符（如 LF，CR 等）。**

```js
let str = '   11 22    '
console.log(str.trim()) //'11 22'
```

---

## `trimStart()` 去除 str 的开端空白字符

**该方法从字符串的开头删除空格。trimLeft() 是此方法的别名。**

```js
let str = '  12  '
console.log(str.trimStart()) //'12  '
```

---

## `trimEnd()` 去除 str 的结尾空白字符

**方法从一个字符串的末端移除空白字符。trimRight() 是这个方法的别名。**

```js
let str = '  12  '
console.log(str.trimStart()) //'  12'
```

---
