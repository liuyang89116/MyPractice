# Problem 437: Path Sum III

> https://leetcode.com/problems/path-sum-iii/

----
##思路
* 这道题相当于是两部分的递归，第一部分递归这个树，对于每个 root，设计到了第二部分的递归 -- 求 count 数
* 这两部分的递归一定要先想清楚，否则主函数的 return 很容易写错

----


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
    public int pathSum(TreeNode root, int sum) {
        if (root == null) return 0;
        
        return countPath(root, sum) + pathSum(root.left, sum) + pathSum(root.right, sum);
    }
    
    private int countPath(TreeNode root, int sum) {
        if (root == null) return 0;
        
        int count = 0;
        if (root.val == sum) count++;
        count += countPath(root.left, sum - root.val);
        count += countPath(root.right, sum - root.val);
        
        return count;
    }
}
```


