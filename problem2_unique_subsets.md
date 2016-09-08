# Problem 90: Unique Subsets 


> https://leetcode.com/problems/subsets-ii/

--------------

* 这道题的一个改变是有重复的元素
* 重复元素带来的麻烦就是，当你上一次选了这个元素的时候，下一次如果再选，他俩相同的话，就会出现相同的结果，那我们把他排除就好了。

-----------------------
```java
public class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<Integer> path = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(path);
        if (nums == null || nums.length == 0) {
            return rst;
        }
        
        Arrays.sort(nums);
        helper(nums, path, 0, rst);
        
        return rst;
    }
    
    private void helper(int[] nums, List<Integer> path, int pos, List<List<Integer>> rst) {
        rst.add(new ArrayList(path));
        
        for (int i = pos; i < nums.length; i++) {
            if (i > pos && nums[i] == nums[i - 1]) {
                continue;
            }  
            path.add(nums[i]);
            helper(nums, path, i + 1, rst);
            path.remove(path.size() - 1);
        }
    }
}
```
----------------------
##易错点
1. 排除重复元素。这道题是在普通的Subsets题目上的延伸，关键的难点在于在之前的模板上稍作调整，去掉重复元素的干扰。
```java 
if (i > pos && nums[i] == nums[i - 1]) {
          continue;
}  
```
