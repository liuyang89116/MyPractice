# Problem 173: Binary Search Tree Iterator

##思路
* 这道题的难点在于理解题目的意思：题目是说找到**下一个最小的数**，而不是判断下一个数在哪儿。否则如果是找下一个数的话，直接找就是当前结点的右边。
* 这道题相当用 DFS 求解，用一个 stack 来维护一个最小值，就是一直把最左边的结点装到 stack 里面，用 stack pop 下一个最小值出来

---------------
```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

public class BSTIterator {

    private Stack<TreeNode> stack = new Stack<TreeNode>();
    private TreeNode curr;
    
    public BSTIterator(TreeNode root) {
        this.curr = root;    
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return curr != null || !stack.isEmpty();
    }

    /** @return the next smallest number */
    public int next() {
        while (curr != null) {
            stack.push(curr);
            curr = curr.left;
        }
        TreeNode node = stack.pop();
        curr = node.right;
        return node.val;
        
    }
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */
```
--------