# Problem 111: Minimum Depth of Binary Tree


> https://leetcode.com/problems/minimum-depth-of-binary-tree/

----------
##思路
* **这道题看着不难，但是不能用 Maximum Depth 的那个方法去做，没想通目前**
* 一样的分治递归的思路

----------
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
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }   
        
        return getMin(root);
    }
    
    private int getMin(TreeNode root) {
        if (root == null) {
            return Integer.MAX_VALUE;
        }
        if (root.left == null && root.right == null) {
            return 1;
        }
        
        return Math.min(getMin(root.left), getMin(root.right)) + 1;
    }
}
```
----
##易错点
1. 最后的返回值要加 1
2. 在 getMin() 中，**如果 root == null 返回最大值**














