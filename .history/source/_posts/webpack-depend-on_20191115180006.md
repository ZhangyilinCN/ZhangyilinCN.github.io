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

![webpack-depend-on1.jpg](https://i.loli.net/2019/11/15/Y1tQWTX4RaA8eLG.jpg)

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

### 修改配置

**然后修改webpack.config.js的配置文件**


![webpack-depend-on2.jpg](https://i.loli.net/2019/11/15/2NMcW1Ymtvur4Gy.jpg)

``` js
{test: /\.scss$/, use: ['style-loader','css-loader','sass-loader']},
{test: /\.less$/, use: ['style-loader','css-loader','less-loader']},
```

---

## img的依赖

**一般情况下，webpack无法处理css中的url地址（背景图片、字体等），所以需要使用插件来进行处理**

### 下载

``` js
npm i url-loader -d
npm i file-loader -d  //基于url-loader的依赖
```

### 修改配置

**然后在webpack.config.js进行配置修改**

![webpack-depend-on3.jpg](https://i.loli.net/2019/11/15/nbslHFyrfUEd1o9.jpg)

``` js
 {test: /\.(jpg|png|gif|bmp|jpeg)$/, use: 'url-loader?limit=1000&name=[hash:8]-[name].[ext]'},
```

### 说明

**其中 ？ 之后的是传参配置**
**limit=xxx 设置图片base64转化的阈值，如果图片大于1000kb不适用base64显示，小于则使用base显示**

![webpack-depend-on4.jpg](https://i.loli.net/2019/11/15/FZwqELWk6QbNDvh.jpg)


![](https://wx3.sinaimg.cn/large/ed984376ly1g8xbeakdicj20j002eglh.jpg)


**name=[hash:8]-[name].[ext]**
**[hash:8]地址路径的前8位用hash的前8位表示**

**[name].[ext]表示使用图片的原名字（注意如果多个div的图片路径为不同路径，但是使相同名字的话，要加[hash]前缀，否则图片只会显示相同名字的最后一张）**

![](https://wx1.sinaimg.cn/large/ed984376ly1g8xbef1og5j20ix06gwee.jpg)

---

## 字体的依赖

### 下载
``` js
//如果在node_modules中找包的话，可以直接这样写
import 'bootstrap/dist/css/bootstrap.css'
```

### 修改配置
**然后在webpack.config.js中进行配置**

![](https://wx2.sinaimg.cn/large/ed984376ly1g8xblckiwtj212o0db74m.jpg)

``` js
{test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader'}
```

---

