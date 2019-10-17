---
title: 倒计时
date: 2019-10-17 11:00:25
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "页面倒计时"
toc: false
---

![](http://pzcertt0r.bkt.clouddn.com/countdown.gif)

---

```css
.box {
  width: 500px;
  padding: 80px 0;
  border-radius: 12px;
  background: cadetblue;
  margin: 200px auto;
  text-align: center;
}
p {
  font-size: 30px;
  line-height: 0;
}
span {
  font-size: 34px;
}
```

```html
<div class="box">
  <p>距离倒计时还有：</p>
  <span></span>
</div>
```

```javascript
window.onload = function() {
  var sp = document.getElementsByTagName("span")[0];
  function fn() {
    var future = new Date(2018, 8, 8).getTime();
    var now = new Date().getTime();
    var gap = future - now;
    var gapDay = Math.floor(gap / 1000 / 60 / 60 / 24);
    var gapHour = Math.floor(gap / 1000 / 60 / 60);
    if (gapHour < 10) {
      gapHour = "0" + gapHour;
    }
    var gapMin = Math.floor((gap / 1000 / 60) % 60);
    if (gapMin < 10) {
      gapMin = "0" + gapMin;
    }
    var gapS = Math.floor((gap / 1000) % 60);
    if (gapS < 10) {
      gapS = "0" + gapS;
    }
    var gapHS = Math.floor(gap % 1000);
    if (gapHS < 100 && gapHS > 10) {
      gapHS = "0" + gapHS;
    } else if (gapHS < 10) {
      gapHS = "00" + gapHS;
    }
    sp.innerHTML =
      gapDay +
      "天" +
      gapHour +
      "时" +
      gapMin +
      "分" +
      gapS +
      "秒" +
      gapHS +
      "毫秒";
  }
  fn();
  setInterval(function() {
    fn();
  }, 50);
};
```
