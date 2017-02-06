# Problem 198: House Robber

> https://leetcode.com/problems/house-robber/

-----
##思路
* 维护四个变量：prevNotRobbed, prevRobbed, currNotRobbed, currRobbed
* 对于每一户当前的人家，存在偷或者不偷。如果偷，好，那么之前一户肯定不能偷了；如果不偷，那么它的值在之前偷或者不偷之间取最大
* 每次判断完以后，更新 prev 值。

----


```java
public class Solution {
    public int rob(int[] nums) {
        int prevNotRobbed = 0;
        int prevRobbed = 0;
        
        for (int i = 0; i < nums.length; i++) {
            int currRobbed = nums[i] + prevNotRobbed;
            int currNotRobbed = Math.max(prevNotRobbed, prevRobbed);
            
            prevNotRobbed = currNotRobbed;
            prevRobbed = currRobbed;
        }
        
        return Math.max(prevNotRobbed, prevRobbed);
    }
}
```

