---
title: 使用构造函数实现拖拽
date: 2019-10-21 19:58:35
tags:
  - "Dom"
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "使用构造函数实现拖拽功能"
toc: false
---

``` css
*{
    padding: 0;
    margin: 0;
}
button {
    display: block;
    border: none;
    outline: none;
    width: 200px;
    height: 50px;
    line-height: 50px;
    font-size: 24px;
    color: red;
    background: #aaa;
    border-radius: 20%;
    margin: 20px auto;
}
div {
    position: absolute;
    border: 1px solid #000;
    top: 0;
    left: 0;
}
```
``` html
<button>叮！！！</button>
```
``` javascript
var btns=document.getElementsByTagName('button')[0];
var bodys=document.getElementsByTagName('body')[0];
function Box() {
    this.width=100;
    this.height=100;
    this.creatBox();
}
Box.prototype.ranColor=function(){
    return Math.floor(Math.random()*255);
}
Box.prototype.creatBox=function () {
    this.ele=document.createElement('div');
    this.ele.style.cssText='width:'+this.width+'px;height:'+this.height+'px;background:rgb('+this.ranColor()+","+this.ranColor()+","+this.ranColor()+");";
    bodys.append(this.ele);
    this.resize();
}
Box.prototype.resize=function () {
    var that=this;
    this.ele.onmousedown=function (ev) {
        var boxX=ev.clientX-this.offsetLeft;
        var boxY=ev.clientY-this.offsetTop;
        document.onmousemove=function (ev) {
            that.ele.style.cssText+='left:'+(ev.clientX-boxX)+'px;top:'+(ev.clientY-boxY)+'px';
        }
        document.onmouseup=function () {
            document.onmouseup=document.onmousemove=null;
        }
    }
}
btns.onclick=function () {
    var a=new Box();
}
```
