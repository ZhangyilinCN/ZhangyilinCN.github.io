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

```js
function roundRect(ctx,x, y, w, h, r) {
    if (w< 2 * r) r = w / 2;
    if (h < 2 * r) r = h / 2;
    ctx.beginPath();
    ctx.moveTo(x + r, y);
    ctx.arcTo(x + w, y, x + w, y + h, r);
    ctx.arcTo(x + w, y + h, x, y + h, r);
    ctx.arcTo(x, y + h, x, y, r);
    ctx.arcTo(x, y, x + w, y, r);
    ctx.closePath();
    ctx.setFillStyle('#fff');
    ctx.fill()
},
```
