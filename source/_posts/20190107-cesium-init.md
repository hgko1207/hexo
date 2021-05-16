---
title: '[Cesium] 초기 설정'
categories:
  - Web
  - Cesium
tags:
  - Web
  - JavaScript
  - CesiumJS
  - 3D
  - Map
date: 2019-01-07 11:37:21
thumbnail: /images/thumbnail/cesium.png
---

GIS 관련 프로젝트를 하다보니 오픈소스인 CesiumJS 나 Openlayers 라이브러리를 사용하게 되었습니다. 최근에는 2D, 3D 모드가 가능한 CesiumJS 를 주로 사용하게 되었습니다.

## Cesium 이란?

- 순수 웹 기불을 이용한 3D Globe 엔진
- WebGL 기반
- 다양한 배경 영상/지도 기본 제공
- 3D / 2.5D / 2D 모드 지원 -> Openlayers3에 통합
- 카메라 움직임 추적, 시간 시뮬레이션 등 다양한 기능 제공

Cesium 을 시작할 때 초기 설정이 복잡합니다. 아래 두 개의 링크를 따라가서 따라하면 쉽게 할 수 있습니다. 하지만 웹에서 커스터마이징을 하기 위해 아래 코드 처럼 Cesium 에서 지원하는 기본적인 기능들을 끄고 지도만 보이도록 설정해야 합니다.
API들은 문서나 인터넷 검색으로 찾아봅시다.

[![](/images/cesium-up-and-running.png)](https://cesiumjs.org/tutorials/cesium-up-and-running/)

[![](/images/cesium-demos.png)](https://cesiumjs.org/demos/)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <!-- Include the CesiumJS JavaScript and CSS files -->
  <script src="https://cesium.com/downloads/cesiumjs/releases/1.81/Build/Cesium/Cesium.js"></script>
  <link href="https://cesium.com/downloads/cesiumjs/releases/1.81/Build/Cesium/Widgets/widgets.css" rel="stylesheet">
</head>
<body>
  <div id="cesiumContainer"></div>

  <script>
    const viewer = new Cesium.Viewer('cesiumContainer', {
      imageryProvider: new Cesium.WebMapServiceImageryProvider({
        url: 'http://localhost:8080/geoserver/gwc/service/wms',
        layers: 'osm:osm',
        parameters: {
          service: 'WMS',
          version: '1.1.1',
          request: 'GetMap',
          layers: 'osm:osm',
          srs: 'EPSG:3857',
          crs: 'EPSG:3857',
          format: 'image/png',
          tranparent: true,
          tiled: true,
        },
        tilingScheme: new Cesium.WebMercatorTilingScheme(),
      }),
      animation: false,
      baseLayerPicker: false,
      fullscreenButton: false,
      vrButton: false,
      geocoder: false,
      homeButton: false,
      infoBox: false,
      sceneModePicker: false,
      selectionIndicator: false,
      timeline: false,
      navigationHelpButton: false,
      projectionPicker: false,
      selectedEntity: false,
      trackedEntity: false,
      clockTrackedDataSource: false,
    });

    const scene = viewer.scene;
    const camera = viewer.camera;
    const handler = new Cesium.ScreenSpaceEventHandler(viewer.canvas);
    const ellipsoid = scene.globe.ellipsoid;
  </script>
 </div>
</body>
</html>
```

위의 예제는 미리 구축된 Geoserver 를 베이스 맵으로 설정하였습니다. Geoserver 가 구축되지 않았다면 Cesium 에서 제공되는 기본 Provider 를 사용하면 됩니다.

```html
// 예시
<script>
  const viewer = new Cesium.Viewer('cesiumContainer', {
    terrainProvider: Cesium.createWorldTerrain(), // 기본 지도를 지형지도로 셋팅
  });
</script>
```

## 참고

- https://cesium.com/docs/tutorials/quick-start/
