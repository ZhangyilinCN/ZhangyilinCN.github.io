---
title: 数组获取重复项
date: 2019-10-28 16:35:09
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "数组获取重复项"
toc: false
---
``` javascript
var arr=[1,17,2,55,55,8];
console.log(res(arr));
// 数组取重函数
function res(array) {
    var newArr=[];
    // 先让原数组进行大小排序
    array.sort(function (a,b) {
        return a-b;
    });
    // console.log(array) [1, 1, 1, 2, 2, 2, 2, 3, 4, 7, 8, 10, 10, 15];
    // 然后运用循环遍历,筛选一次重复项
    for(var i=0;i<array.length;i++){
        if(array[i]==array[i+1]){
            newArr.push(array[i])
        }
    }
    // 如果数组中没有重复项则直接返回原数组
    if(newArr.length<=0){
        return array;
    }
    // console.log(newArr)  [1, 1, 2, 2, 2, 10];
    // 创建一个新的数组,并先赋予它排好后数组的第一个值
    var winArr=[newArr[0]];
    // console.log(winArr) [1];
    // 双重循环开始遍历
    for(var i=0;i<newArr.length;i++){
        for(var j=0;j<winArr.length;j++){
            var flag=false;
            // 运用闭合开关提取和新数组不相同的项
            if(newArr[i]!=winArr[j]){
                flag=true;
            }
        }
        if(flag){
            // 然后添加至新数组当中
            winArr.push(newArr[i]);
        }
    }
    return winArr;
}
```
