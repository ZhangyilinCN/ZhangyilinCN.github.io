---
title: vue时间过滤器(moment)
date: 2019-11-14 10:55:30
tags:
  - 'Vue-cli'
  - '插件'
categories:
  - '插件'
keywords:
description: 'vue时间过滤器(moment)'
toc: false
---

## 安装

``` js
npm i moment -s
```

## 引入

``` js
import moment from 'moment';
```

## 配置

``` js
Vue.filter('dateFormat',function (dataStr,pattern='YYYY-MM-DD HH:mm:ss') {  
  return moment(dataStr).format(pattern)
})
```

## 使用

``` html
<span>发表时间：{{item.add_time | dateFormat('YYYY-MM-DD')}}</span> //出来是2018-01-10
<span>发表时间：{{item.add_time | dateFormat}}</span> //出来是2018-01-10 12:12:30
```



