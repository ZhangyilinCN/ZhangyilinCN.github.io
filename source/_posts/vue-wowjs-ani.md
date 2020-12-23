---
title: 在vue中使用wowjs
date: 2020-12-23 16:28:16
tags:
  - 'Vue-cli'
  - '动画'
categories:
  - 'Vue-cli'
---

**在 vue 中使用 wowjs+animated.css，进行一些动画效果**

## 当前版本

```json
"wowjs": "^1.1.3"
"animate.css": "^3.7.2",
```

## 下载

```js
// 注意这里的版本,animatev4 修改了命名方式，所以这里使用的是 v3
npm i wowjs animate.css -S
```

## 注入

```js
import 'animate.css'
import { WOW } from 'wowjs'
export default {
  mounted() {
    this.$nextTick(() => {
      let wow = new WOW({
        live: false,
      })
      wow.init()
    })
  },
}
```

## 使用

```html
<!-- 在div上使用wow+动画名就可以使用了 -->
<div class="name wow slideInUp"></div>
```
