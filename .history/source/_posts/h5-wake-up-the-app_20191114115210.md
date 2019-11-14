---
title: html5点击唤醒app
date: 2019-11-14 11:49:08
tags:
  - 'Javascript'
  - 'Demo'
categories:
  - '小练习'
keywords:
description: 'html5点击唤醒app'
toc: false
---

**h5页面唤醒app，以淘宝为例子**

``` html
<a οnclick="openApp()">点击唤醒app</a>	
```

``` js
var download_schema = 'taobao://'; //app的协议有安卓同事提供，这里是用的淘宝
var universal_link = 'ios下载地址';//ios下载地址
var getVersionUrl = 'Android下载地址';//Android移动端下载地址
var u = navigator.userAgent.toLocaleLowerCase();
//console.log(u);
var isWeixin = u.match(/MicroMessenger/i) == 'micromessenger'; //判断是不是微信浏览器
var isAndroid = u.indexOf('android') > -1 || u.indexOf('linux') > -1; //android终端或者uc浏览器
var isiOS = !! u.match(/(iphone|ipod|ipad|mac)/i);
 
function openApp() {
    //alert('1');
    //alert(isAndroid);
    //alert(isiOS);
    if (isAndroid) {
        android1();
    }
    if (isiOS) {
        ios();
    }
    //alert("调用下载失败"); //此处弹窗时，是没有version参数，如果在app中打开，是会有这个参数的
}
 
function android1() {
    //如果是微信,直接下载
    if (isWeixin) {
        window.location.href = "Android下载地址 "; /***Android移动端下载地址***/
    } else {
        window.location.href = download_schema; /***打开app的协议，有安卓同事提供***/
        window.setTimeout(function () {
            //window.location.href = "Android下载地址";/***Android移动端下载地址***/
            window.location.href = getVersionUrl; /***Android移动端下载地址***/
        }, 100);
    }
}
 
function ios() {
    window.location.href = universal_link + "?schema=" + encodeURIComponent(download_schema);
} 
```