---
title: 使用canvas绘制带阴影的矩形
date: 2019-12-24 09:22:35
tags:
  - 'Canvas'
categories:
  - '小练习'
keywords:
description: '使用canvas绘制带阴影的矩形'
toc: false
---

![canvasBoxShadow.png](https://i.loli.net/2019/12/24/zun4s8x71PA5MYN.png)

```js
ctx.shadowOffsetX = 0 // 设置水平位移
ctx.shadowOffsetY = 2 // 设置垂直位移
ctx.shadowBlur = 13 // 设置模糊度
ctx.shadowColor = 'rgb(227,2,10,0.2)' // 设置阴影颜色
ctx.fillStyle = '#fff' //设置背景色
ctx.fillRect(Xnum, Ynum, Width, Height)
```
