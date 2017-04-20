# Problem 168. Excel Sheet Column Title

> https://leetcode.com/problems/excel-sheet-column-title/\#/description

---------

## 思路

* 这道题类似于 get 一个数字的每一位
* 需要注意的是，insert 的时候是从个位向高位走的

----------

```java
public class Solution {
    public String convertToTitle(int n) {
        StringBuilder sb = new StringBuilder();
        while (n > 0) {
            n--;
            sb.insert(0, (char)('A' + n % 26));
            n /= 26;
        }
        
        return sb.toString();
    }
}
```



