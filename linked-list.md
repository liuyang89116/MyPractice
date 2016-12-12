# Linked List

## 与 Two Pointers 紧密相关
首先 LeetCode 上几乎所有的 Linked list 的题目都可以用 two pointers 来解决，或者会用到 two pointers 这个基本编程技巧。因此 two pointers 跟 linked list 是紧密相关的。

## “List” 的特性
因为 LinkedList 和 Array/ArrayList 一样都具备有List的特性，因此很多题目都
出现在了两种数据结构上，或者说很多题目都是可以把这两种数据结构互换的。

```
lc2: Add Two Numbers

lc108: Convert Sorted List to Binary Search
Tree

lc57: Insert Interval

lc56: Merge Intervals

lc23: Merge k Sorted Lists

lc21: Merge Two Sorted Lists

lc83: Remove Duplicates from Sorted List

lc82: Remove Duplicates from Sorted List II

```

## iteration Vs. recursion
LinkedList 的题目大多自然而然使用 iteration 来解决的，但是我发现有些时候 iteration 比较容易出 bug，换成 recursion 实现更容易。面试的时候万一 iteration 卡住,可以换换 recursion 的思路。


## dummy node
dummy head 非常有用，可以使代码简洁很多，并且容易写 bug free 的 code。这个技巧可以大量使用。

##易错点
* two pointers loop 完之后常常会有一个收尾的工作，比如 Add Two Numbers 需要处理 carrier > 0 的情况。
* 在 swap 了 nodes 之后，新的 tail 需要把 next 置空，不然就出现死循环了。





















