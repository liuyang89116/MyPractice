# Problem 349: Intersection of Two Arrays


> https://leetcode.com/problems/intersection-of-two-arrays/

----------
##思路
* 思路很直接，就是两次 HashSet

---------------
```java
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> set = new HashSet<Integer>();
        HashSet<Integer> resSet = new HashSet<Integer>();
        for (Integer i : nums1) {
            set.add(i);
        }
        for (Integer i : nums2) {
            if (set.contains(i)) {
                resSet.add(i);
            }
        }
        int[] res = new int[resSet.size()];
        int index = 0;
        for (Integer i : resSet) {
            res[index++] = i;
        }
        
        return res;
    }
}
```
