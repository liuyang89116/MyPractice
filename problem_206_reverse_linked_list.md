# Problem 206: Reverse Linked List


> https://leetcode.com/problems/reverse-linked-list/

---------------------------

##思路
这是一道经典并且基本的题目，理解这道题可以很好地理解 Linked List。先附上一个讲解的视频

> https://www.youtube.com/watch?v=sYcOK51hl-A

* 反转链表，主要地是要学会反转指针
* 思路上可以说就是交换所有的prev和next指针











---------------------------
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
    public ListNode reverseList(ListNode head) {
        if (head == null) {
            return head;
        }
        
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




