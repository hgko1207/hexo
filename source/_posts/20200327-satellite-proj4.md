---
title: PROJ.4 란?
categories:
  - IT
  - Satellite
tags:
  - Satellite
  - PROJ.4
  - Coordinate System
  - EPSG
date: 2020-03-27 09:38:26
thumbnail: /images/thumbnail/satellite.png
---

## PROJ.4 란?

- ​다양한 좌표계 변환을 제공하는 라이브러리
- 자유롭게 인자를 지정하여 표준이 아닌 좌표계 간도 변환 가능
- USGS의 Gerald Evenden에 의해 만들어진 오픈소스 라이브러리
- 현재 OSGeo 프로젝트 중 하나이며 MIT 라이선스
- GeoServer, OpenLayers, PostGIS, QGIS, GDAL, OGR, GeoTools 등 엄청나게 많은 프로그램에서 사용 중
- C, C++, JAVA, Javascript 등 다양한 언어로 포팅 되어 있음​

## 경위도 좌표계(WGS84)

- GPS가 사용하는 좌표계
- EPSG:4326
- +proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs
- https://epsg.io/4326

## 구글 좌표계(Mercator)

- EPSG:3857, EPSG:900913
- +proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +no_defs
- https://epsg.io/3857

## TM(Transverse Mercator)

- 국토지리정보원 기준 좌표계
- +proj=tmerc +lat_0=38 +lon_0=127 +k=1 +x_0=200000 +y_0=600000 +ellps=GRS80 +units=m +no_defs

## UTM(Universal Transverse Mercator)

- 전 세계를 6도 단위로 나누는 표준적인 TM으로 군사지도에서 많이 사용

1. UTM52N: 경도 120 ~ 126도 사이에서 사용

   - EPSG:32652
   - +proj=utm +zone=52 +ellps=WGS84 +datum=WGS84 +units=m +no_defs
   - https://epsg.io/32652

2. UTM51N: 경도 126 ~ 132도 사이에서 사용

   - EPSG:32651
   - +proj=utm +zone=51 +ellps=WGS84 +datum=WGS84 +units=m +no_defs
   - https://epsg.io/32651

## Polar Stereographic

- 기상청 북반구 표현에 사용
- +proj=stere +lat_0=90 +lat_ts=90 +lon_0=0 +k=0.994 +x_0=2000000 +y_0=2000000 +ellps=WGS84 +datum=WGS84 +units=m +no_defs
- https://spatialreference.org/ref/epsg/wgs-84-ups-north/

## 참고

- [epsg.io](http://epsg.io/)
- [한국 주요 좌표계 EPSG코드 및 proj4 인자 정리](https://www.osgeo.kr/17)
