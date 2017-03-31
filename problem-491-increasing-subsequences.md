# Problem 491: Increasing Subsequences

> https://leetcode.com/problems/increasing-subsequences/\#/description

---------

## 思路

* 通过用 set 来去除重复元素
* 退出条件很 tricky，只要 path 的元素个数大于 2 就可以了。**注意：这里不需要退出！如果在这里 return 了，只能得到元素个数为 2 的一组数。**

---------

```java
public class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList();
        }
        Set<List<Integer>> rstSet = new HashSet<List<Integer>>();
        List<Integer> path = new ArrayList<Integer>();
        
        helper(nums, 0, path, rstSet);
        List rst = new ArrayList(rstSet);
        
        return rst;
    }
    
    private void helper(int[] nums, int index, List<Integer> path, Set<List<Integer>> rstSet) {
        if (path.size() >= 2) {
            rstSet.add(new ArrayList(path));
        }
        
        for (int i = index; i < nums.length; i++) {
            if (path.size() == 0 || nums[i] >= path.get(path.size() - 1)) {
                path.add(nums[i]);
                helper(nums, i + 1, path, rstSet);
                path.remove(path.size() - 1);
            }
        }
    }
}
```



