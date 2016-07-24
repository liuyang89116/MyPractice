# Problem 34: Search for a Range


> https://leetcode.com/problems/search-for-a-range/

--------------------------------------------------------------------

##思路
这道题要求的复杂度是O(logn)，所以很明显地应该想到二分法。而这道题求的是一个range，但是一个二分法问题定位的是一个值的点。所以*我们可以用两次二分法分别定位这两个点！*

```java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return new int[] {-1, -1};
        }

        int[] result = new int[2];

        //search left bound
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] >= target) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (nums[start] == target) {
            result[0] = start;
        } else if (nums[end] == target) {
            result[0] = end;
        } else {
            return new int[] {-1, -1};
        }

        //search right bound
        start = 0;
        end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] > target) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (nums[end] == target) {
            result[1] = end;
        } else if (nums[start] == target) {
            result[1] = start;
        } else {
            return new int[] {-1, -1};
        }

        return result;
    }
}
```
##易错点

1. 首先check数组的空指针问题
2. 左右指针的判断条件可以合并
   ```java
   if (nums[mid] >= target) {
       end = mid;
   } else {
       start = mid;
   } 
   ```

3. 返回值的时候，一定要加“new”
   ```java
   return new int[] {-1, -1};
   ```





















