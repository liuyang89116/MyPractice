# Problem 20: Valid Parentheses

>https://leetcode.com/problems/valid-parentheses/

-----------
##思路
*　运用　stack 来判断是否是一对括号

----------
```java
public class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; i++) {
            char c = arr[i];
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            }
            if (c == ')' || c == '}' || c == ']') {
                if (stack.isEmpty()) {
                    return false;
                } 
                char prev = stack.pop();
                switch (c) {
                    case ')':
                        if (prev != '(') return false;
                        break;
                    case '}':
                        if (prev != '{') return false;
                        break;
                    case ']':
                        if (prev != '[') return false;
                        break;
                    default: break;
                }
            }
        }
   
        return stack.isEmpty();
    }
}
```
-------
##易错点
1. switch 的格式
>https://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html
每个 case 里面是一定要有 break 的！否则即使有 return 也没用
2. 活学活用 stack






















