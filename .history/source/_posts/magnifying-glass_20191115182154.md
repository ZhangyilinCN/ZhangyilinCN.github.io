---
title: 图片的放大效果预览
date: 2019-10-28 16:17:01
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "模仿电商的宝贝滑过放大效果"
toc: false
---

![magnifying-glass1.jpg](https://i.loli.net/2019/11/15/KbQ2jMgWO1hwvUI.jpg)

---

```css
.main {
  position: relative;
  width: 90px;
  height: auto;
}
.box1 {
  width: 90px;
  height: 90px;
}
.box2 {
  width: 200px;
  height: 200px;
  overflow: hidden;
  margin-top: 10px;
  border: 1px solid #000;
}
.a {
  width: 30px;
  height: 30px;
  background: gold;
  display: none;
  position: absolute;
}
```

```html
<div class="main">
  <div class="box1"><img src="1.png" alt="" /></div>
  <div class="box2"><img src="2.png" alt="" /></div>
  <div class="a"></div>
</div>
```

```javascript
// 获取相关元素
var box1 = document.getElementsByClassName("box1")[0];
var box2 = document.getElementsByClassName("box2")[0];
var box2Img = box2.getElementsByTagName("img")[0];
var a = document.getElementsByClassName("a")[0];
// 添加划上事件
box1.onmousemove = function(event) {
  // 获取鼠标位置
  var box1X = event.clientX;
  var box1Y = event.clientY;
  // 修改小方块状态
  a.style.display = "block";
  // 获取最大与最小的X/Y的数值
  var maxX = box1.offsetWidth - a.offsetWidth / 2;
  var minX = a.offsetWidth / 2;
  var maxY = box1.offsetHeight - a.offsetHeight / 2;
  var minY = a.offsetHeight / 2;
  // 为了不让小方块出去，进行判断
  if (box1X >= maxX) {
    box1X = maxX;
    if (box1Y >= maxY) {
      box1Y = maxY;
    }
  }
  if (box1X <= minX) {
    box1X = minX;
    if (box1Y <= minY) {
      box1Y = minY;
    }
  }
  if (box1Y >= maxY) {
    box1Y = maxY;
    if (box1X >= maxX) {
      box1X = maxX;
    }
  }
  if (box1Y <= minY) {
    box1Y = minY;
    if (box1X <= minX) {
      box1X = minX;
    }
  }
  // 获取大图与小图的比例
  var box2X = -((box2Img.offsetWidth / box1.offsetWidth) * box1X);
  var box2Y = -((box2Img.offsetHeight / box1.offsetHeight) * box1Y);
  // 让小方块的中心与鼠标相同
  a.style.top = box1Y - a.offsetHeight / 2 + "px";
  a.style.left = box1X - a.offsetWidth / 2 + "px";
  // 让大图移动
  box2Img.style.marginTop = box2Y + a.offsetHeight + "px";
  box2Img.style.marginLeft = box2X + a.offsetWidth + "px";
};
// 添加划下事件
box1.onmouseout = function() {
  a.style.display = "none";
};
```
