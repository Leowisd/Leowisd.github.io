---
title: Leetcode1235-Maximum Profit In Job Scheduling
categories: leetcode
tags: [DP, Binary Search, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-04 22:07:19
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

We have n jobs, where every job is scheduled to be done from startTime[i] to endTime[i], obtaining a profit of profit[i].

You're given the startTime , endTime and profit arrays, you need to output the maximum profit you can take such that there are no 2 jobs in the subset with overlapping time range.

If you choose a job that ends at time X you will be able to start another job that starts at time X.

## Example
**Example 1:**
![](https://assets.leetcode.com/uploads/2019/10/10/sample1_1584.png)
```
Input: startTime = [1,2,3,3], endTime = [3,4,5,6], profit = [50,10,40,70]
Output: 120
Explanation: The subset chosen is the first and fourth job. 
Time range [1-3]+[3-6] , we get profit of 120 = 50 + 70.
```
**Example 2:**
![](https://assets.leetcode.com/uploads/2019/10/10/sample22_1584.png)
```
Input: startTime = [1,2,3,4,6], endTime = [3,5,10,6,9], profit = [20,20,100,70,60]
Output: 150
Explanation: The subset chosen is the first, fourth and fifth job. 
Profit obtained 150 = 20 + 70 + 60.
```
**Example 3:**
![](https://assets.leetcode.com/uploads/2019/10/10/sample3_1584.png)
```
Input: startTime = [1,1,1], endTime = [2,3,4], profit = [5,6,4]
Output: 6
``` 

**Constraints:**
* 1 <= startTime.length == endTime.length == profit.length <= 5 * 10^4
* 1 <= startTime[i] < endTime[i] <= 10^9
* 1 <= profit[i] <= 10^4

## Solution

* Time Complexity: $$O(NlogN)$$ in total, sort $$O(NlogN)$$, binary search $$O(NlogN)$$
* Space Complexity: $$O(N)$$

### Solution 1: DP + Binary Search

Sort the jobs by endTime.

dp[time] = profit means that within the first time duration,

we cam make at most profit money.

Intial dp[0] = 0, as we make profit = 0 at time = 0.

For each job = [s, e, p], where s,e,p are its start time, end time and profit,

Then the logic is similar to the knapsack problem.

If we don't do this job, nothing will be changed.

If we do this job, binary search in the dp to find the largest profit we can make before start time s.

So we also know the maximum cuurent profit that we can make doing this job.

Compare with last element in the dp,
we make more money,

it worth doing this job,

then we add the pair of [e, cur] to the back of dp.

Otherwise, we'd like not to do this job.

```java
class Solution {
    class Job{
        int start;
        int end;
        int profit;
        
        public Job(int s, int e, int p){
            start = s;
            end = e;
            profit = p;
        }
    }
    
    class DpEntry{
        int end;
        int profit;
        public DpEntry(int e, int p){
            end = e;
            profit = p;
        }
    }
    
    public int jobScheduling(int[] startTime, int[] endTime, int[] profit) {
        int n = startTime.length;
        Job[] jobs = new Job[n];
        for (int i = 0; i < n; i++){
            jobs[i] = new Job(startTime[i], endTime[i], profit[i]);
        }
        Arrays.sort(jobs, (a, b) -> (a.end - b.end));
        
        List<DpEntry> dp = new ArrayList<>();
        dp.add(new DpEntry(0, 0));
        for (Job job: jobs){
            int cur = dp.get(helper(dp, job.start + 1)).profit + job.profit;
            if (cur > dp.get(dp.size() - 1).profit){
                dp.add(new DpEntry(job.end, cur));
            }
        }
        return dp.get(dp.size() - 1).profit;
    }
    
    private int helper(List<DpEntry> dp, int target){
        int left = 0;
        int right = dp.size() - 1;
        while(left + 1< right){
            int mid = left + (right - left) / 2;
            if (dp.get(mid).end < target){
                left = mid;
            }
            else right = mid - 1;
        }
        return dp.get(right).end < target ? right : left;
    }
}
```

### Solution 2: DP + TreeMap
```java
    public int jobScheduling(int[] startTime, int[] endTime, int[] profit) {
        int n = startTime.length;
        int[][] jobs = new int[n][3];
        for (int i = 0; i < n; i++) {
            jobs[i] = new int[] {startTime[i], endTime[i], profit[i]};
        }
        Arrays.sort(jobs, (a, b)->a[1] - b[1]);
        TreeMap<Integer, Integer> dp = new TreeMap<>();
        dp.put(0, 0);
        for (int[] job : jobs) {
            int cur = dp.floorEntry(job[0]).getValue() + job[2];
            if (cur > dp.lastEntry().getValue())
                dp.put(job[1], cur);
        }
        return dp.lastEntry().getValue();
    }
```

<hr />