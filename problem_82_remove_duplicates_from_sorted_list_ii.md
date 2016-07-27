# Problem 82: Remove Duplicates from Sorted List II


> https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/

----------------------
##思路
这道题和上一道题的区别就是，这道题可能把“头”删除造成空指针异常。这就需要我们引入dummy node，哨兵结点

--------------------
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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        while (head.next != null && head.next.next != null) {
            if (head.next.val == head.next.next.val) {
                int val = head.next.val;
                while (head.next != null && head.next.val == val) {
                    head.next = head.next.next;
                }
            } else {
                head = head.next;
            }
        }
        return dummy.next;
    }
)
```
--------------
##易错点


