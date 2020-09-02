---
title: '[딥러닝] Preprocess 준비'
categories:
  - Programming
  - AI
tags:
  - DeepLearning
  - 딥러닝
date: 2020-09-01 23:10:35
thumbnail: /images/thumbnail/ai.png
---

로컬 데이터를 불러와 전처리시 필요한 내용입니다.

## Load Packages

```python
import os
from glob import glob

import numpy as np

import tensorflow as tf
from PIL import Image

import matplotlib.pyplot as plt
%matplotlib inline
```

```python
# 현재 경로를 알려준다.
os.getcwd()

# 경로를 넣으면 경로의 파일명만 목록 형식으로 보여준다.
os.listdir()
os.listdir('dataset/mnist_png/training/')

# 경로가 포함된 모든 파일들을 목록 형식으로 보여준다.
# 원하는 포맷의 파일만을 가져올 수 있다.(png, txt 등)
glob('dataset/mnist_png/training/*.png')
```

## 데이터 분석

```python
label_nums = os.listdir('dataset/mnist_png/training/')
> ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']

# Label 데이터 갯수 확인
len(label_nums)
> 10
```

데이터 별 갯수 비교

```python
nums_dataset = []

for lbl_n in label_nums:
    data_per_class = os.listdir('../dataset/mnist_png/training/' + lbl_n)
    nums_dataset.append(len(data_per_class))

> [5923, 6742, 5958, 6131, 5842, 5421, 5918, 6265, 5851, 5949]
```

## TensorFlow로 열기

```python
gfile = tf.io.read_file(path)
image = tf.io.decode_image(gfile)
```

## 데이터 이미지 사이즈 알기

```python
from tqdm import tqdm_notebook

heights = []
widths = []

for path in tqdm_notebook(data_paths):
    image_pil = Image.open(path)
    image = np.array(image_pil)
    h, w = image.shape

    heights.append(h)
    widths.append(w)
```
