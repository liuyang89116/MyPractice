# Problem 272: Closest Binary Search Tree Value II

> https://leetcode.com/problems/closest-binary-search-tree-value-ii/\#/description

----------

![](/assets/272.png)

-----

## 思路

* 用两个 stack 来维护，一个 small，存比 target 小的 node；另一个 large，存比 target 大的 nodes.
* 当取出一个 small value 的时候，再补充一个和 target 接近的 node，也就是 push 右子树进去。large value 同理。



----------

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
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        List<Integer> list = new ArrayList<>();
        Stack<TreeNode> small = new Stack<>();
        Stack<TreeNode> large = new Stack<>();
        TreeNode cur = root;
        while (cur != null) {
            if (cur.val >= target) {
                large.push(cur);
                cur = cur.left;
            } else {
                small.push(cur);
                cur = cur.right;
            }
        }
        
        while (k > 0) {
            if (small.isEmpty() && large.isEmpty()) {
                break;
            } else if (small.isEmpty()) {
                list.add(getLargeValue(large));
            } else if (large.isEmpty()) {
                list.add(getSmallValue(small));
            } else if (Math.abs(target - small.peek().val) < Math.abs(target - large.peek().val)) {
                list.add(getSmallValue(small));
            } else {
                list.add(getLargeValue(large));
            }
            
            k--;
        }
        
        
        return list;
     }
     
     private int getSmallValue(Stack<TreeNode> stack) {
         TreeNode node = stack.pop();
         TreeNode left = node.left;
         while (left != null) {
             stack.push(left);
             left = left.right;
         }
         
         return node.val;
     }
     
     private int getLargeValue(Stack<TreeNode> stack) {
         TreeNode node = stack.pop();
         TreeNode right = node.right;
         while (right != null) {
             stack.push(right);
             right = right.left;
         }
         
         return node.val;
     }
    
}

```



