---
title: webpack的js转化工具babel配置
date: 2019-11-13 17:06:54
tags:
  - "Webpack"
categories:
  - "Webpack"
keywords:
description: "webpack的js转化工具babel配置"
toc: false
---

## 在js中写一些高级的es6的语法，进行打包处理会报错，因为会不识别，所以需要安装转化工具-babel 

``` js
//安装babel的转化工具,这里的babel-loader要安装版本7，高版本8，则需要更改其他的安装项
npm i babel-core babel-loader@7 babel-plugin-transform-runtime -d
//安装语法字典
npm i babel-preset-env babel-preset-stage-0 -d
```

## 然后在webpack.config.js中进行配置

![](https://wx3.sinaimg.cn/large/ed984376ly1g8wiva451tj20zp0asglx.jpg)

``` js
 {test: /\.js$/, use: 'babel-loader', exclude: /node_modules/}
```

## 最后在项目的根目录下新建一个 .babel 的文件来进行babel的配置

![](https://wx4.sinaimg.cn/large/ed984376ly1g8wiveyjdwj20sy0ab0st.jpg)

``` js
{
  "presets":["env","stage-0"],
  "plugins":["transform-runtime"]
}
```
