# Problem 77: Combinations


> https://leetcode.com/problems/combinations/

----------------
##思路
* 经典模板
* 想好退出条件：当 path 当中元素的个数等于 k 的时候，就可以退出了。

-------
```java
public class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<Integer> path = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(path);
        if (n < k) {
            return rst;
        }
        
        helper(n, k, 1, path, rst);
        
        return rst;
    }
    
    private void helper(int n, int k, int pos, List<Integer> path, List<List<Integer>> rst) {
        if (path.size() == k) {
            rst.add(new ArrayList(path));
            return;
        }
        for (int i = pos; i <= n; i++) {
            path.add(i);
            helper(n, k, i + 1, path, rst);
            path.remove(path.size() - 1);
        }
    }
}
```
-------
##易错点
1. 循环开始从 ```for (int i = pos; i <= n; i++)```，而不是从 1 开始
2. helper 第二次调用的时候，从 i + 1 开始找，以免遇到重复元素
































