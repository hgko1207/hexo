---
title: '[Python] Numpy 기초(1)'
categories:
  - Programming
  - Language
  - Python
tags:
  - Python
  - AI
  - Numpy
date: 2020-07-01 17:11:52
thumbnail: /images/thumbnail/numpy.png
---

## Numpy 란

> Numpy는 C언어로 구현된 파이썬 라이브러리로써, 고성능의 수치계산을 위해 제작되었습니다. Numerical Python의 줄임말이기도 한 Numpy는 벡터 및 행렬 연산에 있어서 매우 편리한 기능을 제공합니다.
> 출처: [Tigercow.Door](https://doorbw.tistory.com/171)

**Numpy**는 고차원적인 데이터를 다루기 쉽게 만들어져 있어 딥러닝을 하게 되면 많이 접하게 됩니다. 
이제 Numpy 사용방법에 대해 알아보겠습니다.

```python
# Numpy 사용하기
import numpy as np
```

### 0차원

numpy array는 1 또는 5, 10와 같이 숫자 데이터를 array화 해줄 수 있습니다.

```python
arr = np.array(5);
arr.shape # 배열의 형태(크기)를 나타냅니다.

# Out
() # shape가 아무것도 없는 것으로 나옵니다.
```

```python
arr.ndim # 배열의 차원을 나타냅니다.

# Out
0 # 0차원을 의미합니다.
```

### 1차원

- 숫자가 10과 같이 하나만 들어간다고 해도 [] 리스트를 한번 씌우게 되면 차원이 생깁니다.
- 이때는 1차원이 되는데 numpy 에서 shape를 표현할 때 (1)이 아닌 (1,) 형식으로 표현하게 됩니다.

```python
arr = np.array([5])
arr.shape

# Out
(1,)
```

(3,)에서 3은 3이라는 값이 들어간 것이 아닌 1차원에 3개의 값이 들어갔다는 의미입니다.

### 2차원

대괄호를 추가적으로 씌우면 차원이 추가적으로 하나 생깁니다.

```python
arr = np.array([[1, 2, 3]])
arr.shape

# Out
(1, 3)
```

아래의 shape를 보면 차원이 2개 있고, 각 차원 마다 각각 3개의 값이 들어있다는 의미입니다.

```python
arr = np.array([[1, 2, 3], [1, 2, 3], [1, 2, 3]])
arr.shape

# Out
(3, 3)
```

참고로 0차원 숫자에 대괄호를 2번 씌우면 두 개의 차원이 됩니다.

```python
arr = np.array([[10]])
arr.shape

# Out
(1, 1)
```

### 다차원

```python
arr = np.array([[[[1, 2, 3], [1, 2, 3], [1, 2, 3]], [[1, 2, 3], [1, 2, 3], [1, 2, 3]]], [[[1, 2, 3], [1, 2, 3], [1, 2, 3]], [[1, 2, 3], [1, 2, 3], [1, 2, 3]]]])

# Out
array([[[[1, 2, 3],
         [1, 2, 3],
         [1, 2, 3]],

        [[1, 2, 3],
         [1, 2, 3],
         [1, 2, 3]]],


       [[[1, 2, 3],
         [1, 2, 3],
         [1, 2, 3]],

        [[1, 2, 3],
         [1, 2, 3],
         [1, 2, 3]]]])
```

4차원의 배열을 나타냅니다.

```python
arr.shape

# Out
(2, 2, 3, 3)
```
