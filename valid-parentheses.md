# Valid Parentheses
> 给你一个 str,里面只有 '(' 和 ')',让你数 valid pairs 一共有多少,如果不是 valid 就返回 -1. (判断是不是 valid 的 parenthesis string，不是的话返回 -1，是的话返回 valid pair 个数，即 String.length() / 2)



```java
package ValidParentheses;

import java.util.Stack;

/**
 * Created by yang on 1/17/17.
 */
public class Solution {
    public static boolean isValidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }

        Stack<Character> stack = new Stack<>();
        char[] arr = s.toCharArray();

        for (int i = 0; i < arr.length; i++) {
            char c = arr[i];
            if (c == '(') {
                stack.push(c);
            } else if (c == ')') {
                if (stack.isEmpty()) {
                    return false;
                }
                char tmp = stack.pop();
                if (tmp != '(') {
                    return false;
                }
            }
        }

        if (!stack.isEmpty()) {
            return false;
        }

        return true;
    }

    public static void main(String[] args) {
        // String s = "(()(()))";
        String s = "(()(()))(";
        System.out.println(isValidParentheses(s));
    }
}

```

