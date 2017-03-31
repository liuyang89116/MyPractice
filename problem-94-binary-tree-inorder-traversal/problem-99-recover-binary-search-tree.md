# Problem 99: Recover Binary Search Tree

> https://leetcode.com/problems/recover-binary-search-tree/\#/description

--------

## 思路

* 一个经典的 inorder 模板，可以解决一类 tree 中顺序增加的题目

```java
private void traverse (TreeNode root) {
   if (root == null) return;
  
   traverse(root.left);
   // Do some business
   traverse(root.right);
}
```

* 这个讲解很好

> https://discuss.leetcode.com/topic/3988/no-fancy-algorithm-just-simple-and-powerful-in-order-traversal

-----

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
    TreeNode firstNode = null;
    TreeNode secondNode = null;
    TreeNode prevNode = new TreeNode(Integer.MIN_VALUE);
    
    public void recoverTree(TreeNode root) {
        traverse(root);
        
        int tmp = firstNode.val;
        firstNode.val = secondNode.val;
        secondNode.val = tmp;
    }
    
    private void traverse(TreeNode root) {
        if (root == null) return;
        
        traverse(root.left);
        
        if (firstNode == null && prevNode.val >= root.val) {
            firstNode = prevNode;
        }
        if (firstNode != null && prevNode.val >= root.val) {
            secondNode = root;
        }
        prevNode = root;
        
        traverse(root.right);
    }
}

```



