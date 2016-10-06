# Problem 21: Merge Two Sorted Lists

> https://leetcode.com/problems/merge-two-sorted-lists/

-------
##思路
*　基础题目，熟练掌握。主要就是按顺序排队，谁小谁排在前面。

-------
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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode lastNode = dummy;
        
        while(l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                lastNode.next = l1;
                l1 = l1.next;
            } else {
                lastNode.next = l2;
                l2 = l2.next;
            }
            lastNode = lastNode.next;
        }
        
        if (l1 != null) {
            lastNode.next = l1;
        } else {
            lastNode.next = l2;
        }
        
        return dummy.next;
    }
}
```
------
##易错点
1. 三根指针都要移动，别忘了 lastNode 的移动
2. 第一个 while 循环完，记得后面 check 两个 list 还有没有剩余
3. 注意最后判断是 if 并不是 while！  
   只有数组才是 while， linkedlist 是连着的，判断一下 head 就可以挂上了。


























