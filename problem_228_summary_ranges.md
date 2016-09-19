# Problem 228: Summary Ranges

> https://leetcode.com/problems/summary-ranges/

-----------
##思路
* 着重在于判断是否到了最后一个元素

-----------
```java
public class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> res = new ArrayList<String>();
        for (int i = 0; i < nums.length; i++) {
            int val = nums[i];
            while (i < nums.length - 1 && nums[i + 1] - nums[i] == 1) i++;
            if (val != nums[i]) {
                res.add(val + "->" + nums[i]);
            } else {
                res.add(val + "");
            }
        }
        
        return res;
    }
}
```
-----
##易错点
1. int 转 String
```java
res.add(val + "");
```

