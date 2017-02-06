# Problem 129: Sum Root to Leaf Numbers

> https://leetcode.com/problems/sum-root-to-leaf-numbers/

----
##思路
* 当时看到这道题的第一反应是遍历整个树，然后把所有的 pattern 存起来，最后相加。但是这样做效率太低，其实可以就像 string 相加那样，一边 traverse，一边就可以相加了。
* 在 recursion 的时候，最后 root.left 和 root.right 是同时进行的，最开始我写成了 `sum += helper(root.left, sum * 10 + root.val)`，这样在递归 right 的时候，**sum 值已经发生了改变！**

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
    public int sumNumbers(TreeNode root) {
        return helper(root, 0);
    }
    
    private int helper(TreeNode root, int sum) {
        if (root == null) return 0;
        
        if (root.left == null && root.right == null) {
            return sum * 10 + root.val;
        }
        
        return helper(root.left, sum * 10 + root.val) + helper(root.right, sum * 10 + root.val);
    }
}
```

