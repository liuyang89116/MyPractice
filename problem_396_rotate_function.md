# Problem 396: Rotate Function

> https://leetcode.com/problems/rotate-function/

---------
##思路
* 通过观察可以发现：  
F(0) = 0A + 1B + 2C +3D  
F(1) = 0D + 1A + 2B +3C  
F(2) = 0C + 1D + 2A +3B  
F(3) = 0B + 1C + 2D +3A  
等同于：  
F(1) = F(0) + sum - 4D  
F(2) = F(1) + sum - 4C  
F(3) = F(2) + sum - 4B  
* 从而得出递推关系：$$F(i) = F(i-1) + sum - n * A[n-i]$$

--------
```java
public class Solution {
    public int maxRotateFunction(int[] A) {
        int len = A.length;
        int sum = 0;
        int f = 0;
        for (int i = 0; i < len; i++) {
            f += i * A[i];
            sum += A[i];
        }
        int max = f;
        for (int i = 1; i < len; i++) {
            f = f + sum - len * A[len - i];
            max = Math.max(max, f);
        }
        
        return max;
    }
}
```