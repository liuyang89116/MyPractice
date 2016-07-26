# Problem 236: Lowest Common Ancestor of a Binary Tree

> https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

--------------------------------------------------------------------
##思路
* 看到二叉树的问题首先考虑分治递归
* 如果左右都有那就是在root上
* 只在左有返回左
* 只在右有返回右

----------------------------------------------------------------------
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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) {
            return root;
        }
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left != null && right != null) {
            return root;
        }
        if (left != null) {
            return left;
        }
        if (right != null) {
            return right;
        }
        return null;
    }
}
```
##易错点
1. 退出条件要考虑好
   ```java
   if (root == null || root == p || root == q) {
       return root;
   }
   ```

