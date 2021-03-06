# Problem 141: Linked List Cycle

> https://leetcode.com/problems/linked-list-cycle/

-----------
##思路
* 快慢指针问题：当快慢指针能相遇，就说明是有环的

------------
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != slow) {
            if (fast == null || fast.next == null) {
                return false;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        return true;
    }
}
```
--------
##易错点
1. 在while循环当中的退出条件
```java
if (fast == null || fast.next == null) {
       return false;
}
```
只需要考虑快指针是否会越界就好了，因为如果快指针都没事儿的话，那么慢指针肯定没问题。  
2. 有环的话是不会走到尽头的，会一直循环。

