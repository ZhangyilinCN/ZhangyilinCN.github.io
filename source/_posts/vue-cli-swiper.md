---
title: vue-cli中使用swiper
date: 2019-11-14 10:42:08
tags:
  - 'Vue-cli'
categories:
  - 'Vue-cli'
keywords:
description: 'vue-cli中使用swiper'
toc: false
---

## 下载

```js
npm i vue-awesome-swiper -s
```

## 使用

### 在 main.js 中

```js
import VueAwesomeSwiper from 'vue-awesome-swiper'
Vue.use(VueAwesomeSwiper)
```

### 在所需要的页面中

```js
import 'swiper/dist/css/swiper.css'
import { swiper, swiperSlide } from 'vue-awesome-swiper'
```

---

```html
<swiper :options="swiperBanner">
  <div class="swiper-slide">
    <img src="../assets/img/1.png" alt />
  </div>
  <div class="swiper-slide">
    <img src="../assets/img/2.png" alt />
  </div>
  <div class="swiper-slide">
    <img src="../assets/img/3.png" alt />
  </div>
  <div class="swiper-slide">
    <img src="../assets/img/4.png" alt />
  </div>
</swiper>
```

```html
<!-- 或者这样的html -->
<swiper :options="swiperBanner" v-if="lunboArr.length>0">
  <div class="swiper-slide" v-for="item in lunboArr" :key="item.id">
    <a :href="item.url">
      <img :src="item.img" alt />
    </a>
  </div>
</swiper>
```

```js
data() {
    return {
      swiperBanner: {
        loop: true, // 循环模式选项
        speed: 1000,
        autoplay: true,
        autoplayDisableOnInteraction: false
      }
    };
  },
  components: {
    swiper,
    swiperSlide
  },
```

---
