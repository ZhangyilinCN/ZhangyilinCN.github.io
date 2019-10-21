---
title: js打字通
date: 2019-10-21 20:13:26
tags:
  - "Dom"
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "使用原生js简单实现打字通效果"
toc: false
---
``` css
p {
    display: inline-block;
    color:green;
}
span {
    color: red;
}
input {
    display: block;
}
p i{
    color: #000;
    font-style: normal;
}
```
``` html 
<p></p>
<span></span>
```
``` javascript
var p=document.getElementsByTagName('p')[0];
var int=document.getElementsByTagName('input')[0];
var span =document.getElementsByTagName('span')[0];
var i=p.getElementsByTagName('i')[0];
var Arr = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'g', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];
function fn() {
    var rd=Arr[Math.floor(Math.random()*26)];
    var thiss=rd.toUpperCase().charCodeAt();
    span.innerHTML=rd;
    int.onkeydown=function(event){
        if(event.keyCode==thiss){
            p.insertAdjacentText("beforeend", rd);
            fn()
        }
        else if (event.keyCode!=thiss&&event.keyCode!=8) {
            p.insertAdjacentHTML("beforeend", '<i>'+rd+'</i>');
            fn()
        }
    }
}
fn()
```
