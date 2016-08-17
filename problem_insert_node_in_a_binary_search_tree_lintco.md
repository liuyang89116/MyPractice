# Problem: Insert Node in a Binary Search Tree (LintCode)


> http://www.lintcode.com/en/problem/insert-node-in-a-binary-search-tree/#

-------------------------------
##思路
* 用recursion来实现。值小于root，挂左边；值大于root，挂右边。

--------------------
```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param node: insert this node into the binary search tree
     * @return: The root of the new binary search tree.
     */
    public TreeNode insertNode(TreeNode root, TreeNode node) {
        if (root == null) {
            return node;
        }
        
        if (node.val < root.val) {
            root.left = insertNode(root.left, node);
        } else {
            root.right = insertNode(root.right, node);
        }
        
        return root;
    }
}
```

------------
##易错点

1. 左右子树要有人接收
```java
root.left = insertNode(root.left, node);
```
之前我只写了```insertNode(root.left, node);```但因为这个函数是有返回值的，所以一定不能忘。































