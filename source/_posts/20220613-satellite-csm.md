---
title: CSM
categories:
  - IT
  - Satellite
tags:
  - Satellite
  - CSM
  - SensorModel
date: 2022-06-13 20:01:13
thumbnail: /images/thumbnail/satellite.png
---

# Community Sensor Model(CSM)

NGA(국가지리정보국, National Geospatial Intelligence Agency)에서는 센서 모델을 동일한 방법으로 접근할 필요성에 따라 CSM(Community Sensor Model)을 개발하여 통일된 인터페이스를 제공합니다.

CSM은 현재 운용되고 있거나 추후 운용이 예상되는 <span style="color:#2e75b6">**위성 센서의 모델, 알고리즘, 소프트웨어에 대한 개발, 시험, 평가를 지원하는 플러그인 소프트웨어 라이브러리**</span>입니다.

CSM은 WGS84 타원체의 ECEF(Earth Centered Earth Fixed) 좌표계를 사용하고 있습니다. 따라서 모든 함수에서 지상 좌표의 입력과 출력 값은 ECEF 좌표로 구성해야 합니다.

**CSM 사용 소프트웨어**

- ENVI, ERDAS, SOCET GXP 등

## CSM 장단점

### 장점

- 센서모델링을 수행하기 위한 소프트웨어 개발 시 모델링에 사용되는 행렬과 반복 알고리즘만 구현하면 되므로 <span style="color:#2e75b6">**소프트웨어의 개발비용 절감효과가 큽니다**.</span>
- 새로운 센서나 모델들이 개발되면, 센서모델에 대한 플러그인만 개발하여 배포하고 응용 소프트웨어에서 호출하여 모델링을 수행하므로 <span style="color:#2e75b6">**센서모델의 확장성이 뛰어납니다**.</span>

### 단점

- ECEF 좌표계 사용을 위해 경우에 따라 중복된 좌표 변환 작업을 수행하게 되어 효율성이 다소 저하됩니다.

## CSM Context Diagram

<img width="80%" src="/images/satellite/csm.png" alt="" title="" >

## CSM API

CSM은 CSMPlugin 클래스와 CSMSensorModel 클래스로 구분됩니다.

### CSMPlugin 클래스

- 플러그인 제조사, 배포 일자와 같은 기본적인 정보를 제공합니다.
- 센서 모델 선택, Image Support Data(ISD) 처리, 센서 모델 생성과 같은 기능을 하는 함수들로 구성됩니다.

### SMSensorModel 클래스

- 영상좌표에서 지상좌표의 상호간 변환, 편미분, 공분산, 파라미터 설정 등 사진 측량에 필요한 함수들로 구성됩니다.

## Sensor Model

<img width="95%" src="/images/satellite/sensorModel.png" alt="" title="" >

## Download

Github Page - Community Sensor Model API

[![](/images/satellite/usgs-csm.png)](https://github.com/USGS-Astrogeology/csm/)

## Build

1. 다운로드가 완료되면 압축을 풀어줍니다.
2. 빌드에 필요한 [CMake](https://cmake.org/download/)를 설치합니다.
3. 설치가 완료되면 CMake gui를 실행합니다.
4. 빌드를 하기 전 CSM 폴더 안에 build 폴더를 생성합니다.
5. CMake gui에서 Source 및 Build(생성한 build 폴더 경로) 경로를 입력하고 **Configure** 버튼을 클릭합니다.
6. 오류 없이 설정이 완료되면 **Generate** 버튼을 클릭합니다.
7. CMake Build가 완료되면 다음과 같이 프로젝트가 생성됩니다.

<img width="75%" src="/images/satellite/csm-build.png" alt="" title="" >

8. 프로젝트를 실행하여 빌드를 실행하면 csmapi.dll, csmapi.lib 파일이 생성됩니다.

CSM 은 공통 인터페이스를 제공하기 때문에 csmapi.dll, csmapi.lib, 헤더 파일을 참조 및 로드하여 위성에 대한 센서 모델을 구현합니다. 기본적으로 Plugin, RasterGM을 상속받아 구현합니다.
