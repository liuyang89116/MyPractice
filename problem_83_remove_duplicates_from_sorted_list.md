# Problem 83: Remove Duplicates from Sorted List


> https://leetcode.com/problems/remove-duplicates-from-sorted-list/

--------------------------------------------------------------------
##思路
* 删除的思路，就好像插队一样。假如你后面有好多人，你的下下个人直接跟在你们之间，那么你后面的人就被“删除”了。

--------------------------------

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
        if (head == null) {
            return head;
        }
        ListNode node = head;
        while (node.next != null) {
            if (node.next.val == node.val) {
                node.next = node.next.next;
            } else {
                node = node.next;
            }
        }
        return head;
    }
}
```

-----------------------
##易错点

1. 和数组类似，链表也是要check corner cases的。
   ```java
   if (head == null) {
       return head;
   }
   ```
2. 如果不担心空指针的时候，可以用两个指针，创建一个指针，随后返回原来的结构
   ```java
   ListNode node = head;
   while (node.next != null) {
       if (node.next.val == node.val) {
           node.next = node.next.next;
       } else {
           node = node.next;
       }
   }
   return head;
   ```




















