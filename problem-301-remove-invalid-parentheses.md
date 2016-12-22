# Problem 301: Remove Invalid Parentheses

> https://leetcode.com/problems/remove-invalid-parentheses/

---------
##思路
* 我们 care 的只是括号，其他的元素一概置之不理。
* 我么用一个 count 来 maintain 括号的数量：如果是`(`我们就加 1；如果是`)`我们就减 1。这个过程实际上起的作用就是一个 stack
* 我么可以先处理右括号多的情况：`()))`类型。`i`先走，走的每一步都看一下 counter，如果属于这个类型，开始递归。`j`这个时候开始走，当它是上一个`j`或者第一个右括号的时候，我们把它删掉。
* 这个过程中，我们要记录上一次`i`和`j`的位置。
* 如果是左括号多的情况：`((()`类型。我们可以复用原来的代码。
![](/assets/RemoveInvalidP.png)
------------
##复杂度
The whole search space is a tree with k leaves. The number of nodes in the tree is roughly `O(k)`. But this is not always true, for example a degenerated tree.
* To generate one node it requires `O(n)` time from the string concatenation among other things. So roughly `O(nk)`. Accurately **`O(nm)`** where m is the total "number of recursive calls" or "nodes in the search tree". Then you need to relate m to n in the worst case.

-------------
```java
public class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> rst = new ArrayList<String>();
        helper(s, rst, 0, 0, new char[] {'(', ')'});
        return rst;
    }
    
    private void helper(String s, List<String> rst, int last_j, int last_i, char[] ch) {
        int count = 0;
        for (int i = last_i; i < s.length(); i++) {
            if (s.charAt(i) == ch[0]) count++;
            if (s.charAt(i) == ch[1]) count--;
            if (count >= 0) continue;
            
            for (int j = last_j; j <= i; j++) {
                if (s.charAt(j) == ch[1] && (j == last_j || s.charAt(j - 1) != ch[1])) {
                    helper(s.substring(0, j) + s.substring(j + 1, s.length()), rst, j, i, ch);
                }
            }
            return;
        }
        String reversed = new StringBuilder(s).reverse().toString();
        if (ch[0] == '(') { // finished left to right
            helper(reversed, rst, 0, 0, new char[] {')', '('});
        } else { // finished right to left
            rst.add(reversed);
        }
    }
}

```
---------
##易错点
1. 记得 return     
dfs 最重要的就是找到退出的场景
2. 仔细理解最后一段 reverse 的过程


























