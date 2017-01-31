# Problem 95: Unique Binary Search Trees II

> https://leetcode.com/problems/unique-binary-search-trees-ii/

-------
##思路
* 用 divide and conquer 的思路来考虑这道题。对于每一个 node 都可以分成左子树和右子树，recursion，然后连接到当前 node 然后加入 list 中

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
    public List<TreeNode> generateTrees(int n) {
        if (n < 1) {
            return new ArrayList<TreeNode>();
        }
        return subtreeHelper(1, n);
    }
    
    private List<TreeNode> subtreeHelper(int start, int end) {
        List<TreeNode> rst = new ArrayList<TreeNode>();
        if (start > end) {
            rst.add(null);
            return rst;
        }
        
        for (int i = start; i <= end; i++) {
            List<TreeNode> leftSubtree = subtreeHelper(start, i - 1);
            List<TreeNode> rightSubtree = subtreeHelper(i + 1, end);
            for (TreeNode left : leftSubtree) {
                for (TreeNode right : rightSubtree) {
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    rst.add(root);
                }
            }
        }
        
        return rst;
    }
}

```

