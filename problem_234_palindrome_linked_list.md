# Problem 234: Palindrome Linked List


> https://leetcode.com/problems/palindrome-linked-list/

---------
##思路
* 这道题就是基本功的训练
* 找到中点，前后一分为二，后面的 reverse 之后应该和前面一样，这样才是 Palindrome

----------
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null) {
            return true;
        }
        
        ListNode mid = getMiddle(head);
        mid.next = reverse(mid.next);
        ListNode p1 = head, p2 = mid.next;
        while (p1 != null && p2 != null && p1.val == p2.val) {
            p1 = p1.next;
            p2 = p2.next;
        }
        
        return p2 == null;
    }
    
    private ListNode getMiddle(ListNode head) {
        if (head == null) {
            return head;
        }
        
        ListNode slow = head, fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
    }
    
    private ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        
        return prev;
    }
}
```
------
##易错点
1. 熟记链表的翻转和找中点
2. p1 和 p2 的初始位置
```java
p2 = mid.next;
```
