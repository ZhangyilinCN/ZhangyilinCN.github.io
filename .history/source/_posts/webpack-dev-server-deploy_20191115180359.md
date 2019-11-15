---
title: webpack-dev-server的指令与配置项
date: 2019-11-13 10:31:39
tags:
  - "Webpack"
categories:
  - "Webpack"
keywords:
description: "webpack-dev-server的指令与配置项"
toc: false
---

## 修改项目中的 package.json 来实现自动打开网页，修改端口等操作

![webpack-dev-server-deploy1.jpg](https://i.loli.net/2019/11/15/F8nqhPivLxzod7Y.jpg)

```js
"dev" : "webnpack-dev-server --open" //npm run dev后自动打开网页
"dev" : "webnpack-dev-server --open --port 3000" //npm run dev后自动打开网页并且端口为3000
"dev": "webpack-dev-server --open --port 3000 --contentBase src"//npm run dev后自动打开网页并且端口为3000并且进入的是src下的页面当中，而不是原来的根目录展示页
"dev" : "webnpack-dev-server --hot" //npm run dev开启热更新功能(不开启的话，每次提交代码后，会重新生成一份新的文件，而开启热更新功能，只是对原来的文件进行修改，并且网页不会进行重载刷新)
```

---

## 在 webpack.config.js 中进行操作(不推荐)

![webpack-dev-server-deploy2.jpg](https://i.loli.net/2019/11/15/XFyfKik3YbzhvM1.jpg)

---
