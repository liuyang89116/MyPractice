# Problem 109: Convert Sorted List to Binary Search Tree


> https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/

--------------
##思路
* 这道题依然是用了分治的思想，但在这之前，学会把问题拆成一些很小的 subproblem
* 这道题分治的主体就是**找中点**。那么显而易见，我们就要知道这个LinkedList的长度。、

------------
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
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
    
    private ListNode current;
    
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) {
            return null;
        }
        current = head;
        int size = getListSize(head);
        
        return sortedListToBSTHelper(size);
    }
    
    private int getListSize(ListNode head) {
        int size = 0;
        
        while (head != null) {
            size++;
            head = head.next;
        }
        return size;
    }
    
    private TreeNode sortedListToBSTHelper(int size) {
        if (size <= 0) {
            return null;
        }
        
        TreeNode left = sortedListToBSTHelper(size / 2);
        TreeNode root = new TreeNode(current.val);
        current = current.next;
        TreeNode right = sortedListToBSTHelper(size - size / 2 - 1);
        
        root.left = left;
        root.right = right;
        
        return root;
    }
}
```
--------------
##易错点

1. 定义一个全局变量 current node
```java
private ListNode current;
```
2. 
















