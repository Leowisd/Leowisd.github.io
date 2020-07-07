---
title: Leetcode658-findKCloestElements
categories: leetcode
tags: [Binary Search, Two Pointers, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 15:04:24
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a sorted array, two integers k and x, find the k closest elements to x in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred.

## Example
**Example 1:**
```
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```
**Example 2:**
```
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]
```

## Solution
**Solution 1: Two Pointers, O(N)**
```java
class Solution {
    // Two pointers, O(N)
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int left = 0;
        int right = arr.length - 1;
        
        while (right - left >= k){
            if (Math.abs(arr[left] - x) > Math.abs(arr[right] - x))
                left++;
            else right--;
        }
        
        List<Integer> res = new ArrayList<>();
        for (int i = left; i <= right; i++)
            res.add(arr[i]);
        return res;
    }
}
```

**Solution 2: Basic Binary Search, O(logN)**
```java
class Solution {
//     Basic binary search method.
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        
        //find the cloest element, r is the index of one of the cloest elements
        int l = 0, r = arr.length-1;
        while(l <= r) {
            int mid = (l + r)/2;
            if(arr[mid] == x) {r = mid; break;}
            else if(arr[mid] > x) r = mid-1;
            else l = mid+1;
        }

        //ensure the range
        l = r;
        r++;
        while(k>0) {
            if( r >= arr.length || (l >= 0 && x-arr[l] <= arr[r] - x) ) {
                l--;
            } else {
                r++;
            }        
            k--;
        }
        
        List<Integer> list =new ArrayList<>();
        for(int i = l+1; i < r; i++) {
            list.add(arr[i]);
        }
        return list;
    }
}

```

**Solution 3: Excellent binary search, O(logN)**

used mid as left bound of k size closeset

```java
class Solution {    
    // O(logN), used mid as left bound of k size closeset, excellent binary search method
    public List<Integer> findClosestElements(int[] A, int k, int x) {
        int left = 0, right = A.length - k;
        while (left < right) {
            int mid = (left + right) / 2;
            if (x - A[mid] > A[mid + k] - x)
                left = mid + 1;
            else
                right = mid;
        }
        List<Integer> res = new ArrayList<>();
        for (int i = left; i < left + k; i++)
            res.add(A[i]);
        return res;
    }
}
```

<hr />