# Problem 156: Binary Tree Upside Down

> https://leetcode.com/problems/binary-tree-upside-down/

------
![](/assets/treeUpsideDown.png)

-----
##思路
![](/assets/upsideGraph.png)
* 观察上图，翻转的过程首先一路向左，找到“极左”的元素，这个点就是新的 tree 的 root。然后跟右边的元素连接并且断掉之前的元素的连接。

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
    public TreeNode upsideDownBinaryTree(TreeNode root) {
        if (root == null || root.left == null && root.right == null) return root;
        
        TreeNode newNode = upsideDownBinaryTree(root.left);
        root.left.left = root.right;
        root.left.right = root;
        
        root.left = null;
        root.right = null;
        
        return newNode;
    }
}
```

