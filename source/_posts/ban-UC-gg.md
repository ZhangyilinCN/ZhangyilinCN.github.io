---
title: '去除uc底部插入的广告'
date: 2020-07-02 15:38:01
tags:
  - 'Dom'
  - 'Jquery'
  - 'Demo'
categories:
  - 'Jquery'
keywords:
description: '去除uc底部插入的广告'
---

```js
//需要先引入jq
setTimeout(function () {
  $("[id^='_']").hide()
}, 500)
```

```js
// 这个亲测有效(这不过有局限性)
$(document).scroll(function () {
  if ($('iframe').length > 0) {
    $('iframe').parent('div').remove()
    $('iframe').remove()
  }
})
```
