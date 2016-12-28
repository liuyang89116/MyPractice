# Problem 218: The Skyline Problem

> https://leetcode.com/problems/the-skyline-problem/

--------------
##思路
* 这道题实在是太经典了，可以用 sweep line algorithm 来算。这里有几个讲解不错。
> https://discuss.leetcode.com/topic/28482/once-for-all-explanation-with-clean-java-code-o-n-2-time-o-n-space/2 
* 首先把每个 building 按 (position, height, start/end) 这种 type 来分类，这里一个 trick 就是，start/end 这个标记可以用 `+/-` 号来标记，加到 height 上面。也就是说，如果是 start，就用 `-` 标记，(position, - height)；反之，end 用 (position, height) 标记。
* start 用 `-` 号因为方便后面的排序，start 可以优先到前面。
* 然后我们对 position 从大到小排序。遍历的时候，如果是 start 就加入 heap 里面，如果是 end 就把它从 heap 里面移除，维持一个当前最大高度。

-----------
##复杂度
* Time: `O(n^2)`    
pq.remove() costs `O(n)` time: pq.poll() which remove the top of priority queue is `O(log n)`, while pq.remove which remove any element is `O(n)` as it needs to search the particular element in all of the elements in the priority queue.  
**优化**： 可以用 TreeMap 来代替 PriorityQueue，这样 remove cost `O(log n)`
* Space: `O(n)`

------------

```java
public class Solution {
    public List<int[]> getSkyline(int[][] buildings) {
        List<int[]> rst = new ArrayList<int[]>();
        List<int[]> height = new ArrayList<int[]>();
        
        //  store in height and sort buildings
        for (int[] b : buildings) {
            height.add(new int[] {b[0], -b[2]});
            height.add(new int[] {b[1], b[2]});
        }
        Collections.sort(height, (h1, h2) -> {
            if (h1[0] != h2[0]) {
                return h1[0] - h2[0];
            }
            return h1[1] - h2[1];
        });
        
        
        Queue<Integer> pq = new PriorityQueue<Integer>((i1, i2) -> (i2 - i1));
        int prev = 0;
        pq.offer(0);
        
        // traverse height
        for (int[] h : height) {
            if (h[1] < 0) {
                pq.offer(-h[1]);
            } else {
                pq.remove(h[1]);
            }    
            
            int curr = pq.peek();
            if (curr != prev) {
                rst.add(new int[] {h[0], curr});
                prev = curr;
            }
        }
        
        return rst;
    }
}
```
--------
##易错点
1. Collections.sort() 的 Lambda 表示
这篇讲得不错
> http://www.codejava.net/java-core/the-java-language/java-8-lambda-collections-comparator-example
2. sort 的时候，先比 x1，如果 x1 相同，那么就接着比 x2
```java
Collections.sort(height, (h1, h2) -> {
     if (h1[0] != h2[0]) {
        return h1[0] - h2[0];
     }
     return h1[1] - h2[1];
});
```
3. 最大堆
```java
Queue<Integer> pq = new PriorityQueue<Integer>((i1, i2) -> (i2 - i1));
```


































