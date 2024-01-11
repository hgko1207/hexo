---
title: '[Python] 시각화 기초(그래프)'
categories:
  - Programming
  - Language
  - Python
tags:
  - Python
  - AI
  - Graph
  - Numpy
  - matplotlib
date: 2020-07-16 18:08:35
thumbnail: /images/thumbnail/matplotlib.png
---

Python에서 **matplotlib**를 사용하여 시각화하는 방법에 대해 알아보겠다.

## Load Packages

```python
import numpy as np
import matplotlib.pyplot as plt

%matplotlib inline
```

## Basic Attributes

```python
alpha : 투명도
king : 그래프 종류 'line', 'bar', 'barh', 'kde'
logy : Y축에 대해 Log scaling
use_index : 객체의 색인을 눈금 이름으로 사용할지 여부
rot : 눈금 이름 돌리기 (rotating) 0 ~ 360
xticks, yticks : X, Y축으로 사용할 값
xlim, ylim : X, Y축의 한계
grid : 축의 그리드를 표현할지 여부

subplots : 각 column에 독립된 subplot 그리기
sharex, sharey : subplots=True 이면 같은 X, Y축을 공유하고 눈금과 한계를 연결
figsize : 생성될 그래프의 크기를 tuple로 지정
title : 그래프의 제목 지정
legend : subplot의 범례 지정
sort_columns : column을 알파벳 순서로 그린다.
```

## Matplotlib 사용하기

### 점선 그래프 그리기

```python
data = np.random.randn(50).cumsum()
plt.plot(data)
plt.show()
```

![](/images/ai/graph/1.png)

### 여러 그래프 그릴 준비 하기

```python
plt.subplot(1, 2, 1)
plt.subplot(1, 2, 2)
plt.show()
```

![](/images/ai/graph/2.png)

### Multi Graph 그리기

```python
hist_data = np.random.randn(100)
scat_data = np.arange(30)

plt.subplot(2, 2, 1)
plt.plot(data)

plt.subplot(2, 2, 2)
plt.hist(hist_data, bins=20)

plt.subplot(2, 2, 3)
plt.scatter(scat_data, np.arange(30) + 3 * np.random.randn(30))

plt.show()
```

![](/images/ai/graph/3.png)

### 그래프 옵션

그래프를 그릴 때 표시 되는 색이나 마커 패턴을 바꾸는 것을 확인한다.

- 색상: r(빨간색), g(초록색), b(파란색), C(청록색), y(노란색), k(검은색), w(흰색)
- 마커: o(원), v(역삼각형), ^(삼각형), s(네모), +(플러스), .(점)

```python
plt.plot(data, 'go')
plt.show()
```

![](/images/ai/graph/4.png)

### 그래프 사이즈 조절

plt.figure 안에 figsize를 이용하여 가로, 세로 길이 조절 가능하다. (inch 단위)

```python
plt.figure(figsize=(10, 10))
plt.plot(data, 'k+')
plt.show()
```

![](/images/ai/graph/5.png)

여러 그래프 그리고 그에 대한 크기 조절을 한다.

```python
# 맨 위에 있어야 한다.
plt.figure(figsize=(10, 5))

plt.subplot(2, 2, 1)
plt.plot(data)

plt.subplot(2, 2, 2)
plt.hist(hist_data, bins=20)

plt.subplot(2, 2, 3)
plt.scatter(scat_data, np.arange(30) + 3 * np.random.randn(30))

plt.show()
```

![](/images/ai/graph/6.png)

### 그래프 겹치기와 legend 표시

```python
data = np.random.randn(30).cumsum()

plt.plot(data, 'k--', label='Default')
plt.plot(data, 'k-', drawstyle='steps-post', label='steps-post')
plt.legend()
plt.show()
```

![](/images/ai/graph/7.png)

### 이름 달기

```python
plt.plot(np.random.randn(1000).cumsum())
plt.title('Random Graph')
plt.xlabel('Stages')
plt.ylabel('Values')
plt.show()
```

![](/images/ai/graph/8.png)

### 종합

```python
plt.title('Graph')
plt.plot(np.random.randn(500).cumsum(), 'k^', label='one')
plt.plot(np.random.randn(500).cumsum(), 'b.', label='two')
plt.plot(np.random.randn(500).cumsum(), 'r', label='three')

plt.legend()
plt.show()
```

![](/images/ai/graph/9.png)

### 그래프 저장하기

```python
# 현재 작업 위치로 저장한다.
plt.savefig('saved_graph.svg')
```
