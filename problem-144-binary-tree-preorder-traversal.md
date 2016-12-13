# Problem 144: Binary Tree Preorder Traversal

> https://leetcode.com/problems/binary-tree-preorder-traversal/

----------
##思路
* 经典题型，推荐用 stack 解决
* preorder 是“根-左-右”，那么就先把“右” push 进去.

---------

```java
/*
    stack 的解法
*/

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
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        List<Integer> rst = new ArrayList<Integer>();
        if (root == null) {
            return rst;
        }
        
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            rst.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        
        return rst;
    }
}
```

```java
/*
    divide and conquer
*/

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> rst = new ArrayList<Integer>();
        if (root == null) {
            return rst;
        }
        
        List<Integer> left = preorderTraversal(root.left);
        List<Integer> right = preorderTraversal(root.right);
        
        rst.add(root.val);
        rst.addAll(left);
        rst.addAll(right);
        
        return rst;
    }
}
```
