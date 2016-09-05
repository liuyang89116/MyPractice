# Problem 39: Combination Sum


> https://leetcode.com/problems/combination-sum/

---------
##思路
* 排列组合模板，不过有很多细节值得留意

-------
```java
public class Solution {
    List<Integer> path = new ArrayList<Integer>();
    List<List<Integer>> result = new ArrayList(path);
    
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        if (candidates == null) {
            return result;
        }
        
        Arrays.sort(candidates);
        helper(candidates, target, path, 0, result);
        return result;
    }
    
    private void helper(int[] candidates, int target, List<Integer> path, int index, List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList(path));
            return;
        }
        
        int prev = -1;
        for (int i = index; i < candidates.length; i++) {
            if (candidates[i] > target) {
                break;
            }
            
            if (prev == candidates[i]) {
                continue;
            }
            
            path.add(candidates[i]);
            helper(candidates, target - candidates[i], path, i, result);
            path.remove(path.size() - 1);
            
            prev = candidates[i];
        }
    }
}
```
-----------
##易错点

1. 在类中设置 global 的变量：因为题目中给的 List<Integer> 和　List<List<Integer>> 都是接口，必须给出一个该接口的实现类
2. **数组必须先　sort !**
```java
Arrays.sort(candidates);
```
3. 推出递归的条件
```java
if (target == 0)
```
4. 递归中的判断
```java
if (candidates[i] > target) {
            break;
}
```
某个数已经比 target 都大了，就不用考虑了

```java
if (prev == candidates[i]) {
            continue;
}
```
这个是**排除重复元素**，eg：2,2,3 和 2,2,3 两个 2 的顺序其实不一样的，但会显示成相同的结果。
























