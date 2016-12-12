# Problem 236: Lowest Common Ancestor of a Binary Tree

> https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

--------------------------------------------------------------------
##思路
* 看到二叉树的问题首先考虑分治递归
* 如果左右都有那就是在root上
* 只在左有返回左
* 只在右有返回右

-------------------------------
##复杂度
* Time: `O(n)`

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
2. 第二次做的时候，还是在第一步退出条件上出现了错误。对于一个递归的题目，最重要的就是退出条件。因为一旦退出条件有问题，递归的时候就会累积得出错误答案。

