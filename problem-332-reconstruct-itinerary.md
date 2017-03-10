# Problem 332: Reconstruct Itinerary

> [https://leetcode.com/problems/reconstruct-itinerary/?tab=Description](https://leetcode.com/problems/reconstruct-itinerary/?tab=Description)

---

## 思路

> https://discuss.leetcode.com/topic/36370/short-ruby-python-java-c

这个讲解不错！

* 因为题目的要求是按 lexical order 输出结果，所以我们可以用一个最小堆 min - heap 来存储周围的 neighbor 元素。这样可以保证永远访问最小的相邻元素。
* 先把所有的 tickets 都放入 map 中，然后把后面一个 元素和当前元素相连。
* 在最后的递归中，用 `addFirst()`方法是因为递归是一层一层的。最后进行递归的元素最先执行 `addFirst()`方法。

---

```java
public class Solution {
    Map<String, PriorityQueue<String>> flights;
    LinkedList<String> path;

    public List<String> findItinerary(String[][] tickets) {
        flights = new HashMap<String, PriorityQueue<String>>();
        path = new LinkedList<String>();
        for (String[] ticket : tickets) {
            flights.putIfAbsent(ticket[0], new PriorityQueue<String>());
            flights.get(ticket[0]).add(ticket[1]);
        }
        dfs("JFK");

        return path;
    }

    private void dfs(String departure) {
        PriorityQueue<String> arrivals = flights.get(departure);
        while (arrivals != null && !arrivals.isEmpty()) {
            dfs(arrivals.poll());
        }
        path.addFirst(departure);
    }

}
```





