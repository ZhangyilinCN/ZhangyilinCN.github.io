---
title: vue-cli中使用swiper
date: 2019-11-14 10:42:08
tags:
  - 'Vue-cli'
  - 'Swiper'
categories:
  - 'Vue-cli'
keywords:
description: 'vue-cli中使用swiper'
toc: false
---

## 由于现在 swiper 更新到了 6，所以这里降级处理，现在为 `"swiper": "^5.4.0",` 的使用配置

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
import 'swiper/css/swiper.css'
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
```

---

```html
<swiper :options="swiperBanner">
  <div class="swiper-slide">slide-1</div>
  <div class="swiper-slide">slide-2</div>
  <div class="swiper-slide">slide-3</div>
  <div class="swiper-slide">slide-4</div>
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
    Swiper,
    SwiperSlide
  },
```

---
