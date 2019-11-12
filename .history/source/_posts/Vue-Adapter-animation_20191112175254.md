---
title: vue-跟随屏幕位置改变的半场动画
date: 2019-11-12 17:51:15
tags:
  - "Vue"
  - "Demo"
categories:
  - "Vue"
keywords:
description: "vue-跟随屏幕位置改变的半场动画"
toc: false
---


**定义小球（如果当前页面有其他的动画效果的定义，不要用默认的v-enter...，要重新定义name，用name-enter，用此方式覆盖污染）**

``` html
<transition @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter">
   <span class="smball" v-show="ballflag" ref="ball">
     <b ref="innerBall"></b>
   </span>
</transition>
```
