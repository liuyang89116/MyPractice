# Problem 202: Happy Number

> https://leetcode.com/problems/happy-number/\#/description

--------

## 思路

* 用一个 set 来记录是否之前已经存过这个值，可以减少重复运算

-------

```java
public class Solution {
    public boolean isHappy(int n) {
        Set<Integer> set = new HashSet<Integer>();
        set.add(n);
        while (n != 1) {
            int sum = 0;
            while (n != 0) {
                sum += Math.pow(n % 10, 2);
                n /= 10;
            }
            if (sum == 1) return true;
            if (set.contains(sum)) return false;
            
            set.add(sum);
            n = sum;
        }
        
        return true;
    }
}
```



