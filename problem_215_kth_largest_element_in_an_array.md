# Problem 215: Kth Largest Element in an Array


> https://leetcode.com/problems/kth-largest-element-in-an-array/

-------------
##思路
* 这道题可以用 heap 快速做出，但其并不是考点。
* 这道题的考点还是在 O(N) 的时间内，用额外 O(1) 的时间找出结果。所以我们考虑用 Quick Sort 的方法。

