---
title: VueX总结
date: 2019-11-12 18:14:26
tags:
  - "Vue"
categories:
  - "Vue"
keywords:
description: "VueX总结"
---

**`vuex`是用来保存组件之间的共享数据，如果组件之间有要共享的数据，可以直接挂载到`vuex`中，而不必通过`props`和`emit`来进行传值**

## 安装

`npm i vuex -s`

---

## 在 main.js 引入并使用

```js
import vuex from "vuex";
vue.use(vuex);
```

---

## 创建

```js
const store =new Vuex.Store( {
    state : {   //state类似于vue中的data，用来存放共享数据的
        count : 0
    },
    mutations : {   //类似于vue中的methods，用来存放方法的
        fn(state) {
            state.count++;
        }
    },
    getters: {  //类似于vue中的computed和filter
        orderFn(state)  {
           return 'count的值为：'+state.count
        }
})
```
### `state`
**其中`state`类似于`vue`中的`data`，用来存放共享数据的**

**在组件中通过`$store.state.count` / `this.$store.state.count`来进行访问**

```html
<p>当前数量为；{{$store.state.count}}</p>
```
### `mutations-1`

**`mutations`类似于`vue`中的`methods`，用来专门操作`state`中的数据的（如果要操作`state`中的数据的话，尽量在`mutations`中使用，而不是在各组件的`methods`中使用）**

**如果组件想要使用`mutations`中的方法的话，需要通过`$store.commit('方法名')` / `this.$store.commit('方法名')` 来进行调用**

```html
<button @click="$store.commit('jianNum')">---</button>
<button @click="jian">---</button>
```
```js
methods: {
    jian() {
        this.$store.commit('jianNum')
    }
}
```
### `mutations-2`

**如果方法有参数的话：(在`mutations`的方法中，最多只支持 2 个参数：1 是`state`、2 是自定义参数[如果想要使用多个参数，可以把 2 定义为`arr`或`obj`])**

```js
    //vuex
    mutations: {
        jianNum(state,num) {
        state.count-=num
        }
    }
    methods: {
        jian() {
            this.$store.commit('jianNum',5)
        }
    }
```
```html
<button @click="$store.commit('addNum',3)">+++</button>
```

### `getters`
**`getters`只负责对外提供数据，不负责修改数据，如果要修改数据，请用`mutations`，`getters`类似于`vue`中的`filter`，没有修改`state`中的值，只不过是对其进行了加工包装，其次和`computed`类似，当`state`中的值发生改变时，也会立即触发`getters`的重新求值**

```js
getters: {  //类似于vue中的computed和filter
    orderFn(state)  {
      return 'count的值为：'+state.count
}
```

```html
<p>{{$store.geeters.orderFn}}</p>
```
---