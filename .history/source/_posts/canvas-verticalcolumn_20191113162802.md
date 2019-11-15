---
title: 使用canvas画立体矩形
date: 2019-10-17 21:19:16
tags:
  - "Javascript"
  - "Demo"
  - "Canvas"
categories:
  - "小练习"
keywords:
description: "使用canvas画升阶3D矩形"
toc: false
---

![](https://wx3.sinaimg.cn/large/ed984376ly1g8wgffb0b0j20hw06tdfn.jpg)

---
``` css
canvas{
    display: block;
    border: 1px solid #000;
    margin: 0 auto;
}
```
``` html
<canvas width="620" height="230"></canvas>
```
``` javascript
var myCanvas = document.querySelector('canvas');
var draw = myCanvas.getContext('2d');
var flagNum=prompt('输入值');

// 点亮
drawjx(draw,26,80,157,187,36,90,146,176,'#caf1ff','#bce6f5','#aedaea',4,
1000,flagNum,'#f9fdff','#f8fcfe','#f6fbfd','T1')
drawjx(draw,108,162,137,187,120,173,125,176,'#a6ddff','#94cdf0','#81bbdf',6,
2000,flagNum,'#f5fbff','#f3fafd','#f1f8fb','T2-1')
drawjx(draw,192,246,112,187,202,256,103,176,'#78cbff','#6ab9ea','#54a3d3',8,
3000,flagNum,'#f0f9ff','#eff7fd','#ecf5fa','T2-2')
drawjx(draw,274,328,91,187,285,339,81,176,'#4bbdff','#39abec','#2395d6',10,
4000,flagNum,'#ebf8ff','#e9f6fd','#e7f3fa','T3-1')
drawjx(draw,357,411,72,187,368,422,59,176,'#32a1ff','#1f87df','#197bce',12,
5000,flagNum,'#e8f5ff','#e6f2fb','#e6f1fa','T3-2')
drawjx(draw,440,494,49,187,452,505,37,176,'#167eff','#1471e4','#1063c8',14,
6000,flagNum,'#e5f1ff','#e5effc','#e5eef9','T4-1')
drawjx(draw,523,577,33,187,534,588,23,176,'#0042ff','#0039dd','#0033c4',16,
7000,flagNum,'#e3eaff','#e3e9fb','#e3e9f9','T4-2')

/*
    canvas立体矩形函数
    ele canvas对象
    zmlx 正面左x
    zmrx 正面右x
    zmuy 正面上y
    zmdy 正面下y
    slx 上面左x
    srx 上面右x
    smy 上面右y
    cmy 侧面y
    zmcolor 正面点亮颜色
    upcolor 上面点亮颜色
    cmcolor 侧面点亮颜色
    pice    分的份数
    num     顶部刻度
    flagnum  传入的数值
    zmcoloroff 正面未亮颜色
    upcoloroff 上面未亮颜色
    cmcoloroff 侧面未亮颜色
    downtxt 底部标签
    */
function drawjx(ele,zmlx,zmrx,zmuy,zmdy,slx,srx,smy,cmy,zmcolor,
upcolor,cmcolor,pice,num,flagnum,zmcoloroff,upcoloroff,
cmcoloroff,downtxt) {
    // 正面
    ele.beginPath()
    ele.lineWidth=1;
    ele.strokeStyle='transparent'
    ele.moveTo(zmlx,zmuy);  //正面左上
    ele.lineTo(zmrx,zmuy);  //正面右上
    ele.lineTo(zmrx,zmdy);  //正面右下
    ele.lineTo(zmlx,zmdy);  //正面左下
    ele.lineTo(zmlx,zmuy);  //正面左上
    if(flagnum>0&&num-flagnum<1000){
        ele.fillStyle=zmcolor
    }else{
        ele.fillStyle=zmcoloroff
    }
    ele.fill()
    ele.closePath();

    // 上面
    ele.beginPath()
    ele.strokeStyle='transparent'
    ele.moveTo(zmlx,zmuy);  //正面左上
    ele.lineTo(slx,smy);  //上面左点
    ele.lineTo(srx,smy);  //上面右点
    ele.lineTo(zmrx,zmuy);  //正面右上
    ele.lineTo(zmlx,zmuy);  //正面左上
    if(flagnum>0&&num-flagnum<1000){
        ele.fillStyle=upcolor
    }else{
        ele.fillStyle=upcoloroff
    }
    ele.fill()
    ele.closePath();

    // 侧面
    ele.beginPath()
    ele.strokeStyle='transparent'
    ele.moveTo(zmrx,zmuy);  //正面右上
    ele.lineTo(zmrx,zmdy);  //正面右下
    ele.lineTo(srx,cmy);  //侧面的点
    ele.lineTo(srx,smy);  //上面右点
    ele.lineTo(zmrx,zmuy);  //正面右上
    if(flagnum>0&&num-flagnum<1000){
        ele.fillStyle=cmcolor
    }else{
        ele.fillStyle=cmcoloroff
    }
    ele.fill()
    ele.closePath();

    // // 底部标签
    ele.beginPath();
    ele.font="12px Serif";
    if(flagnum<=num &&flagnum>(num-1000)){
        ele.fillStyle='red'
    }else{
        ele.fillStyle='#333'
    }
    ele.fillText(downtxt,(zmrx-zmlx)/3+zmlx,zmdy+15)
    ele.closePath();

    // 循环刻度
    ele.beginPath();
    ele.strokeStyle='#fff'
    var item=(zmuy-zmdy)/pice;
    for(var i=1;i<pice;i++){
        var sum=item*i
        if(flagnum>0&&num-flagnum<1000) {
                ele.moveTo(zmlx, (zmdy + sum))
            ele.lineTo(zmlx + 8, (zmdy + sum))
            ele.lineTo(zmlx, (zmdy + sum))
            if (i == (pice - 1)) {
                ele.fillStyle = '#000'
                ele.font = "14px Serif";
                ele.fillText(num, zmlx + 12, zmdy + sum - item / 2, 22)
            }
        }
    }
    ele.closePath();
    ele.stroke();
}
```
