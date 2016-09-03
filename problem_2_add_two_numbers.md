# Problem 2: Add Two Numbers

> https://leetcode.com/problems/add-two-numbers/

----------
##思路
* 这道题就是“逐位加法”的例子：进位 carrier，每个位置顺序往上加，超过 10 就进位。
* carrier 最后如果大于 0 的话，扩大原来的 size，把这一位补上 1

-----------
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null && l2 == null) {
            return null;
        }
        
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;
        int carrier = 0;
        while (l1 != null && l2 != null) {
            int sum = carrier + l1.val + l2.val;
            head.next = new ListNode(sum % 10);
            carrier = sum / 10;
            l1 = l1.next;
            l2 = l2.next;
            head = head.next;
        }
        while (l1 != null) {
            int sum = carrier + l1.val;
            head.next = new ListNode(sum % 10);
            carrier = sum / 10;
            l1 = l1.next;
            head = head.next;
        }
        while (l2 != null) {
            int sum = carrier + l2.val;
            head.next = new ListNode(sum % 10);
            carrier = sum / 10;
            l2 = l2.next;
            head = head.next;
        }
        
        if (carrier != 0) {
            head.next = new ListNode(carrier);
        }
        
        return dummy.next;
    }
}
```
----
##易错点
1. 记得设置 dummy node，否则会对整个 list 失去“控制”


