# Subtree



```java
package Subtree;

/**
 * Created by yang on 1/17/17.
 */
class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int x) {
        this.val = x;
    }
}

public class Solution {
    public static boolean isSubTree(TreeNode T1, TreeNode T2) {
        if (T2 == null) {
            return true;
        }
        if (T1 == null) {
            return false;
        }

        return (isSameTree(T1, T2)) || (isSubTree(T1.left, T2)) || (T1.right,T2);
    }

    public static boolean isSameTree(TreeNode T1, TreeNode T2) {
        if (T1 == null && T2 == null) {
            return true;
        }
        if (T1 == null || T2 == null) {
            return false;
        }
        if (T1.val != T2.val) {
            return false;
        }

        return isSameTree(T1.left, T2.left) && isSameTree(T1.right, T2.right);
    }
}

```



