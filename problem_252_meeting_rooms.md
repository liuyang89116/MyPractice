# Problem 252: Meeting Rooms

> https://leetcode.com/problems/meeting-rooms/

----------
##思路
* 这道题的思路在于：当前的 start 要大于之前的 end，（**注意： 是之前的 end 而不是上一个 end，因为有可能最前面有一个会议非常地长**）。这样可以保证会议之间是有空隙的。
* 但是在这之前，这道题的关键在于按照会议开始的时间来 sort 这个数组。这就需要用到 Comparator 了。

------------
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
    public boolean canAttendMeetings(Interval[] intervals) {
        if (intervals == null || intervals.length == 0) {
            return true;
        }
        
        Arrays.sort(intervals, new Comparator<Interval>() {
            public int compare(Interval i1, Interval i2) {
                return i1.start - i2.start;
            }
        });
        int end = intervals[0].end;
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i].start < end) {
                return false;
            }
            end = Math.max(end, intervals[i].end);
        }
        
        return true;
    }
}
```
--------
##易错点
1. Comparator 的写法
```java
Arrays.sort(intervals, new Comparator<Interval>() {
       public int compare(Interval i1, Interval i2) {
             return i1.start - i2.start;
       }
});
```
2. 要比的是之前最长的 end
```java
end = Math.max(end, intervals[i].end);
```




















