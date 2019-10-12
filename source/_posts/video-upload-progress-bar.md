---
title: 带进度条显示的视频上传
date: 2019-10-12 16:25:30
tags:
  - "Jquery"
  - "upload"
categories:
  - "Jquery"
keywords:
description: "使用ajax的xhr来实现带进度条显示的视频上传"
toc: false
---
``` javascript
// 上传视频的删除按钮
    var stopAjax=''
    $('#delUploadBtn').on('click',function () {
       stopAjax.abort(); //停止ajax上传
    })
 
// 上传视频实时进度
    $('#file').on('change',function () {
        var videoUrl=$(this).val();
        var urlType=videoUrl.substring(videoUrl.lastIndexOf(".")).toLowerCase();
        if(!urlType.match(/.mp4|.flv|.avi|.rmvb|.wmv|.mov|.mkv|.rm|.mpg|.webm|.mpeg4|.ts/)){
            alert('上传错误,视屏格式必须为：mp4/flv/avi/rmvb/wmv/mov/mkv/rm/mpg/webm/mpeg4/ts')
        }else{
            $('#videoName').html($(this).val().slice($(this).val().lastIndexOf("\\")+1)) //显示视频名
            ajaxUploadingFn()
        }
    })
// 上传实时信息函数
    function onprogress(evt){
        var loaded = evt.loaded;     //已经上传大小情况
        var tot = evt.total;      //附件总大小
        var per = Math.floor(100*loaded/tot);  //已经上传的百分比
        $('.baifenbiNum').html(per +"%") 
        $('.baifenbiWid').css("width" , per +"%"); //控制进度条的长度
    }
    // 上传视频的ajax函数执行
    function ajaxUploadingFn() {
        var videoText=new FormData();
        videoText.append("file" , $("#file").files[0]);
        stopAjax=$.ajax({
            url:"xxxxxxx",
            type:'post',
            dataType:'json',
            data:videoText,
            processData : false,
            contentType : false ,
            xhr: function(){
                var xhr = $.ajaxSettings.xhr();
                if(onprogress && xhr.upload) {
                    xhr.upload.addEventListener("progress" , onprogress, false);
                    return xhr;
                }
            },
            success:function (res) {
                if(data.code==1){
                   XXXXX
                }
            }
        })
     }
```