---
title: Merge Sort
tags: [Algorithms, Sort]
mathjax: true
date: 2018-12-28 10:23:06
categories: Algorithms
description: Algorithms review for coming interviews
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029gy1fym950zqvbj212w0m8q9p.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Implementation

```python
from copy import deepcopy 

def mergeSort(a1, s, m, t, a):
    i = s
    j = m + 1
    k = s - 1

    while (i <= m) and (j <= t):
        k += 1
        if (a1[i] <= a1[j]):
            a[k] = a1[i]
            i += 1
        else:
            a[k] = a1[j]
            j += 1
    
    while (i<=m):
        k += 1
        a[k] = a1[i]
        i += 1
    while (j<=t):
        k += 1
        a[k] = a1[j]
        j += 1
    

def mergeSortStep(a, s, t):
    a1 = deepcopy(a)
    if (s<t):
        m = (s+t)//2
        mergeSortStep(a1, s, m)
        mergeSortStep(a1, m+1, t)
        mergeSort(a1, s, m, t, a)

n = int(input('Please input the number of the list: '))
a = list(map(int, input('Please input the unsorted list: ').split()))
mergeSortStep(a, 0, n-1)
for i in range(n):
    print(a[i], end=' ')
```

**Hint: shadow/deep copy for lists**



<hr />