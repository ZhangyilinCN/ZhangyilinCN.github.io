---
title: '处理string中的img标签'
date: 2022-11-16 18:18:33
tags:
  - "Javascript"
categories:
  - "Javascript"
keywords:
description: '在字符串中把img的所有替换为src的路径'
toc: false
---


### 在字符串中把img的所有替换为src的路径

#### 效果如下

``` javascript
// let stringA = "12哈哈<img src='123.png' class='aa' style='color:red' />321嘻嘻"
// let NewA = 12哈哈[123.png]321嘻嘻
```


##### 实际代码

``` javascript
// 注意这边的 class、style 一定要放到src之后！！！！！！！
let str =
  '11<img  src="blob:https://192.168.3.253:8080/5ee83f8c-a5d0-4f44-bc57-105e80b4c412" class="pasteImgs">1114<img  src="blob:https://192.168.3.253:8080/0feff3da-743a-4157-b150-b8e4b3a55c32" class="pasteImgs">443';

function fn1(article) {
  var regExp = /<img\s*src=\"([^\"]*?)\"[^>]*>/gi;
  let result = article.replace(regExp, (match, offset) => {
    return `[${offset}]`;
  });
  return result;
}
let aa = fn1(str);
//11[blob:https://192.168.3.253:8080/5ee83f8c-a5d0-4f44-bc57-105e80b4c412]1114[blob:https://192.168.3.253:8080/0feff3da-743a-4157-b150-b8e4b3a55c32]443
```


