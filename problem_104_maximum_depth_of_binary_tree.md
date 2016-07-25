# Problem 104: Maximum Depth of Binary Tree


> https://leetcode.com/problems/maximum-depth-of-binary-tree/

-------------------------------------------------------------
##思路
* Binary Tree的问题首先想到的就是*“分治-递归”*
* *“分治-递归”*要想好的一点就是考虑好**return条件**


-----------------------------------------------------------------
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
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```