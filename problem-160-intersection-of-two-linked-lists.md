# Problem 160: Intersection of Two Linked Lists

> https://leetcode.com/problems/intersection-of-two-linked-lists/

-------------
##思路
* 这道题的潜意识是说，两个 list 在最后的某一段会重合（也许根本就不会）
* 所以我们先把两个 list 的长度对齐，然后挨个进行比较。

-----------


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        
        int lenA = getLength(headA);
        int lenB = getLength(headB);
        if (lenA < lenB) {
            return getIntersectionNode(headB, headA);
        }
        
        while (lenA > lenB) {
            headA = headA.next;
            lenA--;
        }
        while (headA != headB) {
            headA = headA.next;
            headB = headB.next;
        }
        
        return headA;
    }
    
    private int getLength(ListNode head) {
        int count = 0;
        while (head != null) {
            head = head.next;
            count++;
        }
        return count;
    }
}
```

