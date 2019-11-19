---
title: scss-mixin的基本（手机1px边框适配）
date: 2019-11-14 10:20:11
tags:
  - 'scss/sass'
  - 'Css'
  - 'mixin'
categories:
  - 'scss/sass'
keywords:
description: 'scss-mixin的基本（手机1px边框适配）'
toc: false
---

``` scss
$border-poses:top,
right,
bottom,
left;
$color:#333;
 
@mixin border-1px($color, $pos) {
  position: relative;
 
  &::after {
   content: '';
    display: block;
    position: absolute;
    width: 100%;
    @each $item in $pos {
      border-#{$item}: 1px solid $color;
      #{$item}: 0;
    }
  }
}
@media (-webkit-min-device-pixel-ratio:1.5),
(min-device-pixel-ratio: 1.5) {
  .border-1px &::after {
    -webkit-transform: scaleY(0.7);
    transform: scaleY(0.7);
  }
}
 
@media (-webkit-min-device-pixel-ratio:2),
(min-device-pixel-ratio: 2) {
  .border-1px &::after {
    -webkit-transform: scaleY(0.5); //像素比为2的时候，我们设置缩放为0.5
    transform: scaleY(0.5);
  }
}
 
@media (-webkit-min-device-pixel-ratio:3),
(min-device-pixel-ratio: 3) {
  .border-1px &::after {
    -webkit-transform: scaleY(0.333333); //像素比为3的时候，我们设置缩放为0.33333
    transform: scaleY(0.333333);
  }
}
```


## 使用

``` scss
@include border-1px(red,bottom);如果想要多边的话可以用类似数组的这种传参方式（[bottom top]）
```

**因为做了dpi的适配，所以需要在，需要的地方给予此类**

``` html
<div class="nav border-1px">
    .....
</div>
```

---



