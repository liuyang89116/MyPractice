# Problem 270: Closest Binary Search Tree Value

> https://leetcode.com/problems/closest-binary-search-tree-value/\#/description

---------

![](/assets/270.png)

--------

## 思路

* 这道题在 Google 面试的时候遇到了，当时竟然懵逼了。主要是当时没有注意是 Binary Search Tree，也就是隐含了一个信息是：

所有的元素是从左到右排列好的。

* 用个一个元素标记最接近的值，然后遇到更接近的就更新。
* root 走的方向通过最接近的路径走。



--------



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
    public int closestValue(TreeNode root, double target) {
        int closest = root.val;
        while (root != null) {
            if (Math.abs(root.val - target) < Math.abs(closest - target)) closest = root.val;
            
            root = (root.val > target ? root.left : root.right);
        }
        
        return closest;
    }
}
```



