# Problem: Convert Binary Search Tree to Doubly Linked List (LintCode)

> http://www.lintcode.com/en/problem/convert-binary-search-tree-to-doubly-linked-list/

----------
##思路
* 还是用 inorder 遍历的方式 traverse 一遍 nodes，然后用他们组成 Doubly Linked List

----------


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
 * Definition for Doubly-ListNode.
 * public class DoublyListNode {
 *     int val;
 *     DoublyListNode next, prev;
 *     DoublyListNode(int val) {
 *         this.val = val;
 *         this.next = this.prev = null;
 *     }
 * }
 */ 
public class Solution {
    /**
     * @param root: The root of tree
     * @return: the head of doubly list node
     */
    public DoublyListNode bstToDoublyList(TreeNode root) {  
        // Write your code here
        if (root == null) {
            return null;
        }
        
        DoublyListNode head = new DoublyListNode(0);
        DoublyListNode tail = head;
        Stack<TreeNode> stack = new Stack<>();
        DoublyListNode prev = null;
        while(root != null || !stack.isEmpty()) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            DoublyListNode curr = new DoublyListNode(root.val);
            tail.next = curr;
            curr.prev = prev;
            tail = tail.next;
            
            prev = new DoublyListNode(root.val);
            root = root.right;
            
        }
        
        return head.next;
    }
}

```

