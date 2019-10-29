---
title: vue时间过滤器(moment)
date: 2019-10-29 18:19:44
tags:
  - "日期"
  - "插件"
  - "Vue"
categories:
  - "插件"
keywords:
description: "vue时间过滤器(moment)"
toc: false
---

## 安装

`npm i moment -s`

## 引入

`import moment from 'moment';`

## 配置

```javascript
Vue.filter("dateFormat", function(dataStr, pattern = "YYYY-MM-DD HH:mm:ss") {
  return moment(dataStr).format(pattern);
});
```

## 使用

```html
<span>发表时间：{{item.add_time | dateFormat('YYYY-MM-DD')}}</span>
//出来是2018-01-10
<span>发表时间：{{item.add_time | dateFormat}}</span> //出来是2018-01-10
12:12:30
```
