# Problem 333: Largest BST Subtree

> https://leetcode.com/problems/largest-bst-subtree/\#/description

----------

![](/assets/333.png)



----------

## 思路

* 通过递归，不断判断更大一些的子树。但这里面有很多易错的地方
* `isValid()`方程的参数，用 Integer 类型来代表 min 和 max 而不是 `Integer.MIN_VALUE`，因为后面需要用 `null`来判断是否为空，要不要继续递归
* BST 要求每个值不能相同，所以是 `>=`

------

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
    public int largestBSTSubtree(TreeNode root) {
        if (root == null) return 0;
        if (root.left == null && root.right == null) return 1;
        if (isValid(root, null, null)) return countNodes(root);
        
        return Math.max(largestBSTSubtree(root.left), largestBSTSubtree(root.right));
    }
    
    private boolean isValid(TreeNode root, Integer min, Integer max) {
        if (root == null) return true;
        if (min != null && root.val <= min) return false;
        if (max != null && root.val >= max) return false;
        
        return isValid(root.left, min, root.val) && isValid(root.right, root.val, max);
    }
    
    private int countNodes(TreeNode root) {
        if (root == null) return 0;
        if (root.left == null && root.right == null) return 1;
        
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}

```



