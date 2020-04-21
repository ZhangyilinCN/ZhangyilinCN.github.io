---
title: 'iframe-多端通信'
date: 2020-04-21 11:25:46
tags:
  - 'Html'
  - 'Dom'
categories:
  - 'H5+C3'
keywords:
description: 'iframe-多端通信'
toc: false
---

# 使用场景：当 M 端的页面，需要在 PC 端展示，并分离出按钮进行操作处理时，可以使用 iframe 的通信进行操作

### PC 端代码

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>我是PC的</title>
    <style>
      .iframme-wrapper {
        width: 400px;
        height: 150px;
        background: pink;
        margin: 50px auto;
        position: relative;
      }
      .mask {
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        z-index: 2;
      }
      .sonBtn-wrapper {
        width: 300px;
        margin: 0 auto;
        display: flex;
        justify-content: space-around;
      }
      #sonBtn1,
      #sonBtn2 {
        width: 120px;
        height: 100px;
        background: #000;
        color: #fff;
      }
      #showPage {
        font-size: 30px;
        text-align: center;
        margin: 50px 0;
      }
    </style>
  </head>
  <body>
    <div class="iframme-wrapper">
      <div class="mask"></div>
      <iframe
        src="http://127.0.0.1:5500/mPage.html"
        width="400"
        height="150"
        id="iframeDom"
        frameborder="0"
      ></iframe>
    </div>
    <div class="sonBtn-wrapper">
      <button id="sonBtn1">变文字</button>
      <button id="sonBtn2">变颜色</button>
    </div>
    <div id="showPage"></div>
  </body>
  <script>
    window.onload = function () {
      let iframeDom = document.getElementById('iframeDom').contentWindow
      let btndom1 = document.getElementById('sonBtn1')
      let btndom2 = document.getElementById('sonBtn2')
      let pageUrl = 'http://127.0.0.1:5500/mPage.html'
      btndom1.onclick = function () {
        // 发送通信
        iframeDom.postMessage({ type: 'changeTest' }, pageUrl)
      }
      btndom2.onclick = function () {
        // 发送通信
        iframeDom.postMessage({ type: 'changeColor' }, pageUrl)
      }
      // 接受通信
      let showPage = document.getElementById('showPage')
      window.addEventListener('message', function (event) {
        let content = event.data.content
        showPage.innerHTML = '我接受了页面通信内容为' + content
      })
    }
  </script>
</html>
```

### M 端代码

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>我是M的</title>
  </head>
  <style>
    .div {
      width: 300px;
      height: 100px;
      border: 1px solid #000;
      display: flex;
      flex-direction: column;
      text-align: center;
    }
  </style>
  <body>
    <div class="div">
      <p id="page">我是公用页面</p>
      <button id="btn">改变</button>
    </div>
  </body>
  <script>
    let btn = document.getElementById('btn')
    let page = document.getElementById('page')
    btn.onclick = function () {
      page.innerHTML = '我改变了哈哈哈'
    }
    // 接受通信
    window.addEventListener('message', function (event) {
      let type = event.data.type
      if (type == 'changeTest') {
        page.innerHTML = '改变了文字~'
      }
      if (type == 'changeColor') {
        page.style.color = 'blue'
      }
      // 接受消息后，并发送消息
      let url = 'http://127.0.0.1:5500/pcPage.html'
      top.postMessage({ content: type }, url)
    })
  </script>
</html>
```
![iframe-Signalpic.png](https://i.loli.net/2020/04/21/dU6lATQj8aCKsYS.png)
![iframe-Signal.gif](https://i.loli.net/2020/04/21/NkiyOB6MHacUoRd.gif)
