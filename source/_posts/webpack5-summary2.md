---
title: webpack5小结-2
date: 2020-10-22 17:22:53
tags:
  - 'node'
  - 'webpack'
categories:
  - 'webpack'
keywords:
description: 'webpack5/loader配置'
---

## webpack.config.js 用处

### 在根目录创建 webpack.config.js 进行 webpack 的配置

**作用：指示 webpack 干哪些活(当你运行 webpack 指令时,会加载里面的配置)**
**所有构件工具都是基于 node.js 平台运行的,模块化默认采用 common.js**

```js
//resolve用来拼接绝对路径的方法
const { resolve } = require('path')

module.exports = {
  //webpack配置
  entry: './src/index.js', //入口起点
  output: {
    filename: 'main.js', //输出的文件名
    path: resolve(__dirname, 'build'), //输出的路径
    // __dirname node.js的变量,代表当前文件的目录绝对路径
  },
  //   loader配置
  module: {
    // 规则
    rules: [
      //详细的loader配置
      {
        test: /\.css$/, //正则表示比配哪些文件
        use: [
          //use数组中的loader执行顺序是：从右到左,从下到上一次执行
          'style-loader', //创建style标签,将js中的样式资源插入进去,添加到header中生效
          'css-loader', //将css文件变成common.js模块加载到js中,里面内容是样式字符串
        ],
      },
    ],
  },
  //   plugins配置
  plugins: [],
  //   指定打包模式
  mode: 'development', //开发模式(development)和生产模式(produciton)
}
```

## 打包样式资源

`npm i style-loader css-loader -D`
**之后在 webpack.config.js 中的 module-rules 下进行配置即可**
