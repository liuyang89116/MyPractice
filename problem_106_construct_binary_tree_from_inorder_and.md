# Problem 106: Construct Binary Tree from Inorder and Postorder Traversal


> https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/

----------------
##思路
* 思路和上一题类似
* 永远都是先找到 root，然后以 inorder 为线索，把左右的长度固定了，进行递归
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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        int inLength = inorder.length;
        int postLength = postorder.length;
        if (inLength != postLength) {
            return null;
        }
        
        return helper(inorder, 0, inLength - 1, postorder, 0, postLength - 1);
    }
    
    private TreeNode helper(int[] inorder, int inStart, int inEnd, int[] postorder, int postStart, int postEnd) {
        if (inStart > inEnd || postStart > postEnd) {
            return null;
        }
        
        int rootVal = postorder[postEnd];
        int rootIndex = findIndex(inorder, inStart, inEnd, rootVal);
        int len = rootIndex - inStart;
        
        TreeNode root = new TreeNode(rootVal);
        root.left = helper(inorder, inStart, rootIndex - 1, postorder, postStart, postStart + len - 1);
        root.right = helper(inorder, rootIndex + 1, inEnd, postorder, postStart + len, postEnd - 1);
        
        return root;
    }
    
    private int findIndex(int[] inorder, int start, int end, int rootVal) {
        for (int i = start; i <= end; i++) {
            if (inorder[i] == rootVal) {
                return i;
            }
        }
        
        return -1;
    }
}
```

