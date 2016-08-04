# Problem 70: Climbing Stairs


> https://leetcode.com/problems/climbing-stairs/

----------------------------------------
##思路
经典问题，一维的DP问题。总的思路是一样的。

-----------------------------------
```java
public class Solution {
    public int climbStairs(int n) {
        if (n <= 1) {
            return 1;
        }
        
        //state
        int[] f = new int[n + 1];
        
        //initiate
        f[0] = 0;
        f[1] = 1;
        f[2] = 2;
        
        //function
        for (int i = 3; i <= n; i++) {
            f[i] = f[i - 1] + f[i - 2];
        }
        //answer
        return f[n];
    }
}
```
----------------------------
##易错点
1. 初始化数组
   ```java
   int[] f = new int[n + 1];
   ```
   为什么是```n + 1```呢？因为是从 0 到 n每个都过一遍。
2. 脚标
   ```java
   int[] f = new int[n + 1];
   ```
   这里的```int[n + 1]```是**数组的大小**，而不是最后一个元素，这个一定要注意。
   另外最后一个元素是```f[n]```
3. 方程的递推关系
   ```java
   f[i] = f[i - 1] + f[i - 2];
   ```
   我原来写的是
   ```java
   f[i] = f[i - 1] + f[i - 2] + 2;
   ```
   认为从```i - 1```跳过来，包含了一种方法，从```i - 2```跳过来，又包含了一种方法，其实是不对的。
   
   **要把这个问题想清楚**
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
