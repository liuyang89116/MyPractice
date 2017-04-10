# Problem 280: Wiggle Sort

> [https://leetcode.com/problems/wiggle-sort/\#/description](https://leetcode.com/problems/wiggle-sort/#/description)

---

![](/assets/280.png)

---

## 思路

> [https://discuss.leetcode.com/topic/57053/java-solution-with-explanation-thoughts/2](https://discuss.leetcode.com/topic/57053/java-solution-with-explanation-thoughts/2)

这个讲解不错！

* 我们有四种情况

![](/assets/280_1.png)

* 也就是说，对于奇数位 （实际上是 index 为奇数， 比如 nums 里面的第二个元素），它要看看是否比上一个大，如果不是

要交换；如果是偶数位，要看它是否比上一个元素小，否则要交换。

-------

```java
public class Solution {
    public void wiggleSort(int[] nums) {
        if (nums == null || nums.length == 0) return;
        
        for (int i = 1; i < nums.length; i++) {
            if (i % 2 == 0 && nums[i] > nums[i - 1]) {
                swap(nums, i - 1, i);
            }
            if (i % 2 != 0 && nums[i] < nums[i - 1]) {
                swap(nums, i - 1, i);
            }
        }
        
    }
    
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```











