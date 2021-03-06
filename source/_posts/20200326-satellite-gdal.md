---
title: Gdal 사용법
categories:
  - Satellite
tags:
  - Satellite
  - Gdal
  - Coordinate System
  - Library
date: 2020-03-26 11:07:02
thumbnail: /images/thumbnail/satellite.png
---

**GDAL**은 래스터 및 벡터 지리 공간 데이터를 조작 할 수 있는 오픈 소스 라이브러리입니다.

- 라이브러리로서 지원되는 모든 형식의 호출 응용 프로그램에 단일 추상 데이터 모델을 제공합니다.
- 데이터 변환 및 처리를 위한 다양한 명령 행 인터페이스 유틸리티가 제공됩니다.
- Windows, Linux 및 MacOS에서 사용가능합니다.

### 1. gdalinfo (http://www.gdal.org/gdalinfo.html)

- GDAL이 지원하는 영상 정보를 확인합니다.
- 예) `gdalinfo test.tif`

### 2. gdal_translate (http://www.gdal.org/gdal_translate.html)

- 다른 형식으로 래스터 데이터를 변환합니다.
- 영상 resize 및 포멧 변경
- 예) `gdal_translate -of GTiff -outsize 50% 50% src_dataset dst_dataset`

### 3. gdalwarp (http://www.gdal.org/gdal_utilities.html)

- image reprojection and warping utility
- 좌표변환, resampling, image mosaicing
- 예) `gdalwarp -t_srs EPSG:4326 input.tif output.tif`

### 4. gdal_merge (https://gdal.org/programs/gdal_merge.html)

- 일련의 이미지를 자동으로 모자이크합니다.
- 모든 이미지는 동일한 좌표계에 밴드 수가 일치해야 합니다.
- 겹치는 영역에서는 마지막 이미지가 이전 이미지에 복사됩니다.
- 예) `gdal_merge.py -init 255 -o out.tif in1.tif in2.tif`

### 5. gdalmanage (http://www.gdal.org/gdalmanage.html)

Mode:

1. identify datasetname : List data format of file. 데이터 포맷 정보 보기
2. copy datasetname newdatasetname : 파일 복사
3. rename datasetname newdatasetname : 이름 수정
4. delete datasetname : 이미지 삭제

- 예) `gdalmanage identify test.tif` -> 파일일 때
  `gdalmanage identify –r test/` -> 폴더일 때

### 6. gdal_contour (http://www.gdal.org/gdal_contour.html)

- 입력 래스터 표고 모델(DEM)로부터 벡터 등고선 파일을 생성합니다.

### 7. gdal_polygonize.py (http://www.gdal.org/gdal_polygonize.html)

- Produces a polygon feature layer from a raster.
- ERS -> Shape 파일로 변환
- 예) `python gdal_polygonize.py inputFile -f ”ESRI Shapefile” outputFile`

### 8. ogr2ogr (http://www.gdal.org/ogr2ogr.html)

1. Shape 파일 좌표 변환
   예) `ogr2ogr -f "ESRI Shapefile" out.shp wgs84.shp -s_srs EPSG:32616 -t_srs EPSG:4326`

2. Shape -> GeoJSON 변환
   예) `ogr2ogr -f GeoJSON -t_srs crs:84 [name].geojson [name].shp`

3. http://www.mercatorgeosystems.com/blog-articles/2008/05/30/using-ogr2ogr-to-re-project-a-shape-file/

### 9. gdaldem (https://gdal.org/programs/gdaldem.html)

1. ERS -> GTiff 파일로 변환
2. 예) `gdaldem color-relief -of GTiff -co "TILED=YES" K220100502_22131215_ref_med_union.ers color_file.txt color.tif`

#### ※ GDAL 에서 .py 파일은 .exe로 만들어서 붙입니다.
