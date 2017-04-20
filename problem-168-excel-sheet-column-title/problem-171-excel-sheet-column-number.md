# Problem 171: Excel Sheet Column Number

> https://leetcode.com/problems/excel-sheet-column-number/\#/description

-------

## 思路

* 和上一题类似，这里相当于是一个逆过程

------

```java
public class Solution {
    public int titleToNumber(String s) {
        int num = 0;
        for (int i = 0; i < s.length(); i++) {
            num = num * 26 + (s.charAt(i) - 'A' + 1);  
        }
        
        return num;
    }
}
```



