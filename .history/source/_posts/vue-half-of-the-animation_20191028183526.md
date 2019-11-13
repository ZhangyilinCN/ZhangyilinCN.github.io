---
title: Vue钩子函数—半场动画（球入框）Demo
date: 2019-10-28 17:38:44
tags:
  - "Demo"
  - "Vue"
categories:
  - "小练习"
keywords:
description: "Vue钩子函数—半场动画（球入框）Demo"
toc: false
---

![](http://pzcertt0r.bkt.clouddn.com/vue-half-of-the-animation.gif)

---

```css
* {
  padding: 0;
  margin: 0;
}
#app {
  position: relative;
  width: 1000px;
  height: 600px;
  border: 1px solid #000;
  margin: 50px auto;
  overflow: hidden;
}
button {
  display: block;
  width: 200px;
  height: 80px;
  background: red;
  font-size: 24px;
  line-height: 80px;
  color: gold;
  text-align: center;
  border: 0;
  outline: 0;
  border-radius: 16px;
  margin: 0 auto;
}
span {
  display: block;
  width: 30px;
  height: 30px;
  background: green;
  border-radius: 50%;
}
p {
  position: absolute;
  bottom: -5px;
  width: 200px;
  height: 10px;
  margin-left: -100px;
  left: 50%;
  background: #000;
}
```

```html
<div id="app">
  <button @click="flag=true">抛！！！</button>
  <!--只设置进场动画，来达到半场动画-->
  <transition @before-enter="befEnt" @enter="enter" @after-enter="aftEnt">
    <span v-show="flag"></span>
  </transition>
  <p></p>
</div>
```

```javascript
// 如果不是使用的Vue-cli,记得引入Vue.js
var vm = new Vue({
  el: "#app",
  data: {
    flag: false, //显示与隐藏
    tan: false, //是否进框
    X: "", //储存随机X轴的值
    Xend: ""
  },
  methods: {
    befEnt: function(el) {
      el.style.transform = "translate(0,0)";
      // 初始化位置
    },
    enter: function(el, done) {
      el.offsetWidth; //强制刷新页面
      this.X = Math.floor(Math.random() * 1000) + "px"; //随机值
      var num = parseInt(this.X); //判断是否进框
      el.style.transform = "translate(" + this.X + ",490px)"; //移动后的值
      el.style.transition = "all 1s"; //移动时间
      if (num >= 400 && num <= 570) {
        //进框事件
        this.tan = false;
        done(); //回调
      } else {
        //没进框事件
        this.tan = true;
        setTimeout(function() {
          this.Xend = Math.floor(Math.random() * 1000) + "px";
          el.style.transform = "translate(" + this.Xend + ",0)";
          el.style.transition = "all 1s";
          done();
        }, 1000);
      }
    },
    aftEnt: function(el) {
      if (this.tan) {
        this.flag = false;
        this.tan = false;
        this.X = "";
        this.Xend = "";
        setTimeout(function() {
          alert("失败");
        }, 1300);
      } else {
        this.flag = false;
        this.X = "";
        this.Xend = "";
        setTimeout(function() {
          alert("成功");
        }, 300);
      }
    }
  }
});
```
