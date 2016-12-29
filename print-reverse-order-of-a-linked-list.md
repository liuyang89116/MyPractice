# Print reverse order of a Linked List

## 思路
* 有两种思路：第一种是用递归来做，另一种方法使用一个额外的 stack 来储存 node，然后再打出来就是 reverse order

----------


```java
package com.yang;

import java.util.List;
import java.util.Stack;

public class Main {
    public static class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            this.val = x;
        }
    }

    // Solution 1: recursion method to print
    public static void printReverse1(ListNode head) {
        if (head == null) {
            return;
        }

        printReverse1(head.next);
        System.out.println(head.val + " ");
    }

    // Solution 2: use stack to store node
    public static void printReverse2(ListNode head) {
        Stack<Integer> stack = new Stack<Integer>();
        while (head != null) {
            stack.push(head.val);
            head = head.next;
        }
        while (!stack.isEmpty()) {
            System.out.println(stack.pop());
        }
    }

    // main function
    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        // printReverse1(head);
        printReverse2(head);
    }
}

```

