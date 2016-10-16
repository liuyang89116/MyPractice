# Problem 230: Kth Smallest Element in a BST

> https://leetcode.com/problems/kth-smallest-element-in-a-bst/

-----------
##思路
* 这道题虽然不难，但是对于理解递归和 Binary Search 很好
* 首先就是看左边有几个 nodes，如果 nodes 数加上 1 为 k 的话，就返回 root 的 val 值。如此一直递归

------------
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
    public int kthSmallest(TreeNode root, int k) {
        if (root == null) {
            return 0;
        }
        
        int nodesNum = countNodes(root.left);
        if (nodesNum + 1 == k) {
            return root.val;
        } else if (nodesNum + 1 > k) {
            return kthSmallest(root.left, k);
        } else {
            return kthSmallest(root.right, k - nodesNum - 1);
        }
    }
    
    private int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```
------
##易错点
1. 判断条件的时候懵了一下，写错了
```java
if (nodesNum + 1 > k) {
       return kthSmallest(root.left, k);
}
```
左边有很多 nodes 的时候，就在左边直接找就好了














