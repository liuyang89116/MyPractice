# Problem 94: Binary Tree Inorder Traversal

> https://leetcode.com/problems/binary-tree-inorder-traversal/

-----------
##思路
* inorder 的顺序是“左-根-右”，先一路下去把“倒着”把最左边装进去，然后再慢慢 pop 出来。

-----------

```java
/*
    stack 解法
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
    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        List<Integer> rst = new ArrayList<Integer>();
        if (root == null) {
            return rst;
        }
        
        TreeNode curr = root;
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.add(curr);
                curr = curr.left;
            }
            curr = stack.peek();
            stack.pop();
            rst.add(curr.val);
            curr = curr.right;
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> rst =  new ArrayList<Integer>();
        if (root == null) {
            return rst;
        }
        
        List<Integer> left = inorderTraversal(root.left);
        List<Integer> right = inorderTraversal(root.right);
        
        rst.addAll(left);
        rst.add(root.val);
        rst.addAll(right);
        
        return rst;
    }
}

```

