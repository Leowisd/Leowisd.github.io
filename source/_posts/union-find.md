---
title: Union-find data structure
tags: [Algorithms, Data Structure]
mathjax: true
date: 2018-12-27 09:36:41
categories: Algorithms
description: Algorithms review for coming interviews
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fyl26sdrq8j212w0m8jwg.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Implementation

```java

public void initial(){
    int[] friends = new int[n];
    for (int i = 0; i < n; i++) friends[i] = i;
}

public int find(int i){
    if (friends[i] != i) friends[i] = find(friends[i]);
    return friends[i];
}

public void union(int i, int j){
    int si = find(i);
    int sj = find(j);
    if (si != sj) friends[si] = sj;
}
```


### MakeSet

```python
def makeSet(a, n):
    for i in range(n):
        a[i] = i
```

### Find

```python
def find(i):
    global a
    if a[i] != i:
        # Optimation 1: Find with path compression
        a[i] = find(a[i]) 
    return a[i]
```

### Union

```python
def union(x, y):
    fx = find(x)
    fy = find(y)

    if (fx == fy):
        return

    global rank
    global a
    # Optimation 2: Union by Rank
    if (rank[fx]>rank[fy]):
        a[fy] = fx
    else:
        a[fx] = fy
        if (rank[fx] == rank[fy]):
            rank[fy] += 1
```

## Example problem 

### Description
If a family is too large, it's really not easy to judge whether two people are relatives. Give a relatives diagram and find out whether any given two people have relatives. Provisions: X and y are relatives, y and Z are relatives, then x and Z are relatives. If X and y are relatives, then x's relatives are relatives of y, and y's relatives are relatives of X.

### Input
The first line: three integers n, m, p, (n <= 5000, m <= 5000, P <= 5000), respectively, denote n individuals and m relatives, and ask P about their relatives. 

The following M lines: Mi, Mj, 1 <= Mi, Mj <= N, two numbers per line, indicating that Mi and Mj are related. 

Next, line p: Pi and Pj are two numbers per line. Ask if Pi and Pj are related.

### Output
P lines, one'Yes'or'No' per line. The answer to the $i^{th}$ question is "have" or "don't have" relatives.

<hr />