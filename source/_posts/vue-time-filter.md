---
title: Vue时间过滤器
date: 2019-11-14 11:40:25
tags:
  - 'Vue'
  - 'Javascript'
  - '日期'
categories:
  - 'Vue'
keywords:
description: 'Vue时间过滤器'
toc: false
---

## vue 时间格式化

### 创建 Date.js

```js
var dateFormat = {
  padLeftZero: function(str) {
    return ('00' + str).substr(str.length)
  },
  formatDate: function(date, fmt) {
    if (/(y+)/.test(fmt)) {
      fmt = fmt.replace(
        RegExp.$1,
        (date.getFullYear() + '').substr(4 - RegExp.$1.length)
      )
    }
    let o = {
      'M+': date.getMonth() + 1,
      'd+': date.getDate(),
      'h+': date.getHours(),
      'm+': date.getMinutes(),
      's+': date.getSeconds()
    }
    for (let k in o) {
      if (new RegExp(`(${k})`).test(fmt)) {
        let str = o[k] + ''
        fmt = fmt.replace(
          RegExp.$1,
          RegExp.$1.length === 1 ? str : this.padLeftZero(str)
        )
      }
    }
    return fmt
  }
}
export default dateFormat
```

### 引入 Date.js

```js
import dateFormat from './js/Date.js'
```

### 创建

``` js
filters: {
    formatDate(time) {
        let date = new Date(time);
        return dateFormat.formatDate(date, "yyyy.MM.dd");
    }
},
```

### 使用

```html
<p>{{item.createDate | formatDate}}</p>
```