---
title: '[Cesium] 개발 팁'
categories:
  - Web
  - JavaScript
tags:
  - CesiumJS
  - JavaScript
  - 3D
date: 2020-04-15 22:04:56
thumbnail: /images/thumbnail/cesium.png
---

## 영상 레이어 추가

Geoserver에 추가된 영상 레이어를 Cesium 지도에 표출 하는 코드입니다.
layers 에는 Geoserver에 있는 레이어의 이름을 넣으면 됩니다.

```js
var imageryLayer = viewer.imageryLayers.addImageryProvider(
  new Cesium.WebMapServiceImageryProvider({
    url: 'http://localhost:8080/geoserver/img/wms',
    layers: 'img:GCOMW1_L2_SMC_20120703',
    parameters: {
      service: 'WMS',
      version: '1.1.0',
      request: 'GetMap',
      styles: '',
      srs: 'EPSG:4326',
      format: 'image/png',
      transparent: 'true',
    },
  })
);
```

## CesiumJS 포인트 그리기

마우스 왼쪽 버튼을 누를 때 포인트 그리기

```js
var ellipsoid = viewer.scene.globe.ellipsoid;

var handler = new Cesium.ScreenSpaceEventHandler(viewer.canvas);

handler.setInputAction(function (event) {
  if (event.position != null) {
    var cartesian = scene.camera.pickEllipsoid(event.position, ellipsoid);
    if (cartesian) {
      var cartographic = Cesium.Cartographic.fromCartesian(cartesian);
      var longitude = Cesium.Math.toDegrees(cartographic.longitude);
      var latitude = Cesium.Math.toDegrees(cartographic.latitude);

      var point = scene.primitives.add(new Cesium.PointPrimitiveCollection());
      point.add({
        position: Cesium.Cartesian3.fromDegrees(longitude, latitude),
        color: Cesium.Color.RED, // default: WHITE
      });
    }
  }
}, Cesium.ScreenSpaceEventType.LEFT_CLICK);
```

## 영상 레이어 추가 시 스타일 지정

영상 레이어 추가와 거의 같지만 styles와 COLORSCALERANGE 파라미터가 추가되었습니다.
styles 에는 Geoserver에 추가된 스타일 이름을 지정하고, COLORSCALERANGE 에는 min, max 값을 지정한다. (COLORSCALERANGE 파라미터는 없어도 됩니다.)

```js
var imageryLayer = viewer.imageryLayers.addImageryProvider(
  new Cesium.WebMapServiceImageryProvider({
    url: 'http://localhost:8080/geoserver/img/wms',
    layers: 'img:GCOMW1_L2_SMC_20120703',
    parameters: {
      service: 'WMS',
      version: '1.1.0',
      request: 'GetMap',
      styles: 'lut_redblue',
      srs: 'EPSG:4326',
      format: 'image/png',
      transparent: 'true',
      COLORSCALERANGE: '0,100',
    },
  })
);
```
