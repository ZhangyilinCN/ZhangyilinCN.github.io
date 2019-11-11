---
title: Vue动画效果
date: 2019-11-11 16:46:06
tags:
  - "Vue"
categories:
  - "Vue"
keywords:
description: "Vue动画效果"
toc: false
---
## 在Vue中所有的动画创建，都需要被`<transition>`标签来包裹
**使用`<transition>`标签可以给任何的元素和组件添加进入、离开的过度**
### 动画的经过：
``` 
v-enter  -->   v-enter-to    ||   v-leave   -->  v-leave-to
```
**所以就可以在css中来给予： 进入时`v-enter`和退出时`v-leave-to`样式**
**在再`v-enter-active`和`v-leave-active`定义过度时间等，来完成完整的动画效果**
``` html 
<style>
   .app1-enter,.app1-leave-to {
        opacity: 0;
   }
   .app1-enter-active,.app1-leave-active {
         transition: opacity 1s linear;
    }
</style>
<div id="app">
    <button @click="flag=!flag" >GO!!!</button>
     <transition name="app1">  //如果不给予name时，css中使用v-enter..,定义了名字后使用名字-enter(app1-enter)..
          <p v-if="flag">我是PPPPPP</p>
      </transition>
</div>
<script>
    var vm=new Vue({
        el:'#app',
        data:{
            flag:false,
        }
     })
</script>
```

---

## 使用第三方库来进行动画效果
``` html
<link rel="stylesheet" href="../vue.js/animate.css"> 这里使用animate.css
<style>
     p {
         display: inline-block;
         font-size: 30px;
         color: red;
     }
     .box {
          width: 50%;
          height: 3000px;
          border: 1px solid #000;
          margin: 100px auto;
      }
</style>
<div id="app">
    <div class="box">
        <input type="button" @click="flag=!flag" value="弹出">
        <transition enter-active-class="bounceIn" leave-active-class="bounceOut" :duration="300">
            <p v-if="flag" class="animated">111111111111111</p>
        </transition>
        <input type="button" @click="flag1=!flag1" value="淡出">
        <transition enter-active-class="fadeIn" leave-active-class="fadeOut" :duration="{ enter:500,leave:300 }">
            <p v-if="flag1" class="animated">111111111111111</p>
        </transition>
        <input type="button" @click="flag2=!flag2" value="滑进">
        <transition enter-active-class="zoomIn" leave-active-class="zoomOut" :duration="{ enter:500,leave:300 }">
            <p v-if="flag2" class="animated">111111111111111</p>
        </transition>
    </div>
</div>
<script>
    var vm=new Vue({
        el:'#app',
        data:{
            flag:false,
            flag1:false,
            flag2:false,
        }
    })
</script>
```

**直接在`<transition>`中 添加  进场类名（enter-active-class） 和 离场类名 （leave-active-class）即可，**
**其中多了属性  `:duration` ：表示设置进出时的时间**

---

## 使用JS钩子函数进行动画（半场动画）:

``` html
<transition
      入场动画
      @before-enter="函数名"   --进入前
      @enter="ent"            --进入
      @after-enter="aftEnt"   --进入后
      @enter-cancelled='..'   --取消进入时  
      离场动画
      @before-leave='函数名'   --离开前
      @leave='lea'            --离开
      @after-leave='aftLea'   --离开时
      @leave-cancelled='..'   --取消进入时  
>
      <span v-show="flag"></span>
</transition>
```
**由此就可以根据命名的函数名在methods中定义需要的动画效果了**

``` js
methods: {
    efEnt:function (el) { 
     此时动画尚未开始，可以在其中设置元素动画开始之前的起始样式，初始位置等..
         el.innerHTML=1;  
         el.style.transform='translate(0,0)'
    },
    ent:function (el,done) {
         el.innerHTML=2;
         el.offsetWidth; 必须加，否则会出现强制位移，没有动画的效果。可以理解为强制刷新页面
         el.style.transform='translate(100px,500px)'
         el.style.transition='all 1s'
         done()  必须加，可以看做是立即执行进入后(aftEnt)的回调
    },
    aftEnt:function (el) {
          this.flag=!this.flag
    }
    .....离开函数同理
}
```













