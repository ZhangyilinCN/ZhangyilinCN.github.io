---
title: 随机排列1-20组成不重复数组
date: 2019-10-28 16:49:02
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "随机排列1-20组成不重复数组"
toc: false
---

``` javascript
var listArr=[];
var len=20;
while (listArr.length<len){
    var flag=true;
    var randomNum=Math.ceil(Math.random()*len);
     for(var i=0;i<listArr.length;i++){
         if(listArr[i]==randomNum){
             flag=false;
             break;
         }
     }
    if(flag){
        listArr.push(randomNum)
    }
}
console.log(listArr);
```
