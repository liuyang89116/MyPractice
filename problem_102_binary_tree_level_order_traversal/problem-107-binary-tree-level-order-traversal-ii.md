# Problem 107: Binary Tree Level Order Traversal II

> https://leetcode.com/problems/binary-tree-level-order-traversal-ii/

------
##思路
* 当时看到这个题的时候，想了好久。怎么才能自下而上地遍历每一个 level 的结点呢？先用 BFS 遍历每一个 level 然后用额外的 stack 存他们？其实想多了，只需要在上一个题目的基础上，每次把新的 level 的元素存到开头就可以了！这样后面的元素反而放在前面！

-----


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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<Integer> level = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(level);
        if (root == null) return rst;
        
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            level = new ArrayList<Integer>();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            rst.add(0, level);
        }
        
        return rst;
    }
}
```

