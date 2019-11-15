---
title: html-webpack-plugin插件的使用和配置
date: 2019-11-14 09:46:31
tags:
  - 'Webpack'
categories:
  - 'Webpack'
keywords:
description: 'html-webpack-plugin插件的使用和配置'
toc: false
---

## 特点

**自动在内存中根据所配置的指定页面生成一个内存的页面；**
**自动把打包好的 js 文件追加到页面当中。**

## 下载

```js
npm i html-webpack-plugin -d  //在项目中来进行安装
```

## 配置

**然后在 webpack.config.js 中进行配置**

![html-webpack-plugin1.jpg](https://i.loli.net/2019/11/15/4KsE8zVbwn7qrtx.jpg)

```js
new htmlWebpackPlugin({
  template: path.join(__dirname, './src/index.html'),
  filename: 'index.html'
})
```

### 使用

**然后在 index 中注释了 js 的引用，并且运行页面，我们会发现，在页面末尾自动给我们追加上了 script 的引用**

![html-webpack-plugin2.jpg](https://i.loli.net/2019/11/15/RmGvCHXe7VsTK3b.jpg)

---
