# Problem 203: Remove Linked List Elements

> https://leetcode.com/problems/remove-linked-list-elements/

---------
##思路
* 利用一个 dummy node 来“领头”，然后遍历整个 list

--------


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
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        
        while (head.next != null) {
            if (head.next.val == val) {
                head.next = head.next.next;
            } else {
                head = head.next;
            }
        }
        
        return dummy.next;
    }
}
```

-------
##易错点
1. 注意逻辑体当中，是 if - else 的关系
**当初没有写 else，导致 删除完元素后又移动了一步，导致越界！
**






























