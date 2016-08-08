# test

```java
public class Test {
	public static void main(String[] args) {
		// initialize the graph
		int[][] capMatrix = {
				{0, 7, 10, 17, 0, 0, 0},
				{0, 0, 0, 0, 9, 6, 0},
				{0, 8, 0, 0, 0, 0, 0},
				{0, 0, 5, 0, 0, 14, 0},
				{0, 0, 0, 0, 0, 4, 10},
				{0, 0, 7, 0, 0, 0, 7},
				{0, 0, 0, 0, 0, 0, 0}
		};
		Graph graph = new Graph(7);
		graph.setCapMatrix(capMatrix);
		
		// find max flow
		int maxFlow = graph.edomondsKarp(0, 6);
		System.out.println("The maximum flow for this graph is: "+maxFlow);
	}
}
```

```java
/**
 * bfs() is the function use to find next augmenting path
 *
 * @param s:source node
 * @param t:sink node
 * @param parent:an array trace the paths
 * @return
 */
private boolean bfs(int s, int t, int parent[]) {
    int n = parent.length;
    int[] visited = new int[n];
    Arrays.fill(visited, -1); // -1 means unvisited; 0 means visited

    // use queue to store vertices
    LinkedList<Integer> queue = new LinkedList<Integer>();
    queue.add(s);
    visited[s] = 0;
    parent[s] = -1;

    // loop the graph to find next path
    while (!queue.isEmpty()) {
        int u = queue.poll();
        for (int v = 0; v < n; v++) {
            if (visited[v] == -1 && capMatrix[u][v] > 0) {
                queue.add(v);
                parent[v] = u;
                visited[v] = 0;
            }
        }
    }
    return (visited[t] == 0 ? true : false);
}

```

```java
/**
 * This is the main function to implement the EdomondsKarp algorithm
 *
 * @param s:source node
 * @param t:sink node
 * @return
 */
public int edomondsKarp(int s, int t) {
    // use to record the max flow value
    int maxFlow = 0;
    // different vertices
    int u, v;

    // traverse the path and find max flow
    while (bfs(s, t, parent)) {
        // cp is the bottle neck value for the path
        int cp = Integer.MAX_VALUE;
        for (v = t; v != s; v = parent[v]) {
            u = parent[v];
            cp = Math.min(cp, capMatrix[u][v]);
        }
        // update capacity matrix
        for (v = t; v != s; v = parent[v]) {
            u = parent[v];
            capMatrix[u][v] -= cp;
            capMatrix[v][u] += cp;
        }
        maxFlow += cp;
    }
    return maxFlow;
}
```
