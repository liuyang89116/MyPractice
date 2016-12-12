# Problem 111: Minimum Depth of Binary Tree


> https://leetcode.com/problems/minimum-depth-of-binary-tree/

----------
##思路
* **这道题看着不难，但是不能直接用 Maximum Depth 的那个方法去做**
* 因为当我们递归的时候：当一个结点只有左子树或者右子树，**我们不能直接返回 0，因为压根儿这边就没有树，谈不上是不是最小**。我们要返回另一半的 depth (也就是 left + 1 或者 right + 1)。

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
        
        int left = minDepth(root.left);
        int right = minDepth(root.right);
        if (left == 0 || right == 0) {
            return left > right ? left + 1 : right + 1;
        }
        
        return Math.min(left, right) + 1;
    }
}

```

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














