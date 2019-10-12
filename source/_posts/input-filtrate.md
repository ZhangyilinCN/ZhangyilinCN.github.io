---
title: "input各种筛选"
date: 2019-10-11 15:09:22
tags:
  - "Html"
  - "Javascript"
categories:
  - "Javascript"
toc: false
description: "关于input的各种筛选"
---

## 标签上直接替换方法：

- **JS 控制不能输入特殊字符**

```html
<input οnkeyup="this.value=this.value.replace(/[^u4e00-u9fa5w]/g,'')" />
```

- **JS 控制文本框只能输入数字**

```html
<input
  οnkeyup="value=value.replace(/[^0-9]/g,'')"
  οnpaste="value=value.replace(/[^0-9]/g,'')"
  oncontextmenu="value=value.replace(/[^0-9]/g,'')"
/>
```

- **JS 控制文本框只能输入数字、小数点**

```html
<input
  οnkeyup="value=value.replace(/[^\0-9\.]/g,'')"
  οnpaste="value=value.replace(/[^\0-9\.]/g,'')"
  oncontextmenu="value=value.replace(/[^\0-9\.]/g,'')"
/>
```

- **JS 控制文本框只能输入英文**

```html
<input
  οnkeyup="value=value.replace(/[^\a-\z\A-\Z]/g,'')"
  οnpaste="value=value.replace(/[^\a-\z\A-\Z]/g,'')"
  oncontextmenu="value=value.replace(/[^\a-\z\A-\Z]/g,'')"
/>
```

- **JS 控制文本框只能输入英文、数字**

```html
<input
  οnkeyup="value=value.replace(/[^\a-\z\A-\Z0-9]/g,'')"
  οnpaste="value=value.replace(/[^\a-\z\A-\Z0-9]/g,'')"
  oncontextmenu="value=value.replace(/[^\a-\z\A-\Z0-9]/g,'')"
/>
```

- **JS 控制文本框只能输入中文**

```html
<input
  οnkeyup="value=value.replace(/[^\u4E00-\u9FA5]/g,'')"
  οnpaste="value=value.replace(/[^\u4E00-\u9FA5]/g,'')"
  oncontextmenu="value=value.replace(/[^\u4E00-\u9FA5]/g,'')"
/>
```

- **JS 控制文本框只能输入中文、英文、数字**

```html
<input
  οnkeyup="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5]/g,'')"
  οnpaste="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5]/g,'')"
  oncontextmenu="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5]/g,'')"
/>
```

- **JS 控制文本框只能输入中文、英文、数字、空格**

```html
<input
  οnkeyup="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5\ ]/g,'')"
  οnpaste="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5\ ]/g,'')"
  oncontextmenu="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5\ ]/g,'')"
/>
```

- **JS 控制文本框只能输入中文、英文、数字、小数点**

```html
<input
  οnkeyup="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5\.]/g,'')"
  οnpaste="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5\.]/g,'')"
  oncontextmenu="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5\.]/g,'')"
/>
```

---

## 输入之后立即清除：

- **验证输入框内不能输入特殊字符,输入就立刻清除**

```javascript
function cleanSpelChar(th) {
  if (/["'<>%;)(&+]/.test(th.value)) {
    $(th).val(th.value.replace(/["'<>%;)(&+]/, ""));
  }
}
```

---

## 如果是特殊字符，禁止输入：

- **验证输入框内不能输入特殊字符，输入前先作判断**

```javascript
function processSpelChar() {
  var code;
  var character;
  if (document.all) {
    code = window.event.keyCode;
  } else {
    code = arguments.callee.caller.arguments[0].which;
  }
  var character = String.fromCharCode(code);
  var txt = new RegExp(/["'<>%;)(&+]/);
  if (txt.test(character)) {
    if (document.all) {
      window.event.returnValue = false;
    } else {
      arguments.callee.caller.arguments[0].preventDefault();
    }
  }
}
```
