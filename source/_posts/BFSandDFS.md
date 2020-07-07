---
title: BFS and DFS 
tags: [Algorithms, Searching, BFS, DFS]
mathjax: true
date: 2018-12-29 11:38:55
categories: Algorithms
description: Algorithms review for coming interviews
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fynh2cx3u2j212w0m8tcu.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Pseudocode

### BFS

```python
from collections import deque

def BFS():
    while (q != None):
        u = q.popleft()
        for v in subState[u]:
            if Flag(v) and Optimize(v):
                setFlag(v)
                v.pre = u
                if goalTest(v):
                    outputResult()
                q.append(v)
```

### DFS

```python
def DFS_working(x):
    if goalTest(x):
        outputResult()
    for xi in subState[x]:
        if Flag(xi) and Optimize(xi):
            setSomeAttrs(flag, pre, ...)
            DFS_working(xi)
            delSomeAttrs(flag, pre, ...)

def DFS():
    for x in subState[source]:
        DFS_working(x)
```

## Stack and Queue in Python

### Using list as stack

```python
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]
```

### Using list as queue

```python
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```

<hr />