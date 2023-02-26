---
title: '[Kibana] 사용 방법'
categories:
  - Server
  - Elasticsearch
tags:
  - Kibana
  - 키바나
  - 윈도우
date: 2023-01-06 16:41:51
thumbnail: /images/thumbnail/elasticsearch.png
---

**키바나(Kibana)** 사용 방법에 대해 알아보겠습니다.

## 운영환경

- Windows
- Kibana Version: 7.17.8

키바나를 실행합니다. 키바나는 기본적으로 5601 포트를 사용하는데, 웹 브라우저를 열고 http://localhost:5601 주소를 입력합니다.

## 서버 상태 확인

키바나의 서버 상태는 http://localhost:5601/status 에서 확인 할 수 있습니다.

![](/images/elastic/kibana/6.png)

## 키바나 콘솔 사용법

키바나 Dev Tools에 있는 콘솔을 이용해 엘라스틱서치 REST API를 호출합니다. 키바나 왼쪽 상단의 토글 메뉴를 클릭하면 키바나 메뉴를 확인할 수 있는데 **Management -> Dev Tools**를 선택하면 됩니다.

![](/images/elastic/kibana/7.png)

왼쪽 입력창에서 엘라스틱서치에서 제공하는 REST API를 입력하고 실행 버튼을 누르면 오른쪽 출력창에서 HTTP의 응답을 확인할 수 있습니다. 또한 키바나 콘솔은 엘라스틱서치 API 자동 완성 기능이 지원됩니다.

## 샘플 데이터 불러오기

엘라스틱 스택은 세 가지 샘플 데이터를 기본으로 제공합니다. 키바나에서 아주 쉽게 가능합니다. 샘플 데이터를 불러와서 검색 테스트를 할 수 있습니다.

키바나의 홈 화면에서 **Try sample data** 링크를 클릭합니다.

![](/images/elastic/kibana/8.png)

샘플 데이터를 추가할 수 있는 화면입니다. 총 3개의 심플 데이터(Sample eCommerce orders, Sample flight data, Sample web logs)가 있고, 각 샘플 데이터마다 **Add data** 버튼을 클릭해서 샘플을 추가할 수 있습니다.

![](/images/elastic/kibana/9.png)

샘플 데이터를 추가하면 키바나의 Visualize(시각화)와 Daashboard(대시보드) 등에도 샘플들이 함께 추가됩니다.
