# Problem 110: Balanced Binary Tree

> [https://leetcode.com/problems/balanced-binary-tree/](https://leetcode.com/problems/balanced-binary-tree/)

---

## 思路

实际上还是求最大深度的问题

---

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
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        return maxDepth(root) != -1;
    }

    private int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        if (left == -1 || right == -1 || Math.abs(left - right) > 1) {
            return -1;
        }
        return Math.max(left, right) + 1;
    }
}
```

---

## 复杂度

* 每个 node 相当于被 access 了一次，所以复杂度为 `O(n)`

---

## 易错点

1. 开始的时候落下一点：

   ```java
   if (left == -1 || right == -1 || Math.abs(left - right) > 1) {
       return -1;
   }
   ```

   其中的

   ```java
   left == -1 || right == -1
   ```

   这个是很重要的一点：如果没有他俩，相当于我只考虑到了最后的左子树和右子树的差值是否大于1，其实任何一  个子树的分支如果大于1,都应该立马断定这是不平衡的。

2. 简洁的写法

   ```java
    return maxDepth(root) != -1;
   ```

   学习一下！



