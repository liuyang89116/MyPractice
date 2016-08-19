# Summary 1: Pointer and update

1. LinkedList的结构
![](LinkedList_01.jpg)
![](LinkedList_02.jpg)

2. insert a node
![](LinkedList_03.jpg)
![](LinkedList_04.jpg)
**注意**：```head = newest```，这是为了把head指针重新更新，指向新的node

3.  delete a node
![](LinkedList_05.jpg)
![](LinkedList_06.jpg)
4. 参考
> http://blog.csdn.net/feliciafay/article/details/6841115

5. 指针的含义
```java
ListNode dummy = new ListNode(0); //建立一个dummynode
dummy.next = head;                //把head连接在dummy后面
head = dummy;                     //把head的指针移动到dummy处
```
**注意**：```head = dummy```，**永远是左边的指针移动到右边去**。




























