---
title: '[Python] Numpy 기초(2)'
categories:
  - Programming
  - Language
  - Python
tags:
  - Python
  - AI
  - Numpy
date: 2020-07-02 10:36:18
thumbnail: /images/thumbnail/numpy.png
---

**Numpy** 기초에 대해 다뤄보겠다.

## Load Package

```python
import numpy as np
```

## data type

배열의 dtype을 봅니다.

```python
arr = np.array([[1, 2, 3], [1, 2, 3]])
arr.dtype

# Out
dtype('int32')
```

`.astype()` 으로 datatype을 변환 가능하다.

```python
arr = arr.astype('float32')
arr = arr.astype(np.float32)

# Out
array([[1., 2., 3.],
       [1., 2., 3.]], dtype=float32)
```

`len(arr.shape)`를 통해서 차원이 개수를 확인할 수 있지만, 다음과 같이 ndim 을 통해 차원 수를 확인하다.

```python
len(arr.shape)
arr.ndim

# Out
2
```

## Reshape

차원을 바꾼다.

```python
arr = arr.reshape([1, 6])
arr.shape

# Out
(1, 6)
```

차원을 몇 개로 나눠야할지 모를 경우 -1을 활용하다.

```python
arr = arr.reshape(-1)
arr.shape

# Out
(6,)
```

3차원으로 늘리는 방법이다.

```python
arr = np.random.randn(8, 8) # (8, 8)
arr = arr.reshape([32, 2]) # (32, 2)
arr = arr.reshape([-1, 2, 1])

# Out
(32, 2, 1)
```

## Ravel

배열을 1차원으로 바꿔준다. 나중에 배열 layer를 flatten 할 때 같은 기능이라 생각하면 된다.

```python
arr = arr.ravel()
arr.shape

# Out
(64,)
```

## np.expand_dims()

안의 값은 유지하되 차원 수를 늘리고 싶을 때 사용한다.

```python
arr = np.expand_dims(arr, 0)
arr.shape

# Out
(1, 64)
```
