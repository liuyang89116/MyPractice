# Problem 148: Sort List


> https://leetcode.com/problems/sort-list/

-------
##思路
* 看到时间复杂度要求o(nlogn)，首先应该想到要用merge sort
* 庖丁解牛的思路：首先是分治思想，sort左边，sort右边，最后merge到一起。
* 这时候就涉及到链表的两个基本操作：找中点和merge

----------------
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
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode mid = findMiddle(head);
        ListNode right = sortList(mid.next);
        mid.next = null;
        ListNode left = sortList(head);
        return merge(left, right);
    }
    
    private ListNode findMiddle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
    }
    
    private ListNode merge(ListNode head1, ListNode head2) {
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        
        while (head1 != null && head2 != null) {
            if (head1.val < head2.val) {
                tail.next = head1;
                head1 = head1.next;
            } else {
                tail.next = head2;
                head2 = head2.next;
            }
            tail = tail.next;
        }
        if (head1 != null) {
            tail.next = head1;
            tail = tail.next;
        }
        if (head2 != null) {
            tail.next = head2;
            tail = tail.next;
        }
        
        return dummy.next;
    }
}

```
--------
##易错点

1. 找中点
```java
private ListNode findMiddle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
}
```
**快慢指针**：慢指针一次走一步，快指针一次走两步，当快指针走到头了，慢指针正好在中点位置。
**注意**：退出条件是
```java
while (fast != null && fast.next != null) {
}
```
2. sort是一个递归的过程
```ListNode right = sortList(mid.next);```而我第一次写的时候是```ListNode right = mid.next;```。这样只sort一次就停止了，是不对的。
3. dummy指针
dummy指针设计的时候永远是两个：一个用来标记“头”，一个用来探路。
```java
ListNode dummy = new ListNode(0);
ListNode tail = dummy;
```































