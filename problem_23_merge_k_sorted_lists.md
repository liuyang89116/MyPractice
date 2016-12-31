# Problem 23: Merge k Sorted Lists


> https://leetcode.com/problems/merge-k-sorted-lists/

---------------
##思想
* 这道题有两种做法，第一种是用一个额外的 heap 来做。首先把所有的 node 都存到最小堆，然后每次 poll() 出来的 node 都是最小的 node。接着我们来查看，如果这个 poll 出来的元素后面还有其他的元素跟着，我们就就把剩下的 push 到 heap 里，依次类推，知道所有的元素都再里面走一圈。

-----
* 用 heap 来做
* 时间复杂度：`n log(k)`，n 代表有 n 个 nodes，每次压入 heap 需要 log(k) 时间

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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        PriorityQueue<ListNode> pq = new PriorityQueue<>(lists.length, new Comparator<ListNode>(){
            public int compare(ListNode l1, ListNode l2) {
                return l1.val - l2.val;
            }
        });
        
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;
        
        for (ListNode node : lists) {
            if (node != null) {
                pq.add(node);
            }
        }
        while (!pq.isEmpty()) {
            head.next = pq.poll();
            head = head.next;
            
            if (head.next != null) {
                pq.add(head.next);
            }
        }
        
        return dummy.next;
    }
}

```
----------

* 分治递归的思想：先把list切割成无数小的 left 和 right,然后把他们merge到一起


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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        return mergeHelper(lists, 0, lists.length - 1);
    }
    
    private ListNode mergeHelper(ListNode[] lists, int start, int end) {
        if (start == end) {
            return lists[start];
        }
        
        int mid = start + (end - start) / 2;
        ListNode left = mergeHelper(lists, start, mid);
        ListNode right = mergeHelper(lists, mid + 1, end);
        
        return mergeTwoLists(left, right);
    }
    
    private ListNode mergeTwoLists(ListNode head1, ListNode head2) {
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
        }
        if (head2 != null) {
            tail.next = head2;
        }
        
        return dummy.next;
    }
}
```

--------
##易错点
1. 同样的找中点递归
```java
int mid = start + (end - start) / 2;
ListNode left = mergeHelper(lists, start, mid);
ListNode right = mergeHelper(lists, mid + 1, end);
```
2. merge两个LinkedList一定要熟练


