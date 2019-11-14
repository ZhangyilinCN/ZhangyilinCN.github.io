---
title: webpack中vue组件的识别与应用
date: 2019-11-14 11:28:59
tags:
  - 'Vue+webpack'
  - 'Vue-cli'
categories:
  - 'Vue-cli'
keywords:
description: 'webpack中vue组件的识别与应用'
toc: false
---

**webpack 打包无法处理.vue 后缀的文件，所以需要先下载**

```js
npm i vue-loader vue-template-compiler -d
```

**如果然后安装的 vue-loader 是 15.x.x 以上的需要配置 webpack.config.js**

![](https://wx3.sinaimg.cn/large/ed984376ly1g8xev5i8gwj20xq0ozmyk.jpg)

```js
const VueloaderPlugin=require('vue-loader/lib/plugin')
new VueloaderPlugin()
{test: /\.vue$/, use: 'vue-loader'}
```

**最后在 main.js 中引入所需的.vue 文件，就可以打包执行了**

```js
import Vue from 'vue'
import login from './login.vue' //引入的vue组件

var vm = new Vue({
  el: '#app',
  data: {
    msg: 123
  },
  render(creatEle) {
    //调用render进行页面的渲染
    return creatEle(login)
  }
})
```

--
