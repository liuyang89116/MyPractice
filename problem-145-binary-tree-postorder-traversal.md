# Problem 145: Binary Tree Postorder Traversal

> https://leetcode.com/problems/binary-tree-postorder-traversal/

----------
##思路
* stack 的思路比较复杂，参考一下这里的讲解
> http://blog.csdn.net/u012249528/article/details/46813583

----------

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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> rst = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        if (root == null) {
            return rst;
        }
        
        TreeNode prev = null; // previously traversed node
        TreeNode curr = root;
        stack.push(root);
        while (!stack.isEmpty()) {
            curr = stack.peek();
            if (prev == null || prev.left == curr || prev.right == curr) { // traverse down the tree
                if (curr.left != null) {
                    stack.push(curr.left);
                } else if (curr.right != null) {
                    stack.push(curr.right);
                }   
            } else if (curr.left == prev) { // traverse up the tree from left
                if (curr.right != null) {
                    stack.push(curr.right);
                }
            } else { // traverse up the tree from right
                rst.add(curr.val);
                stack.pop();
            }
            prev = curr;
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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> rst = new ArrayList<Integer>();
        if (root == null) {
            return rst;
        }
        
        List<Integer> left = postorderTraversal(root.left);
        List<Integer> right = postorderTraversal(root.right);
        
        rst.addAll(left);
        rst.addAll(right);
        rst.add(root.val);
        
        return rst;
    }
}
```

