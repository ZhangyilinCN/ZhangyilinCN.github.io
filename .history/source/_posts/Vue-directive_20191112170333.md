---
title: Vue自定义指令
date: 2019-11-12 16:59:11
tags:
  - "Vue"
categories:
  - "Vue"
keywords:
description: "Vue自定义指令"
toc: false
---

**像 v-if，v-show 等，是 Vue 已经内置的指令，我们也可以使用 directive 来自定义指令**

```html
<input type="text" v-focus v-color="'blue'" />
其中的blue要被引号所包裹，不然会被识别为变量来进行查找
```

```js
//全局自定义指令;
Vue.directive("focus", {
  inserted: function(el) {
    el.focus();
  }
});
Vue.directive("color", {
  bind: function(el, binding) {
    el.style.color = binding.value;
  }
});
```

```js
var vm = new Vue({
  el: "#app",
  //私有自定义指令
  directives: {
    demo: {
      bind: function(el, binding) {
        el.style.color = binding.value.color;
        el.style.fontWeight = binding.value.weight;
        el.style.background = binding.value.background;
      }
    }
    /*简写形式，代表我们这个demo写在了bind和update这两个之中
        demo:function (el,binding) {
            el.style.color=binding.value.color;
            el.style.fontWeight=binding.value.weight;
            el.style.background=binding.value.background;
        }
        */
  }
});
```

---

## Vue.directive（'定义的指令名字'，{ 对象方法 }）

**定义是不需要添加 v-前缀，在使用时则需要添加 v-前缀**

```
其中在对象方法中：
    --元素是从内存渲染到页面上的，
    bind:function...
    每当指令绑定到元素上的时候，会立即执行这个，且只执行1次
    *在此上绑定的事件，在内存中的时候就已经被从里（一般用于样式的绑定处理）

    inserted:function....
    当元素插入到DOM中的时候，会执行，且执行一次
    *在内存到页面上时，才做处理的（一般用于js的行为处理）
    update:function...
    当VNode（组件）更新的时候，会执行，可能会触发多次
bind：function（el,binding,Vnode,oldVnode）{ xxx }
其中：
el：表示被绑定的那个元素，是个原生js对象，可以时候js的行为方法；
binding：一个对象，里面包含了name（不加前缀的名字）、value（绑定的值）、expression（未处理的绑定值等等..）
Vnode和oldVnode：虚拟节点
```

**如果需要传多个值，可以使用字面量的形式**

```
 <p v-demo="{color:'red',weight:'800',background:'green'}">1231313</p>
   Vue.directive('demo',{
        bind:function (el,binding) {
            el.style.color=binding.value.color;
            el.style.fontWeight=binding.value.weight;
            el.style.background=binding.value.background;
        }
    })
```
