---
title: webpack+vue路由的配置与分离
date: 2019-11-14 11:00:30
tags:
  - 'Vue+webpack'
  - 'Vue-cli'
categories:
  - 'Vue-cli'
keywords:
description: 'webpack+vue路由的配置与分离'
toc: false
---

## 因为要使用路由，所以先下载
``` js
npm i vue-router -s
```

## 然后在main.js中导入与使用它

``` js
import VueRouter from 'vue-router'
Vue.use(VueRouter);
```

## 路由的分离，是新建一个js文件（router.js）然后在里面进行配置

``` js
import VueRouter from 'vue-router' 配置路由要先引入路由
import login from './main/login.vue' 导入需要的组件
import reg from './main/reg.vue'
import aa from './main/aa.vue'
import bb from './main/bb.vue'
 
var router=new VueRouter({  //进行路由配置
  routes: [
    {path:'/',redirect:'/login'},
    {path:'/login',component:login,children:[
        {path:'/',redirect: 'aa'},
        {path:'aa',component:aa},
        {path:'bb',component:bb}
      ]},
    {path:'/reg',component:reg}
  ]
})
export default router  //最后记得要暴露一下成员，否则main.js拿不到配置项
```

## 最后在main.js中导入，并引入路由就可以了

![](https://wx1.sinaimg.cn/large/ed984376ly1g8xe01vro7j20jj0as3yg.jpg)

---