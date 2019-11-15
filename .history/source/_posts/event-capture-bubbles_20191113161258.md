---
title: 事件的捕获与冒泡
date: 2019-10-16 10:51:44
tags:
  - "Dom"
  - "Javascript"
categories:
  - "Javascript"
keywords:
description: "事件的捕获与冒泡"
toc: false
---

## 当你点击了一个事件的时候，系统会先从最外层进行捕获事件到此最深层的事件源，然后在从事件源冒泡到最外层的 document。

**注意 IE8 和 Opera 老版本仅支持冒泡事件，不支持捕获事件**

```html
<div class="box">
  <div class="box1"></div>
</div>
```

- 父元素和子元素都是捕获事件的时候: 输出结果为 1,2
```javascript
var box =document.getElementsByClassName('box')[0];
var box1 =document.getElementsByClassName('box1')[0];
box.addEventListener('click',function(){
    console.log(1);;
},true)
box1.addEventListener('click',function(){
    console.log(2);
},true)
```
- 父元素和子元素都是冒泡事件的时候: 输出结果为 2,1
```javascript
var box =document.getElementsByClassName('box')[0];
var box1 =document.getElementsByClassName('box1')[0];
box.addEventListener('click',function(){
    console.log(1);;
},false)
box1.addEventListener('click',function(){
    console.log(2);
},false)
```

- 父元素为捕获,子元素为冒泡的时候:输出返回 1,2
```javascript
var box =document.getElementsByClassName('box')[0];
var box1 =document.getElementsByClassName('box1')[0];
box.addEventListener('click',function(){
    console.log(1);;
},true)
box1.addEventListener('click',function(){
    console.log(2);
},false)
```

- 父元素为冒泡,子元素为捕获的时候:返回 2,1
```javascript
var box =document.getElementsByClassName('box')[0];
var box1 =document.getElementsByClassName('box1')[0];
box.addEventListener('click',function(){
    console.log(1);;
},false)
box1.addEventListener('click',function(){
    console.log(2);
},true)
```


![](https://wx2.sinaimg.cn/large/ed984376ly1g8wgfl29onj20ff0ert9a.jpg)
