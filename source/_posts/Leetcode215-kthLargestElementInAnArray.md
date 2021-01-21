---
title: Leetcode215-kthLargestElementInAnArray
categories: leetcode
tags: [Sort, Priority Queue, Bloomberg, TikTok]
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

### Solution 1: Heap

**Time Complexity:** $$O(NlogK)$$

**Space Complexity:** $$O(K)$$

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

### Solution 2: Quick Select

**Time Complexity:** $$O(N)$$, worest case: $$O(N^2)$$

**Space Complexity:** $$O(1)$$

```java
class Solution{
    public int findKthLargest(int[] nums, int k) {
        return quickSelect(nums, 0, nums.length - 1, k);
    }

    int quickSelect(int[] nums, int low, int high, int k) {
        int pivot = low;

        // use quick sort's idea
        // put nums that are <= pivot to the left
        // put nums that are  > pivot to the right
        for (int j = low; j < high; j++) {
            if (nums[j] <= nums[high]) {
            swap(nums, pivot++, j);
            }
        }
        swap(nums, pivot, high);
        
        // count the nums that are > pivot from high
        int count = high - pivot + 1;
        // pivot is the one!
        if (count == k) return nums[pivot];
        // pivot is too small, so it must be on the right
        if (count > k) return quickSelect(nums, pivot + 1, high, k);
        // pivot is too big, so it must be on the left
        return quickSelect(nums, low, pivot - 1, k - count);
    }
    void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

<hr />