# Problem 26: Remove Duplicates from Sorted Array


> https://leetcode.com/problems/remove-duplicates-from-sorted-array/

---------
##思路
![](Remove duplicates.jpg)

* 循环一遍数组，用size来标记不同的元素，相当于是两个指针，一个是```i```，一个是```size```
* 当```size```和```i```对应的值不一样的时候，```size```往前挪一个，并且把```i```的值copy过来