---
title: webpack初识
date: 2019-11-13 16:51:27
tags:
  - "Webpack"
categories:
  - "Webpack"
keywords:
description: "webpack初识"
toc: false
---

## 使用

```js
npm i webpack -g //进行全局安装（本地的话使用后缀 -d）
```

## 安装之后再项目中使用

```js
npm init -y  //生成package.json文件
```

## 如果要在项目中装插件什么的 可以使用

```js
npm i jquery -s //（-s是项目中要使用的，-d是项目实际运行时不需要的，如gulp）
```

## npm 装包时-S 和-D 的区别

### npm install name -save 简写（npm install name -S） 自动把模块和版本号添加到 dependencies。

**-S 后，安装包会在 package 中的 dependencies 对象中。简称 dep。dep 是在生产环境中要用到的。**

**项目插件：例如 element ui、echarts 这种插件要在运行中使用的，就要放在 dep 中所以就用 -S**

**一般我们项目插件，在 api 中都可以看到，一般都是-S。因为这些插件是在程序运行中使用的。**

---

### npm install name -save-dve 简写（npm install name -D） 自动把模块和版本号添加到 devdependencies。

**-D 后，安装包会在 package 中的 devDependencies 对象中。简称 dev。dev 是在开发环境中要用到的。**

**构建工具：gulp 和 webpack 是用来压缩代码，打包等需要的工具，程序实际运行的时候并不需要，就要放在 dev 中所以要用 -D**

---
