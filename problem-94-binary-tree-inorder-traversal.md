# Problem 94: Binary Tree Inorder Traversal

> https://leetcode.com/problems/binary-tree-inorder-traversal/

-----------
##思路
* inorder 的顺序是“左-根-右”，先一路下去把“倒着”把最左边装进去，然后再慢慢 pop 出来。

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
