---
title: webpack导入vue
date: 2019-11-14 10:30:26
tags:
  - 'Vue+webpack'
  - 'Vue-cli'
categories:
  - 'Vue-cli'
keywords:
description: 'webpack导入vue'
toc: false
---

**在项目中安装 vue 并使用**

```js
npm i vue -s
```

**然后在 main.js**

```js
import Vue from 'vue'
var vm = new Vue({
  el: '#app',
  data: {
    msg: 123
  }
})
```

## 打包后发现会报错，因为 vue 在 webpack 中使用的是 vue.common.js 然不是完整的 vue.js，所以如果想要使用实例化这种的 vue 方法需要以下配置

### 第一种-修改路径

```js
import Vue from 'vue/dist/vue.js'
```

### 第二种-配置 webpack.config.js

```js
import Vue from 'vue' //这边不动
```

![webpack-go-vue1.jpg](https://i.loli.net/2019/11/15/5KokFRbaZBY3WlJ.jpg)

```js
resolve: {
 alias: {
   "vue$":"vue/dist/vue.js"
 }
}
```

---