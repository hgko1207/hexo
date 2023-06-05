---
title: '[Openlayers] getGetFeatureInfoUrl 함수 사용'
categories:
  - Programming
  - Language
  - JavaScript
tags:
  - Openlayers
  - JavaScript
  - Map
date: 2020-04-16 10:02:45
thumbnail: /images/thumbnail/openLayers.png
---

Geoserver 에서 필요한 정보를 가져오기 위해 **OpenLayers** 의 `getGetFeatureInfoUrl` 함수를 사용하였습니다.

feature의 정보 중에 GRAY_INDEX라는 컬럼의 정보를 가져와야 합니다.
아래 방식으로 image 형태인 layer 를 구성하였습니다.

```js
var wmsLayer = new ol.layer.Image({
  source: new ol.source.ImageWMS({
    ratio: 1,
    url: 'http://localhost:8080/geoserver/img/wms',
    params: {
      FORMAT: 'image/png',
      VERSION: '1.1.1',
      STYLES: '',
    },
  }),
});
```

`getGetFeatureInfoUrl` 함수를 사용하여 feature 정보를 불러와 표출하였습니다.
아래에서 url 에 요청할 때 Cross-Origin Read Blocking(CORN) 문제가 있어 ajax 대신 XMLHttpRequest 를 사용하였습니다.

```js
var url = wmsLayer.getSource().getGetFeatureInfoUrl([longitude, latitude], view.getResolution(), view.getProjection(), {
  INFO_FORMAT: 'application/json',
  FEATURE_COUNT: 10,
  QUERY_LAYERS: imageLayers,
  LAYERS: imageLayers,
});
if (url) {
  var parser = new ol.format.GeoJSON();

  var xhr = new XMLHttpRequest();
  xhr.onreadystatechange = function () {
    if (xhr.readyState === xhr.DONE) {
      // 요청이 완료되면
      if (xhr.status === 200 || xhr.status === 201) {
        var result = parser.readFeatures(xhr.responseText);
        if (result.length) {
          var info = result[0].get('GRAY_INDEX');
          $('#measurement_text').text(
            'Val: ' + info + ', Lon: ' + longitude.toFixed(3) + ', Lat: ' + latitude.toFixed(3)
          );
        }
      }
    }
  };
  xhr.open('GET', url);
  xhr.send();
}
```
