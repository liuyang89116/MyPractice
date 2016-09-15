# Problem 227: Basic Calculator II


> https://leetcode.com/problems/basic-calculator-ii/

----------
##思路

* 用 stack 来存每个数字，最后把他们加起来
* 由于乘除的运算的优先级，要把他们先弹出来，再乘以 num，得到的数再存入 stack 里面

------
```java
public class Solution {
    public int calculate(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        
        Stack<Integer> stack = new Stack<Integer>();
        int num = 0;
        char sign = '+';
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                num = num * 10 + (c - '0');
            }
            
            if (!Character.isDigit(c) && c != ' ' || i == s.length() - 1) {
                if (sign == '+') {
                    stack.push(num);
                }
                if (sign == '-') {
                    stack.push(-num);
                }
                if (sign == '*') {
                    stack.push(stack.pop() * num);
                }
                if (sign == '/') {
                    stack.push(stack.pop() / num);
                }
                sign = c;
                num = 0;
            }
        }
        int rst = 0;
        for (Integer i : stack) {
            rst += i;
        }
        
        return rst;
    }
}
```
------
##易错点
1. 最后一个元素的时候
```java
if (!Character.isDigit(c) && c != ' ' || i == s.length() - 1
)
```
很容易把 ```i == s.length() - 1``` 漏掉，最后一个元素必须要入 stack，并且此时的 sign 肯定是 '+'
























