---
title: Vue路由
date: 2019-11-12 17:07:10
tags:
  - "Vue"
categories:
  - "Vue"
keywords:
description: "Vue路由"
---

**和锚点类似**

## 路由的引用

**在模块化的开发中，需要手动明确安装路由功能**

```js
import Vue from "vue";
import VueRouter from "vue-router";
Vue.use(VueRouter);
```

```js
var haha={ template:'<h3>哈哈</h3>' }
var hehe={ template:'<h3>呵呵</h3>' }
var xixi={ template:'<h3>嘻嘻</h3>' }
var rtobj=new VueRouter({
    routes: [
        {path:'/',redirect:'/haha'},  这条表示如果地址为根目录，则重新跳转为'/haha'地址
        {path:'/haha',component: haha},
        {path:'/hehe',component: hehe},
        {path:'/xixi',component: xixi}
    ]
})
var vm=new Vue({
    el:'#app',
    router: rtobj,
})
```

**其中在 VueRouter 的实例中，path(路径地址)和 component(组件对象)这两个参数是必须的**

**在 component 中的值为一个组件对象**

```js
 //正确的
var login={
    template:'<p>xxx</p>'
}
//错误的
Vue.component('login',{
    template:'<p>xxx</p>
}
```

**注：记得在 Vue 的实例中使用 router：xx 来挂载这个 VueRouter 实例对象**

**最后只需要在页面中相关联的 div 里**

```html
<div id="app">
  <router-link to="/haha" tag="span">哈哈</router-link>
  <!--router-link在页面上默认渲染为a标签，也可以使用tag来改变其标签-->
  <router-link to="/hehe">呵呵</router-link>
  <!-- 相当于<a href='#/hehe'>呵呵</a> -->
  <router-link to="/xixi">嘻嘻</router-link>
  <router-view></router-view> 可以让路由在此显示
</div>
```

---

## 路由的按需加载

```js
{
  path: '/home',
  name:'home',
  component: resolve => require(['@/components/home'], resolve),
},
```

```html
//添加name后，可以在路由出使用name跳转
<router-link :to="{name:'home' , query:{id:'999'}}"></router-link>
<router-link :to="{name:'home' , params:{id:'999'}}"></router-link>
//这种是/home/:id/这种的
```

---

## 路由跳转的页面位置

```js
scrollBehavior (to, from, savedPosition) {
    return { x: 0, y: 0 }
},
//在配置路由中加上这个，每次跳转都会在顶部
```

---

## 编程式导航（网页的跳转）

**js中使用 `window.location.href="xxxx"`来进行跳转**
**在vue中，使用`this. $router.push(''xxxx'')`来进行跳转**
**`this.$route.query`....是用来获取url的信息**
**`this.$router.push`...是来跳转网页的**
---

## 取消 url 中的

```js
mode: "history";
```

---

## 路由的传参

### 在组件上，不修改 routes 中的 path 规则：

```html
<div id="app">
    <router-link to="/login?id=10&name=zs">登陆</router-link>
    <router-view></router-view>
</div>
<script>
var login={
    template:'<p>我是登陆,你的名字是：{{$route.query.name}}</p>',
    created:function () {
        console.log(this.$route);
        console.log(this.$route.query.id);
        console.log(this.$route.query.name);
    }
}
var rtobj=new VueRouter({
    routes:[
        {path:'/login',component:login},
    ]
})
var vm=new Vue({
    el:'#app',
    router:rtobj,
})
```

### 在 VueRouter 实例中修改 path 的值：

```html
<div id="app">
    <router-link to="/reg/10/ls">注册</router-link>
    <router-view></router-view>
</div>
<script>
var reg={
    template: '<p>我是注册,你要注册的名字是：{{$route.params.name}}</p>',
    created:function(){
        console.log(this.$route);
        console.log(this.$route.params.id);
        console.log(this.$route.params.name);
    }
}
var rtobj=new VueRouter({
    routes:[
        {path:'/reg/:id/:name',component:reg},
                    :id 站位符、表示此处的属性
    ]
})
var vm=new Vue({
    el:'#app',
    router:rtobj,
})
```

---

## 路由的命名视图

**在 VueRouter 的实例中，如果需要一次展示多个组件的话，可以使用**

```js
{
  path:'xx',
  components: {
       'default'(默认)：xxx(组件),
        'leftBox'(自定义命名): xx(组件名),
        xxx(自定义名)： xx(组件名),
  }
}
```

**然后在`<router-view>`中的 name 属性上，就可以使用自定义名来控制了**

```html
<router-view></router-view> 默认显示的
<router-view name="leftBox"></router-view> 只显示名字为leftBox上的组件
<router-view name="rightBox"></router-view> 只显示名字为leftBox上的组件
```

```html
<div id="app">
  <router-view></router-view>
  <router-view name="leftBox"></router-view>
  <router-view name="rightBox"></router-view>
</div>
<script>
  var header = {
    template: "<h4>我是头部</h4>"
  };
  var left = {
    template: "<p>我是左边</p>"
  };
  var right = {
    template: "<p>我是右边</p>"
  };
  var rtobj = new VueRouter({
    routes: [
      {
        path: "/",
        components: {
          default: header,
          leftBox: left,
          rightBox: right
        }
      }
    ]
  });
  var vm = new Vue({
    el: "#app",
    router: rtobj
  });
</script>
```

---

## 父子路由（路由的嵌套）

**在 VueRouter 的实例中的`routes`里的对象中，除了`path`，`component`还有一个`children`属性，可以在其中来设置子路由的指向与跳转等**

**注意：因为已经是在其中指明，所以子路由中的 path 不需要加前缀 '/'**

```html
<template id="home">
  <!-- 创建组件 -->
  <div>
    <h1>我是主页</h1>
    <router-link to="/home/login">登陆</router-link>
    <router-link to="/home/reg">注册</router-link>
    <router-view></router-view>
  </div>
</template>

<div id="app">
  <router-link to="/home">主页</router-link>
  <!--跳转/home地址 -->
  <router-view></router-view>
</div>

<script>
  //创建组件对象
  var login = { template: "<p>我是登陆</p>" };
  var reg = { template: "<p>我是注册</p>" };
  // 创建组件对象赋指引到#home
  var home = { template: "#home" };
  var rtobj = new VueRouter({
    routes: [
      {
        path: "/home",
        component: home,
        children: [
          { path: "login", component: login },
          { path: "reg", component: reg }
        ]
      }
    ]
  });
  var vm = new Vue({
    el: "#app",
    router: rtobj
  });
</script>
```