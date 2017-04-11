# Problem 324: Wiggle Sort II

> [https://leetcode.com/problems/wiggle-sort-ii/\#/description](https://leetcode.com/problems/wiggle-sort-ii/#/description)

---

## 思路

> [https://discuss.leetcode.com/topic/41464/step-by-step-explanation-of-index-mapping-in-java](https://discuss.leetcode.com/topic/41464/step-by-step-explanation-of-index-mapping-in-java)

这个讲解不错！

* 这道题的思路和 sort color 类似，把所有的数分成三类：比 median 大，median， 比 median 小。这样的话我们先要找到 median
* $$O(n)$$ 时间 $$O(1)$$ space 找到 median，可以联想用 quick sort 找第 k 大的元素 `findKthLargest`
* 算 index 的方法很好: `(1 + 2 * index) % (n | 1)`，其中 `(n | 1)` 的意义在于找到最接近 n 的大于等于  n 的值

---

```java
public class Solution {
    public void wiggleSort(int[] nums) {
        int n = nums.length;
        int median = findKthLargest(nums, (n + 1) / 2);
        int left = 0, right = n - 1, i = 0;

        while (i <= right) {
            if (nums[getIndex(i, n)] > median) {
                swap(nums, getIndex(i, n), getIndex(left, n));
                left++;
                i++;
            } else if (nums[getIndex(i, n)] < median) {
                swap(nums, getIndex(i, n), getIndex(right, n));
                right--;
            } else {
                i++;
            }
        }
    }

    private int getIndex(int i, int n) {
        return (1 + 2 * i) % (n | 1);
    }

    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }

    private int findKthLargest(int[] nums, int k) {
        k = nums.length - k;
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int pos = partition(nums, left, right);
            if (pos == k) {
                break;
            } else if (pos < k) {
                left = pos + 1;
            } else {
                right = pos - 1;
            }
        }

        return nums[k];
    }

    private int partition(int[] nums, int left, int right) {
        int i = left, j = right + 1;
        int pivot = nums[left];
        while (true) {
            while (i < right && nums[++i] < pivot);
            while (j > left && nums[--j] >= pivot);
            if (i >= j) break;
            swap(nums, i, j);
        }
        swap(nums, left, j);

        return j;
    }
}
```



