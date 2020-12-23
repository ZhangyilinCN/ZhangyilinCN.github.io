---
title: 环形3D轮播图
date: 2019-10-28 17:54:11
tags:
  - "Jquery"
  - "插件"
  - "Demo"
  - 'Swiper'
categories:
  - "小练习"
keywords:
description: "使用Jquery和Swiper两种方式实现3D轮播图"
---

## Swiper 版

![rotate-3D-rotations1.gif](https://i.loli.net/2019/11/15/fHUdMsBJjvQ95S7.gif)

**记得要先引入 Swiper.css 和 Swiper.js(演示用的 Swiper4)**

```css
* {
  padding: 0;
  margin: 0;
}
.swiper-container {
  width: 800px;
  height: 400px;
  border: 1px solid #000;
  margin: 50px auto 0;
}
.swiper-slide {
  width: 600px;
  height: 400px;
}
.swiper-slide > img {
  width: 100%;
  height: 100%;
}
```

```html
<div class="swiper-container">
  <div class="swiper-wrapper">
    <a href="javascript:;" class="swiper-slide">
      <img src="./1.jpg" />
    </a>
    <a href="javascript:;" class="swiper-slide">
      <img src="./2.jpg" />
    </a>
    <a href="javascript:;" class="swiper-slide">
      <img src="./3.jpg" />
    </a>
  </div>
  <div class="swiper-pagination"></div>
</div>
```

```javascript
var swiper = new Swiper(".swiper-container", {
  loop: true,
  effect: "coverflow",
  centeredSlides: true,
  slidesPerView: "auto",
  autoplay: {
    delay: 3000
  },
  pagination: {
    el: ".swiper-pagination",
    clickable: true
  },
  coverflowEffect: {
    rotate: 10, //滑动时旋转角度
    stretch: 0, //聚合宽度
    depth: 200, //景深
    modifier: 1, //覆盖叠加层数
    slideShadows: false //是否阴影
  }
});
```

---

## 兼容 IE8 的环形轮播(基于 Jquery)

![rotate-3D-rotations2.gif](https://i.loli.net/2019/11/15/Rclr4xNLpTSouYm.gif)

**记得要先引入 Jquery.js**

```css
* {
  padding: 0;
  margin: 0;
}
.hxlbt {
  width: 1200px;
  height: 600px;
  border: 1px solid #000;
  margin: 100px auto;
  position: relative;
}
.hxlbt > .main {
  width: 100%;
  height: 100%;
  overflow: hidden;
  position: relative;
}
.hxlbt > .main > li {
  width: 800px;
  height: 600px;
  overflow: hidden;
  position: absolute;
  left: 200px;
}
.hxlbt > .main > li > img {
  width: 100%;
  height: auto;
}
.hxlbt > a {
  display: none;
  width: 40px;
  height: 80px;
  background: #000;
  position: absolute;
  color: #fff;
  text-decoration: none;
  font-size: 34px;
  line-height: 80px;
  text-align: center;
  top: 50%;
  margin-top: -40px;
  z-index: 10;
}
.hxlbt > a.leftBtn {
  left: 50px;
}
.hxlbt > a.rightBtn {
  right: 50px;
}
.hxlbt > .down {
  width: 200px;
  height: 20px;
  position: absolute;
  left: 50%;
  margin-left: -100px;
  bottom: 10px;
  z-index: 10;
}
.hxlbt > .down > li {
  width: 20px;
  list-style: none;
  height: 20px;
  float: left;
  cursor: pointer;
  margin: 0 10px;
  border-radius: 50%;
  background: #f40;
}
.hxlbt > .down > li.on,
.hxlbt > .down > li:hover {
  background: deepskyblue;
}
```

```html
<div class="hxlbt">
  <ul class="main">
    <li><img src="img/1.jpg" alt="" /></li>
    <li><img src="img/2.jpg" alt="" /></li>
    <li><img src="img/3.jpg" alt="" /></li>
    <li><img src="img/4.jpg" alt="" /></li>
    <li><img src="img/5.jpg" alt="" /></li>
  </ul>
  <a class="leftBtn" href="javascript:;"><</a>
  <a class="rightBtn" href="javascript:;">></a>
  <ul class="down">
    <li></li>
    <li></li>
    <li class="on"></li>
    <li></li>
    <li></li>
  </ul>
</div>
```

```javascript
// 各个图片的位置
var lists = [
  {
    width: "640px",
    height: "480px",
    top: "-150px",
    left: 0,
    z: 2,
    opacity: 0
  },
  {
    width: "640px",
    height: "480px",
    top: "60px",
    left: 0,
    z: 3,
    opacity: 0.6
  },
  {
    width: "800px",
    height: "600px",
    left: "200px",
    top: 0,
    z: 4,
    opacity: 1
  },
  {
    width: "640px",
    height: "480px",
    top: "60px",
    left: "560px",
    z: 3,
    opacity: 0.6
  },
  {
    width: "640px",
    height: "480px",
    top: "-150px",
    left: "560px",
    z: 2,
    opacity: 0
  }
];
var lbt = $(".hxlbt");
var lbtLis = $(".hxlbt>.main>li");
var timer = null;
var flag = true;
var leftBtn = $(".hxlbt>a.leftBtn");
var rightBtn = $(".hxlbt>a.rightBtn");
var downOn = 2;
var btmCir = $(".hxlbt>.down>li");
// 给予各个图片位置
lbtFn();
function lbtFn() {
  $.each(lists, function(index, ele) {
    // 不加ie8以下会报错
    if (typeof ele != "undefined") {
      lbtLis
        .eq(index)
        .css("z-index", ele.z)
        .stop()
        .animate(ele, 500, function() {
          flag = true;
        });
    }
    // 在ie8以下，会多出来一个undefined，所以要删除
    if (typeof ele == "undefined") {
      lists.splice(index, 1);
    }
  });
}
// 让图片轮播
timer = setInterval(function() {
  lists.unshift(lists.pop());
  lbtFn();
  downOn = btnOnFn();
  btmCir
    .eq(downOn)
    .addClass("on")
    .siblings()
    .removeClass("on");
}, 2000);
// 悬停取消轮播
lbt.hover(
  function() {
    clearInterval(timer);
    leftBtn.css("display", "block");
    rightBtn.css("display", "block");
  },
  function() {
    timer = setInterval(function() {
      lists.unshift(lists.pop());
      lbtFn();
      downOn = btnOnFn();
      btmCir
        .eq(downOn)
        .addClass("on")
        .siblings()
        .removeClass("on");
    }, 2000);
    leftBtn.css("display", "none");
    rightBtn.css("display", "none");
  }
);
// 左右按钮点击换图
leftBtn.click(function() {
  if (flag) {
    flag = false;
    lists.push(lists.shift());
    lbtFn();
    downOn = btnOnFn();
    btmCir
      .eq(downOn)
      .addClass("on")
      .siblings()
      .removeClass("on");
  }
});
rightBtn.click(function() {
  if (flag) {
    flag = false;
    lists.unshift(lists.pop());
    lbtFn();
    downOn = btnOnFn();
    btmCir
      .eq(downOn)
      .addClass("on")
      .siblings()
      .removeClass("on");
  }
});
// 下方小圆点判断
function btnOnFn() {
  var idx = 0;
  $.each(lists, function(index, ele) {
    if (typeof ele != "undefined") {
      if (ele.z == 4) {
        idx = index;
        return;
      }
    }
  });
  return idx;
}
// 点击换图
btmCir.click(function() {
  var oldOn = btnOnFn();
  var nowOn = $(this).index();
  var newOn = oldOn - nowOn;
  if (newOn > 0) {
    for (var i = 0; i < newOn; i++) {
      lists.push(lists.shift());
    }
  }
  if (newOn < 0) {
    for (var i = 0; i < -newOn; i++) {
      lists.unshift(lists.pop());
    }
  }
  lbtFn();
  $(this)
    .addClass("on")
    .siblings()
    .removeClass("on");
});
```
