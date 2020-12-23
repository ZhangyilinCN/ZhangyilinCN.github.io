---
title: vue-cli中使用swiper的省略图
date: 2020-12-23 16:02:50
tags:
  - 'Vue-cli'
  - 'Swiper'
categories:
  - 'Vue-cli'
keywords:
description: 'vue-cli中使用swiper'
toc: false
---

## 当前实践的版本

```json
"swiper": "^5.4.0",
"vue-awesome-swiper": "^4.1.1",
```

```html
<template>
  <div class="demo">
    <swiper :options="swiperObj" class="swiper1">
      <div class="swiper-slide" v-for="item in swiperList" :key="item.id">
        {{item.title}}
      </div>
    </swiper>
    <swiper :options="swiperObj.thumbs.swiper" class="swiper2">
      <div class="swiper-slide" v-for="item in swiperList" :key="item.id">
        {{item.id}}
      </div>
    </swiper>
    <div class="demo-next-btn"></div>
    <div class="demo-prev-btn"></div>
  </div>
</template>
<script>
  import 'swiper/css/swiper.css'
  import { Swiper } from 'vue-awesome-swiper'
  export default {
    data() {
      return {
        swiperObj: {
          effect: 'cube', //设置切换时候的效果
          loop: 'true', //是否为循环轮播
          autoplay: {
            delay: 5000, //多少秒进行自动切换
          },
          autoplayDisableOnInteraction: false, //false为当用户自己切换后还会进行自动轮播
          navigation: {
            //设置左右按钮
            nextEl: '.demo-next-btn',
            prevEl: '.demo-prev-btn',
          },
          thumbs: {
            //设置缩略图
            swiper: {
              //里面跟swiper的设置项
              el: '.products-swiper2',
              spaceBetween: 7, //间距7px
              slidesPerView: 6, //同屏出现几个swiper-slide
              slideToClickedSlide: true, //设置为true则点击slide会过渡到这个slide。
            },
            slideThumbActiveClass: 'slide-thumb-active',
            //设置选中的active类，在缩略图的swiper中,原来默认的active类是失效的，需要重新命名一个新的active类，用此类进行一些active的样式编写
          },
        },
        swiperList: [xxx],
      }
    },
    components: {
      Swiper,
    },
  }
</script>
```
