---
title: 微信分享
date: 2019-11-14 10:27:31
tags:
  - 'WeChat'
  - 'Javascript'
categories:
  - 'WeChat'
keywords:
description: '微信分享'
toc: false
---

``` js
export const defaultWxshare = (shareImg,shareDesc,shareTitle) => {
  let LocUrl = encodeURIComponent(location.href.split("#")[0]);
  LocUrl = LocUrl.replace(/\&/g, "%26");
  axios
    .get(`http://api.pinpaizw.com/interface/pinpai3/mobile/wx_get_signature.php?url=${LocUrl}`)
    .then(response => {
      let link = response.data.res.url;
      let shareUrl = link
      // 微信分享基本配置
      let wxConfig = {
        debug: false, //生产环境需要关闭debug模式
        appId: response.data.res.appid, //appId通过微信服务号后台查看
        timestamp: response.data.res.timestamp, //生成签名的时间戳
        nonceStr: response.data.res.nonceStr, //生成签名的随机字符串
        signature: response.data.res.signature, //签名
        jsApiList: [
          //需要调用的JS接口列表
          "checkJsApi", //判断当前客户端版本是否支持指定JS接口
          "onMenuShareTimeline", //分享给好友
          "onMenuShareAppMessage" //分享到朋友圈
        ]
      }
      wx.config(wxConfig); // 微信分享配置
      wx.ready(function () {
        let shareConfig = {
          title: shareTitle,
          link: shareUrl,
          desc: shareDesc,
          imgUrl: shareImg
        }
        console.log(shareTitle);
        console.log(shareDesc);
        console.log(shareImg);
        wx.onMenuShareTimeline(shareConfig);
        wx.onMenuShareAppMessage(shareConfig);
 
        wx.error(function (errText) {
          console.log(errText);
        });
 
      });
    })
    .catch(errorVal => {
      console.log(errorVal.errMsg);
    });
}
```

