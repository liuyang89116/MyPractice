# Problem 263: Ugly Number

> https://leetcode.com/problems/ugly-number/\#/description

-------

## 思路

* 通过不断地把 num 中的 factor 都除掉，来算最后的结果

-----

```java
public class Solution {
    public boolean isUgly(int num) {
        if (num <= 0) return false;
        if (num == 1) return true;
        if (num % 2 == 0) return isUgly(num / 2);
        if (num % 3 == 0) return isUgly(num / 3);
        if (num % 5 == 0) return isUgly(num / 5);
        
        return false;
    }
}
```



