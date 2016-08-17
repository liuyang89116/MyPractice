# Problem 98: Validate Binary Search Tree

> https://leetcode.com/problems/validate-binary-search-tree/

--------------------------
##思路
* 分治思想，有几个点很容易出错;
* 关键点：左边的最大要小于root，右边的最小要小于root。这样才能成为一个 binary search tree.
--------------
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
    public class ResultType {
        boolean is_bst;
        int min, max;
       
        public ResultType(boolean is_bst, int max, int min) {
            this.is_bst = is_bst;
            this.max = max;
            this.min = min;
        }
    }
    
    public boolean isValidBST(TreeNode root) {
        ResultType result = validateHelper(root);
        return result.is_bst;
    }
    
    private ResultType validateHelper(TreeNode root) {
        if (root == null) {
            return new ResultType(true, Integer.MIN_VALUE, Integer.MAX_VALUE);
        }
        
        ResultType left = validateHelper(root.left);
        ResultType right = validateHelper(root.right);
        
        if (!left.is_bst || !right.is_bst) {
            return new ResultType(false, 0, 0);
        }
        if (root.left != null && left.max >= root.val || root.right != null && right.min <= root.val) {
            return new ResultType(false, 0, 0);
        }
        
        int min = Math.min(root.val, left.min);
        int max = Math.max(root.val, right.max);
        
        return new ResultType(true, max, min);
        
    }
}

```
------------------
##易错点

1. root为空的情况。
```java
if (root == null) {
       return new ResultType(true, Integer.MIN_VALUE, Integer.MAX_VALUE);
}
```
这里的 min 和 max 跟 ResultType 里正好是相反的！原因我感觉是因为是空，所以就把原来的彻底地反过来。

2. 条件判断，**非常易错**
```java
if (root.left != null && left.max >= root.val || root.right != null && right.min <= root.val) {
       return new ResultType(false, 0, 0);
}
```
注意看这里是```root.left != null```和```left.max >= root.val```！

  而我错就错在写成了```left.max >= root.val```！这种情况下，当 left 本身为空的时候，直接就会出错。
