---
title: 使用formData上传并显示图片
date: 2019-10-12 15:08:27
tags:
  - "Jquery"
  - "upload"
categories:
  - "Jquery"
keywords:
description: 使用formData上传图片到服务器并显示图片
toc: false
---

## 本地直接显示图片浏览

```javascript
$("#file").on("change", function() {
  var imgUrl = $(this).val();
  var lookImgSrc = window.URL.createObjectURL(this.files[0]);
  var urlType = imgUrl.substring(imgUrl.lastIndexOf(".")).toLowerCase();
  if (!urlType.match(/.png|.jpg|.jpeg/)) {
    alert("上传错误,文件格式必须为：png/jpg/jpeg");
  } else {
    $(this)
      .siblings("img")
      .attr("src", lookImgSrc);
  }
});
```

---

## 图片上传到服务器并回显图片

```javascript
var formdata = new FormData();
formdata.append("file(接口的参数名字)", $("#files").files[0]);
$.ajax({
  url: "xxxxxx", //后台接口地址
  type: "post",
  dataType: "json",
  data: formdata,
  contentType: false, //必须写 确认格式等
  processData: false, // ....
  cache: false, // ...
  success: function(res) {
    $("#img").attr("src", res.files); //根据后台的返回参数给予img的网络路径
  }
});
```
