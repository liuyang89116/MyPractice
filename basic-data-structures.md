# Basic Data Structures

## 常考的数据结构

```
Array, ArrayList

String, StringBuffer

LinkedList

HashMap, HashSet

Stack and Queue

Heap: PriorityQueue

Grpah
```

```
Tree:

BT: binary tree

BST: binary search tree,

Balanced BST (red-black tree): TreeMap, TreeSet

Trie: prefix tree

```
* Array 和 Linkedlist 是最最基本的数据结构，因为他们可以构造很多其他的数据结构，比如 String (C语言里String就是字符数组），HashMap, Stack 和 Queue (**Java** 里 Queue 就是 LinkedList 实现了 Queue 的 interface; **Ruby** 里 stack 和 queue 都是 array）, 以及 Heap。
* Heap is a **tree logically**, but **array physically**.
* HashMap, Stack 和 Queue 通常不会出现在问题里的数据结构中，因此一般作为solution 的数据结构。但是 面试中也常会让你实现这三种数据结构，另外就是 **CC150 的3.2 和 3.5 都是典型的 Stack 和 Queue 的题**。Leetcode中并不涵盖这些内容，这几种数据结构在 Leetcode 中都是作为 solution数据结构出现的(没有的原因是这些题目不太适合 OJ，因此需要单独练习）。

------------------
##常考的算法

```
Sort: quick sort, merge sort, count sort, heap sort, bucket sort,
radix sort, external sort, K selection etc.

Merge: 2 array/list merge, k-way merge, interval merge
etc.

Binary search:

Stack:

Recursion and Iteration:

DFS：pre-order, in-order, post-order for trees

BFS: 需要用Queue

DP: Top down and bottom up

Greedy:

Toposort: 需要用Queue

```
* Leetcode 并没有包含各种 sort 算法，而通常面试很少让你直接去实现 sort 算法，但是大部分的相关编程技巧是包含在很多题目当中的, 比如 **quick sort** 的two pointers。
* Merge 跟 sort 是紧密相关的，单独拿出来是因为有很多这个类型的题目，需要一起总结。Merge 操作的对象基本都是已经排好序的。
* Stack 虽说是数据结构，但是一般出现在 solution 里，因此代表了一类算法.
* Toposort面试作为难题也很有可能遇到.




















