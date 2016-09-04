# Problem 108: Convert Sorted Array to Binary Search Tree


> https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

---------
##思路
* 依然是分治递归的思路

--------
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
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null) {
            return null;
        }
        
        return buildTree(nums, 0, nums.length - 1);
    }
    
    private TreeNode buildTree(int[] nums, int start, int end) {
        if (start > end) {
            return null;
        }
        
        int mid = (start + end) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = buildTree(nums, start, mid - 1);
        root.right = buildTree(nums, mid + 1, end);
        
        return root;
    }
}
```
-----
##易错点
1. 分段的结点： (start, mid - 1), mid, (mid + 1, end)
2. 想清楚 index
```java
root.left = buildTree(nums, start, mid - 1);
```
当时写的是
```java
root.left = buildTree(nums, 0, mid - 1);
```
初看是对的，但实际上这是一个递归的方程，对第一次递归数字是 0，但后面的不一定是 0，而是 start























