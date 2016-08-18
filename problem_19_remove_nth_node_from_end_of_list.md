# Problem 19: Remove Nth Node From End of List


> https://leetcode.com/problems/remove-nth-node-from-end-of-list/

------------------
##思路
* 这是一个快慢指针的经典问题
* 因为LinkedList的特殊性，我们很难得到它的size并定位要删除的元素。那怎么从末尾向前数 n 个呢？
* 快慢指针！两个指针都在同一个出发点。快指针先走 n 步，那快慢指针之间的距离就是 n 步。这是他们再同时出发，当快指针到达最末尾的时候，慢指针所在的位置就是要删除的位置！

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (n <= 0) {
            return null;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode preDelete = dummy;
        for (int i = 0; i < n; i++) {
            head = head.next;
        }
        while (head != null) {
            head = head.next;
            preDelete = preDelete.next;
        }
        preDelete.next = preDelete.next.next;
        
        return dummy.next;
    }
}
```

--------
##易错点

1. 删掉一个元素
```java
preDelete.next = preDelete.next.next;
```
就是跳过这个元素与他后边的元素连接。

2. 从 0 开始出发
```java
for (int i = 0; i < n; i++) {
       head = head.next;
}
```






























