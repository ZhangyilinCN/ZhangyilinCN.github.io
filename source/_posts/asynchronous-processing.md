---
title: 'promise处理接口'
date: 2022-11-16 18:00:56
tags:
  - "Javascript"
categories:
  - "Javascript"
keywords:
description: '循环接口同步处理后，在执行下面逻辑代码'
toc: false
---

### 应用场景：要多次调取一个接口上传图片，等所有图片上传完成后，在进行后边的代码逻辑(提交表单等等..)

``` javascript
let arr = [1, 2, 3, 4, 5]; //模拟存放的图片集合

// 循环批量处理图片上传
async function uploadMoreFilesFn() {
//这里一定要用for，不能用其他的循环（forEach，map...）
  for (let i = 0; i < arr.length; i++) {
    await uploadFileFn(arr[i]);
  }
}

// 单次提交的接口 
function uploadFileFn(item) {
  return new Promise((res) => {
    setTimeout(() => {
      console.log(item);
      res();
    }, 1000);
  });
}

// 最后逻辑代码块
async function formSubmitFn() {
  await uploadMoreFilesFn();
  setTimeout(() => { //模拟最后的form表单提交
    console.log("成功;");
  }, 4000);
}

fn2();
//最后的执行为，每1秒打印一次i，执行完毕后，再等4秒打印成功
```