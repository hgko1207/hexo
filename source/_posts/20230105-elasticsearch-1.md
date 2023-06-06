---
title: '[Elasticsearch] 윈도우에 설치 및 실행 방법(7.X 버전)'
categories:
  - Programming
  - DB
  - Elasticsearch
tags:
  - Elasticsearch
  - 엘라스틱서치
  - Database
  - 윈도우
date: 2023-01-05 15:50:51
thumbnail: /images/thumbnail/elasticsearch.png
---

## Elasticsearch(엘라스틱서치): 분산 검색 엔진

> 루씬 기반의 검색 엔진이다. HTTP 웹 인터페이스와 스키마에서 자유로운 JSON 문서와 함께 분산 멀티테넌트 지원 전문 검색 엔진을 제공한다. 일래스틱서치는 자바로 개발되어 있으며 아파치 라이선스 조항에 의거하여 오픈 소스로 출시되어 있다.
> [위키백과](https://ko.wikipedia.org/wiki/%EC%9D%BC%EB%9E%98%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98)

엘라스틱서치는 모든 레코드를 JSON 도큐먼트 형태로 입력하고 관리하고 있으며, 일반적인 데이터베이스와 마찬가지로, 쿼리한 결과에 대해 일치하는 원본 도큐먼트를 반환합니다. 또한 엘라스틱서치는 텍스트 외에도 숫자, 날짜, IP 주소, 지리 정보 등 다양한 데이터 타입에 대해 최적화되어 있습니다.

또한 엘라스틱서치는 사용자의 모든 입력을 REST API 형태로 받아들이기 때문에 별도의 드라이버 라이브러리가 없더라도 웹 브라우저나 curl 명령어를 이용해 기능을 활용할 수 있습니다.

## 개요

윈도우 환경에서 **Elasticsearch 7.X** 버전을 설치 및 실행하는 방법에 대해 알아보겠습니다.
윈도우에서는 파일을 다운로드하고 압축을 푼 다음 실행 파일을 실행하면 엘라스틱서치가 설치되는 구조입니다.

## 다운로드

먼저 설치를 위해 공식홈페이지로 이동합니다.

https://www.elastic.co/kr/downloads/elasticsearch

현재 기준으로 8.5.3 버전이 최신입니다. 7.X 버전을 설치하므로 오른쪽의 **View pas releases**를 클릭합니다.

![](/images/elastic/elasticsearch/2.png)

7.X 버전 중 원하는 버전을 선택하고 **Download** 버튼을 클릭합니다.

![](/images/elastic/elasticsearch/3.png)

버전을 확인하고 **WINDOWS** 링크를 클릭하여 다운로드 받습니다.

![](/images/elastic/elasticsearch/4.png)

## 설치하기

다운로드가 완료되면 zip 파일이 나오는데 압축을 해제합니다. 이 글에서는 윈도우 C 드라이브 밑에 **elasticsearch-7.17.8** 이라는 폴더에 압축을 해제했습니다.

압축을 해제하면 다음과 같은 폴더 구조가 나옵니다.

![](/images/elastic/elasticsearch/6.png)

bin 폴더에는 실행 파일과 플러그인 설치나 키 생성 등의 실행 작업을 위한 파일들이 있습니다. config 폴더에는 설정 파일(elasticsearch.yml)을 포함하여 설정에 관한 파일들이 있습니다.

## 실행하기

엘라스틱서치를 실행해봅니다. bin 폴더에 있는 **elasticsearch.bat** 파일을 실행하면 됩니다. 윈도우에서 기본으로 제공하는 명령 프롬프트(CMD)을 실행하고 다음 명령어를 실행합니다.

```sh
C:\elasticsearch-7.17.8> .\bin\elasticsearch.bat
```

기본적으로 포그라운드로 실행되고 로그를 출력합니다. 백그라운드로 실행을 원할 경우 실행 명령문 뒤에 `-d`를 추가하면 됩니다.

## 확인하기

엘라스틱서치를 실행하고 동작 여부를 확인하기 위해 **curl**이라는 툴을 이용합니다. 윈도우를 설치하면 기본으로 설치되어 있습니다. 윈도우 bat 파일의 경우 기본적으로 백그라운드 실행이 안 되기 때문에 명령 프롬프트를 하나 더 실행하고 다음 명령을 실행합니다.

```sh
C:\elasticsearch-7.17.8> curl -X GET "localhost:9200/?pretty"
{
  "name" : "DESKTOP-08OF09U",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "Qd8gx2FzSnyFb4zCvx9C6Q",
  "version" : {
    "number" : "7.17.8",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "120eabe1c8a0cb2ae87cffc109a5b65d213e9df1",
    "build_date" : "2022-12-02T17:33:09.727072865Z",
    "build_snapshot" : false,
    "lucene_version" : "8.11.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

엘라스틱서치는 기본적으로 9200 포트를 사용하는데, localhost:9200 주소에 GET 메소드 요청을 해서 응답이 있다면 엘라스틱서치가 정상적으로 실행 된 것입니다. 응답 결과를 JSON 형태로 보여주는데, URL 뒤에 `?pretty`를 추가하면 가독성 좋은 형태로 결과를 보여줍니다.

브라우저에서 http://localhost:9200 으로 접속해서 확인 할 수 있습니다.

![](/images/elastic/elasticsearch/7.png)
