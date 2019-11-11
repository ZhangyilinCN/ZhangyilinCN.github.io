---
title: Masonry（瀑布流插件）和 Imagesloaded（图片加载插件）
date: 2019-11-06 14:54:40
tags:
  - "瀑布流"
  - "懒加载"
  - "插件"
categories:
  - "插件"
keywords:
description: "Masonry（瀑布流插件）和 Imagesloaded（图片加载插件）"
toc: false
---

## [点我进Masonry官网下载](https://masonry.desandro.com/)

```html
<div class="pull">
  <div class="pullBox"><img src="img/1.jpg" alt="" /></div>
  <div class="pullBox"><img src="img/2.jpg" alt="" /></div>
  <div class="pullBox"><img src="img/3.jpg" alt="" /></div>
  ...........
</div>
```

```javascript
var aa=$('.pull').masonry({
    itemSelector:'.pullBox',  //选择其子元素（必选）
    columnWidth:300,           //规定其一个盒子的宽度(必选）
    gutter ： 30,          //设置其每个盒子之间的横向距离，纵向距离在css中设置就行
    horizontalOrder: true ,   //使内容都从左到右
    transitionDuration: 1000,  //当改变视口大小后，需要多少时间来调整的动画效果
    stagger: 0,       //当列间隙发生改变后，需要多少秒的判定，才进入transitionDuration(整合效果)
    resize:false  //当视口发生改变时，盒子是否会进行调整，默认为true
})
// 给予图片加载完毕才出现的插件方法
aa.imagesLoaded().progress( function() {
    aa.masonry('layout');
});

//点击盒子，删除自身
$('.pull').on('click','.pullBox',function () {
    aa.masonry('remove',this).masonry('layout')
})
//点击按钮，增加盒子
$('button').on('click',function () {
    var ran=Math.ceil(Math.random()*70);
    var box='<div class="pullBox"><img src="img/'+ran+'.jpg"</div>'
    box=$(box);
    aa.append(box).masonry('appended',box)
    aa.imagesLoaded().progress(function () {
        aa.masonry('layout');
    })
})
```
