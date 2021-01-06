---
title: Leetcode239-slidingWindowMaximum
categories: leetcode
tags: [Heap, Deque, Amazon, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-08 11:32:45
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

## Example
```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```
**Note:**
You may assume k is always valid, 1 ≤ k ≤ input array's size for non-empty array.

**Follow up:**
Could you solve it in linear time?

## Solution
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k == 0 || nums.length < k) return new int[]{};
        
        int[] res = new int[nums.length - k + 1];
        
        // Method 2: O(N), q stores the index.
        Deque<Integer> q = new LinkedList<>();
        for (int i = 0; i < nums.length; i++){
            // remove numbers out of range k
            while(!q.isEmpty() && (q.peek() < i- k + 1)){
                q.poll();
            }
            // remove smaller numbers in k range as they are useless
            while(!q.isEmpty() && (nums[q.peekLast()] < nums[i])){
                q.pollLast();
            }
            
            q.offer(i);
            if (i >= k-1){
                res[i-k+1] = nums[q.peek()];
            }
            
        }
        
        
//         Method: HashMap and PriorityQueue, O(N*Klog(K))
//         HashMap<Integer, Integer> map = new HashMap<>();
//         PriorityQueue<Integer> pq = new PriorityQueue<>((a,b) -> b-a);
//         for (int i = 0; i < nums.length; i++){
//             if (i < k){
//                 pq.offer(nums[i]);
//                 map.put(nums[i], map.getOrDefault(nums[i], 0)+1);
//             }
//             else{
//                 int tmp = pq.peek();
//                 while (!map.containsKey(tmp)){
//                     pq.poll();
//                     tmp = pq.peek();
//                 }
//                 res[i-k] = tmp;
                
//                 map.put(nums[i-k], map.get(nums[i-k])-1);
//                 if (map.get(nums[i-k]) == 0) map.remove(nums[i-k]);

//                 map.put(nums[i], map.getOrDefault(nums[i], 0)+1);
//                 pq.offer(nums[i]);
//             }
//         }
//         int last = pq.poll();
//         while (!map.containsKey(last)){
//             last = pq.poll();
//         }
//         res[nums.length - k] = last;
        
        return res;        
    }
}
```

<hr />