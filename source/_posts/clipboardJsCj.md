---
title: 兼容ios和安卓的复制插件(clipboard.js)
date: 2019-10-29 10:46:54
tags:
  - "复制"
  - "插件"
categories:
  - "插件"
keywords:
description: "兼容ios和安卓的复制插件(clipboard.js)"
toc: false
---

### 首先下载插件

`npm install clipboard --save`

- **2个元素的复制呼应**

    ```html
    <div class="copydiv">
    <p>链接：<span id="urlSpan">http://www.10pinping.com/vote...</span></p>
    <button data-clipboard-target="#urlSpan" class="copyBtn">复制</button>
    </div>
    ```

- **单个元素的复制**

    ```html
    <button data-clipboard-text="我是复制内容xxxx" class="copyBtn">复制</button>
    ```

---

### 最后在js中进行初始化
``` javascript
var clipboard = new ClipboardJS('.copyBtn'); //初始化
绑定成功与失败事件
clipboard.on('success', function (e) {
    alert('复制成功！')
});
clipboard.on('error', function (e) {
    alert('复制失败！')
});
```

### 其中的自定义属性
``` javascript
//触发按钮身上的属性：
data-clipboard-target='映射到被绑定元素的#xx（id名）'
data-clipboard-action="cut" 表明要剪切(cut-只能在input和textarea生效)还是复制(copy)，默认为copy
data-clipboard-text='复制的内容' 
```
