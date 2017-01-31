# Problem 101: Symmetric Tree

> https://leetcode.com/problems/symmetric-tree/

---------
##思路
* 递归的思路就是判断是否都为空，或者值是否相等；然后就是判断左子树的右边和右子树的左边是否一样，左子树的左边和右子树的右边是否一样
* 递归的函数有时候原方程的结构不合适，需要改写（比如 parameter 的个数不一样）

---------
* 递归解法


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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        
        return helper(root.left, root.right);
    }
    
    private boolean helper(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        
        if (p == null || q == null) return false;
        
        return (p.val == q.val) && helper(p.left, q.right) && helper(p.right, q.left);
    }
}
```

