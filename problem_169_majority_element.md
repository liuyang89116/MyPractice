# Problem 169: Majority Element


> https://leetcode.com/problems/majority-element/

------------
##思路
* 首先看清楚题目，majority number出现的次数是要**超过一半的**，有了这个前提才有了后面的解决方法
* 可以看作是投票选方案，赞成的投一票，不赞成就减一票，当目前的方案赞成数为0的时候，就换方案

-----------------
```java
public class Solution {
    public int majorityElement(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int count = 0; 
        int candidate = -1;
        for (int i = 0; i < nums.length; i++) {
            if (count == 0) {
                candidate = nums[i];
                count++;
            } else if (nums[i] == candidate) {
                count++;
            } else {
                count--;
            }
        }
        
        return candidate;
    }
}
```

----------
##易错点

1. 办事情的过程想清楚
```java
if (count == 0) {
         candidate = nums[i];
         count++;
} else if (nums[i] == candidate) {
         count++;
} else {
         count--;
}
```
赞成数为0,**换方案**，同时别忘了把当前的count数加1

























