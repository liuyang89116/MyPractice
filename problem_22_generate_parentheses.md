# Problem 22: Generate Parentheses

> https://leetcode.com/problems/generate-parentheses/

------
##思路
* 如果左括号数还没有用完，那么我们能继续放置左括号
* 如果已经放置的左括号数大于已经放置的右括号数，那么我们可以放置右括号 （如果放置的右括号数大于放置的左括号数，会出现不合法组合）
* 所以，运用dfs在每一层递归中，如果满足条件先放置左括号，如果满足条件再放置右括号

------
```java
public class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> rst = new ArrayList<String>();
        if (n <= 0) {
            return rst;
        }
        
        helper(n, n, "", rst);
        return rst;
    }
    
    private void helper(int left, int right, String path, List<String> rst) {
        if (left == 0 && right == 0) {
            rst.add(path);
            return;
        }
        
        if (left > 0) {
            helper(left - 1, right, path + "(", rst);
        }
        if (left < right) {
            helper(left, right - 1, path + ")", rst);
        }
    }
}
```
-------
##易错点
1. 这道题其实就是 combination sum III 的变形。这里控制左右括号的两个 n，就对应那道题的 n 和 k。




