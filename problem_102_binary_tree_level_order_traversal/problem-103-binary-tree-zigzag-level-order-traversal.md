# Problem 103: Binary Tree Zigzag Level Order Traversal

> https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

----
##思路
* 这道题和前面是一样的，只是这里需要一个 flag 来标记，是从前往后加元素还是从后往前加元素
* 如果上一次是从前往后，那么下一次就是从后往前。把这个搞清楚，就没有问题了。

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<Integer> level = new ArrayList<Integer>();
        List<List<Integer>> rst = new ArrayList(level);
        if (root == null) return rst;
        
        boolean flag = false;
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            level = new ArrayList<Integer>();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (flag) {
                    level.add(0, node.val);
                } else {
                    level.add(node.val);
                }
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            rst.add(level);
            flag = !flag;
        }
        
        return rst;
    }
}
```


