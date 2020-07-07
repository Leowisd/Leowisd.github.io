---
title: Leetcode096-uniqueBianrySearchTrees
categories: leetcode
tags: [DP]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-22 21:01:39
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?

**Example:**
```
Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

## Solution
Catelan
```java
// C0 = 1;
// C(n + 1) = C(0)C(n) + C(1)C(n - 1)....

class Solution {
    public int numTrees(int n) {
        int[] Catelan = new int[n + 1];
        Catelan[0] = 1;
        
        for (int i = 1; i <= n; i++){
            for (int j = 0; j < i; j++){
                Catelan[i] += Catelan[j] * Catelan[i - j - 1];
            }
        }
        
        return Catelan[n];
    }
}
```

<hr />