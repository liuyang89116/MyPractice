# Problem 250: Count Univalue Subtrees

> https://leetcode.com/problems/count-univalue-subtrees/

------
![](/assets/CountUniValue.png)

----
##思路
* subtree 一样，是说 node 的值和它左右子树的值都想同
* 那我们如何统计所有的结点呢？可以 preorder 遍历所有的结点，然后对于每一个结点，判断它的孩子们是否和它的值都相同，这样就可以没有遗漏也不重复地扫过所有的 nodes 了。
* 对于判断每一个 node 的时候，用一个 flag 来标记它是否是唯一的。然后递归所有的子树。

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
    public int countUnivalSubtrees(TreeNode root) {
        if (root == null) return 0;
        
        int count = isUni(root) ? 1 : 0;
        return count + countUnivalSubtrees(root.left) + countUnivalSubtrees(root.right);
    }
    
    private boolean isUni(TreeNode root) {
        boolean flag = true;
        if (root.left != null) {
            flag &= (root.val == root.left.val);
            flag &= isUni(root.left);
        }
        if (root.right != null) {
            flag &= (root.val == root.right.val);
            flag &= isUni(root.right);
        }
        
        return flag;
    }
}
```

