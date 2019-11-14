---
title: 图片缩略图插件(vue-preview)
date: 2019-11-14 10:40:01
tags:
  - 'Vue-cli'
  - '插件'
categories:
  - '插件'
keywords:
description: '图片缩略图插件(vue-preview)'
toc: false
---

``` js
npm i vue-preview -s
```

``` js
import VuePreview from 'vue-preview'
Vue.use(VuePreview)
```

``` html
<div class="imgContent">
     <vue-preview :slides="imgArr" @close="handleClose"></vue-preview>
</div>
<!--其中的imgArr是你的数组对象，其中要包括属性：w/h/msrc/src
handleClose 为关闭函数 -->
```
