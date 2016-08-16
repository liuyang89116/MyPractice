# Problem 81: Search in Rotated Sorted Array II


> https://leetcode.com/problems/search-in-rotated-sorted-array-ii/

--------------------------------------------
##思路
* 这个问题在面试中不会让实现完整程序。只需要举出能够最坏情况的数据是 [1,1,1,1... 1] 里有一个0即可。
* 在这种情况下是无法使用二分法的，复杂度是O(n)。因此写个for循环最坏也是O(n)，那就写个for循环就好了。如果你觉得，不是每个情况都是最坏情况，你想用二分法解决不是最坏情况的情况，那你就写一个二分吧。
* 反正面试考的不是你在这个题上会不会用二分法。这个题的考点是你想不想得到最坏情况。

--------------------------------------
```java
public class Solution {
    public boolean search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return false;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (target == nums[i]) {
                return true;
            }
        }
        return false;
    }
}
```