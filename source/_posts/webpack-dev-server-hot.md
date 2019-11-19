---
title: webpack修改代码后自动打包(webpack-dev-server)
date: 2019-11-14 10:00:59
tags:
  - "Webpack"
categories:
  - "Webpack"
keywords:
description: "webpack修改代码后自动打包(webpack-dev-server)"
toc: false
---

**需要安装 webpack-dev-server**

``` js
npm i webpack-dev-server -d //安装到本地依赖(只需要装到本地项目中，不需要-g)
```

**因为webpack-dev-server是依赖于本地的webpack和webpack-cli的，所以，如果本地中没有安装。则需要先安装，才能使用**

``` js
npm i webpack -d
npm i webpack-cli -d
```

**如果不知道自己是否安装过可以查看package.json文件**

![webpack-dev-server-hot1.jpg](https://i.loli.net/2019/11/15/LflQKsqHu1pCzi9.jpg)

**配置好之后，再修改代码，保存之后，会自动执行打包，不用再手动输入命令行来实现了**

![webpack-dev-server-hot2.jpg](https://i.loli.net/2019/11/15/l2RtIAPpHQorek3.jpg)

---
