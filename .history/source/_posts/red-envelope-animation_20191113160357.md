---
title: 红包晃动动画
date: 2019-10-17 15:10:00
tags:
  - "Javascript"
  - "Demo"
  - "Css"
categories:
  - "小练习"
keywords:
description: "使用css/js两种方式完成红包晃动动画效果"
---

![](https://wx2.sinaimg.cn/mw690/ed984376ly1g8wgj53nt1g20ci08pabl.gif)

---

## 使用css来实现：
``` css 
span {
    display: block;
    width: 150px;
    height: 200px;
    background-color: red;
    line-height: 200px;
    font-size: 24px;
    overflow: hidden;
    text-align: center;
    position: fixed;
    right: -75px;
    bottom: 500px;
    transform: rotate(-30deg);
    animation: bagAnimation 3s  linear infinite ;
}
@keyframes bagAnimation {
    0% {
        transform: rotate(-30deg);
    }
    /* 0-30一样是为了模拟每次的延迟生效时间 */
    30% {
        transform: rotate(-30deg); 
    }
    40% {
        transform: rotate(0deg);
    }
    50% {
        transform: translateX(-200px);
    }
    55% {
        transform: translateX(-200px) rotate(-15deg);
    }
    60% {
        transform: translateX(-200px) rotate(15deg);
    }
    65% {
        transform:  translateX(-200px) rotate(-15deg);
    }
    70% {
        transform: translateX(-200px) rotate(15deg);
    }
    75% {
        transform: translateX(-200px) rotate(0deg);
    }
    85% {
        transform: translateX(0);
    }
    100% {
        transform: translateX(0) rotate(-30deg);
    }
}
```
``` html
<span>红包</span>
```
---
## 使用js来实现
**因为是生成dom,对dom的反复操作,并且是使用定时器来完成，所以不推荐**

``` javascript
// 记得要先引入Jquery.js
/*
    a : 初始角度
    b : 到达晃动时，a为右晃动，b的初始为a的有晃动峰值
    c : c为b的左晃动的峰值
    d : 为更替循环到a时的变量
    sun ：晃动的次数
    lDis : 距离右侧的初始距离
    rDis ：与lDis的最大移动到的距离相同
    cont : 测试用，用来实验循环动画一次，所需要的时间，并非与外侧定时器时间，从而达到执行一周后出现停顿效果
timer ：给予里的定时器的变量
    */
 
var a=-30;
var b=15;
var c=-15;
var d=0;
var sun=0;
var lDis=-50;
var rDis=100;
var cont=0
var timer=null
 
setInterval(function () {
    timer=setInterval(function () {
        // cont++;
        // 一开始是-30deg，然后慢慢的变正
        if(a<0){
            $('span').css('transform','rotate('+a+'deg)');
            a++;
        }
        // 正了之后,给予lDis最大的移动距离，开始移动
        if(a==0&&lDis<100){
            $('span').css('right',lDis+'px');
            lDis+=2;
            if(lDis==100){
                rDis=100;
            }
        }
        // 移动到规定距离后，开始右晃到指定角度
        if(lDis==100&&a>=0&&a<15){
            a++;
            if(a==15){
                b=15;
            }
            $('span').css('transform','rotate('+a+'deg)');
        }
        // 右晃到指定角度后，开始左晃到指定角度
        if(lDis==100&&a==15&&b>-15){
            b--
            if(b==-15){
                c=-15
            }
            $('span').css('transform','rotate('+b+'deg)');
        }
        // 然后左晃到指定角度后，让他回正
        if(lDis==100&&b==-15&&c<0){
            c++
            if(c==0) {
                a = 0;
                sun++
                // 晃动循环3次
                if(sun>3){
                    sun=3;
                }
            }
            $('span').css('transform','rotate('+c+'deg)');
        }
        // 循环3次后，初始下各个值，然后向回移动
        if(sun==3&&rDis>-50){
            a=0;
            rDis-=2;
            b=15;
            c=-15;
            d=0;
            $('span').css('right',rDis+'px');
        }
        // 移动到一开始的位置后，使用d来执行到a原来的-30角度（如果这里直接用a会出现闪动）
        if(rDis==-50&&d>-30){
            d--;
            $('span').css('transform','rotate('+d+'deg)');
        // 把a、sun、和lDis变为初始值
            if(d==-30){
                lDis=-50;
                sun=0;
                a=-30
                // 停止计时器，即为执行了整整一次完整的动画循环
                clearInterval(timer)
                // console.log(cont);
            }
        }
    },10)
    // 根据cont的值，为外侧定时器给予秒数，从而达到停顿效果
},5000)
```