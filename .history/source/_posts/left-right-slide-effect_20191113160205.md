---
title: 手机左右滑动效果
date: 2019-10-28 16:51:04
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "模仿电商左右滑出现删除按钮效果"
toc: false
---

![](https://wx3.sinaimg.cn/mw690/ed984376ly1g8wgihhu1ej208006f3ya.jpg)

---

## 手机端，记得开始先定义 ：

```html
<meta name="viewport" content="width=device-width,initial-scale=1.0 minimum-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
```

```css
* {
  margin: 0;
  padding: 0;
}
li {
  list-style: none;
}
.box {
  width: 80%;
  overflow: hidden;
  margin: 0 auto;
  border: 1px solid #000;
}
.box > ul {
  width: 100%;
  overflow: hidden;
}
.box > ul > li {
  width: 120%;
  font: 16px/30px "Microsoft yahei";
  background: skyblue;
  margin-bottom: 10px;
  left: 0;
}
.box > ul > li > span {
  float: right;
}
```

```html
<div class="box">
  <ul>
    <li>我是宝贝001<span>删除</span></li>
    <li>我是宝贝002<span>删除</span></li>
    <li>我是宝贝003<span>删除</span></li>
    <li>我是宝贝004<span>删除</span></li>
    <li>我是宝贝005<span>删除</span></li>
  </ul>
</div>
```

```javascript
// 记得要先引入Jquery.js
$(".box>ul>li").on("touchstart", function(event) {
  var startX = 0; //点击点
  var moveX = 0; //移动点
  var endX = 0; //结束点
  var bi = 0; //百分比
  var e = event || window.event;
  e.preventDefault();
  // 获取点击点X坐标
  startX = e.originalEvent.changedTouches[0].pageX;
  //获取marginleft的数值
  var mgl = parseInt($(this).css("marginLeft"));
  // 如果现在是右面隐藏的话
  if (mgl == 0) {
    // 添加移动事件
    $(this).on("touchmove", function(event) {
      var e = event || window.event;
      e.preventDefault();
      // 实时获取移动点的X值
      moveX = e.originalEvent.changedTouches[0].pageX;
      // 继续左滑
      if (startX < moveX) {
        //让他之中为0
        $(this).css("marginLeft", "0%");
      }
      //右滑判断
      else if (startX > moveX) {
        // 进行百分比转化，赋予给变量bi
        bi = ((startX - moveX) / $(".box>ul").width()) * 100;
        // 因为li的wid为120%，所以bi最大为20
        if (bi > 20) {
          bi = 20;
        }
        // 给予css样式
        $(this).css("marginLeft", -bi + "%");
      }
    });
  }
  // 如果是右侧显示的话
  else if (mgl < 0) {
    // 同理，添加移动事件
    $(this).on("touchmove", function(event) {
      var e = event || window.event;
      e.preventDefault();
      // 获取移动变量
      moveX = e.originalEvent.changedTouches[0].pageX;
      // 继续向左滑
      if (startX > moveX) {
        $(this).css("marginLeft", "-20%");
      }
      // 向右滑动
      else if (startX < moveX) {
        // 转换百分比，赋予变量
        bi = ((moveX - startX) / $(".box>ul").width()) * 100;
        if (bi > 20) {
          bi = 20;
        }
        // 更改css样式
        $(this).css("marginLeft", -20 + bi + "%");
      }
    });
  }
  /* 至此我们已经做好了，滑动效果了
    但是为了,更好的体验,我们添加end抬起事件*/
  $(this).on("touchend", function(event) {
    // 获取百分比
    var aa = bi;
    var e = event || window.event;
    e.preventDefault();
    // 获取结束时点的X值
    endX = e.originalEvent.changedTouches[0].pageX;
    // 判断mgl的值(即为判断盒子现在的状态)
    // 右侧隐藏时
    if (mgl == 0) {
      // 向左滑动,并且滑动的浮动大于10%的话,就让他全部显示
      if (startX > endX && aa > 10) {
        aa = 20;
      }
      // 否侧让他不显示
      else {
        aa = 0;
      }
      // 给予css样式
      $(this).css("marginLeft", -aa + "%");
    }
    // 右侧显示的时候
    else if (mgl < 0) {
      // 向右滑动,并且滑动的浮动大于10%的话,就让他全部显示
      if (startX < endX && aa > 10) {
        aa = 20;
      }
      // 否侧让他不显示
      else {
        aa = 0;
      }
      // 给予css样式
      $(this).css("marginLeft", -20 + aa + "%");
    }
  });
});
```
