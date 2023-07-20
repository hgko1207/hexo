---
title: '[Python] Numpy 기초(3)'
categories:
  - Programming
  - Language
  - Python
tags:
  - Python
  - AI
  - Numpy
date: 2020-07-09 16:16:50
thumbnail: /images/thumbnail/numpy.png
---

## zeros

0으로 채워진 numpy 배열을 만든다.

```python
np.zeros([3, 3])

# Out
array([[0., 0., 0.],
       [0., 0., 0.],
       [0., 0., 0.]])
```

## ones

1로 채워진 numpy 배열을 만든다.

```python
np.ones([3, 3])

# Out
array([[1., 1., 1.],
       [1., 1., 1.],
       [1., 1., 1.]])
```

## arange

하나의 값만 입력하면 1씩 증가하는 1차원 배열을 만든다.

```python
np.arange(10)

# Out
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
```

두 개의 인자를 넣으면 입력한 값의 범위만큼 배열을 만든다.

```python
np.arange(4, 9)

# Out
array([4, 5, 6, 7, 8])
```

### reshape

1차원 배열의 차원 수를 바꿀때 사용된다.

```python
np.arange(9).reshape(3, 3)

# Out
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]])
```

## Index

기본적으로 python 에서 쓰는 방식과 동일하다.

```python
arr = np.arange(9).reshape(3, 3)
arr[1]

# Out
array([3, 4, 5])
```

## Slicing

다차원 배열의 원소 중 복수 개를 접근하기 위해 사용한다.

```python
arr = np.arange(9).reshape(3, 3)
arr[1:]

# Out
array([[3, 4, 5],
       [6, 7, 8]])
```

```python
arr[1:, 1:]

# Out
array([[4, 5],
       [7, 8]])
```

### Boolean Indexing

원하는 행 또는 열의 값만 얻을 수 있고, 값들을 변경할 수 있다.

```python
data = np.random.randn(3, 3)
data <= 0

# Out
array([[-0.43152818, -2.40848595, -0.00309727],
       [ 0.74972847,  0.18525482, -0.39854904],
       [ 1.09053126,  0.32096086,  0.31703319]])

array([[ True,  True,  True],
       [False, False,  True],
       [False, False, False]])
```

```python
data[data <= 0]

# Out
array([-0.43152818, -2.40848595, -0.00309727, -0.39854904])
```

```python
data[data <= 0] = 1

# Out
array([[1.        , 1.        , 1.        ],
       [0.74972847, 0.18525482, 1.        ],
       [1.09053126, 0.32096086, 0.31703319]])
```

## Broadcast

연산 하려는 서로 다른 두 개의 행렬의 shape가 같지 않고, 한쪽의 차원이라도 같거나 또는 값의 갯수가 한 개 일 때 이를 여러 복사를 하여 연산한다.

```python
arr = np.arange(9).reshape(3, 3)
arr + 3

# Out
array([[ 3,  4,  5],
       [ 6,  7,  8],
       [ 9, 10, 11]])
```

```python
arr * 3

# Out
array([[ 0,  3,  6],
       [ 9, 12, 15],
       [18, 21, 24]])
```

```python
arr + np.array([1, 2, 3])

# Out
array([[ 1,  3,  5],
       [ 4,  6,  8],
       [ 7,  9, 11]])
```

## Math Function

배열 연산에 대해 여러가지 예제다.

```python
arr + 5
arr * 5
arr + arr

np.add(arr, 1)
np.multiply(arr, 3)
```

```python
np.sum(arr)
np.sum(arr + arr_2)
np.sum(arr, 0) # 0차원 기준으로 더해서 배열을 만든다.

np.max(arr)
np.max(arr, 0) # 0차원에서 가장 큰 값들을 배열로 만든다.

np.min(arr)

np.mean(arr)
```

```python
arr = np.array([1, 6, 3, 7, 3, 2, 9, 0, 2])
np.argmax(arr) # 가장 큰 수의 index값을 리턴한다.

# Out
6

np.argmin(arr)

# Out
7
```

```python
arr = np.array([3, 5, 6, 6, 3, 3, 1])
np.unique(arr) # 유니크한 값들을 리턴한다.

# Out
array([1, 3, 5, 6])
```
