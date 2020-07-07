---
title: Leetcode119-pascalsTriangleII
categories: leetcode
tags: [Array, Cerner]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-31 11:39:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)
In Pascal's triangle, each number is the sum of the two numbers directly above it.

## Example
```
Input: 3
Output: [1,3,3,1]
```

**Follow up:**

Could you optimize your algorithm to use only O(k) extra space?

## Solution
```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> res = new ArrayList<Integer>();
        res.add(1);
        if (rowIndex == 0) return res;
        res.add(1);
        if (rowIndex == 1) return res;
        
        for (int i = 2; i <= rowIndex; i++){
            for (int j = i - 1; j >= 1; j--){
                int tmp = res.get(j - 1) + res.get(j);
                res.set(j, tmp);
            }
            res.add(1);
            // newLine.add(1);
            // for (int j = 0; j < res.size() - 1; j++){
            //     newLine.add(res.get(j) + res.get(j + 1));
            // }
            // newLine.add(1);
            // res = newLine;
            // newLine = new ArrayList<Integer>();
        }
        
        return res;
    }
}
```

<hr />