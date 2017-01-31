# Problem 114: Flatten Binary Tree to Linked List

> https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

----------
##思路
* 通过 recursion 的方法，把左边的 nodes 都挂到右边来。这个过程中，在保存了 left 之后，要把 root.left 置空。
* 然后挂的时候，左边和右边已经分别 flatten 好了，先把左边的挂上，然后一路沿着 root 往下走，把剩下的 right 挂上去。

-------


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
    public void flatten(TreeNode root) {
        if (root == null) return;
        
        TreeNode left = root.left;
        TreeNode right = root.right;
        root.left = null;
        
        flatten(left);
        flatten(right);
        
        root.right = left;
        TreeNode cur = root;
        while (cur.right != null) cur = cur.right;
        cur.right = right;
    }
}
```


