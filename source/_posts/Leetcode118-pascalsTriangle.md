---
title: Leetcode118-pascalsTriangle
categories: leetcode
tags: [Array, Cerner]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-31 11:25:36
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)
In Pascal's triangle, each number is the sum of the two numbers directly above it.


## Example
```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## Solution
```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new ArrayList<>();
        if (numRows == 0) return res;
        
        res.add(new ArrayList<Integer>());
        res.get(0).add(1);        
        if (numRows == 1) return res;
        
        res.add(new ArrayList<Integer>());
        res.get(1).add(1);
        res.get(1).add(1);
        if (numRows == 2) return res;
        
        for (int i = 3; i <= numRows; i++){
            List<Integer> preLine= res.get(i - 2);
            List<Integer> newLine = new ArrayList<Integer>();
            newLine.add(1);
            for (int j = 0; j < preLine.size() - 1; j++){
                newLine.add(preLine.get(j) + preLine.get(j + 1));
            }
            newLine.add(1);
            res.add(newLine);
        }
        
        return res;
    }
}
```

<hr />