# Problem 117: Populating Next Right Pointers in Each Node II

> https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/

-----
##思路
* 这道题不是 perfect tree 了，不能再用简单的 recursion 来解决，所以我们要用 iterative 的方法遍历整个 tree
* 总的思路就是先挂左边的结点，然后再挂右边的结点，这里用一个 dummy node 来 maintain 所有的结点顺序。
![](/assets/nextNode.png)
* 这里有几点需要注意的。比如`pre = dummy`是把 pre 的 pointer 移到 dummy 的位置
* `root = dummy.next`, `dummy.next = null` 这里把 dummy.next 的地址赋给了 root，然后把 dummy 和后面的连接断掉

-------
##复杂度
* Time: O(n)
* Space: O(1)

-------


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
        TreeLinkNode dummy = new TreeLinkNode(0);
        TreeLinkNode pre = dummy;
        while (root != null) {
            if (root.left != null) {
                pre.next = root.left;
                pre = pre.next;
            }
            if (root.right != null) {
                pre.next = root.right;
                pre = pre.next;
            }
            root = root.next;
            if (root == null) {
                pre = dummy;
                root = dummy.next;
                dummy.next = null;
            }
        }
    }
}
```

