---
title: 事件委托
date: 2019-10-12 14:11:56
tags:
  - "Javascript"
categories:
  - "Javascript"
keywords:
description: "js原生的事件委托"
toc: false
---

**为 ul 下的所有 li 循环依次绑定事件，会增大页面的 Dom 数，会影响速度与性能**

```javascript
var aLi = document.getElementsByTagName("li");
var aUl = document.getElementsByTagName("ul")[0];
//for循环为每个li绑定点击事件,
for (var i = 0; i < aLi.length; i++) {
  aLi[i].οnclick = function() {
    alert(123);
  };
}
```

**所以此时就可以使用事件委托来优化我们的代码**

```javascript
aUl.οnclick = function(event) {
  //委托其父元素执行
  var e = event || window.event; //兼容
  if (event.target.tagName.toLocaleLowerCase() == "li") {
    //判断如果点击的位置的元素名字和li一样的话，执行绑定内容
    alert(123);
  }
};
```
