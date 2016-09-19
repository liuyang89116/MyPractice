# Problem 219: Contains Duplicate II


> https://leetcode.com/problems/contains-duplicate-ii/

--------
##思路
* 这道题用 HashMap 来存元素

-------
```java
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        HashMap<Integer, Integer> hm = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (hm.containsKey(nums[i])) {
                int diff = i - hm.get(nums[i]);
                if (diff <= k) {
                    return true;
                } else {
                    hm.put(nums[i], i);
                }
            } else {
                hm.put(nums[i], i);
            }
        }
        
        return false;
    }
}
```
-----
1. 键值对谁是键谁是值
```java
hm.put(nums[i], i);
```
因为这样便于定位元素的 index
2. 这道题 tricky 的一点就是，当发现重复元素以后，有可能超过 k，但是！后面可能还有重复元素，不能直接退出  
eg： [1 0 1 1]，k = 1. 这时，后面两个 1 是满足条件的，所以我们要多一个判断  
```java
int diff = i - hm.get(nums[i]);
if (diff <= k) {
         return true;
} else {
         hm.put(nums[i], i);
}
```















