# Problem 337: House Robber III

> https://leetcode.com/problems/house-robber-iii/

-------
##思路
* 首先一个原则，对于每个 node，存在两种情况：偷或者不偷。所以，我们可以用 0，1 来表示这两种情况。
* 所以，我们可以用 dfs 来返回一个大小为 2 的数组，0 的位置表示没有偷，1 的位置表示偷了，递归遍历整个 tree

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
    public int rob(TreeNode root) {
        int[] value = helper(root);
        return Math.max(value[0], value[1]);
    }
    
    public int[] helper(TreeNode root) {
        if (root == null) {
            return new int[2];
        }
        
        int[] left = helper(root.left);
        int[] right = helper(root.right);
        int[] value = new int[2];
        value[0] += Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
        value[1] += root.val + left[0] + right[0];
        
        return value;
    }
}
``` 