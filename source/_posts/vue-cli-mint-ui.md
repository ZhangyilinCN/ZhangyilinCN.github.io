---
title: mint-ui使用
date: 2019-11-14 10:50:18
tags:
  - 'Vue-cli'
  - '插件'
categories:
  - '插件'
keywords:
description: 'mint-ui使用'
toc: false
---


## 下载

``` js
npm i mint-ui -s
```

## 使用

### 全局导入使用--main.js中

``` js
import MintUI from 'mint-ui'
import 'mint-ui/lib/style.css'
Vue.use(MintUI)
```

**然后就可以直接使用css的封装组件了，如果要使用js的组件的话，需要按需加载需要的组件，官方文档都有**

![vue-cli-mint-ui1.jpg](https://i.loli.net/2019/11/15/j5Z2CQxLrNtlYTI.jpg)

### 按需加载导入使用

```
npm install babel-plugin-component -d
```

**下载之后再配置.babelrc文件**


![vue-cli-mint-ui2.jpg](https://i.loli.net/2019/11/15/bBRWE7jk3SCJs1p.jpg)

**之后需要哪个就引那个就行**

![vue-cli-mint-ui3.jpg](https://i.loli.net/2019/11/15/n7gAh2iJbumdVWC.jpg)

---