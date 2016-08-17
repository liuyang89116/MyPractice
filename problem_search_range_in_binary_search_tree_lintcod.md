# Problem: Search Range in Binary Search Tree (LintCode)


> http://www.lintcode.com/en/problem/search-range-in-binary-search-tree/#

-----------------
##思路
* 二叉树就俩思路：一个是分治， 一个是recursion。
* 这道题要考虑清楚k1，k2 和 root 的关系

---------

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param k1 and k2: range k1 to k2.
     * @return: Return all keys that k1<=key<=k2 in ascending order.
     */
    
    ArrayList<Integer> result; 
     
    public ArrayList<Integer> searchRange(TreeNode root, int k1, int k2) {
        result = new ArrayList<Integer>();
        searchHelper(root, k1, k2);
        return result;
    }
    
    private void searchHelper(TreeNode root, int k1, int k2) {
        if (root == null) {
            return;
        }
        
        if (root.val > k1) {
            searchHelper(root.left, k1, k2);
        } 
        if (root.val >= k1 && root.val <= k2) {
            result.add(root.val);
        }
        if (root.val < k2) {
            searchHelper(root.right, k1, k2);
        }
    }
}
```
---------------
##易错点

1. 条件判断，**非常容易弄错**

```java
if (condition) {
    执行语句1;
} else {
    执行语句2;
}
```
这种情况下，**执行语句1,2是二选一的！**如果符合condition，就没有后面啥事了！再看下面这种，

```java
if (condition1) {
    执行语句1;
}
if (condition2) {
    执行语句2;
}
```
这种情况下，就是先执行语句1,进行一些操作，如果继续condition2,那么接着执行语句2. 非常容易搞错，一定要想清楚一个过程。

2.
   k1，k2位置的条件判断
![](SearchRange.jpg)

root如果大于k1,那么肯定在左边有一部分，就搜查一下左边；然后搜查中间；最后搜查右边。




























