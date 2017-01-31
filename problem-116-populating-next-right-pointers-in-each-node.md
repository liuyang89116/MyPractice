# Problem 116: Populating Next Right Pointers in Each Node

> https://leetcode.com/problems/populating-next-right-pointers-in-each-node/

--------------
##思路
* 题目已经强调了是 perfect tree
* 这道题的意思是，在原有的树的结构上，再把剩下的叶子根据条件也连起来。每次连的过程是由上边的“顶点”连它下面的左叶子和右叶子，如果顶点没有了 next，那么下边右子树将要直接指向 null。画个图就明白了。

----------


```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        while (root != null) {
            TreeLinkNode node = root;
            while (node != null && node.left != null) {
                node.left.next = node.right;
                node.right.next = (node.next == null ? null : node.next.left);
                node = node.next;
            }
            root = root.left;
        }
    }
}
```

