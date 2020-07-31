---
title: DPPDB
categories:
  - Satellite
tags:
  - Satellite
  - DPPDB
  - NITF
date: 2020-04-14 09:39:41
thumbnail: /images/thumbnail/satellite.png
---

# Digital Point Positioning Database

**네이버 백과사전**

> 정밀영상위치제공 지형정보로서 미(美) 국가영상지도국(NIMA)이 1970년대 베트남전 중 미 공군의 B-52와 F-111에서 정밀항법 유도무기를 사용하기 위해 개발했다가 1995년 IT 발달에 따라 디지털로 전환시켰습니다. 3차원 지형데이터에 각종 건물 등 지상 구조물 데이터를 통합해 매우 정밀한 위치정보를 제공합니다. 이 데이터와 미군용 GPS를 결합하면 수십km 밖에서도 미사일 등 유도 무기를 1m의 오차로 공격할 수 있습니다.

DPPDB는 <span style="color:#2e75b6">**스테레오 이미지 쌍 및 관련 보조 데이터의 모음**</span>으로, 이미지에서 식별할 수 있는 모든 점 또는 특징에 대한 정확한 위치 데이터를 신속하게 확인할 수 있는 기능을 제공합니다. 이 데이터는 스테레오 이미지를 분할, 방사 보정, 합리적인 다항식 구성 및 압축 등의 추가 처리를 함으로써 얻을 수 있습니다. 일반적으로 1도 면적(60 x 60 NM)을 커버하며 NITF 파일로 제공됩니다.

참고로 DPPDB는 NITF(National Imagery Transmission Format ) 2.0 사양의 제품입니다.

DPPDB 제품은 세 가지 주요 구성 요소로 구성된 디지털 제품입니다.

**1. imagery support data** : Master Product File(MPF)
**2. a map graphic for reference(참고 용 지도)** : CADRG 프레임 파일
**3. stereo imagery(입체 영상)** : 전체 해상도 및 Overview 이미지 파일

## NITF 란

<span style="color:#2e75b6">**National Imagery Transmission Format Standard**</span> (국가 영상정보 전송 포맷 표준)

NITF는 공중에서 영상을 획득하는 플랫폼들로부터 얻어진 원본 영상을 기반으로 **영상, 서브-영상(sub-images), 그래픽, 심볼, 텍스트 뿐 아니라 영상과 관련된 정보**를 담을 수 있는 하나의 패키지(package)로서 2차 디지털 영상(secondary digital imagery)의 배포 또는 유통을 지원하기 위한 포맷입니다. 따라서 단순히 영상 자체만을 저장하는 일반 영상 포맷과 차별화됩니다.

NITF에 대한 개발은 1987년 미국 정부에 의하여 시작되었으며, 1991년 미국 국방부(DoD) 내에서 영상 파일에 대한 표준인 MIL-STD-2500B로 지정되었으며, 현재 MIL-STD-2500C로 발전되었습니다. NITF는 영상유통포맷의 최초 개발로 1989년 NITF 1.1 발표 이후, 1991년 국방부 표준으로 지정되면서 이름을 NITFS(National Imagery Transmission Format Standard)로 개명하게 되었습니다.

## DPPDB 구조

DPPDB 제품 파일은 아래 그림과 같이 순차적으로 배열됩니다. 첫 번째 파일은 MPF(Master Product File)이며 DPPDB 및 참조 그래픽에 대한 정보를 제공하는 수많은 서브 헤더 파일이 있습니다. MPF 다음에는 참조 그래픽 프레임을 구성하는 파일이 있습니다. DPPDB에 포함 된 나머지 파일은 이미지 파일입니다.

<img width="90%" src="/images/dppdb/1.png" alt="" title="" >

### 1) MPF (Master Product File)

정확도, 세그먼트간 이격점 데이터, 진단점, 불량 지역 정보, 풋 프린트 및 이미지 파일과 참조 그래픽에 대한 정보와 같은 보조 데이터를 포함하고 있습니다. 그림은 기본 구성 요소만 보여주는 MPF의 파일 구조입니다.

<img width="80%" src="/images/dppdb/2.png" alt="" title="" >

### 2) Reference Graphic files

MPF 다음으로 구성된 그래픽 파일은 사용자가 지정한 영역에 대한 디지털 맵을 제공합니다. 다양한 벡터 오버레이를 표시하고 대상의 대략적인 위치를 식별하기 위해 사용됩니다. DPPDB 제품의 사각형보다 약간 큰 영역을 포함하는 8 비트 컬러 래스터 이미지입니다. 그래픽의 소스는 CADRG(Compressed ARC Digitized Raster Graphics) 데이터입니다.

<img width="80%" src="/images/dppdb/3.png" alt="" title="" >

### 3) Image Files

이미지 파일은 전체 해상도 및 overview(전체 해상도 이미지의 1/8x 또는 1/4x 축소 된 이미지) 세그먼트 이미지 세트로 구성되어 있습니다.
각 전체 해상도 및 overview 이미지 파일에는 해당 이미지에 대한 정보 및 함수 계수도 포함되어 있습니다.
이미지 파일은 4 개의 그룹 (왼쪽과 오른쪽의 전체 해상도 및 overview 이미지)으로 구성되며 각 그룹은 단일 DPPDB 모델에 포함됩니다.
아래 그림은 전체 해상도 및 overview 이미지 세그먼트의 파일 구조를 보여줍니다.

<img width="80%" src="/images/dppdb/4.png" alt="DPPDB Overview Segment Image File" title="DPPDB Overview Segment Image File" >

<img width="80%" src="/images/dppdb/5.png" alt="DPPDB Full Resolution Segment Image File" title="DPPDB Full Resolution Segment Image File" >

## DPPDB 생성

NITF 영상 및 위치결정자료 생성 절차를 설명합니다.

<img width="100%" src="/images/dppdb/6.png" alt="" title="" >

#### 세그먼트 분할

입체시 영상에 대한 세그먼트 이미지를 분할합니다.

#### 불량지역 생성

불량지역 생성 기능을 통해 영상에서 유효하지 않는 영역을 식별 또는 추가합니다.
불량지역은 구름으로 관측이 어려운 지역이나, 바다, 호수와 같이 수계지역을 의미합니다.

#### 정확도 평가

각 세그먼트간 측정오차, 절대정확도, 상대정확도를 계산합니다.

#### 세그먼트간 이격점 생성

각 세그먼트 간 중복지역에서 특징점을 추출하고, 매칭을 통해 자동으로 점을 생성합니다.

## 참고문헌

**미국 군사규격서**

1. MIL-PRF-89034 : Digital Point Positioning Data Base(DPPDB)
2. MIL-STD-2500A: National Imagery Transmission Format(NITF) for NITFS
3. MIL-STD-2301A : Computer Graphics Metafile(CGM) Implementation Standard for the National Imagery Transmission Format Standard(NITFS)
4. MIL-PRF-89038 : Compressed ARC Digitized Raster Graphics(CARRG)
5. MIL-PRF-89041: Controlled Image Base(CIB)

**NITF**

1. NITFS : https://terms.naver.com/entry.nhn?docId=3480012&cid=58439&categoryId=58439
2. NITF/NSIF Background : https://www.harrisgeospatial.com/docs/BackgroundNITFNSIFFormat.html#Main
