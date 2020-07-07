---
title: Leetcode155-minStack
categories: leetcode
tags: [Stack, Design, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-13 10:23:02
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push(x) -- Push element x onto stack.
* pop() -- Removes the element on top of the stack.
* top() -- Get the top element.
* getMin() -- Retrieve the minimum element in the stack.

## Example
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

## Solution

Only push the minVal when it need to updated

```java
class MinStack {

    private Stack<Integer> st;
    private int minVal;
    /** initialize your data structure here. */
    public MinStack() {
        st = new Stack<>();
        minVal = Integer.MAX_VALUE;
    }
    
    public void push(int x) {
        if (x <= minVal){
            st.push(minVal);
            minVal = x;
        }
        st.push(x);
    }
    
    public void pop() {
        if (minVal == st.pop()) minVal = st.pop();
    }
    
    public int top() {
        return st.peek();
    }
    
    public int getMin() {
        return minVal;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

<hr />