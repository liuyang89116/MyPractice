# Problem 217: Contains Duplicate

> https://leetcode.com/problems/contains-duplicate/

-------
##思路
* hashset 的一道题，没啥好说的，直接实现

----------
```java
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> hs = new HashSet<Integer>();
        for (Integer i : nums) {
            if (hs.contains(i)) {
                return true;
            } else {
                hs.add(i);
            }
        }
        
        return false;
    }
}
```


