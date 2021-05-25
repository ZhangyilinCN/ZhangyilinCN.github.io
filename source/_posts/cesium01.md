---
title: vue中cesium初始化
date: 2021-05-25 16:58:24
tags:
  - "cesium"
  - "map"
  - "3D"
categories:
  - "cesium"
keywords:
description: "初步使用cesium创建3d地球"
toc: false
---

## 首先下载 `cesium` 包放置到 vue 的 public 文件夹下，然后在 public 中的 `index.html` 中进行引用

![cesium1.png](https://i.loli.net/2021/05/25/ny3q76VtbCiwERc.png)

---

## 然后在页面中进行初始化

```html
<template>
  <div class="wrap">
    <div id="map"></div>
  </div>
</template>
<script>
  export default {
    data() {
      window.viewer = null; //挂载到全局
      return {};
    },
    mounted() {
      this.createballFn();
    },
    methods: {
      createballFn() {
        Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
          90,
          -20,
          110,
          90
        ); //设置地球初始定位的位置
        Cesium.Ion.defaultAccessToken =
          "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI1YzRhOGE5YS0yOWM3LTQ4NWYtOWMwYi0zNjU5OTJjZjA1ZjYiLCJpZCI6NTQxMzUsImlhdCI6MTYxOTU5Mzg3Mn0.gma-xUFLKsltb3ijWbpUh6E9ca1rGcg9Oh_hOUu2ZTc"; //你的token
        viewer = new Cesium.Viewer("map", {
          animation: true, //是否创建动画小器件，左下角仪表
          shouldAnimate: true,
          baseLayerPicker: false, //是否显示图层选择器
          fullscreenButton: false, //是否显示全屏按钮
          geocoder: false, //是否显示geocoder小器件，右上角查询按钮
          homeButton: true, //是否显示Home按钮
          infoBox: false, //是否显示信息框
          sceneModePicker: false, //是否显示3D/2D选择器
          selectionIndicator: false, //是否显示选取指示器组件
          timeline: true, //是否显示时间轴
          navigationHelpButton: false, //是否显示右上角的帮助按钮
          scene3DOnly: false, //如果设置为true，则所有几何图形以3D模式绘制以节约GPU资源
        });
        //隐藏底部logo
        viewer._cesiumWidget._creditContainer.style.display = "none";
        //移除默认的双击事件
        viewer.cesiumWidget.screenSpaceEventHandler.removeInputAction(
          Cesium.ScreenSpaceEventType.LEFT_DOUBLE_CLICK
        );
      },
    },
  };
</script>
<style scoped lang="scss"></style>
```

---

## 最后就可以在页面上显示出来了

![cesium2.png](https://i.loli.net/2021/05/25/cbF5JTe3mdWKOZC.png)
