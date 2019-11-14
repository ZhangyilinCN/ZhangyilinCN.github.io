---
title: html-webpack-plugin插件的使用和配置
date: 2019-11-14 09:46:31
tags:
  - "Webpack"
categories:
  - "Webpack"
keywords:
description: "html-webpack-plugin插件的使用和配置"
toc: false
---

## 特点

**自动在内存中根据所配置的指定页面生成一个内存的页面；**
**自动把打包好的js文件追加到页面当中。**

## 下载

``` js
npm i html-webpack-plugin -d  //在项目中来进行安装
```
## 配置

**然后在webpack.config.js中进行配置**

![](https://wx2.sinaimg.cn/large/ed984376ly1g8xbxp75g3j212r0eygm4.jpg)

``` js
new htmlWebpackPlugin({
      template: path.join(__dirname,'./src/index.html'), 
      filename: "index.html" 
})
```
### 使用

**然后在index中注释了js的引用，并且运行页面，我们会发现，在页面末尾自动给我们追加上了script的引用**

![](https://wx1.sinaimg.cn/large/ed984376ly1g8xbxu8fhej20h407mt8o.jpg)

---

