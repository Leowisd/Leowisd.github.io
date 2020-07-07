---
title: Copy & Array Creating In Python
tags: [Python, Copy, shadow copy, deep copy, Array creating]
date: 2018-10-04 21:05:59
categories: Python
description: Details about copy problems and Array creating problems in python
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvx5bbi8asj212w0m8my4.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Array Creating

At first, let's see some examples.

```python
>>> l = [[0 for i in range(5)] for i in range (5)]
>>> l
[[0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]
>>> l
[[10, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]
>>> n = [[0]*5 for i in range (5)]
>>> n
[[0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]
>>> n[0][0] = 10
>>> n
[[10, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]
>>> N = [[0]*5]*5
>>> N
[[0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]
>>> N[0][0] = 10
>>> N
[[10, 0, 0, 0, 0], [10, 0, 0, 0, 0], [10, 0, 0, 0, 0], [10, 0, 0, 0, 0], [10, 0, 0, 0, 0]]
>>> L1 = [0 for i in range (5)]
>>> L = [L1 for i in range(5)]
>>> L
[[0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]
>>> L[0][0] = 10
>>> L
[[10, 0, 0, 0, 0], [10, 0, 0, 0, 0], [10, 0, 0, 0, 0], [10, 0, 0, 0, 0], [10, 0, 0, 0, 0]]
```

It's obvious that changing the (0,0) element of list l and n will not change other elements, but changing the first element of list N and L will change each sub-list's first element.

The reason of such situation is sub-lists in l and n have different addresses but in N and L have the same address, which is releated to the concept of copy in python.

What above also shows the two methods creating n-dimensional arraies: coping list [0]*n and assigning in loop

#### [0]*n

[[0] * a] * b will create a 2-dimensional array with a*b

And the [0, 0, 0] * a is a shadow copy.

Let's see an example:

```python
>>> A=[0]*4
>>> A
[0, 0, 0, 0]
>>> A[0]=1
>>> A
[1, 0, 0, 0]

>>> A=[[0]*3]*4
>>> A
[[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
>>> A[0][1]=1
>>> A
[[0, 1, 0], [0, 1, 0], [0, 1, 0], [0, 1, 0]]
>>> A[1][1]=0
>>> A
[[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
```

#### Assigning in loop

Using for loop to initialize the array can avoid the shadow copy problem.

```python
>>> B=[[0 for i in range(2)]for j in range(3)]
>>> B
[[0, 0], [0, 0], [0, 0]]
>>> B[0][1]=1
>>> B
[[0, 1], [0, 0], [0, 0]]
```

To summarize, the recommanded way to initialize an array is using for loop, which can avoid the shadow copy problem in [0]*n

## Assignment

First, let's talk about ASSISGNMENT in python.

In Python, the assignment of an object is a simple transference of object reference(memory address), which is different from C++.

For assignment, there are some points we need to know:

* Assignment is assigning the address of an object to a variable which points to the address (old wine in old bottle).
* Modifying the immutable objects (STR, tuple) need to open up new space.
* Modifying variable objects (list, etc.) do not need to open up new space.

Let's see an example:
```python
will = ["Will", 28, ["Python", "C#", "C++"]]
wilber = will
print id(will)
print will
print [id(ele) for ele in will]
print id(wilber)
print wilber
print [id(ele) for ele in wilber]
 
will[0] = "Wilber"
will[2].append("Markdwon")
print id(will)
print will
print [id(ele) for ele in will]
print id(wilber)
print wilber
print [id(ele) for ele in wilber]
```

Result is:
```python
54638912
['Will', 28, ['Python', 'C#', 'C++']]
[60622688, 1882077872, 54638752]
54638912
['Will', 28, ['Python', 'C#', 'C++']]
[60622688, 1882077872, 54638752]

54638912
['Wilber', 28, ['Python', 'C#', 'C++', 'Markdwon']]
[60622944, 1882077872, 54638752]
54638912
['Wilber', 28, ['Python', 'C#', 'C++', 'Markdwon']]
[60622944, 1882077872, 54638752]
```
It's easy to find wilber is will, wilber[i] is will[i]

One thing to note here: str is an immutable object, so when we change the will[0], it will open a new space. However, list is a variable object, so the address of will[2] does not change. 

## Shadow Copy

Shallow copy just copies the addresses of the elements in the container.

Let's see some codes:

```python
>>> a=['hello',[1,2,3]]
>>> b=a[:] # b = copy.copy(a)
>>> id(a)
54637832
>>> id(b)
54638992
>>> [id(x) for x in a]
[55792504, 6444104]
>>> [id(x) for x in b]
[55792504, 6444104]
>>> a[0]='world'
>>> a[1].append(4)
>>> a
['world', [1, 2, 3, 4]]
>>> b
['hello', [1, 2, 3, 4]]
```
Shallow copy creates a new variable or container in another address, but the addresses of the elements in the container are copies of the addresses of the elements of the source object, which means, the new container points to old elements (old wine in a new bottle).

**Shadow copy will be appied when we use following operations:**

* Using slice operation [:]
* Using factory functions (list/dir/set)
* Using copy() function from copy module
  

## Deep Copy

A copy is copied completely, and the addresses inside the container are totally different.

```python
>>> from copy import deepcopy
>>> a=['hello',[1,2,3]]
>>> b=deepcopy(a)
>>> id(a)
60715456
>>> id(b)
54637832
>>> [id(x) for x in a]
[55792504, 55645000]
>>> [id(x) for x in b]
[55792504, 58338824]
>>> a[0]='world'
>>> a[1].append(4)
>>> a
['world', [1, 2, 3, 4]]
>>> b
['hello', [1, 2, 3]]
```

Deep copy createa a new variable or container in another address, and the addresses of elements in the container is also new. The two things just have the same values. That is to say, new wine in a new bottle.

## Special circumstances of copying

* For objects are not container, such as string, number and other 'atom' objects, there is no copy. What's generated is refernece of object. That's to say, obj is copy.copy(obj), obj is copy.deepcopy(obj).
* If a tuple contains 'atom' elements only, it can only be shadow copied even it uses deepcopy. For example:
  ```python
  >>> a = (1, 2, 3, 4)
  >>> b = copy.copy(a) 
  >>> a is b
  True
  >>> a = (1, 2, 3, 4)
  >>> b = copy.deepcopy(a)
  >>> a is b
  True
  ```

<hr />