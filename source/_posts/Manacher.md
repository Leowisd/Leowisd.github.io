---
title: Manacher
tags: [Palindrome]
mathjax: true
date: 2019-10-16 09:51:48
permalink:
categories: Algorithms
description:
image:
---
<p class="description"></p>

<img src="https://" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Implementation

```java

public int[] manacher(String s){
    List<Character> a = new List<>();
    a.add('@');
    a.add('#');
    for (char ch: s.toCharArray()){
        a.add(ch);
        a.add('#');
    }
    a.add('?');

    int n = a.size();
    int maxID = 0;
    int id = 0;
    int[] p = new int[n];

    for (int i = 1; i < n- 1; i++){
        if (maxID > i) p[i] = Math.min(p[2 * id - i], maxID - i);
        else p[i] = 1;

        while (a.get(i - p[i]) == a.get(i + p[i])) p[i]++;

        if (i + p[i] > maxID){
            maxID = i + p[i];
            id = i;
        }
    }

    return p;
}
```

## Time Complexity

O(N)

<hr />