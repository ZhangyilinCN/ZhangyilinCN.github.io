---
title: 使用canvas绘制圆角矩形和圆角图片
date: 2019-12-04 20:50:31
tags:
  - 'Canvas'
categories:
  - '小练习'
keywords:
description: '使用canvas绘制圆角矩形和圆角图片'
toc: false
---

```js
const ctx = uni.createCanvasContext('myCanvas')
this.roundRect(
  ctx,
  parseInt(this.divWidth * 0.21),
  parseInt(this.divHeight * 0.4),
  parseInt(this.divWidth * 0.581),
  parseInt(this.divHeight * 0.276),
  6
)
ctx.save()
this.roundRect(
  ctx,
  parseInt(this.divWidth * 0.217),
  parseInt(this.divHeight * 0.404),
  parseInt(this.divWidth * 0.568),
  parseInt(this.divHeight * 0.266),
  6
)
ctx.clip()
ctx.drawImage(
  locationImgSrc,
  parseInt(this.divWidth * 0.217),
  parseInt(this.divHeight * 0.404),
  parseInt(this.divWidth * 0.568),
  parseInt(this.divHeight * 0.266)
)
ctx.restore()
```
