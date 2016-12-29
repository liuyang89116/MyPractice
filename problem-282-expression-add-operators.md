# Problem 282: Expression Add Operators

> https://leetcode.com/problems/expression-add-operators/

----------
##思路
* 这道题一看就是 backtracking DFS 的类型。
* 首先 DFS 的过程中，我们要记录 pos，path，rst，num 这些最基本的东西。其次，作为这道题来说，我们还应该 keep track 上一次的结果 prev（用来做乘法的时候用），还有当前的计算值 calc。
* 计算乘法的 trick：  
因为我们利用算法计算的过程永远都是从左往右依次计算的，那么如何才能实现优先计算乘法呢？ 没有办法。只能再后面的步骤中调整。举个例子：    
`2 + 3 * 2`我们由左到右，当计算完 2 + 3 这一步的时候，当前的结果 calc 是 5 (2 + 3)，接下来乘法来了，我们要把之前加的“吐出来”： `5 - 3 + 3 * 2`。总的来讲，就是 `calc - prev + prev * cur`
* 为了避免数据溢出，我们用 long 来计算中间的结果

-------------


```java
public class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> rst = new ArrayList<String>();
        if (num == null || num.length() == 0) {
            return rst;
        }
        
        helper("", rst, num, target, 0, 0, 0);
        return rst;
    }
    
    private void helper(String path, List<String> rst, String num, int target, int pos, long calc, long prev) {
        if (pos == num.length()) {
            if (calc == target) {
                rst.add(path);
            }
            return;
        }
        
        for (int i = pos; i < num.length(); i++) {
            if (num.charAt(pos) == '0' && i != pos) break;
            
            long cur = Long.parseLong(num.substring(pos, i + 1));
            if (pos == 0) {
                helper(path + cur, rst, num, target, i + 1, cur, cur);
            } else {
                helper(path + "+" + cur, rst, num, target, i + 1, calc + cur, cur);
                helper(path + "-" + cur, rst, num, target, i + 1, calc - cur, -cur);
                helper(path + "*" + cur, rst, num, target, i + 1, calc - prev + prev * cur, prev * cur);
            }
        }
    }
}
```
--------
##易错点
1. 小心 `0` 作为首位
```java
if (num.charAt(pos) == '0' && i != pos) break;
```






























