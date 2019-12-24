---
title: canvas跨域操作图片
date: 2019-12-24 09:35:11
tags:
  - 'Canvas'
categories:
  - '小练习'
keywords:
description: 'canvas跨域操作图片'
toc: false
---

## canvas 无法对跨域的图片进行操作，想要使用裁剪保存功能。就必须要开启允许跨域，其中，除了服务端要允许当前页面允许跨域之外，在 canvas 操作前也要开启跨域。

```js
let img = new Image()
img.setAttribute('crossOrigin', 'anonymous')
img.onload = function() {
  xxxxxxx
}
img.src = 'xxxxxx' //src 属性一定要写到 onload 的后面，否则程序在 IE 中会出错
ctx.drawImage(img, x, y, width, height)
```

## 这样在进行`ctx.toDataURL`等操作就不会出现报错了
