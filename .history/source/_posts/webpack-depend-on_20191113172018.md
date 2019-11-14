---
title: webpack常用的打包依赖配置
date: 2019-11-13 17:12:00
tags:
  - "Webpack"
categories:
  - "Webpack"
keywords:
description: "webpack常用的打包依赖配置"
---

**因为webpack默认只能打包处理js类型的文件**
**如果需要处理非js类的文件，我们需要手动安装一些合适的第三方 loader 加载器**

## css的依赖

### 下载

**下载所需要的依赖**
``` js
npm i style-loader -d //先安装两个依赖
npm i css-loader -d
```
### 修改配置

**修改webpack.config.js的配置文件**

![](https://wx4.sinaimg.cn/large/ed984376ly1g8wj6bosd0j20w90gk74s.jpg)

``` js
{test: /\.css$/, use: ['style-loader','css-loader']},
```

### 使用

**之后就能识别css类型的文件了**

``` js
import $ from 'jquery';  //只能识别js的
import './css/index.css' //安装并且配置好loader之后就可以识别使用了
```

---

## less/scss的依赖

### 下载

**less配置**
``` js
npm i less -d
npm i less-loader -d
```

**sass/scs配置**
``` js
npm i node-sass -d
npm i sass-loader -d
```
