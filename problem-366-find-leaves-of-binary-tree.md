# Problem 366: Find Leaves of Binary Tree

> https://leetcode.com/problems/find-leaves-of-binary-tree/\#/description

---------

## 思路

* 对于一个叶子来说，就是左子树和右子树均为空。所以我们的任务其实就是一层一层地取叶子。
* 怎么判断叶子呢？ 求最大深度。为什么是最大深度？因为每次都是把当前的最大深度的那层叶子先放到 list 里面，然后去找下一层。
* 也就是说，rst 的 size 和最大深度是同步增加的。

--------------

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
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> rst = new ArrayList<>();
        height(root, rst);
        
        return rst;
    }
    
    private int height(TreeNode root, List<List<Integer>> rst) {
        if (root == null) return -1;
        
        int level = 1 + Math.max(height(root.left, rst), height(root.right, rst));
        if (rst.size() < level + 1) {
            rst.add(new ArrayList<>());
        }
        rst.get(level).add(root.val);
        
        return level;
    }
}







```





