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
### 使用`v-if`来进行切换时，`v-else`与`v-else-if`一定要紧跟着v-if后面

---

## 使用`<component>`定义多个切换：
``` html
<div id="app">
    <a href="#" @click.prevent="tips='A'">AAA</a> 在其中tips的赋予值一定要用引号所包裹
    <a href="#" @click.prevent="tips='B'">BBB</a> 不然会被当做变量来处理
    <a href="#" @click.prevent="tips='C'">CCC</a>
    <a href="#" @click.prevent="tips='D'">DDD</a>
    <component :is="tips"></component>    然后使用：is来绑定变量，进行切换
</div>
<script>
    Vue.component('A',{
        template:'<p>AAAAAAA</p>'
    })
    Vue.component('B',{
        template:'<p>BBBBBBB</p>'
    })
    Vue.component('C',{
        template:'<p>CCCCCCC</p>'
    })
    Vue.component('D',{
        template:'<p>DDDDDDD</p>'
    })
    var vm=new Vue({
        el:'#app',
        data:{
            tips:'A'
        }
    })
</script>
```



