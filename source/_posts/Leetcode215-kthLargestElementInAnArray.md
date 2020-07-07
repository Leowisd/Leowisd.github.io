---
title: Leetcode215-kthLargestElementInAnArray
categories: leetcode
tags: [Sort, Priority Queue, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-18 22:10:11
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

## Example
**Example 1:**
```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Example** 2:
```
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```
## Solution
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        // sort and print
        // Arrays.sort(nums);
        // return nums[nums.length - k];
        
        //PriorityQueue
        PriorityQueue<Integer> pq = new PriorityQueue<>(new Comparator<Integer>(){
            @Override
            public int compare(Integer a, Integer b){
                return a-b;
            }
        });           
        for (int e : nums){
            pq.offer(e);
            if (pq.size() > k){
                pq.poll();
            }
        }
        return pq.poll();
    }
}
```

<hr />