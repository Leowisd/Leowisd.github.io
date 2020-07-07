---
title: PythonInput
tags: [Python, Input, Format]
mathjax: true
date: 2018-12-31 11:27:36
categories: Python
description: Bacis methods of how to get integer from keyboard
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvx5bbi8asj212w0m8my4.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

### Input one parameter

```python
x = int(input('Input one parameter: '))
```

### Input muti parameters

```python
x, y = map(int, input('Input two parameters: ').split(' '))
```

### Input a list

```python
l = list(map(int, input('Input a list').split(' ')))
```

### Input muli-d list

```python
l = []
n = int(input())
for i in range(n):
    l.append(list(map(int, input().split(' '))))
```
<hr />