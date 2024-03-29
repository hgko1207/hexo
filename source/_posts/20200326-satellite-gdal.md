---
title: Gdal 사용 방법
categories:
  - IT
  - Satellite
tags:
  - Satellite
  - Gdal
  - Coordinate System
  - Library
date: 2020-03-26 11:07:02
thumbnail: /images/thumbnail/satellite.png
---

**GDAL** 은 래스터 및 벡터 지리 공간 데이터를 조작할 수 있는 오픈 소스 라이브러리다.

- 라이브러리로서 지원되는 모든 형식의 호출 응용 프로그램에 단일 추상 데이터 모델을 제공한다.
- 데이터 변환 및 처리를 위한 다양한 명령 행 인터페이스 유틸리티가 제공된다.
- Windows, Linux 및 MacOS 에서 사용 가능하다.

## 1. gdalinfo (http://www.gdal.org/gdalinfo.html)

- GDAL 이 지원하는 영상 정보를 확인한다.

```shell
gdalinfo test.tif
```

## 2. gdal_translate (http://www.gdal.org/gdal_translate.html)

- 다른 형식으로 래스터 데이터를 변환
- 영상 resize 및 포멧 변경

```shell
gdal_translate -of GTiff -outsize 50% 50% src_dataset dst_dataset
```

## 3. gdalwarp (http://www.gdal.org/gdal_utilities.html)

- image reprojection and warping utility
- 좌표변환, resampling, image mosaicing

```shell
gdalwarp -t_srs EPSG:4326 input.tif output.tif
```

## 4. gdal_merge (https://gdal.org/programs/gdal_merge.html)

- 일련의 이미지를 자동으로 모자이크한다.
- 모든 이미지는 동일한 좌표계에 밴드 수가 일치해야 한다.
- 겹치는 영역에서는 마지막 이미지가 이전 이미지에 복사된다.

```shell
gdal_merge.py -init 255 -o out.tif in1.tif in2.tif
```

## 5. gdalmanage (http://www.gdal.org/gdalmanage.html)

Mode:

1. identify datasetname : List data format of file. 데이터 포맷 정보 보기
2. copy datasetname newdatasetname : 파일 복사
3. rename datasetname newdatasetname : 이름 수정
4. delete datasetname : 이미지 삭제

```shell
# 파일일 때
gdalmanage identify test.tif

# 폴더일 때
gdalmanage identify –r test/
```

## 6. gdal_contour (http://www.gdal.org/gdal_contour.html)

- 입력 래스터 표고 모델(DEM)로부터 벡터 등고선 파일을 생성한다.

## 7. gdal_polygonize.py (http://www.gdal.org/gdal_polygonize.html)

- Produces a polygon feature layer from a raster.
- ERS -> Shape 파일로 변환

```shell
python gdal_polygonize.py inputFile -f ”ESRI Shapefile” outputFile
```

## 8. ogr2ogr (http://www.gdal.org/ogr2ogr.html)

Shape 파일 좌표 변환

```shell
ogr2ogr -f "ESRI Shapefile" out.shp wgs84.shp -s_srs EPSG:32616 -t_srs EPSG:4326
```

Shape -> GeoJSON 변환

```shell
ogr2ogr -f GeoJSON -t_srs crs:84 [name].geojson [name].shp
```

3. http://www.mercatorgeosystems.com/blog-articles/2008/05/30/using-ogr2ogr-to-re-project-a-shape-file/

## 9. gdaldem (https://gdal.org/programs/gdaldem.html)

ERS -> GTiff 파일로 변환한다.

```shell
gdaldem color-relief -of GTiff -co "TILED=YES" K220100502_22131215_ref_med_union.ers color_file.txt color.tif
```

**※ GDAL 에서 .py 파일은 .exe로 만들어서 붙입니다.**
