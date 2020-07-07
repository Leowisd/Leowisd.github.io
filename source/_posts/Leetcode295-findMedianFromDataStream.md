---
title: Leetcode295-findMedianFromDataStream
categories: leetcode
tags: [Design, Heap, Amazon, Bloomberg, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-06 09:36:20
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

For example,
[2,3,4], the median is 3

[2,3], the median is (2 + 3) / 2 = 2.5

Design a data structure that supports the following two operations:

* void addNum(int num) - Add a integer number from the data stream to the data structure.
* double findMedian() - Return the median of all elements so far.

## Example
```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```
Follow up:

1. If all integer numbers from the stream are between 0 and 100, how would you optimize it?
2. If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?
## Solution
```java
class MedianFinder {

    PriorityQueue<Integer> min;
    PriorityQueue<Integer> max;
    // List<Integer> nums;
    /** initialize your data structure here. */
    public MedianFinder() {
        // nums = new ArrayList<>();
        min = new PriorityQueue<>();
        max = new PriorityQueue<>((a,b) -> b-a);
    }
    
    public void addNum(int num) {
        max.offer(num);
        min.offer(max.poll());
        if (max.size() < min.size())
            max.offer(min.poll());
        
        // nums.add(num);
    }
    
    public double findMedian() {
        if (min.size() == max.size()) return (max.peek() + min.peek())/2.0;
        else return max.peek();
        
        // Collections.sort(nums);
        // int len  = nums.size();
        // if (len % 2 == 0) return (nums.get(len/2)+nums.get(len/2-1))/2.0;
        // else return nums.get(len/2);
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

<hr />