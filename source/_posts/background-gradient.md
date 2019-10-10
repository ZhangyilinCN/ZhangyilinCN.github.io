---
title: 背景色渐变
date: 2019-10-10 15:05:00
tags: 
    - "Html"
    - "Css"
categories: 
    - "H5+C3"
keywords:
toc: false
description: "css3的背景色渐变"
cover: /img/html_css.jpg
---
## 线性渐变
```
background-image: -webkit-linear-gradient(30deg,red 0,red 300px,blue 300px,yellow 600px);
```
**如果给予单色开始和结尾项的话，那么就是突然转变，不给结尾项就是渐变； deg表示两色之间的角度大小；**
{% asset_img 01.png [线性渐变] %}
***
## 线性重复渐变：
```
background-image: -webkit-repeating-linear-gradient(30deg,red 0,green 300px);
```
{% asset_img 02.png [线性重复渐变] %}
***
## 径向渐变
**center和50%都表示的是圆心；**
```
background:-webkit-radial-gradient(center,red 0px,blue 150px);
```
{% asset_img 03.png [径向渐变] %}
***
## 径向重复渐变
```
background:-webkit-repeating-radial-gradient(center,red 0px,blue 50px);
```
{% asset_img 04.png [径向重复渐变] %}




