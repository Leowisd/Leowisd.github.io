---
title: 'Useful C# Data Structures'
tags: [C#, Data Structure, Array, ArrayList, List<>, Linked List, Queue, Stack, Dictionary]
date: 2018-10-03 20:43:56
categories: C#
description: Some usual data structures 
image:
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvw28hncf5j212w0m8dh3.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Usual Data Structures

#### Array

Array is the simplest data structure in C#. It has the following characteristics:

* Array is stored in continuous memory.
* The contents of the array are all of the same type.
* Array can be accessed directly through subscript.

The creation of Array:
```C#
int size = 5;
int[] array = new int[size];
```

Because Array is stored in contiguous memory, its indexing speed is very fast. The time to access an element is constant, which means it is independent of the number of elements in the array. The assignment and modification of elements is also very simple.

```C#
string[] test2 = new string[3];
//Assisgnmennt
test2[0] = "yao";
test2[1] = "y";
test2[2] = "f";
//Modification
test2[0] = "yaoyf";
```

But if there are advantages, then it will be accompanied by shortcomings. Because it is continuous storage, it is inconvenient to insert new elements between the two elements. And as the code above shows, when you declare a new array, you have to specify its length, which has the potential problem of wasting memory when we declare it too long, and the risk of overflowing when we declare it too short.

In order to avoid such disadvantages， there is a data structure called ArrayList.

#### ArrayList

ArrayList is part of the System.Collections namespace, so you must introduce System.Collections to use it. As mentioned above, ArrayList solves some of the shortcomings of arrays.

* It is not necessary to specify the length of an ArrayList when it is declared, because the length of an ArrayList object is dynamically increased and reduced according to the data stored therein.
* ArrayList can store different types of elements. This is because ArrayList treats all its elements as Object.

```C#
ArrayList test3 = new ArrayList();
//Add new element
test3.Add("yao");
test3.Add("y");
test3.Add("f");
test3.Add("is");
test3.Add(22);
//Modification
test3[4] = 666;
//Delete
test3.RemoveAt(4);
```

Disadvantages:
* ArrayList is not type safe. Because different types are treated as objects, it's very likely that type mismatches occur when ArrayList is used.
* Boxing does not occur when an array stores value types, but because ArrayList treats all types as Objects, it is inevitable that boxing occurs when inserting value types, and unboxing occurs when index values are taken. There will be time wastage, that is, the reduction of efficiency.

#### List<T>

In order to overcome the shortcomings of ArrayList insecure types and boxed and unboxed, the concept of generics was introduced as a new array type. It is also an array type commonly used in work. Similar to Array List, the length can be flexibly changed. The biggest difference is that when we declare a List collection, we also need to declare the object type of the data in the List collection for it. This is similar to Array , which is implemented internally in List <T>.

```C#
List<string> test4 = new List<string>();  
//Add new element  
test4.Add(“abcdefg”);  
test4.Add(“1234556”);  
//Modification
test4[1] = “WeAreTheBest”;  
//Remove element  
test4.RemoveAt(0); 
```

The best advantages of List are:

* That can ensure type safety.
* The operation of boxing and unboxing is cancelled.
* It combines the advantages of fast access to Array and the flexibility of length to ArrayList.

#### LinkedList<T>

That's the linked list. The biggest difference from the above array types is that the linked list may not be sequenced in memory storage. This is because the list is arranged by pointing to the next element from the previous element, so it may not be accessible by subscript.

Since the greatest feature of linked lists is that the space stored in memory is not necessarily continuous, the greatest advantages and disadvantages of linked lists over arrays are obvious:

* Inserting or deleting nodes into the linked list does not need to adjust the capacity of the structure, because it's not consecutive storage. It's determined by the pointer of each object, so adding and deleting elements has an advantage over arrays.
* Linked lists are good for adding new elements in situations where ordering is required. Here's a comparison with arrays. For example, adding new elements at a certain location in the middle of an array may require moving many elements, but for a linked list it may be just the direction of several elements changes.
* There are advantages and disadvantages, because it is not necessarily sequential in memory space, so access to the subscript can not be used, but must start from the beginning node, traverse the next node until the target is found. So when you need to quickly access objects, arrays are undoubtedly more advantageous.

In summary, the linked list is suitable for the unfixed number of elements.

#### Queue<T>

In a Queue <T> data structure, the first element inserted will be deleted first while the last element inserted will be deleted at last, so queues are also called FIFO - first in first out linear tables. Through the use of Enqueue() and Dequeue() those two methods to achieve access to Queue<T>.

Notes:

* First in first out scenario.
* By default, the initial capacity of Queue<T> is 32, and the growth factor is 2.0.
* When Enqueue is used, the length of the queue is judged to be sufficient. If not, the capacity is increased according to the growth factor. For example, when the initial 2.0 is used, the queue capacity is doubled. 

#### Stack<T>

As opposed to Queue <T>, we need Stack <T> when we need to use a LIFO data structure.

Notes:

* Last in first out scenario.
* The default capacity is 10.
* Use pop and push two methods to operate.

#### Dictionary<K,T>

Very fast to add, modify, delete and find elemets. However, in order to speed up, we use more memory space.

## When to use Which

**Array**: The number of elements and the need to use subscript can be considered, but List<T> is recommended.

**ArrayList**: It is not recommended. List<T> is recommended.

**List**: The number of elements is not sure. Most usual.

**LinkedList**: Linked list suitable for the number of elements is not fixed and need to constantly increase or decrease the node. The 2 sides can be increased or reduced.

**Queue**: FIFO

**Stack**: LIFO

**Dictionary**: Require pairs of keys and values. Fast operation.

<hr />