# Problem 100: Same Tree


> https://leetcode.com/problems/same-tree/

---------
##思路

* 分治递归的思路非常重要。

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        }
        
        if (p != null && q != null) {
            return p.val == q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
        }
        
        return false;
    }
}
```
-----
##易错点
1. 在判断的过程中，要用递归的思想来判断剩下的树结构是否相等
```java
if (p != null && q != null) {
         return p.val == q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```
当时错写成了，
```java
return p.val == q.val && p.left == q.left && p.right == q.right;
```
这样做实际上判断的是 root 以及 root 的左右是否相等。 



















