---
title: vue-跟随屏幕位置改变的半场动画
date: 2019-10-17 21:45:26
tags:
  - "Vue"  
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "js点击按钮唤醒app"
toc: false
---
``` scss
.smball {
  display: block;
  position: absolute;
  right: 10px;
  top: 10px;
  z-index: 666;
  transition: all 0.4s cubic-bezier(0.49, -0.29, 0.75, 0.41);
  b {
    display: block;
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background: red;
    transition: all 0.4s linear;
  }
}
```
- **定义小球（如果当前页面有其他的动画效果的定义，不要用默认的v-enter...，要重新定义name，用name-enter，用此方式覆盖污染）**
    ``` html
    <transition @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter">
    <span class="smball" v-show="ballflag" ref="ball">
        <b ref="innerBall"></b>
    </span>
    </transition>
    ```
- **小球上所绑定的函数以及data**
    ``` javascript
    data() {
    return {
        ballflag:false
    };
    },
    methods: {
    beforeEnter(el) {
        el.style.transform = "translate(0,0)";
        this.$refs.innerBall.style.transform = "translate(0,0)";
    },
    enter(el, done) {
        el.offsetWidth;
        //this.$refs.ball---给予小球ref：'ball';
        var ball = this.$refs.ball.getBoundingClientRect();
        //getElementById("bigball")---给予底部要定位的如购物车的小红点此id;
        var bigball = document.getElementById("bigball").getBoundingClientRect();
        var x = bigball.x - ball.x;
        var y = bigball.y - ball.y;
        el.style.transform = `translate3d(0,${y}px,0)`;
        this.$refs.innerBall.style.transform = `translate3d(${x}px,0,0)`;
        done();
    },
    afterEnter() {
        this.ballflag = !this.ballflag;
    }
    }
    ```

- **其中要给点击的dom绑定显示与隐藏**
    ``` html
    <div class="cart-add" @click="ballfalg=!ballfalg"></div>
    ```


