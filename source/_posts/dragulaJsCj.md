---
title: 拖动插件(dragula.js)
date: 2019-10-31 18:25:17
tags:
  - "拖动"
  - "插件"
categories:
  - "插件"
keywords:
description: "拖动插件(dragula.js)"
toc: false
---

## 首先需要下载插件
`npm install dragula --save`

``` css
ul {
    width: 500px;
    height: 500px;
    border: 1px solid #000;
    margin: 100px auto;
}
li {
    width: 48%;
    height: 50px;
    box-sizing: border-box;
    border: 1px solid red;
    background: yellowgreen;
}
```

``` html
<ul id="uuu">
    <li>11111111111111</li>
    <li>22222222222222</li>
    <li>33333333333333</li>
    <li>44444444444444</li>
    <li>55555555555555</li>
    <li>66666666666666</li>
</ul>
<button>drag</button>
```

``` javascript
//记得要引入Jquery.js、dragula.js、dragula.css
var drake=dragula([document.getElementById('uuu')])
$('button').on('click',function () {
    drake.destroy(); //取消拖动
})
 ```












