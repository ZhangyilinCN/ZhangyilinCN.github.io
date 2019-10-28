---
title: js点击按钮复制文本
date: 2019-10-17 16:18:39
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "js点击按钮复制文本"
toc: false
---
``` css
input {
    width: 1px;
    height: 1px;
    opacity: 0;

}
div {
    width: 300px;
    height: 50px;
    border: 1px solid #000;
    margin: 100px auto;
    overflow: hidden;
}
```
``` html
<div>
    <a href="#">111111111111111111111<input type="text"><span>复制</span></a>
</div>
```
``` javascript
// 记得要先引入Jquery.js
$('div>a>span').click(function (e) {
    e.preventDefault();
    $(this).siblings('input').val($(this).parent().text().replace('复制',''))
    var copytext=$(this).siblings('input')
    copytext.select(); //选择其中的文本
    document.execCommand("Copy"); //执行浏览器中的自带复制指令
    alert("已复制到粘贴板");
})
```
