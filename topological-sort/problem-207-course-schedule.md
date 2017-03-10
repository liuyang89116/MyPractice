# Problem 207: Course Schedule

> [https://leetcode.com/problems/course-schedule/?tab=Description](https://leetcode.com/problems/course-schedule/?tab=Description)

---

## 思路

* Topological Sort 对于有依赖关系\(如果想做 B, 必须先做 A\), 非常实用. 相当于在这个过程中表明了有向图中 edge 的方向。
* Topological Sort 的思路主要是，首先找到没有 incoming edge 的 node，这就是起点（当然可能有几个 node 都满足）。然后沿着这个 node 找下一个。如果下一个 node 的没有 children 可以访问了，就是走到头了。
* 如果整个图当中存在“环”，那么就报错，不存在 Topological Sort。否则可以一种通过这种方法往下走，最后移除所有的 node 和 edge
* 这道题用 `ArrayList[] graph`代表不同的 nodes 之间的连接情况；用 `int[] nodes`代表不同的 nodes。用 `nodes[i]`来 maintain incoming edges；然后用 BFS 来便利所有的 nodes，并且同 count number 来 check 最后是否有“环”。

----------

## 复杂度

* 时间复杂度： $$ O(V^2 + E) $$







---

```java
public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        ArrayList[] graph = new ArrayList[numCourses];
        int[] nodes = new int[numCourses];
        Queue<Integer> queue = new LinkedList<Integer>();
        int count = 0;

        for (int i = 0; i < numCourses; i++) {
            graph[i] = new ArrayList();
        }
        for (int i = 0; i < prerequisites.length; i++) {
            nodes[prerequisites[i][1]]++;
            graph[prerequisites[i][0]].add(prerequisites[i][1]);
        }
        for (int i = 0; i < nodes.length; i++) {
            if (nodes[i] == 0) {
                queue.offer(i);
                count++;
            }
        }

        while (queue.size() != 0) {
            int course = queue.poll();
            for (int i = 0; i < graph[course].size(); i++) {
                int pointer = (int) graph[course].get(i);
                nodes[pointer]--;
                if (nodes[pointer] == 0) {
                    queue.offer(pointer);
                    count++;
                }
            }
        }

        if (count == numCourses) {
            return true;
        } else {
            return false;
        }

    }
}
```



