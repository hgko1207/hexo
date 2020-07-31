---
title: 시각화 기초(이미지)
categories:
  - Programming
  - AI
tags:
  - Python
  - AI
  - Numpy
  - matplotlib
date: 2020-07-17 18:20:17
thumbnail: /images/thumbnail/matplotlib.png
---

## Image Visualization

### Load Packages

```python
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

%matplotlib inline
```

### 이미지 불러오기

```python
path = 'images/dog.jpg'

image_pil = Image.open(path)
image = np.array(image_pil)

image.shape

# Out
(300, 400, 3)
```

### 이미지 들여다 보기

```python
np.min(image), np.max(image)

# Out
(0, 255)
```

### 그래프로 시각화 하기

```python
plt.hist(image.ravel(), 256, [0, 256])
plt.show()
```

![](/images/ai/image/1.png)

### 그림 나타내기

```python
plt.imshow(image)
plt.show()
```

![](/images/ai/image/2.png)

### 이미지 흑백으로 열기

```python
image_pil = Image.open(path).convert("L")
image_bw = np.array(image_pil)

image_bw.shape

# Out
(300, 400)
```

### 흑백 이미지 열기

```python
plt.imshow(image_bw, 'gray')
plt.show()
```

![](/images/ai/image/3.png)

### 다른 색상으로 cmap 표현하기

#### gray scale

```python
plt.imshow(image_bw, 'gray')
plt.show()
```

![](/images/ai/image/3.png)

#### RdBu(Red and Blue)

```python
plt.imshow(image_bw, 'RdBu')
plt.show()
```

![](/images/ai/image/4.png)

#### jet

색상 값이 높을수록 빨간색, 낮을수록 파란색으로 표현한다.

```python
plt.imshow(image_bw, 'jet')
plt.show()
```

![](/images/ai/image/5.png)

### Colorbar 추가하기

```python
plt.imshow(image_bw, 'jet')
plt.colorbar()
plt.show()
```

![](/images/ai/image/6.png)

### 이미지 설정

이미지 보기 사이즈를 조절한다.

```python
plt.figure(figsize=(10, 10))
plt.imshow(image)
plt.show()
```

![](/images/ai/image/7.png)

### 이미지에 제목 추가

```python
plt.title('Dog')
plt.imshow(image)
plt.show()
```

![](/images/ai/image/8.png)

### 두 번째 이미지 열기

```python
cat_path = 'images/cat.jpg'

cat_pil = Image.open(cat_path)
cat_image = np.array(cat_pil)

plt.imshow(cat_image)
plt.show()
```

![](/images/ai/image/9.png)

### 두 번째 이미지를 첫 번째 이미지 모양에 맞추기

#### 준비

```bash
# Install
pip install opencv-python
```

```python
# In
import cv2

dog_image = cv2.resize(image, (400, 300))
dog_image.shape, cat_image.shape

# Out
((300, 400, 3), (300, 400, 3))
```

#### 이미지 합치기

```python
plt.imshow(dog_image)
plt.imshow(cat_image, alpha=0.5)
plt.show()
```

![](/images/ai/image/10.png)

### Subplot

```python
plt.figure(figsize=(10, 10))
plt.subplot(221)
plt.imshow(dog_image)
plt.subplot(222)
plt.imshow(image_bw, 'gray')
plt.subplot(223)
plt.imshow(cat_image)
plt.show()
```

![](/images/ai/image/11.png)
