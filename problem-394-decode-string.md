# Problem 394: Decode String


> https://leetcode.com/problems/decode-string/

--------
##思路
* 这道题和上一题思路类似，都是应用 stack 来维护同一 level 元素的同步
* 设置两个 stack，一个用来维护 count，一个用来拼接字符串，这里用 StringBuilder 来节省空间。
* `[`意味着字符串的“开始”，我们从这里开始拼接；`]`意味着字符串拼接的结束，开始打印。

-----------


```java
public class Solution {
    public String decodeString(String s) {
        Stack<Integer> intStack = new Stack<>();
        Stack<StringBuilder> strStack = new Stack<>();
        int count = 0;
        StringBuilder cur = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                count = count * 10 + (c - '0');
            }else if (c == '[') {
                intStack.push(count);
                strStack.push(cur);
                count = 0;
                cur = new StringBuilder();
            }else if (c == ']') {
                count = intStack.pop();
                StringBuilder tmp = cur;
                cur = strStack.pop();
                for (int i = 0; i < count; i++) {
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



