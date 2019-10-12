---
title: "client、offset、scroll三大系列"
date: 2019-10-11 15:37:37
tags:
  - "Dom"
  - "Javascript"
categories:
  - "Javascript"
keywords:
description: "简单的了解下原生js的client、offset、scroll三大系列"
toc: false
---

## client：

```javascript
var box = document.querySelector(".box");
console.log(box.clientWidth);
//获取元素的可见宽度(width+padding，不包括margin和border)只有数值，没有单位
console.log(box.clientHeight);
//获取元素的可见高度(width+padding，不包括margin和border)只有数值，没有单位
console.log(window.getComputedStyle(box).width);
// 而getcomputerStyle获取的是带有单位的单纯的width值
```

---

## offset：

```javascript
var box = document.querySelector(".box");
console.log(box.offsetWidth);
//获取元素的可见宽度(width+padding+border，不包括margin)只有数值，没有单位
console.log(box.offsetHeight);
//获取元素的可见高度(width+padding+border，不包括margin)只有数值，没有单位
console.log(box.offsetLeft);
console.log(box.offsetTop);
//返回距离上级盒子（带有定位）左边的位置
//如果父级都没有定位则以body 为准
//从父亲的padding 开始算,父亲的border 不算
//获取元素距离父元素的偏移量，如果在最外层，则以窗口为标准
console.log(window.getComputedStyle(box).width);
// 而getcomputerStyle获取的是带有单位的单纯的width值
```

---

## scroll：

```javascript
var box = document.querySelector(".box");
console.log(box.scrollWidth);
//获取元素的可见宽度(width+padding，不包括margin和border,如果内容超出的话算其超出内容宽度)只有数值，没有单位
console.log(box.scrollHeight);
//获取元素的可见高度(width+padding，不包括margin和border,如果内容超出的话算其超出内容高度)只有数值，没有单位
console.log(window.getComputedStyle(box).width);
// 而getcomputerStyle获取的是带有单位的单纯的width值
```
