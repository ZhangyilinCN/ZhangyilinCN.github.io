---
title: Vue计算属性
date: 2019-11-11 17:09:22
tags:
  - "Vue"
categories:
  - "Vue"
keywords:
description: "Vue计算属性"
toc: false
---

## 计算属性：
**根据`data`中的值，定义一个函数方法，使其经过二次计算运算等，返回其他值来运用；**

``` js
var vm=new Vue({
    el:'xx',
    data:{   //属性
        msg:'xxx',
        },
    watch:{  //监听
        xx:function(newval,oldval){
            .....
           }},
    methods:{  //方法
        xxx:function(){
            ....    
        }},
    computed:{  //计算属性  
    //计算属性：当所用的属性data被改变时，其所运用到的计算属性也会被改变      
        xx:function(){
            xxxxdataxxxx
            return xx;
        }}
});
```
---
## 计算属性的缓存 VS 方法`methods`
**在`computed`（计算属性）中，计算属性的方法是基于属性的依赖来进行处理与缓存的，所以只有当所运用的`data`属性发生改变时，在`computed`中，所包含其`data`属性的计算属性`computed`才会跟着改变。**
**而方法则不然，方法`methods`所用之处每次都会调用执行。**
**在某些巨大数据开销上，使用计算属性所产生的缓存后，就可以防止相同属性进行多次的访问。**
---
## 计算属性和侦听器`watch`
**`watch`监听时，因为监听方法的特性，所以会有`oldval`和`newval`的产生，所以会出现大量冗余代码,**
**而直接使用`computed`，应为其依赖`data`，所以会更好的运用。**

---
## 计算属性的setter
**`computer`（计算属性）默认的话是只有`getter`，在需要的时候，也可以为其添加`setter`属性（要为对象添加时才能添加`getter`和`setter`）**

``` js
new Vue({
   data:{xxx},
   watch: {xx:function(oldval,newval){xxxxx}},
   methods: {xx:function(){xxxx}},
   computer:{
        xxxx:{
            get:function(){......}
            set:function(){......}
   }
}) 
// setter-一般都会定义来控制改写父层data
// 在调用运用computer中的对象xxxx时，其中的set会为其改变父层的data,从而重渲染
```

---









