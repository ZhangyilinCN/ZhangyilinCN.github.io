---
title: webpack的配置项--(打包)
date: 2019-11-13 16:46:02
tags:
  - "Webpack"
categories:
  - "Webpack"
keywords:
description: "webpack的配置项--(打包)"
toc: false
---

## 修改打包指令和路径：

**在webpack3中 是使用**
``` js
webpack  .\src\main.js  .\dist\bundle.js 
```
---
**在webpack4中分离出了webpack-cli （所以要先下载webpack-cli）来进行以后的操作;**

``` js
npm i webpack-cli -g (全局下载)
webpack .\src\main.js -o .\dist\bundls.js -- mode development //进行打包
```
**但是每次输入这些又显的复杂，所以可以在项目的根目录下新建一个webpack.cinfig.js的文件来进行配置项**

``` js
const path =require('path')
module.exports = {
  mode: "development", // "production" | "development" | "none" 选择生产环境
  entry: "./src/main.js", // string | object | array  // 默认为 './src'
  // 这里应用程序开始执行
  // webpack 开始打包
  output: {
    // webpack 如何输出结果的相关选项
    path: path.resolve(__dirname, "dist"), // string
    // 所有输出文件的目标路径
    // 必须是绝对路径（使用 Node.js 的 path 模块）
    filename: "bundle.js", // string
  }
}
```

**之后就可以使用webpack指令来直接进行打包处理了**




