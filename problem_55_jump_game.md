# Problem 55: Jump Game


> https://leetcode.com/problems/jump-game/

-----------------------------------------
##思路
1. dynamic programming 的思路在判断大的数据的时候超时，这时用greedy programming
2. 像头标枪一样，我不关心最后我是否到最后一个index了，先闷头扔一下，一直维护到最后一次，然后比较我最后所在的位置和数组最后一个的位置之间的关系



--------------------------------------
```java
public class Solution {
    public boolean canJump(int[] nums) {
        if (nums == null || nums.length == 0) {
            return true;
        }
        
        int n = nums.length;
        int farest = nums[0];
        for (int i = 1; i < n; i++) {
            if (i <= farest && i + nums[i] >= farest) {
                farest = i + nums[i];
            }
        }
        
        return farest >= n - 1;
    }
}
```
-----------------------
##易错点
1. dp的做法
```java
public class Solution {
    public boolean canJump(int[] A) {
        boolean[] can = new boolean[A.length];
        can[0] = true;
        
        for (int i = 1; i < A.length; i++) {
            for (int j = 0; j < i; j++) {
                if (can[j] && j + A[j] >= i) {
                    can[i] = true;
                    break;
                }
            }
        }
        
        return can[A.length - 1];
    }
}
```
这个做法的时间复杂度是O(n^2)，当数据过大时，会超过时间要求
2. 判断的条件
```java
if (i <= farest && i + nums[i] >= farest) {
     farest = i + nums[i];
}
```
这两个条件是缺一不可的。如果没有第一个条件，有可能是i很大，已经超过了farest

3. 比较条件
```java
return farest >= n - 1;
```
开始的时候，错误地
```java
return farest >= nums[n - 1];
```
这里我们要比的是farest最后的index，而nums[n - 1]表示的是**最后还能再跳几个值**。他们是明显不同的。

















