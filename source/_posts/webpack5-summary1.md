---
title: webpack5小结-1
date: 2020-10-22 15:29:39
tags:
  - 'node'
  - 'webpack'
categories:
  - 'webpack'
keywords:
description: 'webpack5-初识'
---

## webpack 初识

![webpack001.jpg](https://i.loli.net/2020/10/22/ADMQ9ceRKSxgX3Z.jpg)

---

## webpack 的五个核心概念

- `Entry`-**入口(Entry)指示 webpack 以哪个文件为入口起点开始打包，分析构建内部依赖图**
- `OutPut`-**输出(OutPut)指示 webpack 打包后的资源 bundles 输出到哪里去，以及如何命名**
- `Loader`-**翻译/转换(loader) 让 webpack 能够去处理那些非 JavaScript 文件(webpack 自身只理解 JavaScript)**
- `Plugins`- **插件(Plugins)可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量等**
- `Mode` - **模式(Mode)指示 webpack 使用相应模式的配置**
  ![webpack002.png](https://i.loli.net/2020/10/22/OpH8GqlUWDAjnZh.png)

---

## webpack 自身所带的功能/指令

- webpack 能处理 js/json 资源,不能处理 css/img 等其他资源
- 生产环境和开发环境将 ES6 模块化编译成浏览器能识别的模块化
- 生产环境比开发环境多一个压缩 js 代码

```js
/* 运行指令:
开发环境：webpack ./src/index.js -o ./build --mode=development
生产环境：webpack ./src/index.js -o ./build --mode=production

./src/index.js 入口文件
-o Output 
./build 在build文件夹下生成main.js,如果有则覆盖此文件 
--mode=development 指定模式 生产模式下代码更为简洁,体积也更小
*/
```

**要想使用 webpack 命令先使用`npm i webpack webpack-cli -g`进行全局安装,如果 package.json 中没有的话，还要使用`npm i webpack webpack-cli -D`安装项目依赖**

![webpack003.png](https://i.loli.net/2020/10/22/pRhgE78qLQWZFBx.png)

---