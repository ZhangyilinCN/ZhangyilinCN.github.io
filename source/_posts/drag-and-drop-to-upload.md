---
title: 拖拽上传
date: 2019-10-17 16:23:41
tags:
  - "Javascript"
  - "Demo"
categories:
  - "小练习"
keywords:
description: "拖拽上传"
toc: false
---

``` css
/*拖拽上传*/
.uploading {
    width: 500px;
    height: 300px;
    border: 1px dashed #aaa;
    background: #eee;
    margin: 50px auto 0;
    overflow: hidden;
}
.uploading > p {
    font-size: 20px;
    line-height: 24px;
    text-align: center;
    margin-top: 100px;
}
.uploading > span {
    display: block;
    width: 300px;
    margin: 50px auto;
    font-size: 16px;
    line-height: 20px;
    text-align: center;
    color: #aaa;
}
.uploading > img {
    width: 500px;
    height: 300px;
    }
.uploading > video {
    width: 500px;
    height: 300px;
    }
form > button {
    display: block;
    width: 300px;
    height: 50px;
    background: #aaa;
    color: #fff;
    font-size: 20px;
    line-height: 50px;
    text-align: center;
    margin: 50px auto;
    cursor: pointer;
}
```
```html
<script src="http://pzcertt0r.bkt.clouddn.com/jquery-1.11.1.min.js"></script>
<form id="#uploading" action="#" method="post" enctype="multipart/form-data" id="form1">
    <div class="uploading">
        <p>文件上传</p>
        <span>(可直接拖入文件，请将Axure生成的html文件压缩成zip格式后上传)</span>
    </div>
    <button>提交</button>
</form>
```
``` javascript 
$(document).on("drop", function(event) {
    var e = event || window.event;
    e.preventDefault();
});
$(document).on("dragleave", function(event) {
    var e = event || window.event;
    e.preventDefault();
});
$(document).on("dragenter", function(event) {
    var e = event || window.event;
    e.preventDefault();
});
$(document).on("dragover", function(event) {
    var e = event || window.event;
    e.preventDefault();
});

var box = $(".uploading");
box.on("drop", function(event) {
    var e = event || window.event;
    e.preventDefault();
    var type = e.originalEvent.dataTransfer.files;
    if (type.length == 0) {
        return false;
    } else if (type.length > 1) {
        alert("请选择单一文件进行上传");
        return false;
    } else {
        var resous = window.URL.createObjectURL(type[0]);
        if (type[0].type.indexOf("image") == 0) {
        var img = "<img src=" + resous + ">";
        box.find("p").remove();
        box.find("span").remove();
        box.html(img);
        } else if (type[0].type.indexOf("video") == 0) {
        var video =
            '<video controls="controls" src=' + resous + " ></video>";
        box.find("p").remove();
        box.find("span").remove();
        box.html(video);
        } else {
        box.html("<p>文件上传</p><span>已选择文件：" + type[0].name + "</span>");
        }
    }
    resultfile = type[0];
});

$("button").on("click", function() {
    console.log(resultfile);
    console.log(1);
    xhr();
});

function xhr() {
    var fd = new FormData($("#form1"));
    fd.append("file", resultfile);
    $.ajax({
        url: "xxx",
        type: "POST",
        data: fd,
        processData: false, // 告诉jQuery不要去处理发送的数据
        contentType: false, // 告诉jQuery不要去设置Content-Type请求头
        success: function(data) {
            console.log(data);
        }
    });
}
```
