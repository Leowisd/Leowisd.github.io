---
title: Leetcode969-pancakeSorting
categories: leetcode
tags: [Array, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-23 11:26:30
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array A, we can perform a pancake flip: We choose some positive integer k <= A.length, then reverse the order of the first k elements of A.  We want to perform zero or more pancake flips (doing them one after another in succession) to sort the array A.

Return the k-values corresponding to a sequence of pancake flips that sort A.  Any valid answer that sorts the array within 10 * A.length flips will be judged as correct.

## Example
**Example 1:**
```
Input: [3,2,4,1]
Output: [4,2,4,3]
Explanation: 
We perform 4 pancake flips, with k values 4, 2, 4, and 3.
Starting state: A = [3, 2, 4, 1]
After 1st flip (k=4): A = [1, 4, 2, 3]
After 2nd flip (k=2): A = [4, 1, 2, 3]
After 3rd flip (k=4): A = [3, 2, 1, 4]
After 4th flip (k=3): A = [1, 2, 3, 4], which is sorted. 
```
**Example 2:**
```
Input: [1,2,3]
Output: []
Explanation: The input is already sorted, so there is no need to flip anything.
Note that other answers, such as [3, 3], would also be accepted.
```
**Note:**
```
1 <= A.length <= 100
A[i] is a permutation of [1, 2, ..., A.length]
```

## Solution
```java
class Solution {
    public List<Integer> pancakeSort(int[] A) {
        List<Integer> res = new ArrayList<>();
        if (A.length == 0) return res;
        
        for (int i = A.length; i > 1; i--){
            int max = Integer.MIN_VALUE;
            int maxIndex = -1;
            for (int j = 0; j < i; j++){
                if (A[j] > max){
                    max = A[j];
                    maxIndex = j;
                }
            }
            if (maxIndex == i - 1) continue;
            reverse(A, maxIndex);
            res.add(maxIndex + 1);
            reverse(A, i - 1);
            res.add(i);
        }
        
        return res;
    }
    
    private void reverse(int[] A, int index){
        int i = 0;
        int j = index;
        while(i < j){
            int tmp = A[i];
            A[i] = A[j];
            A[j] = tmp;
            i++;
            j--;
        }
    }
}

```

<hr />