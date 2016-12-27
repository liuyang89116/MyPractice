# Problem 128: Longest Consecutive Sequence

> https://leetcode.com/problems/longest-consecutive-sequence/

-------
##思路
* 用一个 HashMap 来记录每个数，极其 neighbor 的个数。当我们遍历数组当中的每一个数 num 的时候，我们 check num - 1 和 num + 1 是否也在 map 里。
* 如果在的化，把 left 和 right 的个数都加给当前的 num，同时更新 map。
* 最后如果 left 和 right 不为 0 的话，我们可以 extend 我们的边界，让一个串儿的元素的边界的个数也更新，为以后的遍历省事儿。

------------
##复杂度
* Time: `O(n)`

----------


```java
public class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int max = 0;
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (Integer num : nums) {
            if (map.containsKey(num)) continue;
            int left = (map.containsKey(num - 1) ? map.get(num - 1) : 0);
            int right = (map.containsKey(num + 1) ? map.get(num + 1) : 0);
            int count = left + right + 1;
            max = Math.max(max, count);
            map.put(num, count);
            
            if (left > 0) {
                map.put(num - left, count);
            }
            if (right > 0) {
                map.put(num + right, count);
            }
        }
        
        return max;
    }
}
```



