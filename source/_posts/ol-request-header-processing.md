---
title: ol地图源+token
date: 2024-07-26 17:23:46
tags:
  - "openlayer"
  - "Vue"
categories:
  - "openlayer"
keywords:
description: "请求地图瓦片的时候，在请求头是加token再去请求"
toc: false
---


###请求地图瓦片的时候，在请求头是加token再去请求

```js
    // 初始化地图
      initMapFn () {
      this.$nextTick(() => {
        if (!this.mapInstance) {
          this.mapInstance = new Map({
            //加载控件到地图容器中
            controls: defaultControls({
              zoom: false, //不显示放大缩小按钮
              rotate: false, //不显示指北针控件
            }).extend([new ScaleLine()]), //比例尺
            target: this.$refs.map, //目标容器
            layers: [
              new TileLayer({
                source: this.sourceMaoHeaderFn()
              }),
            ],
            loadTilesWhileAnimating: true, //加载时的动画过度
            interactions: new defaults({
              doubleClickZoom: false,
            }),
            view: new View({
              //视口地图相关配置
              projection: "EPSG:3857", //3857为墨卡托坐标，4326为gps经纬度
              center: this.gisPosTransform1(this.centerCoodinate), //设置默认的视角中心点
              zoom: 4, //缩放级别
              minZoom: 2,
              maxZoom: 8
            }),
          });
        }
      })
    },
    // 给source 添加请求头
    sourceMaoHeaderFn () {
      let source = new XYZ({
        url: process.env.VUE_APP_BASE_API + '/underwater-sound/maps/{z}/{x}/{y}.png',
      })
      source.setTileLoadFunction((tile, src) => {
        const xhr = new XMLHttpRequest();
        xhr.responseType = 'blob';
        xhr.addEventListener('loadend', function (evt) {
          const data = this.response;
          if (data !== undefined) {
            tile.getImage().src = URL.createObjectURL(data);
          } else {
            tile.setState(TileState.ERROR);
          }
        });
        xhr.addEventListener('error', function () {
          tile.setState(TileState.ERROR);
        });
        xhr.open('GET', src);
        xhr.setRequestHeader('Authorization', `Bearer ${this.$store.state.token}`);
        xhr.send();
      });
      return source
    },
```
