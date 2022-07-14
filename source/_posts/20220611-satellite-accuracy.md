---
title: 지리공간자료 정확도
categories:
  - IT
  - Satellite
tags:
  - Position Accuracy
  - Accuracy
  - Error
  - Satellite
date: 2022-06-11 22:29:25
thumbnail: /images/thumbnail/satellite.png
---

## 지리공간자료 정확도의 형태

- Spatial (position, geometry, topology)
- Attributional (correctness of attributes)
- Spectral (band depth)
- Temporal (appropriate date)
- Radiometric (capture piece of electromagnetic spectrum)

## 지리공간자료

- 기하보정된 위성영상
- 정사영상(Orthoimagery)
- DTM(Digital Terrain Model)
- DEM(Digital Elevation Model)
- DSM(Digital Surface Model)
- TIN(Triangulated Irregular Network)

## 정확도(Accuracy)

과학, 산업, 공업, 통계학 분야에서 재거나 계산된 양이 실제 값과 얼만큼 가까운지를 나타내는 기준이며, 관측의 정교성이나 균질성과는 무관합니다.

측정에 의해 얻은 최고 추정 값과 측정 된 수량의 "참"값에 대한 근접성입니다.

## 위치 정확도(Position Accuracy)

두 지리 공간 레이어 사이 또는 지리 공간 레이어와 현실 사이의 위치 차이를 나타내는 정량화 가능한 값 입니다.

## Root Mean Square Error(RMSE)

- 평균 제곱근 편차(Root Mean Square Deviation; **RMSD**) 또는 평균 제곱근 오차(Root Mean Square Error; **RMSE**)는 추정 값 또는 모델이 예측한 값과 실제 환경에서 관찰되는 값의 차이를 다룰 때 흔히 사용하는 측도이다. 정밀도를 표현하는데 적합합니다. 각각의 차이 값은 잔차(residual)라고도 하며, 평균 제곱근 편차는 잔차들을 하나의 측도로 종합할 때 사용됩니다.
- 잔차 값 간의 분산을 통계적으로 측정 한 것 입니다.

## Standard Deviation(StDev) : 표준 편차

- 자료의 산포도를 나타내는 수치로, 분산의 양의 제곱근으로 정의됩다.

## Circular Error(CE) : 원형 오차

- CE는 X, Y 모두에 대한 2차원 오차를 측정합니다.
- CE90, CE95, CE99 형식으로 표현합니다.
  - 원형 분포에서 모든 오차가 n%를 초과하지 않는 반경 오차
  - 예) CE 90 = 2미터인 경우 : 오차들이 반지름 2미터인 원 안에 있을 확률이 90%라는 것을 나타낸다.

## Linear Error(LE) : 선형 오차

- Z축(고도)에 대한 오차 측정을 합니다.
- 측정된 값과 실제 또는 알려진 값과의 차이를 계산합니다.
- 지형의 수직 정확도 측정(예: DEM 또는 TIN)
- LE90, LE95, LE99 형식으로 표현합니다.
  - 예) LE 95 = 10m인 경우: 오차들이 10 미터 내에 있을 확률이 90%라는 것을 나타낸다.

## Circular Error Probable(CEP)

- **Circular Error Probability** 또는 **Circular Error Probable**, 원형 공산 오차 라고 하며 탄도학 에서 무장의 정밀도를 측정하는 단위.
- CEP는 폭탄 등이 투하되었을 경우, 그 중의 반수가 명중하는 원의 반경을 가리킵니다. 즉 10발 공격했을 때 5발이 들어가는 원을 그렸을 때 그 반경이 5m이라고 하면 CEP는 5m라고 합니다.
- 2차원의 수평방향 성분에 대해 50%의 원형 확률 오차(CEP)의 수치는 원의 반경과 같으며, 측점들의 각각의 계산 값에 포함되는 잔차들 중 50%는 이 원안에 들어오고 나머지는 원 밖에 존재합니다.
- 항해시의 위치정밀도 측정치로, 실제 수평자표에서 오차 타원에서 그 반경을 나타냅니다. 이 값은 현재 위치가 실제 위치에 있을 확률이 50%임을 나타냅니다.
- 실제위치를 중심으로 한 위치추정값의 50%를 함유하는 원의 반경 수치입니다.
- CE50 형식과 같습니다.

## 참고자료

- [GPS 기초](https://www.gps.re.kr/outline/outline_17.asp)
- [GCP 용어정리](https://m.blog.naver.com/PostView.nhn?blogId=pig9456&logNo=191149079&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
- [Introduction to GPS](http://introgps.uga.edu/course/CEP.html)
