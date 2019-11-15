---
title: 兼容IE的三角导航切换
date: 2019-10-28 17:08:59
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "仿京东的三角热区域导航栏"
toc: false
---

![triangular-navigation-bar.gif](https://i.loli.net/2019/11/15/acOwAdSWiU17mML.gif)

---
``` css
* {
    padding: 0;
    margin: 0;
}
ul {
    list-style: none;
}
.box {
    position: relative;
    top: 100px;
    left: 200px;
    width: 200px;
    height: 500px;
}
.navBox {
    position: relative;
    width: 200px;
    height: 500px;
    margin-top: 0;
    cursor: pointer;
    background-color: skyblue;
    text-align: center;
}
.navBox .navboxs {
    position: relative;
    line-height: 50px;
    color: #333333;
}
.navBox .navboxs.on {
    background: #f40;
    color: #fff;
}
.textBox {
    display: none;
    position: absolute;
    top: 0;
    left: 200px;
    width: 600px;
    height: 500px;
    text-align: center;
    overflow: hidden;
}
.textBox.show-block,.textBox .textBoxs.show-block {
    display: block;
}
.textBox .textBoxs {
    display: none;
    width: 100%;
    height: 100%;
    background-color: blue;
    color: #ffffff;
    font-size: 100px;
    line-height: 500px;
}
```
``` html
<div class="box">
    <div class="navBox" id="navBox">
        <div class="navboxs">衣服</div>
        <div class="navboxs">食物</div>
        <div class="navboxs">住宿</div>
        <div class="navboxs">旅行</div>
        <div class="navboxs">不知道</div>
    </div>
    <div class="textBox" id="textBox">
        <div class="textBoxs">衣服</div>
        <div class="textBoxs">食物</div>
        <div class="textBoxs">住宿</div>
        <div class="textBoxs">旅行</div>
        <div class="textBoxs">不知道</div>
    </div>
</div>
```
``` javascript
if(!Array.from){
    Array.from = function (el) {
        return Array.apply(this, el);
    }
}
var navBox = document.getElementById('navBox'),
    navBoxLIs = Array.from(navBox.getElementsByClassName('navboxs')),
    textBox = document.getElementById('textBox'),
    textBoxLIs = Array.from(textBox.getElementsByClassName('textBoxs')),
    box = document.getElementsByClassName('box')[0];
console.log(navBoxLIs);
// 存储鼠标移动时的坐标
var  xyArr = [];
// box 右上角和右下角坐标
var  A = {x: navBox.offsetWidth, y: 0}, B = {x: navBox.offsetWidth, y: navBox.offsetHeight};
navBoxLIs.forEach(function (item,index) {
    return item.index = index
})
navBox.addEventListener('mouseover', moveGoing);
navBox.addEventListener('mousemove', getXY);
navBox.addEventListener('mouseout', clearTimer);
function moveGoing(e) {
    if (e.target.nodeName.toUpperCase() === 'DIV') {
        var currentnavBox = e.target, flag;
        textBox.className = 'textBox show-block';
        currentnavBox.timer = null;
        try {
            flag = inORout(xyArr[0], xyArr[2], A, B);
        } catch (err) {

        }
        if (flag) {
            currentnavBox.timer = setTimeout(function () {
                toggle(textBoxLIs, currentnavBox.index);
            }, 300)
        } else {
            toggle(textBoxLIs, currentnavBox.index)
        }
    }
}
// 获取XY坐标的函数
function getXY(e) {
    if (e.target.nodeName.toUpperCase() === 'DIV') {
        // 坐标原点在 box 右上角
        var x = e.clientX - box.offsetLeft, y = e.clientY - box.offsetTop;
        xyArr.push({x:x, y:y});
        if (xyArr.length > 3) {
            xyArr.shift();
        }
    }
}
// 清除定时器判断函数
function clearTimer(e) {
    if (e.target.nodeName.toUpperCase() === 'DIV') {

        if (e.target.timer) {
            clearTimeout(e.target.timer);
        }
    }
}
// 显示与隐藏函数
function toggle(eleArr, id) {
    eleArr.forEach(function (item,index) {
        navBoxLIs[index].className = 'navboxs';
        item.className = 'textBoxs';
    })
    navBoxLIs[id].className = 'navboxs on';
    eleArr[id].className = 'textBoxs show-block';
}
/* 判断是否在三角形内函数
moveStar xyArr中的开始坐标
moveEnd xyArr中的结束坐标
star 已知右上点坐标
end 已知右下点坐标*/
function inORout(moveStar, moveEnd, star, end) {
    var x = moveEnd.x,
        y = moveEnd.y,
        x1 = moveStar.x,
        y1 = moveStar.y,
        x2 = star.x,
        y2 = star.y,
        x3 = end.x,
        y3 = end.y,
        r1 = y - y1 - (y2 - y1) / (x2 - x1) * (x - x1),
        r2 = y - y2 - (y3 - y2) / (x3 - x2) * (x - x2),
        r3 = y - y3 - (y1 - y3) / (x1 - x3) * (x - x3);
    return (r1 * r2 * r3 < 0) && (r1 > 0);
}
```



