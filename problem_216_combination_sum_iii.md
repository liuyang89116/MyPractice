# Problem 216: Combination Sum III

>https://leetcode.com/problems/combination-sum-iii/

---------
##思路
* 和之前的思路是一样的

-------------
```java
public class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<Integer> path = new ArrayList<Integer>();
        List<List<Integer>> res = new ArrayList(path);
        if (n <= 0) {
            return res;
        }
        
        helper(k, n, 1, path, res);
        return res;
    }
    
    private void helper(int k, int target, int pos, List<Integer> path, List<List<Integer>> res) {
        if (k < 0 || target < 0) {
            return; 
        }
        if (target == 0 && k == 0) {
            res.add(new ArrayList(path));
        }
        
        for (int i = pos; i <= 9; i++) {
            path.add(i);
            helper(k - 1, target - i, i + 1, path, res);
            path.remove(path.size() - 1);
        }
        
    }
}
```

-----
##易错点

1. 循环的时候没搞清楚变量的意义
```java
for (int i = pos; i <= 9; i++) {
          path.add(i);
          helper(k - 1, target - i, i + 1, path, res);
          path.remove(path.size() - 1);
}
```
其中，
```java
helper(k - 1, target - i, i + 1, path, res);
```
错写成了
```java
helper(k - 1, target - i,  pos + 1, path, res);
```
这样导致的结果是有重复的元素。因为 pos 实际上是固定值，而 i 才是整个过程中的变量


















