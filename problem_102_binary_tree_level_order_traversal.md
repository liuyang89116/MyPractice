# Problem 102: Binary Tree Level Order Traversal


> https://leetcode.com/problems/binary-tree-level-order-traversal/

------------------
##思路
* 这道题是典型的 BFS 的实现问题

---------------
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<Integer> level = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(level);
        if (root == null) {
            return rst;
        }
        
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            level = new ArrayList<Integer>();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode head = queue.poll();
                level.add(head.val);
                if (head.left != null) {
                    queue.offer(head.left);
                }
                if (head.right != null) {
                    queue.offer(head.right);
                }
            }
            rst.add(level);
        }
        
        return rst;
    }
}
```
-----------
##易错点
1. 每次在 while 循环里都要重新建一个新的 ArrayList， 否则就会放在一起了，没有任何意义
```java
level = new ArrayList<Integer>();
```






















