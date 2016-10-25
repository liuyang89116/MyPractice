# Problem 35: Search Insert Position


> https://leetcode.com/problems/search-insert-position/

--------------------------------------------------------------

##思路
这道题其实就是二分法的变种题

不难，但是要细心

-------------------------------------------------------------
```java
public class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end) {
            int mid =  start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }

        if (target <= nums[start]) {
            return start;
        }
        if (target <= nums[end]) {
            return end ;
        } else {
            return end + 1;
        }
    }
}
```
--------------------------------------
##易错点
1. 判断条件的部分，用target和两个点比较，其实就是相当于是一个数轴分段的问题，写成 ```target <= nums[start]```比较容易理解
2. 最后比较的部分，很容易漏掉括号，写成 ```target <= start```，立马就错了
3. 细心！
   ```java
   if (target <= nums[end]) {
       return end ;
   }
   ```
   target比nums[end]小，他的位置是end，**不是end-1！**
   就像跑步比赛一样，你超过了第二名，你不是第一名，你就是第二名！！
4. 最后的部分非常容易出错。按理说 left, right 两根指针，最后可以分成三段。就按照这三段来划分区间给结论，不要偷懒，一偷懒就会错。尤其是 corner cases： ```[1], [1,2]```等等
