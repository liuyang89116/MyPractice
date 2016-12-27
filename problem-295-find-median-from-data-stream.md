# Problem 295: Find Median from Data Stream

> https://leetcode.com/problems/find-median-from-data-stream/

----------
##思路
* 这道题十分巧妙。要想得到中位数，那么我们可以把一串数从中间一劈为二，如果左右的个数相同，那么左边右边加起来除以二；如果不相等，那么取you