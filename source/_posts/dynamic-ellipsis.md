---
title: 动态省略号
date: 2019-10-11 13:35:45
tags: 
    - "Css"
categories: 
    - "H5+C3"
keywords:
description: "纯css实现动态省略号"
---
### 通过使用css的keyframes来实现动态省略号
**Css：**
```
.loading {
    font-family: simsun;
}
:root .loading {
    display: inline-block;
    width: 1.5em;
    vertical-align: bottom;
    overflow: hidden;
}
@-webkit-keyframes loading {
    0% { width: 0; margin-right: 1.5em; }
    33% { width: .5em; margin-right: 1em; }
    66% { width: 1em; margin-right: .5em; }
    100% { width: 1.5em; margin-right: 0;}
}
.loading {
    -webkit-animation: loading 3s infinite step-start;
}

@keyframes loading {
    0% { width: 0; margin-right: 1.5em; }
    33% { width: .5em; margin-right: 1em; }
    66% { width: 1em; margin-right: .5em; }
    100% { width: 1.5em; margin-right: 0;}
}
.loading {
    animation: loading 3s infinite step-start;
}
```
**Html：**
```
<p>上传中<span class="loading">...</span></p>
```
