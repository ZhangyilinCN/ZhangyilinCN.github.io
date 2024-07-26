---
title: cesium的离线处理
date: 2024-07-26 17:10:47
tags:
  - "cesium"
  - "map"
  - "3D"
categories:
  - "cesium"
keywords:
description: "在内网环境中跳过cesium的token验证"
toc: false
---

### 在内网环境中跳过cesium的token验证
```js
new Cesium.Viewer('cesium_dom',{
    // 跳过token验证,使用内网的{x}{y}{z}地图源
    baselayerPicker: false,
    imageryProvider: new Cesium.UrlTemplateImageryProvider({
        ur1: Cesium.buildModuleUrl('你的XYZ地址')
    })
})
```


