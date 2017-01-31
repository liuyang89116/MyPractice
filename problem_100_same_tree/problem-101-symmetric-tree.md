# Problem 101: Symmetric Tree

> https://leetcode.com/problems/symmetric-tree/

---------
##思路
* 递归的思路就是判断是否都为空，或者值是否相等；然后就是判断左子树的右边和右子树的左边是否一样，左子树的左边和右子树的右边是否一样
* 递归的函数有时候原方程的结构不合适，需要改写（比如 parameter 的个数不一样）
* 对于非递归解法，用一个 queue 来记录 node 的顺序，然后依次对比。注意在 while 循环的里面，是分两部分来处理的。

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
---------
* 非递归解法



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
        if (root == null || root.left == null && root.right == null) return true;
        if (root.left == null || root.right == null) return false;
        
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root.left);
        queue.offer(root.right);
        while (!queue.isEmpty()) {
            TreeNode left = queue.poll();
            TreeNode right = queue.poll();
            if (left.val != right.val) return false;
            
            if (left.left != null && right.right != null) {
                queue.offer(left.left);
                queue.offer(right.right);
            } else if (left.left == null && right.right != null || left.left != null && right.right == null) {
                return false;
            }
            
            if (left.right != null && right.left != null) {
                queue.offer(left.right);
                queue.offer(right.left);
            } else if (left.right != null && right.left == null || left.right == null && right.left != null) {
                return false;
            }
        }
        
        return true;
    }
}
```

























