---
title: Vue组件的切换与过渡
date: 2019-11-12 18:09:33
tags:
  - "Vue"
  - "Demo"
categories:
  - "Vue"
keywords:
description: "vue组件的切换与过渡"
toc: false
---

## 使用`v-if`、`v-else-if`、`v-else`来进行组件之间的切换

``` html
<div id="app">
    <a href="javascript:;" @click="flag=0">000</a>
    <a href="javascript:;" @click="flag=1">111</a>
    <a href="javascript:;" @click="flag=2">222</a>
    <f0 v-if="flag==0"></f0>
    <f1 v-else-if="flag==1"></f1>
    <f2 v-else></f2>
</div>
<script>
    Vue.component('f0',{
        template:'<p>我是000</p>'
    })
    Vue.component('f1',{
        template:'<p>我是111</p>'
    })
    var vm=new Vue({
        el:'#app',
        data: {
            flag:0
        },
        components:{
            f2:{
                template: '<p>我是222</p>'
            }
        }
    })
</script>

```
