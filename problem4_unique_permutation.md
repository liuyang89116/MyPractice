# Problem 47: Unique Permutations 


> https://leetcode.com/problems/permutations-ii/

----------
##思路
* 这道题最主要的就是去重复。


-----------------------------
```java
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<Integer> path = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(path);
        if (nums == null || nums.length == 0) {
            return rst;
        }
        
        boolean[] visited = new boolean[nums.length];
        Arrays.sort(nums);
        helper(nums, path, visited, rst);
        
        return rst;
    }
    
    private void helper(int[] nums, List<Integer> path, boolean[] visited, List<List<Integer>> rst) {
        if (path.size() == nums.length) {
            rst.add(new ArrayList(path));
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i] == false) {
                path.add(nums[i]);
                visited[i] = true;
                helper(nums, path, visited, rst);
                path.remove(path.size() - 1);
                visited[i] = false;
                while (i < nums.length - 1 && nums[i] == nums[i + 1]) i++;
            }
        }
    }
}
```
-------------------------

## 易错点
1. 去重复
```java
while (i < nums.length - 1 && nums[i] == nums[i + 1]) i++;
```
我像之前一样用了一个方法，但报错了
```java
if (i > 0 && nums[i] == nums[i - 1]) {
    continue;
}
```