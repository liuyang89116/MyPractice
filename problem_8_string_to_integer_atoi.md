# Problem 8: String to Integer (atoi)


> https://leetcode.com/problems/string-to-integer-atoi/

----------------------
##思路
* 题目不难，但是考虑的东西很多：
* 首位的空白
* “+/-” 首位是否是符号，首位如果有符号，后面再有的话就要报错了
* 是否越界

-------------------
```java
public class Solution {
    public int myAtoi(String str) {
        if (str == null || str.length() == 0) {
            return 0;
        }
        
        str = str.trim();
        boolean isNegative = false;
        int pos = 0;
        if (str.charAt(0) == '+') {
            pos++;
        }
        if (str.charAt(0) == '-') {
            isNegative = true;
            pos++;
        }
        
            
        double rst = 0;
        while (pos < str.length() && str.charAt(pos) == '0') pos++;
        while (pos < str.length()) {
            char c = str.charAt(pos);
            if (c < '0' || c > '9') {
                break;
            }
            
            rst = 10 * rst + (c - '0'); 
            pos++;
        }
        if (isNegative) {
            rst = -rst;
        }
        
        if (rst > Integer.MAX_VALUE) {
            return Integer.MAX_VALUE;
        }
        if (rst < Integer.MIN_VALUE) {
            return Integer.MIN_VALUE;
        }
        
        return (int) rst;
    }
}
```
---------





















