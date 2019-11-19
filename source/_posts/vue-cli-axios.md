---
title: axios的使用
date: 2019-11-14 10:57:44
tags:
  - 'Vue-cli'
  - '插件'
categories:
  - '插件'
keywords:
description: 'axios的使用'
toc: false
---

## 安装

```js
npm i axios vue-axios -s
```

## 引用

```js
import axios from 'axios'
import vueAxios from 'vue-axios'
Vue.use(vueAxios, axios)
```

## 配置

```js
axios.defaults.baseURL = 'https://api.example.com' //前缀名
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN //token值
axios.defaults.headers.post['Content-Type'] =
  'application/x-www-form-urlencoded' //格式
```

## 使用

```js
this.axios
    .get("api/getlunbo",{参数，没有可以不写})
    .then(res => {
        if (res.data.status == 0) {
        this.lunboArr = res.data.message;
        } else {
        alert("加载失败");
        }
    });
}
```
---