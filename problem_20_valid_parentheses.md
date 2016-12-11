# Problem 20: Valid Parentheses

> [https://leetcode.com/problems/valid-parentheses/](https://leetcode.com/problems/valid-parentheses/)

---

## 思路

* 典型的 stack 的问题。
* 这道题的思路就是，遇到左边的括号类型就 push 到 stack 里面去，遇到右边的括号就把上一个元素 pop\(\) 出来进行比对。

---

```java
public class Solution {
    public boolean isValid(String s) {
       Stack<Character> stack = new Stack<Character>();
       char[] arr = s.toCharArray();

       for (int i = 0; i < arr.length; i++) {
           char c = arr[i];
           if (c == '(' || c == '{' || c == '[') {
               stack.push(c);
           } else if (c == ')' || c == '}' || c == ']') {
               if (stack.isEmpty()) {
                   return false;
               }
               char tmp = stack.pop();
               switch (c) {
                   case ')':
                        if (tmp != '(') {
                            return false;
                        }
                        break;
                   case '}':
                        if (tmp != '{') {
                            return false;
                        }
                        break;
                   case ']':
                        if (tmp != '[') {
                            return false;
                        }
                        break;
                   default: break;
               } 

           }
       }

       if (!stack.isEmpty()) {
           return false;
       }

       return true;

    }
}
```

---

## 易错点

1. stack 接口
   ```java
   Stack<Character> stack = new Stack<Character>();
   ```

2. switch 选择结构，每个要有 break ！
   > [https://www.tutorialspoint.com/java/switch\_statement\_in\_java.htm](https://www.tutorialspoint.com/java/switch_statement_in_java.htm)

3. 记得遍历完每个元素之后，check 一下 stack 是否为空。