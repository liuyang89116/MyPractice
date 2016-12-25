# Problem 56: Merge Intervals

> https://leetcode.com/problems/merge-intervals/

-----------
##思路
* 首先对所有的 interval 进行排序，排序的原则按照 start 进行
* 然后遍历整个数组。如果中间有 overlap 的话，合并 end，然后删掉 next interval。

-------------
##复杂度
* sort 花费 `O(nlogn)` 的时间，便利（merge）花费`O(n)`的时间
* Time: `**O(nlogn)**`

---------


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
    public List<Interval> merge(List<Interval> intervals) {
        Collections.sort(intervals, new Comparator<Interval>() {
            public int compare(Interval i1, Interval i2) {
                return i1.start - i2.start;
            }
        });
        
        int index = 0;
        while (index < intervals.size() - 1) {
            Interval curr = intervals.get(index);
            Interval next = intervals.get(index + 1);
            if (next.start <= curr.end) {
                curr.end = Math.max(curr.end, next.end);
                intervals.remove(index + 1);
            } else { 
                index++;
            }
        }
        
        return intervals;
    }
}

```
-----
##易错点
1. Comparator 的应用以及 Collections 的排序
2. 遍历数组的时候别忘了边界
```java
while (index < intervals.size() - 1)
```



























