# Problem 258: Add Digits

> https://leetcode.com/problems/add-digits/\#/description

-------

## 思路

* 这其实算数学题，有现成的公式可以用。

> https://en.wikipedia.org/wiki/Digital\_root\#Congruence\_formula



------------

```java
public class Solution {
    public int addDigits(int num) {
        return 1 + (num - 1) % 9;
    }
}
```





