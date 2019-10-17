---
title: 判断页面的打开来源
date: 2019-10-17 21:53:17
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "简单的利用JS来判断页面是在手机端还是在PC端打开的方法"
toc: false
---
``` javascript
window.location.href = /Android|webOS|iPhone|iPod|BlackBerry/i.test(navigator.userAgent) ? "https://www.baidu.com/" :  "http://news.baidu.com/";
```
**以上代码利用了正则表达式和三目运算符，含义就是如果是移动端打开的话那就跳转到 `https:www.baidu.com/` ，如果不是就跳转到`http://new.baidu.com/`，这个看不懂的话，那我下面这样写就很容易理解了吧**

``` javascript
if(/Android|webOS|iPhone|iPod|BlackBerry/i.test(navigator.userAgent)) {
    window.location.href = "https://www.baidu.com/"; //m端
} else {
    window.location.href = "http://news.baidu.com/";  //pc端
}
```

