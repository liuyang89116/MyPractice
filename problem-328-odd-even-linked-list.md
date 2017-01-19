# Problem 328: Odd Even Linked List

> https://leetcode.com/problems/odd-even-linked-list/

----------
##思路
* 这道题的思路就是，单数连单数，双数连双数，最后把 odd 和 even 的头连接起来。所以我们需要维护一个 even 的头。
* 注意这里 odd 和 even 是两个两个跳的，所以 `odd = odd.next` 实际上是跳了两个。
![](/assets/oddEvenLinkedList.png)

--------
##复杂度
* Time: O(n)
* Space: O(1)
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
public class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode odd = head;
        ListNode even = head.next, evenHead = head.next;
        while (even != null && even.next != null) {
            odd.next = odd.next.next;
            even.next = even.next.next;
            odd = odd.next;
            even = even.next;
        }
        odd.next = evenHead;
        
        return head;
    }
}
```
------
##易错点
1. 注意判断 head 的情况，在最开始的时候


