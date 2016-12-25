# Problem 57: Insert Interval

> https://leetcode.com/problems/insert-interval/

-----------
##思路
* 先定位插入的起点：用原来区间的每个 end 和 新区间的 start 比，如果没有交集，就可以停下了，开始 merge
* 插入的时候：用原来区间的每个 start 和新区间的 end 比，然后建立（merge）新区间

----------


```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        int i = 0;
        while (i < intervals.size() && intervals.get(i).end < newInterval.start) i++;
        while (i < intervals.size() && intervals.get(i).start <= newInterval.end) {
            newInterval = new Interval(Math.min(intervals.get(i).start, newInterval.start), Math.max(intervals.get(i).end, newInterval.end));
            intervals.remove(i);
        }
        intervals.add(i, newInterval);
        
        return intervals;
    }
}
```
------
##易错点
1. List add() 方法
```java
public void add(int index, E element)
```
```java
intervals.add(i, newInterval);
```
按照 index 插入

































