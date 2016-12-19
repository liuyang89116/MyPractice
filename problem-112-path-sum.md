# Problem 112: Path Sum

> https://leetcode.com/problems/path-sum/

----------
##思路
* 二叉树的题首先考虑递归，紧接着就是递归后退出条件是什么
* 退出条件就是递归到叶子的时候，`sum == 0`

-----------
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
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        
        if (root.left == null && root.right == null && sum - root.val == 0) {
            return true;
        }
        
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```
