---
title: 导入和暴露用法
date: 2019-11-14 11:17:38
tags:
  - 'Vue-cli'
categories:
  - 'Vue-cli'
keywords:
description: '导入和暴露用法'
toc: false
---


**node中的导入为var 名称=require('模块的标识符')、暴露为module.exports和exports**

**es6 中的导入为import、暴露为export default和export**

``` js
export default {
  name:'zs',
  age:55
}
export var ex1 = {name:'ex1',age:99}
export var ex2 = {name:'ex2',age:88}
```

