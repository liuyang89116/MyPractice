# Summary 1: Binary Search Template

```java
/**
    Binary Search Template
*/

public class Solution {
    public int findPosition(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                return mid;
            } else {
                end = mid;
            }
        }

        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        return -1;
    }
}
```
-----------------------------------------
##分析
1. 数组要敏感，一看数组，就要想到corner case
   ```java
   if (nums == null || nums.length == 0) {
       return -1;
   }
   ```
2. 中间数怎么找
   ```java
   int mid = start + (end - start) / 2;
   ```
   这样是为了防止数据溢出
3. while条件
   ```java
   while (start + 1 < end) {
    
   }
   ```
   这样是为了配合最后的check值更方便
4. 结尾check目标值
   ```java
   if (nums[start] == target) {
       return start;
   }
   if (nums[end] == target) {
       return end;
   }
   ```
5. 最后剩下 left， right 两根指针，但是有三个区间都是可能的，要想到 

   
   
   