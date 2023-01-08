---
title: 'WGS84 - 도분초 변환'
categories:
  - IT
  - Satellite
tags:
  - WGS84
  - 도분초
date: 2022-11-03 16:58:10
thumbnail: /images/thumbnail/satellite.png
---

> 세계 지구 좌표 시스템(World Geodetic System, WGS) 1984년에 제정된 범 지구적 측위 시스템으로 지도학, 측지학, 항법에 많이 사용된다. GPS측량 시 WGS84 타원체를 사용한다.
> 통칭 및 약칭은 WGS 84 (aka WGS 1984, EPSG:4326, WGS84)라고 부르며, 2004년에 마지막으로 개정되었다. 이전에 쓰던 초안으로 WGS 72, WGS 66, 그리고 WGS 60이 있다.
> [위키백과](https://ko.wikipedia.org/wiki/%EC%84%B8%EA%B3%84_%EC%A7%80%EA%B5%AC_%EC%A2%8C%ED%91%9C_%EC%8B%9C%EC%8A%A4%ED%85%9C)

- 3735.0079 는 위도로서 37도 35.0079분을 뜻합니다. 도(degree) 단위로 환산시, 대략 37.5도가 됩니다.
- 12701.6446 은 경도로서 127도 1.6446분을 뜻합니다. 도(degree) 단위로 환산시, 대략 127.0도가 됩니다.
- DDMM.MMMM , DDDMM.MMMM 형식입니다.

일반적으로 WGS84 좌표라고 하면서 37.494961 , 127.030380 이런식으로 이용하면
그냥 37점494961도 라고 읽으면 됩니다.

## 도분초 변환

도를 도 분 초로 변환하는 자바 소스 코드입니다.

```java
float lat = 37.494961;
float lon = 127.030380;

lat_do = (int)lat;
lat_min = (lat - (int)lat) * 60;
lat_sec = ((lat - (int)lat) * 60 - lat_min) * 60;

lon_do = (int)lon;
lon_min = (lon - (int)lon) * 60;
lon_sec = ((lon - (int)lon) * 60 - lon_min) * 60;
```
