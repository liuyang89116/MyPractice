# Summary 1: DFS Template

-------------------------------------------------------------
##Template 1: Traverse

其实本质上也是一种分治递归

```java
/*
    Template 1: Traverse
*/

public class Solution {
    public void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        // do something with root
        traverse(root.left);
        // do something with root
        traverse(root.right);
    }
}

```
------------------------------------
