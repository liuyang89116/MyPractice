# test

```java
  /**
	 * Prim's algorithm
	 */
	public boolean prim(int rootNode) {
		if (!dfs(rootNode)) {
			System.out.println("The graph doesn't have a minimum spanning tree.");
			return false;
		}
		// initialize visited
		for (int i = 0; i < visited.length; i++) {
			visited[i] = 0;
		}
		visited[rootNode] = 1;

		// create parameters
		LinkedList<Integer> nodes = new LinkedList<Integer>();

		nodes.add(nodeList[rootNode]);
		while (hasNext(visited)) {
			int minNode = findMinNode();
			nodes.add(nodeList[minNode]);
		}
		printMstNodes(nodes);
		printEdges(edges);
		return true;
	}

```

```java
    /**
	 * find the minimum path for next node
	 * 
	 * @return
	 */
	public int findMinNode() {
		int min = Integer.MAX_VALUE;
		int minNode = 0;
		for (int i = 0; i < nodeList.length; i++) {
			if (visited[i] == 1) {
				for (int j = 0; j < nodeList.length; j++) {
					if (visited[j] == 0 && weightMatrix[i][j] != 0 && weightMatrix[i][j] < min) {
						min = weightMatrix[i][j];
						minNode = j;
					}
				}
			}
		}
		visited[minNode] = 1;
		weight += min;
		edges.add(min);
		return minNode;
	}
```
```java
    /**
	 * print each edge to users
	 * 
	 * @param edges
	 */
	private void printEdges(LinkedList<Integer> edges) {
		System.out.println();
		System.out.println("The minimum edges are: ");
		for (Integer i : edges) {
			System.out.print(i + " ");
		}
		System.out.println();
		System.out.println("The total weight is " + weight);
	}
```