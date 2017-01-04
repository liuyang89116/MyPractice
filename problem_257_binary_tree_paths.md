# Problem 257: Binary Tree Paths

>https://leetcode.com/problems/binary-tree-paths/

-------------
##思路
* 经典题目，主要在于如何设置递归的情景

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> rst = new ArrayList<String>();
        if (root == null) {
            return rst;
        }
        
        helper(root, String.valueOf(root.val), rst);
        return rst;
    }
    
    private void helper(TreeNode root, String path, List<String> rst) {
        if (root == null) {
            return;
        }
        
        if (root.left == null && root.right == null) {
            rst.add(path);
            return;
        }
        if (root.left != null) {
            helper(root.left, path + "->" + String.valueOf(root.left.val), rst);
        }
        if (root.right != null) {
            helper(root.right, path + "->" + String.valueOf(root.right.val), rst);
        }
    }
}

```
--------
##易错点
1. 递归 path
```java
helper(root.left, path + "->" + String.valueOf(root.left.val), rst);
```
这里 path 是一个变量，下一层递归的时候，作为之前的变量带入给对方

2. 加完 path 后，记得要 return
```java
if (root.left == null && root.right == null) {
        rst.add(path);
        return;
}
```

---------
##Follow Up
> 如果所有的node在一条线上，时间复杂度?

* `O(n)`

> 如果是 full binary tree，时间复杂度？

* 如果不优化，直接用 String 来做的话，每次相当于创建一个 String，`O(n^2)`
* 如果优化的话，是`O(nlogn)`










