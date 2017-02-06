# Problem 113: Path Sum II

> https://leetcode.com/problems/path-sum-ii/

-----
##思路
* 这道题是二叉树类型的排列组合，思路上大同小异

----


```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<Integer> path = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(path);
        helper(root, sum, 0, path, rst);
        
        return rst;
    }
    
    private void helper(TreeNode root, int sum, int count, List<Integer> path, List<List<Integer>> rst) {
        if (root == null) return;
        
        path.add(root.val);
        count += root.val;
        if (root.left == null && root.right == null && count == sum) {
            rst.add(new ArrayList(path));
        }
        helper(root.left, sum, count, path, rst);
        helper(root.right, sum, count, path, rst);
        path.remove(path.size() - 1);
    }
}
```

