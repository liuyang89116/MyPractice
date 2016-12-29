# Problem 300: Longest Increasing Subsequence


> https://leetcode.com/problems/longest-increasing-subsequence/

---------------------------------
##思路
这篇讲得很好。
> https://discuss.leetcode.com/topic/39681/fast-java-binary-search-solution-with-detailed-explanation/2

* 主要的思路就是 DP + Binary Search
* traverse from 0 to len - 1, the DP array keep the longest sequence.
* if the val is bigger than largest in the dp array, add it to the end;
* if it is among the sequence, return the pos that bigger than pres, update the array with this position if val is smaller than dp[pos];
This is to keep the sequence element with the smallest number.
* 简单点说就是，相当于整理扑克，遍历数组，每次遍历完了都用二分法搜索一下应该放在 DP 数组的哪个位置。如果是递增的，插进去，如果不是，更换对应元素。举个例子：

```
10, 9, 2, 5, 3, 7, 101, 18

10 
9
2
2,5
2,3
2,3,7
2,3,7,101
2,3,7,18
```

----------------------------------------
##复杂度
* Time: `O(nlogn)`

---------------
* 最优解

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        int index = 0;
        for (int i = 1; i < nums.length; i++) {
            int pos = binarySearch(dp, nums[i], index);
            if (pos <= index) {
               dp[pos] = nums[i];
            } else {
                index = pos;
                dp[index] = nums[i];
            }
            
        }
        
        return index + 1;
        
    }
    
    private int binarySearch(int[] dp, int val, int index) {
        int left = 0, right = index;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (val == dp[mid]) {
                return mid;
            } else if (val < dp[mid]) {
                right = mid;
            } else {
                left = mid;
            }
        }
        
        if (val <= dp[left]) {
            return left;
        } else if (val > dp[right]) {
            return index + 1;
        } else {
            return right;
        }
    }
}

```


-----


* 这是一个 O(n^2) 的答案，不是最优。
核心部分
```java
for (int i = 0; i < nums.length; i++) {
      f[i] = 1;
      for (int j = 0; j < i; j++) {
           if (nums[j] < nums[i]) {
               f[i] = f[i] > f[j] + 1 ? f[i] : f[j] + 1;
           }
      }
      if (f[i] > max) {
           max = f[i];
      }
}
```
![](LIS.jpg)

作为第```i```号位置的元素，前面的每一个元素```j```都要和他进行相比，如果元素```j```小于元素```i```，那么max就要进行一次更迭。

其中，```f[i] > f[j] + 1```是为了选出一次当中最大的```i```值。


```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int max = 0;
        int[] f = new int[nums.length];
        
        for (int i = 0; i < nums.length; i++) {
            f[i] = 1;
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    f[i] = f[i] > f[j] + 1 ? f[i] : f[j] + 1;
                }
            }
            if (f[i] > max) {
                max = f[i];
            }
        }
        return max;
    }
}
```

------------------
##易错点
1. 二分法最后分三段，画个数轴想清楚
2. index 记录的是 index 不是 length，先把第一个元素放进去，后面的元素好插入






















