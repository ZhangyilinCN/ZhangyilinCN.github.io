---
title: 'node-sass-err'
date: 2020-04-15 13:57:42
tags:
  - 'scss/sass'
  - 'Css'
categories:
  - 'scss/sass'
keywords:
description: 'vue-cli下node-sass安装不成功'
toc: false
---

## 设置一下`node-sass`的数据源

```
npm config set sass_binary_site=https://npm.taobao.org/mirrors/node-sass
```

## 然后重新 `npm i node-sass sass-loader`即可
