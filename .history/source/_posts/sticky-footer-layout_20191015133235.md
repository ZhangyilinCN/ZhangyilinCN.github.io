---
title: "sticky footer布局"
date: 2019-10-15 13:13:40
tags:
  - "Html"
  - "Css"
categories:
  - "H5+C3"
keywords:
description: "sticky footer布局"
toc: false
---
**到页面内容铺不满页面时候，下方div始终定在下面;**
**当页面内容多余一屏的时候，出现滚动条下方的div会被顶到下面去;**
``` html
<div id="main">
    <div class="main_top clearfix">
        <div class="main_top_content">
            我是第1行哈
            我是第2行哈
        </div>
    </div>
    <div class="main_bottom">X</div>
</div>
```
``` css
#main {
    position: fixed;
    top: 0%;
    left: 0;
    width: 100%;
    max-width: 640px;
    height: 100%;
    overflow: auto;
    font-size: 50px;
    background: rgba(0, 0, 0, 0.5);
}
.main_top {
      
}
.main_top_content {
    padding-bottom: 100px; /*和下方的 div+div距离底部的距离和 保持高度一致*/
}
.main_bottom {
    position: relative;
    padding-top: 30px;
    margin-top: -100px;
    text-align: center;
}
/*清除浮动*/
.clearfix:after {
    content: " ";
    height: 0;
    clear: both;
    display: block;
    visibility: hidden;
}
.clearfix {
    *zoom: 1;
}
```
![](http://pzcertt0r.bkt.clouddn.com/sticky-footer-layout.jpg)


