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


**node中的导入为`var 名称=require('模块的标识符')`、暴露为`module.exports`和`exports`**

**es6 中的导入为`import`、暴露为`export default`和`export`**

``` js
export default {
  name:'zs',
  age:55
}
export var ex1 = {name:'ex1',age:99}
export var ex2 = {name:'ex2',age:88}
```

``` js
import aaa,{ex1,ex2 as ex222} from  "./test.js"
//第一个aaa是导入export default暴露的，所以变量名随意
//第二个ex1是导入export暴露的，要在{}之中写，并且名字要相同
//第三的是修改暴露成员ex2的自定义名字
console.log(aaa);
console.log(ex1);
console.log(ex222);
```

**使用`export default`向外暴露的，在使用`import`接收的时候，参数名随意，但是在js中有且只能有一个使用`export default`暴露的成员**

**而使用`export`可以向外暴露多个，但是使用`import`接收的时候，要在{}之中写，并且名字要与暴露的名字相同，如果想要使用自定义的名字的话，可以在暴露成员后接 `as` 自定义名字  （这种叫做按需导出）**

