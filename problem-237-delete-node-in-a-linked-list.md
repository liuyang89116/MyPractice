# Problem 237: Delete Node in a Linked List

> https://leetcode.com/problems/delete-node-in-a-linked-list/

-------
##思路
* 删除结点就是把这个节点和下下个节点相连。这里有个前提条件是**删除的结点不是最后一个尾巴结点**。
* 我们可以通过赋值的方法删除。

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
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```


