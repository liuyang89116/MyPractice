# Problem 40: Combination Sum II


> https://leetcode.com/problems/combination-sum-ii/

---------
##思路
* 这道题和上一题的区别就是，同一个元素只能使用一次。
* 所以上一题中，在递归的时候是从 i 开始的（因为当前元素还是可以选的），而这一题目中，要从 i + 1 处开始递归。

--------------
```java
public class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<Integer> path = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(path);
        if (candidates == null || candidates.length == 0) {
            return rst;
        }
        
        Arrays.sort(candidates);
        helper(candidates, target, 0, path, rst);
        
        return rst;
    }
    
    private void helper(int[] candidates, int target, int pos, List<Integer> path, List<List<Integer>> rst) {
        if (target < 0) {
            return;
        }
        
        if (target == 0) {
            rst.add(new ArrayList(path));
            return;
        }
        
        for (int i = pos; i < candidates.length; i++) {
            path.add(candidates[i]);
            helper(candidates, target - candidates[i], i + 1, path, rst);
            path.remove(path.size() - 1);
            while (i < candidates.length - 1 && candidates[i] == candidates[i + 1]) i++;
        }
        
    }
}
```
------
##易错点

1. 从 i + 1 处开始递归
```java
helper(candidates, target - candidates[i], path, i + 1, result);
```
2. 去掉重复元素
```java
while (i < candidates.length - 1 && candidates[i] == candidates[i + 1]) i++;
```
为什么上一道题不用呢？因为上一道题目可以重复取每一个元素




















