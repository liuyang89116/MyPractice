# Problem 133: Clone Graph

> https://leetcode.com/problems/clone-graph/

-------------
##思路
* 这道题用 dfs 和 bfs 都可以解决。
* 思路就是建立 map，映射关系就是：原来的 node - copyNode。然后遍历原来 node 的 neighbors，然后都加给 copyNode。这样，整个图就被 copy 了。

----------
##复杂度
* Time： O(n)  
* Space: O(n)
------------
```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null) {
            return node;
        }
        
        HashMap<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();
        return dfs(node, map);
    }
    
    private UndirectedGraphNode dfs(UndirectedGraphNode node, HashMap<UndirectedGraphNode, UndirectedGraphNode> map) {
        if (map.containsKey(node)) {
            return map.get(node);
        }
        
        UndirectedGraphNode copyNode = new UndirectedGraphNode(node.label);
        map.put(node, copyNode);
        for (UndirectedGraphNode neighborNode : node.neighbors) {
            copyNode.neighbors.add(dfs(neighborNode, map));
        }
        
        return copyNode;
    }
}
```