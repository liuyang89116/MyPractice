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
## Template 2: Divide and Conquer
```java
/*
    Template 2: Divide and Conquer
*/

public class Solution {
    public ResultType traverse(TreeNode root) {
        if (root == null) {
            //do something and return;
            //return condition
        }

        //divide
        ResultType left = traverse(root.left);
        ResultType right = traverse(root.right);
        //conquer
        ResultType result = Merge from left and right;
        return result;
    }
}


```