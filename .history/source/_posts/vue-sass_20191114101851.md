---
title: scss/sass在vue的使用
date: 2019-11-14 10:11:34
tags:
  - 'Vue'
  - 'scss/sass'
categories:
  - 'scss/sass'
keywords:
description: 'scss/sass在vue的使用'
toc: false
---

**在 vue 的 css 样式中，使用@import 和@include 可以导入和使用外部的 scss/sass**

![](https://wx1.sinaimg.cn/large/ed984376ly1g8xclpat3ij20lh05t748.jpg)

**就是在.talk 这个类中使用外层 scss 中定义好的 mixin 方法；**

---

## scss 的全局使用

**如果想要全局定义使用某个 scss 文件时，除了 scss 的 2 个依赖（sass-loader 和 node-sass）外，还需要现在（sass-resources-loader）这个依赖**

```js
npm sass-resources-loader -d
```

## 修改配置

**下载完成后，在 build 中的 utils.js 中进行配置 （注意修改你引入的路径）**

![](https://wx2.sinaimg.cn/large/ed984376ly1g8xcltc2kuj20tt0cj3yr.jpg)

## 使用

**之后就可以在你的 vue-cli 中的任何组件中，使用@include 来使用这里面的内容了**

```js
scss: generateLoaders('sass').concat({
  loader: 'sass-resources-loader',
  options:{
  resources: path.resolve(__dirname,'../src/common/mixin/scale-1px.scss')
  }
}),
```

---
