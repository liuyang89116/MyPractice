# Problem 146: LRU Cache

> https://leetcode.com/problems/lru-cache/

----------------
##思路
* **双向链表 + HashMap**
* 为了能够快速删除最久没有访问的数据项和插入最新的数据项，我们将双向链表连接Cache 中的数据项，并且保证链表维持数据项从最近访问到最旧访问的顺序。每次数据项被查询到时，都将此数据项移动到链表头部（O(1)的时间复杂度）。这样，在进行过多次查找操作后，最近被使用过的内容就向链表的头移动，而没有被使用的内容就向链表的后面移动。
* 当需要替换时，链表最后的位置就是最近最少被使用的数据项，我们只需要将最新的数据项放在链表头部，当 Cache 满时，淘汰链表最后的位置就是了。

---------
##复杂度
* 首先是 Cache 中块的命中可能是随机的，和 Load 进来的顺序无关。其次，双向链表插入、删除很快，可以灵活的调整相互间的次序，时间复杂度为 **`O(1)`**。
* 为了能减少整个数据结构的时间复杂度，就要减少查找的时间复杂度，所以这里利用 HashMap 来做，这样时间苏咋读就是 **`O(1)`**。

----------
* Solution 1: Doubly LinkedList + HashMap

```java
public class LRUCache {
    class DoubleLinkedList {
        int key;
        int val;
        DoubleLinkedList prev;
        DoubleLinkedList next;
        
        public DoubleLinkedList(){}
        
        public DoubleLinkedList(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
    
    // parameters
    private HashMap<Integer, DoubleLinkedList> cache;
    private int count, capacity;
    private DoubleLinkedList head, tail;
    
    // constructor
    public LRUCache(int capacity) {
        this.cache = new HashMap<Integer, DoubleLinkedList>();    
        this.count = 0;
        this.capacity = capacity;
        
        head = new DoubleLinkedList();
        head.prev = null;
        tail = new DoubleLinkedList();
        tail.next = null;
        head.next = tail;
        tail.prev = head;
    }
    
    public void addNodeFirst(DoubleLinkedList node) {
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }
    
    public void removeNode(DoubleLinkedList node) {
        DoubleLinkedList pre = node.prev;
        DoubleLinkedList post = node.next;
        pre.next = post;
        post.prev = pre;
    }
    
    public void moveToHead(DoubleLinkedList node) {
        removeNode(node);
        addNodeFirst(node);
    }
    
    public DoubleLinkedList popTail() {
        DoubleLinkedList pre = tail.prev;
        removeNode(pre);
        return pre;
    }
    
    public int get(int key) {
        DoubleLinkedList node = cache.get(key);
        if (node == null) {
            return -1;
        }
        moveToHead(node);
        return node.val;
    }
    
    public void set(int key, int value) {
        DoubleLinkedList node = cache.get(key);
        if (node == null) {
            DoubleLinkedList newNode = new DoubleLinkedList(key, value);
            cache.put(key, newNode);
            addNodeFirst(newNode);
            count++;
            
            if (count > capacity) {
                DoubleLinkedList tail = popTail();
                cache.remove(tail.key);
                count--;
            }
        } else {
            node.val = value;
            moveToHead(node);
        }
    }
}

```
* Solution 2: LinkedHashMap


```java
public class LRUCache {
    private Map<Integer, Integer> cache;
    private int capacity;
    
    public LRUCache(int capacity) {
        this.cache = new LinkedHashMap<Integer, Integer>();
        this.capacity = capacity;
    }
    
    public int get(int key) {
        Integer val = cache.get(key);
        if (val == null) {
            return -1;
        }
        cache.remove(key);
        cache.put(key, val);
        return val;
    }
    
    public void set(int key, int value) {
        cache.remove(key);
        cache.put(key, value);
        if (cache.size() > capacity) {
            cache.remove(cache.keySet().iterator().next());
        }
    }
}
```



------
##易错点
1. 双向链表插入 node
![](/assets/addNodeFirst.png)
这个插入的过程，首先连接：把 node 的 prev 和 head 相连；把 node 的 next 和 head.next 相连。接下来就是删掉不必要的连接。   
**注意**：这里**顺序千万不能变**！  
```java
head.next.prev = node;
head.next = node;
```
因为如果先把 head.next 设成 node，那么 head.next.prev 的值已经发生了改变。
2. head 和 tail 都是 dummy node
他们俩用来作为定位结点，防止删除更新结点的过程中，不好定位。































