# Problem 450: Delete Node in a BST

> https://leetcode.com/problems/delete-node-in-a-bst/

------
##思路
* 这道题递归和 iterative 都可以做，这里讨论的是递归的解法。
* 如果 key 小于 root，那么就走左边，把 root.left 递归为 deleteNode 的返回值。当时出错是之间返回了 deleteNode，但是这样只返回了左子树删掉 key 的情况！同理，如果 key 大于 root，就接着走右边。
* 通过递归，被删的元素永远是root，也就是 else 中的情况：**要删的值就是当前的 root！**找到右子树的最小值来顶替被删元素。

------
##复杂度
* Time ：O(height)

------


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
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return null;
        
        if (key < root.val) {
            root.left = deleteNode(root.left, key);
        } else if (key > root.val) {
            root.right = deleteNode(root.right, key);
        } else {
            if (root.left == null) return root.right;
            if (root.right ==  null) return root.left;
            
            TreeNode  smallRight = findSmall(root.right);
            root.val = smallRight.val;
            root.right = deleteNode(root.right, root.val);
        }
        
        return root;
    }
    
    private TreeNode findSmall(TreeNode root) {
        while (root.left != null) root = root.left;
        return root;
    }
}
```

