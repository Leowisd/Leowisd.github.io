---
title: Leetcode060-permutationSequence
categories: leetcode
tags: [Math]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-08 22:18:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

The set [1,2,3,...,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for n = 3:
```
1. "123"
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"
```
Given n and k, return the kth permutation sequence.

**Note:**

* Given n will be between 1 and 9 inclusive.
* Given k will be between 1 and n! inclusive.

## Example
**Example 1:**
```
Input: n = 3, k = 3
Output: "213"
```
**Example 2:**
```
Input: n = 4, k = 9
Output: "2314"
```
## Solution

Math Solution
```java
class Solution {
    public String getPermutation(int n, int k) {
        StringBuilder sb = new StringBuilder();
        List<Integer> num = new ArrayList<>();
        int factorial = 1;
        for (int i = 1; i <= n; i++){
            factorial *= i;
            num.add(i);
        }
        k--; //The key point, because num starts from 0
        for (int i = 0; i < n; i++){
            factorial /= (n-i);
            int index = k / factorial;
            sb.append(num.get(index));
            num.remove(index);
            k -= index * factorial;
        }
        return sb.toString();
    }
}
```

Backtracking, but will be TLE.
```java
class Solution {    
    public String getPermutation(int n, int k) {
        List<String> res = new ArrayList<>();
        HashSet<Integer> set = new HashSet<>();
        helper(res, "", n, k, set);
        return res.get(k-1);
    }
    private boolean helper(List<String> res, String cur, int n, int k, HashSet<Integer> set){
        if (cur.length() == n){
            res.add(cur);
            if (res.size() == k){
                return true;
            }
            return false;
        }
        for (int i = 1; i <= n; i++){
            if (set.contains(i)) continue;
            set.add(i);
            if (helper(res, cur + String.valueOf(i), n, k, set)) return true;
            set.remove(i);
        }
        return false;
    }
}
```

<hr />