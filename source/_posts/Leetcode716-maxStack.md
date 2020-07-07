---
title: Leetcode716-maxStack
categories: leetcode
tags: [Stack, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 16:06:43
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Design a max stack that supports push, pop, top, peekMax and popMax.

1. push(x) -- Push element x onto stack.
2. pop() -- Remove the element on top of the stack and return it.
3. top() -- Get the element on the top.
4. peekMax() -- Retrieve the maximum element in the stack.
5. popMax() -- Retrieve the maximum element in the stack, and remove it. If you find more than one maximum elements, only remove the top-most one.

## Example
```
MaxStack stack = new MaxStack();
stack.push(5); 
stack.push(1);
stack.push(5);
stack.top(); -> 5
stack.popMax(); -> 5
stack.top(); -> 1
stack.peekMax(); -> 5
stack.pop(); -> 1
stack.top(); -> 5
```

**Note:**
1. -1e7 <= x <= 1e7
2. Number of operations won't exceed 10000.
3. The last four operations won't be called when stack is empty.

## Solution
```java
class MaxStack {

    private Stack<Integer> st;
    private Stack<Integer> stMax;
    /** initialize your data structure here. */
    public MaxStack() {
        st = new Stack<>();
        stMax = new Stack<>();
    }
    
    public void push(int x) {
        st.push(x);
        if (stMax.isEmpty())
            stMax.push(x);
        else{
            if (x >= stMax.peek())
                stMax.push(x);
            else stMax.push(stMax.peek());
        }
    }
    
    public int pop() {
        stMax.pop();
        return st.pop();
    }
    
    public int top() {
        return st.peek();
    }
    
    public int peekMax() {
        return stMax.peek();
    }
    
    public int popMax() {
        Stack<Integer> temp = new Stack<>();
        int max = stMax.peek();
        while(st.peek() != max){
            temp.push(st.pop());
            stMax.pop();
        }
        st.pop();
        stMax.pop();    
        while(!temp.isEmpty()){
            this.push(temp.pop());
        }
        
        return max;
    }
}

/**
 * Your MaxStack object will be instantiated and called as such:
 * MaxStack obj = new MaxStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.peekMax();
 * int param_5 = obj.popMax();
 */
```

<hr />