# Problem 515: Find Largest Value in Each Tree Row

> https://leetcode.com/problems/find-largest-value-in-each-tree-row/\#/description

----------

## 思路

* 这道题实际上就是 binary tree level order 遍历的思想，在遍历的时候每次取出最大值存入 list 即可
* 注意 add max 的位置：while 循环里面，for 循环外面。for 循环为的是遍历整个 level



---------

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
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> rst = new ArrayList<Integer>();
        if (root == null) return rst;
        
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            int max = Integer.MIN_VALUE;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                max = Math.max(max, node.val);
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            
            rst.add(max);
        }
        
        return rst;
    }
}
```



