---
title: Dijstra and Floyd
tags: [Algorithms, Shortest path, Dijstra, Floyd]
mathjax: true
date: 2018-12-31 09:59:02
categories: Algorithms
description: Algorithms review for coming interviews
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fyprl5cr2nj212w0m87a8.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Implementation

```python

def dijstra(s):
    global n
    global cost
    len = [1000 for i in range(n)]
    visit = [0 for i in range(n)]

    for i in range(n):
        len[i] = cost[s][i]
        visit[i] = 0
    visit[s] = 1

    for i in range(n-1):
        min = 10000
        for j in range(n):
            if (visit[j]==0  and min>len[j]):
                min = len[j]
                pos = j

        visit[pos] = 1

        for j in range(n):
            if (visit[j] == 0 and len[j]>len[pos] + cost[pos][j]):
                len[j] = len[pos] + cost[pos][j]

    print(len)



def floyd():
    global n
    global cost
    path = [[0 for i in range(n)]for j in range(n)]
    length = [[0 for i in range(n)]for j in range(n)]
    for i in range(n):
        for j in range(n):            
            length[i][j] = cost[i][j]
            if cost[i][j] < 1000:
                path[i][j] = i
            else:
                path[i][j] = -1

    for k in range(n):
        for i in range(n):
            for j in range(n):
                if (length[i][k] < 1000)and (length[k][j] < 1000):
                    if (length[i][j] > length[i][k] + length[k][j]):
                        length[i][j] = length[i][k] + length[k][j]
                        path[i][j] = k
    
    for i in range(n):
        print(length[i])

global n 
n = int(input('Please input the number of notes: '))
cost = []
for i in range(n):
    cost.append(list(map(int, input().split(' '))))

s = int(input('Please input the source: '))
dijstra(s)


input('Please run floyd')
floyd()
```

<hr />