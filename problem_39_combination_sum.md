# Problem 39: Combination Sum


> https://leetcode.com/problems/combination-sum/

---------
##思路
* 排列组合模板，不过有很多细节值得留意
* 同一个元素可以用多次
* 当 target < 0 的时候，无解，return; 当 target ＝＝ 0 的时候，发现解，添加进res里面，然后return

-------
```java
public class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
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
            helper(candidates, target - candidates[i], i, path, rst);
            path.remove(path.size() - 1);
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
4. 如果不用pos，从数组开头往数组尾巴扫，会出现什么问题？ 会出现重复集合的问题，这里的重复不是指顺序完全相同的Set，而是对于每一种组合，我们输出一次就可以了 比如Sum = 3 不加pos会出现 [1,2],[2,1]两种一样的解，我们加入一个pos，限制每次添加只能再添加和这个数字相等或者比这个数字大的数字（数组之前sort过升序排列）这样就会避免问题
























