# Problem 357: Count Numbers with Unique Digits

> [https://leetcode.com/problems/count-numbers-with-unique-digits/](https://leetcode.com/problems/count-numbers-with-unique-digits/)

---

## 思路

* 数学题，排列组合
* 相当于是 n 位的一串数，求最后能组成多少个各位都不相同的数字

---

```java
public class Solution {
    public int countNumbersWithUniqueDigits(int n) {
        if (n == 0) return 1;

        int rst = 10;
        int uniqueDigit = 9;
        int availableDigit = 9;
        while (n > 1 && availableDigit > 0) {
            uniqueDigit = uniqueDigit * availableDigit;
            rst += uniqueDigit;
            availableDigit--;
            n--;
        }

        return rst;
    }
}
```



