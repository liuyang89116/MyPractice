# Problem 207: Course Schedule

> [https://leetcode.com/problems/course-schedule/?tab=Description](https://leetcode.com/problems/course-schedule/?tab=Description)

---

## 思路

* Topological Sort 对于有依赖关系\(如果想做 B, 必须先做 A\), 非常实用. 相当于在这个过程中表明了有向图中 edge 的方向。
* Topological Sort 的思路主要是，首先找到没有 incoming edge 的 node，这就是起点（当然可能有几个 node 都满足）。然后沿着这个 node 找下一个。如果下一个 node 的没有 children 可以访问了，就是走到头了。
* 如果整个图当中存在“环”，那么就报错，不存在 Topological Sort。否则可以一种通过这种方法往下走，最后移除所有的 node 和 edge
* 


