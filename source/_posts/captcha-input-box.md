---
title: 验证码输入框
date: 2019-10-21 20:07:39
tags:
  - 'Dom'
  - 'Jquery'
  - 'Demo'
categories:
  - '小练习'
keywords:
description: '4位验证码输入框（支持字母、数字、中文等）'
toc: false
---

```css
* {
  padding: 0;
  margin: 0;
}

.demo {
  width: 230px;
  height: 50px;
  margin: 200px auto;
  overflow: hidden;
  position: relative;
}

.demoInput {
  position: absolute;
  opacity: 1;
  top: 200px;
  left: 50%;
  transform: translateX(-50%);
}

.numberDiv {
  width: 50px;
  height: 50px;
  border: 1px solid #ccc;
  box-sizing: border-box;
  float: left;
  margin-left: 10px;
  font-size: 24px;
  color: red;
  line-height: 48px;
  text-align: center;
}

.numberDiv.on {
  border-color: red;
}

.numberDiv:first-child {
  margin-left: 0;
}
```

```html
<div class="demo">
  <div class="numberDiv"></div>
  <div class="numberDiv"></div>
  <div class="numberDiv"></div>
  <div class="numberDiv"></div>
  <input type="text" class="demoInput" />
</div>
```

```javascript
// 要先引入jquery.js
$('.numberDiv').click(function () {
  $('.demoInput').focus()
})
var inputLock = false
$('.demoInput').on('compositionstart', function () {
  inputLock = true
})
$('.demoInput').on('compositionend', function () {
  inputLock = false
  changeNum()
})
$('.demoInput').on('input', function () {
  changeNum()
})
function changeNum() {
  if (!inputLock) {
    var numbers = $('.demoInput').val()
    var arr = numbers.split('')
    var numberDiv = $('.numberDiv')
    $.each(numberDiv, function (idx, ele) {
      var text = arr[idx] == undefined ? '' : arr[idx]
      var addClassFlag = arr[idx] == undefined ? '' : 'on'
      $(ele).html(text).removeClass('on').addClass(addClassFlag)
    })
    $('.demoInput').val($('.demoInput').val().slice(0, 4))
  }
}
```
