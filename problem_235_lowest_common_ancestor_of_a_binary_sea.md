# Problem 235: Lowest Common Ancestor of a Binary Search Tree


> https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

---------------
##思路
* 和上一题实际上是一样的

--------------
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
-----
##易错点

1. 分治递归的思路很简单，但是难点在于退出条件上
```java
if (root == null || root == p || root == q) {
         return root;
}
```




















