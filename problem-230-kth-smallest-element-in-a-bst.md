# Problem 230: Kth Smallest Element in a BST

> https://leetcode.com/problems/kth-smallest-element-in-a-bst/

----------
##思路
* 利用 iterative 的方法遍历整个 tree，到了第 k 个的时候就停下

---------
##复杂度
* Time: `O(n)`
* Space: `O(n)`

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
        Stack<TreeNode> stack = new Stack<>();
        while (root != null || !stack.isEmpty()) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            if (--k == 0) break;
            root = root.right;
        }
        
        return root.val;
    }
}
```

