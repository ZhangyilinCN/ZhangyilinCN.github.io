---
title: 原生瀑布流图片墙
date: 2019-10-21 19:50:00
tags:
  - "Jquery"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "使用jquery来完成瀑布流的图片墙"
toc: false
---
``` css
* {
    padding: 0;
    margin: 0;
}
.main {
    width: 100%;
    position: relative;
    background: skyblue;
}
.boxs {
    width: 200px;
    border: 1px solid #000;
    padding: 5px;
    background: #ccc;
    position: absolute;
}
.boxs img {
    width: 100%;
}
.boxs h2,.box p {
    text-align: center;
}
```
``` html
<script src="http://pzcertt0r.bkt.clouddn.com/jquery-1.11.1.min.js"></script> 
<div class="main"></div>
```
``` javascript
$(function () {
    //在页面显示出全部盒子
    var boxs=''
    for(var i=1;i<=70;i++){
        boxs+='<div class=\'boxs\'><h2>哈哈哈哈</h2><img src=img/'+i+'.jpg><p>为什么这么的难啊难</p></div>';
    }
    $('.main').html(boxs);
    var obj= {
        // 初始化
        init: function () {
            this.lie = Math.floor($('.main').width() / $('.boxs').outerWidth());
            this.space = ($('.main').width() - this.lie * $('.boxs').outerWidth()) / (this.lie + 1);
            this.gao = 15;
            this.arrXY=[];
            this.two();
        },
        two: function(){
            for(var i=0;i<this.lie;i++){
                var pos={
                    left:(i*$('.boxs').eq(i).outerWidth()+(this.space*(i+1))),
                    top: $('.boxs').eq(i).outerHeight()+this.gao*2
                }
                $('.boxs').eq(i).animate({
                    top:this.gao,
                    left:(i*$('.boxs').eq(i).outerWidth()+(this.space*(i+1)))
                },1000);
                this.arrXY.push(pos);
            }
            this.three();
        },
        three:function () {
            for(var i=this.lie;i<=70;i++){
                var index=this.getMinTop();
                $('.boxs').eq(i).animate({
                    left:this.arrXY[index].left,
                    top:this.arrXY[index].top
                },1000)
                this.arrXY[index].top+=$('.boxs').eq(i).outerHeight()+this.gao;
            }
        },
        getMinTop:function(){
            var mixHeight=this.arrXY[0].top;
            var index=0;
            for(var i=0;i<this.arrXY.length;i++){
                if(mixHeight>this.arrXY[i].top){
                    mixHeight=this.arrXY[i].top;
                    index=i;
                }
            }
            return index;
        }
    }
    obj.init()
    $(window).resize(function(){
        obj.init();
    })
})
```
