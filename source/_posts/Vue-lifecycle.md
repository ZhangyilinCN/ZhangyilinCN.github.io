---
title: Vue生命周期与构造方法
date: 2019-11-11 17:21:35
tags:
  - "Vue"
categories:
  - "Vue"
keywords:
description: "Vue生命周期与构造方法"
toc: false
---

``` js
var vm=new Vue({
    el:'#app',
    data:{
        msg:123456,
    },
    methods:{
        show:function () {
            console.log('Go,Show!');
        },
        go:function () {
            this.msg+='AAAAA';
        }
    },
    ！！创建阶段！！
    beforeCreate:function () { 实例化被完全创建之前，会先执行此函数(其中data和methods中的数据还未被初始化)
        console.log(this.msg); undefined
            this.show();  报错显示没有此方法
    },
    created:function () {  在这之中，data和methods中的数据都已经被初始化好了，可以用来使用与变更
            console.log(this.msg); 123456
            this.show();           Go Show!
    },
    beforeMount:function () { 表示模板已经在内存中完成编辑了，但是还没有渲染到页面当中
            console.log(document.getElementsByTagName('p')[0].innerText); 输出页面中的p中的内容，结果为{{msg}}
    },
    mounted:function () { 表示模板已经在内存中完成了编辑了,用户已经可以看到已经渲染好的页面了
            console.log(document.getElementsByTagName('p')[0].innerText); 结果为123456
    },

    ！！运行阶段！！
    运行中的两个事件
    beforeUpdate:function () {  此时data中的数据已经被更新，而在页面上却依旧是原来旧的数据（页面尚未和最新的数据保持同步）
            console.log(this.msg);   改变后的123456AAAAA
            console.log(document.getElementsByTagName('p')[0].innerText); 为改变的123456
    },
    updated:function () {  此时data与页面上的数据保持了同步，都是最新的了
        console.log(this.msg);   改变后的123456AAAAA
        console.log(document.getElementsByTagName('p')[0].innerText); 为改变的123456AAAAA
    },

        ！！销毁阶段(当用户关闭页面是，就处于了销毁阶段)
    beforeDestroy:function(){    销毁前，所有的数据都处于可用状态，未被真正的销毁
    },
    destroyed:function () {   什么都不可用了
    }
})
```
