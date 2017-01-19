# Problem 147: Insertion Sort List

> https://leetcode.com/problems/insertion-sort-list/

--------
##思路
* 通过一个 dummy node 和一个 prev 的指针配合来遍历整个 list。有 sort 好的就放到 dummy node 下边存着，直到上面的元素全部存完。
* prev 指针实际上就是上一个元素存到 dummy 里的位置标记，所以他永远在最后面。当 prev 比当前的 node 大了，他才重新回到 dummy 的位置，再 sort 一遍。
* 每次 head 进来 sort 的时候，都把 head.next 存好，相当于去超市存包。只比较当前的 node 在 dummy 中所排的位置。
![](/assets/insertionList.png)

----------


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
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        ListNode prev = dummy;
        while (head != null) {
            ListNode tmp = head.next;
            
            if (prev.val >= head.val) {
                prev = dummy;
            }
            while (prev.next != null && prev.next.val < head.val) {
                prev = prev.next;
            }
            head.next = prev.next;
            prev.next = head;
            head = tmp;
        }
        
        return dummy.next;
    }
}
```


