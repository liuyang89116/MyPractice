# Problem 394: Decode String

> https://leetcode.com/problems/decode-string/

----------
##思路
* 这道题对于 stack 的运用十分巧妙！
* 首先我们创建两个 stack，一个用来存 count，另一个用来存 char（实际上我们存的是 StringBuilder，因为这样更节省空间，提高效率）。
* 然后分情况来讨论。当进来的是数字的时候，我们就转化为数字，这个数字用 count 来维护；当进来的是 [ 的时候，我们就把元素存入栈内，然后再新建一个。
* 这个 cur 的过程就相当于每次 build 完之后，赶紧存入 stack 内，然后进行下一步的元素存储。

-------------
```java
public class Solution {
    public String decodeString(String s) {
        Stack<Integer> intStack = new Stack<Integer>();
        Stack<StringBuilder> strStack = new Stack<StringBuilder>();
        StringBuilder cur = new StringBuilder();
        int count = 0;
        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                count = 10 * count + c - '0';
            } else if (c == '[') {
                intStack.push(count);
                strStack.push(cur);
                count = 0;
                cur = new StringBuilder();
            } else if (c == ']') {
                count = intStack.pop();
                StringBuilder tmp = cur;
                cur = strStack.pop();
                for (int i = count; i > 0; i--) {
                    cur.append(tmp);
                }
                count = 0;
            } else {
                cur.append(c);
            }
        }
        
        return cur.toString();
    }
}
```
---------
##易错点
1. count 要及时归 0
2. 数字的转化，非常精妙
```java
count = 10 * count + c - '0';
```

























