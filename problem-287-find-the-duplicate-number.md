# Problem 287: Find the Duplicate Number

> [https://leetcode.com/problems/find-the-duplicate-number/\#/description](https://leetcode.com/problems/find-the-duplicate-number/#/description)

---

## 思路

* 直观的思路就是用一个 HashSet 来存所有的元素，如果有重复就响应。这样的话，时间复杂度是 $$ O(n) $$，空间复杂度是 $$ O(n) $$
* 如果用 $$ O(1) $$ 的空间如何解决呢？ - Binary Search!
* 先找出中间元素 mid，然后遍历整个数组，如果小于 mid 的元素的 count 大于 mid，**说明在左半边有重复元素！反之，重复元素就在右边。**

--------

## 复杂度

* 时间复杂度：$$ O(nlogn) $$
* 空间复杂度：$$O(1)$$

------

```java
public class Solution {
    public int findDuplicate(int[] nums) {
        int start = 1, end = nums.length - 1, mid;
        
        while (start < end) {
            mid = start + (end - start) / 2;
            
            int count = 0;
            for (int num : nums) {
                if (num <= mid) count++;
            }
            
            if (count > mid) {
                end = mid;
            } else {
                start = mid + 1;
            }
        }
        
        return start;
    }
}
```



