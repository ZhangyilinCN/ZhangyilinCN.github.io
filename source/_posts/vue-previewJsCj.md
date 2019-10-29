---
title: 图片缩略图插件(vue-preview)
date: 2019-10-29 17:40:51
tags:
  - "Vue"
  - "插件"
categories:
  - "插件"
keywords:
description: "图片缩略图插件(vue-preview)"
toc: false
---
## 首先下载插件
`npm i vue-preview -s`

## 然后在引用
``` javascript
import VuePreview from 'vue-preview'
Vue.use(VuePreview)
```
## 使用
``` html
<div class="imgContent">
     <vue-preview :slides="imgArr" @close="handleClose"></vue-preview>
</div>
```
**其中的imgArr是你的数组对象，其中要包括属性：w/h/msrc/src**
**handleClose 为关闭函数**
