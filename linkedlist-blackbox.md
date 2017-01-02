# LinkedList BlackBox

> 给一个 linkedlist，里面的 element 都排序好了，但是是一个 blackbox，有三个 function 可以调用。pop() 随机 pop 出最前面或最后面的 element，peek() 随机偷看最前面或最后面的 element，isEmpty()回传linkedlist是不是空了。问设计一个资料结构，list 或是 array 都可以，把 linkedlist 里面所有的 element 都拿出来，并保持他们的排序。
------
##思路
* 设计两个 LinkedList， 一个 small, 一个 large。遇到小的就挂到小的上面，遇到大的就挂到大的上。

-------------


```java
class ListNode {
	int val;
	ListNode next;
	public ListNode(int val) {
		this.val = val;
		next = null;
	}
}

// use peek();
public ListNode getLinkedList(ListNode head) {
	if (head == null) {
		return null;
	}

	ListNode small = new ListNode(0);
	ListNode dummyS = small;
	ListNode large = new ListNode(0);
	ListNode dummyL = large;
	while (!head.isEmpty()) {
		ListNode first = head.peek();
		ListNode newNode = head.pop();
		if (newNode.val > first.val) {
			large.next = newNode;
			large = large.next;
		} else {
			small.next = newNode;
			small = small.next;
		}
	}

	small.next = reverse(dummyL.next);

	return dummyS.next;
}

private ListNode reverse(ListNode head) {
	if (head == null) {
		return null;
	}

	ListNode prev = null;
	while (head != null) {
		ListNode tmp = head.next;
		head.next = prev;
		prev = head;
		head = tmp;
	}

	return prev;
}
```
---------
##Follow Up
> 如果不能用peek()该怎么做。

* 设置两个链表 small 和 large。 所有 pop 出来的点都先接到 small 的末尾上，如果再 pop 出来的点比 small 末尾的那个值要小 就把 small 末尾的这个点接到 large 后面 再把这个 pop 出来的接到 small 后面。
```
比如 1->5->7->9->11
不管先 pop 出来 1 或者 11，都先接到 small 的后面。假设这里 pop 出来 11，就是 small->11 
然后再 pop 出来的点就和这个末尾比较：如果这里 pop 出来的是 9，那么就把 11 放到上面，Large->11 small->9 
然后如果 pop 出来 1，那么就变成 Large->11->9 small->1.
然后如果 pop 出来 7，Large->11->9 small->1->7
然后如果 pop 出来 5，Large->11->9->7 smal->1->5
这样应该就能保证顺序不乱，最后把两个链表拼起来就行了。
```



























