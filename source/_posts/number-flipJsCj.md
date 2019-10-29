---
title: 数字滚动效果(number-flip)
date: 2019-10-29 10:39:35
tags:
  - "动画"
  - "插件"
categories:
  - "插件"
keywords:
description: "数字滚动效果(number-flip)"
toc: false
---

**先下载插件`npm install --save number-flip`**

```html
<script src="./number-flip.min.js"></script>
<div id="demo"></div>
<script>
  var demo = new Flip({
    node: document.getElementById("demo"),
    from: 0, //开始的数
    to: 186, //结束的数
    duration: 0.5, //过度时间
    delay: 1 //等待时间
  });
</script>
```
