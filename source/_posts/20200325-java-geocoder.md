---
title: '[java] Geocoder을 이용해 주소를 위도/경도로 변환하기'
categories:
  - Programming
  - Java
tags:
  - Java
  - Geocoder
  - 자바스크립트
  - 위도
  - 경도
date: 2020-03-25 10:18:14
thumbnail: /images/thumbnail/java.png
---

Geocoding 이란 주소를 위도, 경도로 변환해주는 Google 에서 제공하는 API 입니다.

링크 : [지오코딩이란?](https://developers.google.com/maps/documentation/geocoding/start#Geocoding)

처음엔 `HttpURLConnection` 으로 접속해서 `InputStreamReader` 로 읽은 후 JSON 으로 파싱하게 만들었는데 해외 사이트에 geocoder 라이브러리를 이용하여 받아오는 예제가 있었다. 어쨌든 더 편리하고 깔끔하게 해결되었습니다.

### Geocoder Maven dependency

```maven
<dependency>
  <groupId>com.google.code.geocoder-java</groupId>
  <artifactId>geocoder-java</artifactId>
  <version>0.16</version>
</dependency>
```

### Method

```java
public static Float[] findGeoPoint(String location) {

    if (location == null)
      return null;

    // setAddress : 변환하려는 주소 (경기도 성남시 분당구 등)
    // setLanguate : 인코딩 설정
    GeocoderRequest geocoderRequest = newGeocoderRequestBuilder().setAddress(location).setLanguage("ko").getGeocoderRequest();

    try {
        Geocoder geocoder = new Geocoder();
        GeocodeResponse geocoderResponse = geocoder.geocode(geocoderRequest);

        if (geocoderResponse.getStatus() == GeocoderStatus.OK & !geocoderResponse.getResults().isEmpty()) {
            GeocoderResult geocoderResult=geocoderResponse.getResults().iterator().next();
            LatLng latitudeLongitude = geocoderResult.getGeometry().getLocation();

            Float[] coords = new Float[2];
            coords[0] = latitudeLongitude.getLat().floatValue();
            coords[1] = latitudeLongitude.getLng().floatValue();
            ​return coords;
        }
    } catch (IOException ex) {
        ex.printStackTrace();
    }
    return null;
}
```

`latitudeLongitude.getLat().floatValue();` 이 부분은 floart 형이 아닌 toString() 으로도 가능합니다.

### 테스트

```java
String location = "대전광역시 유성구 궁동";
Float[] coords = CommonUtil.findGeoPoint(location);

System.out.println(location + ": " + coords[0] + ", " + coords[1]);
```

### 결과

```java
대전광역시 유성구 궁동 : 36.366701, 127.344510
```
