---
title: Leetcode364-nestedListWeightSumII
categories: leetcode
tags: [Backtracking, Linkedln]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-10 21:34:45
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

Different from the previous question where weight is increasing from root to leaf, now the weight is defined from bottom up. i.e., the leaf level integers have weight 1, and the root level integers have the largest weight.

## Example
**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/27/nestedlistweightsumiiex1.png)
```
Given the list [[1,1],2,[1,1]], return 8. (four 1's at depth 1, one 2 at depth 2)
```
**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/27/nestedlistweightsumiiex2.png)
```
Given the list [1,[4,[6]]], return 17. (one 1 at depth 3, one 4 at depth 2, and one 6 at depth 1; 13 + 42 + 6*1 = 17)
```
## Solution
```java
public int depthSumInverse(List<NestedInteger> nestedList) {
    return DFS(nestedList, 0);
}
public int DFS(List<NestedInteger> nestedList, int intSum) {
    //关键点在于把上一层的integer sum传到下一层去，这样的话，接下来还有几层，每一层都会加上这个integer sum,也就等于乘以了它的层数
    List<NestedInteger> nextLevel = new ArrayList<>();
    int listSum = 0;
    for (NestedInteger list : nestedList) {
        if (list.isInteger()) {
            intSum += list.getInteger();
        } else {
            nextLevel.addAll(list.getList());
        }
    }
    listSum = nextLevel.isEmpty() ? 0 : DFS(nextLevel, intSum);
    return listSum + intSum;
}
```

<hr />