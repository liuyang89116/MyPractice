# Problem 40: Combination Sum II


> https://leetcode.com/problems/combination-sum-ii/

---------
##思路
* 这道题和上一题的区别就是，同一个元素只能使用一次。
* 所以上一题中，在递归的时候是从 i 开始的（因为当前元素还是可以选的），而这一题目中，要从 i + 1 处开始递归。

--------------
```java
public class Solution {
    List<Integer> path = new ArrayList<Integer>();
    List<List<Integer>> result = new ArrayList(path);
    
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        if (candidates == null) {
            return result;
        } 
        Arrays.sort(candidates);
        helper(candidates, target, path, 0, result);
        
        return result;
    }
    
    private void helper(int[] candidates, int target, List<Integer> path, int pos, List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList(path));
        }
        
        int prev = -1;
        for (int i = pos; i < candidates.length; i++) {
            if (candidates[i] > target) {
                break;
            }
            
            if (prev != candidates[i]) {
                path.add(candidates[i]);
                helper(candidates, target - candidates[i], path, i + 1, result);
                path.remove(path.size() - 1);
                
                prev = candidates[i];
            }
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
2. 理解 prev 的作用





















