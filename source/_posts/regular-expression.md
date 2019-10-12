---
title: 正则表达式
date: 2019-10-11 16:18:02
tags:
  - "正则表达式"
  - "Javascript"
categories:
  - "Javascript"
keywords:
description: "简单的了解正则表达式"
toc: false
---

## 正则的创建

```javascript
let re = new RegExp("a", "g");
let re2 = /a/g;
// 通过new来创建一个正则对对象,
// 其中参数1：指定了正则表达式的模式或者其他正则表达式；
// 参数2：为可选模式的字符串，g全文匹配查询，i忽略大小写查询，m多行匹配查询；
```

---

## 使用正则判断字符串

- **使用`re.test(str)`来判断**

```javascript
var str = "abcauhfidsbg";
var re = /a/g;
var re2 = /z/i;
// re.test(str)用来测试，该匹配的字符串中是否含有指定字符项，如果有返回true，反之返回false；
console.log(re.test(str)); //true
console.log(re2.test(str)); //false
```

- **使用`re.exec(str)`来判断**

```javascript
var str = "abcauhfidsbg";
var re = /a/g;
var re2 = /z/i;
// re.exec(str)用来测试，匹配字符串中如果有指定项，则返回匹配到的数组，如果没有则返回null；
console.log(re.exec(str)); //["a",index:0,input:"abcauhfidsbg"]
console.log(re2.exec(str)); // null
```

---

## 正则表达式的诠释

**注意所有书写的正则表达式都应当有头(^)有尾(\$)!!**

- **字符类**

```javascript
/[^0-5]/  //表示匹配非0-5之间字符 [^..]非..
/\d/      //匹配任意一个数字0-9
/\D/      //匹配任意非数字的字符
/\s/      //匹配任意空白字符(如空格，换行符等)
/\S/      //匹配任意非空白字符
/\w/      //匹配任何英文字母，数字以及下划线
```

- **量词**

```javascript
/ab?/     //表示匹配前一项b 0次或者1次
/a+/      //表示匹配前一项a  至少1次或者多次
/a*/      //表示匹配前一项a  0次或着多次
/ab{3}/   //表示匹配的前一项b正好3次
/ab{3,}/  //表示匹配的前一项b至少3次
/ab{3,5}/ //表示匹配的前一项b出现3-5次之间(包含3次和5次)
```

- **demo**

```javascript
var re = /^[abc]{3,5}(\d)+[^a-z]?$/;
//该正则表示：
// 开头以[abc]任意一个开始，并且持续3-5位，
//随后跟\d(0-9)之间的随机数字至少一次或者多次，
//最后跟[^a-z]非小写字母a-z的字符0次或者一次；
var str1 = "aaaaaaA";
var str2 = "aa123A0";
var str3 = "abbc123A";
console.log(re.test(str1));
false;
console.log(re.test(str2));
false;
console.log(re.test(str3));
true;
```
