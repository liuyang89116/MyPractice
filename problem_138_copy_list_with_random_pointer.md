# Problem 138: Copy List with Random Pointer


> https://leetcode.com/problems/copy-list-with-random-pointer/

--------------
##思路

* 这道题的难点就在于，不知道某个点之前存了没有。所以我们可以用HashMap来存储这样的映射关系
* 用newNode来记录每一个新存入的点。有就直接get，没有就put到map里面。

--------
```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return null;
        }
        
        RandomListNode dummy = new RandomListNode(0);
        RandomListNode pre = dummy;
        RandomListNode newNode;
        HashMap<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
        while (head != null) {
            if (map.containsKey(head)) {
                newNode = map.get(head);
            } else {
                newNode = new RandomListNode(head.label);
                map.put(head, newNode);
            }
            pre.next = newNode;
            
            if (head.random != null) {
                if (map.containsKey(head.random)) {
                    newNode.random = map.get(head.random);
                } else {
                    newNode.random = new RandomListNode(head.random.label);
                    map.put(head.random, newNode.random);
                }
            }
            
            pre = newNode;
            head = head.next;
        }
        
        return dummy.next;
    }
}

```

----
##易错点

1. corner cases的情况
```java
if (head == null) {
       return null;
}
```
之前多此一举地考虑了```head.next == null```的情况，返回```head```出错。
2. node 和 random 关系分别处理
```java
if (map.containsKey(head)) {
       newNode = map.get(head);
} else {
       newNode = new RandomListNode(head.label);
       map.put(head, newNode);
}
pre.next = newNode;
```
```java
if (head.random != null) {
        if (map.containsKey(head.random)) {
             newNode.random = map.get(head.random);
        } else {
             newNode.random = new RandomListNode(head.random.label);
             map.put(head.random, newNode.random);
        }
}
```



































