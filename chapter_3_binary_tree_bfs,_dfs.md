# Chapter 3 Binary Tree (BFS, DFS)


> https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

----------
##思路
* preorder: 根-左-右  
  inorder: 左-根-右  
  可以发现的规律是：
	1. 先序遍历的从左数第一个为整棵树的根节点。
	2. 中序遍历中根节点是左子树右子树的分割点。
* 具体解决方法是：  
	1.通过先序遍历找到第一个点作为根节点，在中序遍历中找到根节点并记录index。  
	2.因为中序遍历中根节点左边为左子树，所以可以记录左子树的长度并在先序遍历中依据这个长度找到左子树的区间，用同样方法可以找到右子树的区间。  
	3.递归的建立好左子树和右子树就好。

---------
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int preLength = preorder.length;
        int inLength = inorder.length;
        if (preLength != inLength) {
            return null;
        }
        
        return helper(preorder, 0, preLength - 1, inorder, 0, inLength - 1);
    }
    
    private TreeNode helper(int[] preorder, int preStart, int preEnd, int[] inorder, int inStart, int inEnd) {
        if (preStart > preEnd || inStart > inEnd) {
            return null;
        }
        int rootVal = preorder[preStart];
        int rootIndex = findIndex(inorder, inStart, inEnd, rootVal);
        int len = rootIndex - inStart;
        
        TreeNode root = new TreeNode(rootVal);
        root.left = helper(preorder, preStart + 1, preStart + len, inorder, inStart, rootIndex - 1);
        root.right = helper(preorder, preStart + len + 1, preEnd, inorder, rootIndex + 1, inEnd);
        
        return root;
    }
    
    private int findIndex(int[] inorder, int start, int end, int rootVal) {
        for (int i = start; i <= end; i++) {
            if (inorder[i] == rootVal) {
                return i;
            }
        }
        
        return -1;
    }
    
}
```
-----
##易错点
1. 先建立了 TreeNode 对象，后面才能进行 left 和 right 的递归
```java
TreeNode root = new TreeNode(rootVal);
```
2. 换算好 index 之间的关系
```java
root.left = helper(preorder, preStart + 1, preStart + len, inorder, inStart, rootIndex - 1);
root.right = helper(preorder, preStart + len + 1, preEnd, inorder, rootIndex + 1, inEnd);
```














