# Problem 86: Partition List


> https://leetcode.com/problems/partition-list/

----------
**类比**: Partion Array 这道题

-----------


##思路
* 创建一个left LinkedList，一个right LinkedList。
* 遇到小的挂left上，遇到大的挂right上
* 最后合并 left 和 right

---------
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
    public ListNode partition(ListNode head, int x) {
        if (head == null) {
            return head;
        }
        
        ListNode leftDummy = new ListNode(0);
        ListNode rightDummy = new ListNode(0);
        ListNode left = leftDummy;
        ListNode right = rightDummy;
        
        while (head != null) {
            if (head.val < x) {
                left.next = head;
                left = head;
            } else {
                right.next = head;
                right = head;
            }
            head = head.next;
        }
        
        right.next = null;
        left.next = rightDummy.next;
        
        return leftDummy.next;
    }
}
```
---------
##易错点

1. 两个指针，left用来探路，leftDummy用来标记“头”
```java
ListNode left = leftDummy;
ListNode right = rightDummy;
```
2. LinkedList的循环
```java
while (head != null) {
    执行语句;
    head = head.next;
}
```
其中，```head = head.next;```作为增加变量使用的。

3. 掐头去尾进行拼接
```java
right.next = null;
left.next = rightDummy.next;
```



































