---
title: Quick Sort
tags: [Algorithms, Sort]
mathjax: true
date: 2018-12-24 09:33:07
categories: Algorithms
description: Algorithms review for coming interviews
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fyhl74f8ruj212w0m8gsy.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Implementation

```python
import random

def QuickSort(a, left, right):
    if left>=right:
        return
    p = left + random.randrange(right-left+1)
    temp = a[left]
    a[left] = a[p]
    a[p] = temp
    i = left
    j = right
    x = a[i]
    while (i<j) :
        while (i<j) and (a[j]>x):
        # From big to small
        # while (i<j) and (a[j]<x):
            j = j - 1
        a[i] = a[j]
        while (i<j) and (a[i]<=x):
        # From big to small
        # while (i<j) and (a[i]>=x):
            i = i + 1
        a[j] = a[i]         
    a[i] = x
    QuickSort(a, left, i-1)
    QuickSort(a, i+1, right)

n = int(input("The number of the list: "))
line = input("The unsorted list: ")
a = list(map(int, line.split()))
QuickSort(a, 0, n-1)
for i in range(n):
    print(a[i], end=' ')
```

## Notes

### Keyboards input

To convert str to speical foramt list, using split() to seperate list and convert items' type

### Outputs format

To print a list in one line seperated by SPACE, using end=' ', which can be used with other symbols like ','

<hr />