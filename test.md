# test

```java
    // parameters
	private int[] nodeList;
	private int[] visited;
	private int[][] adjMatrix;
	private int[][] weightMatrix;

	// maintain edges and weight
	LinkedList<Integer> edges = new LinkedList<Integer>();
	private int weight = 0;

	// initialize the graph
	public Graph(int size) {
		nodeList = new int[size];
		visited = new int[size];
		for (int i : visited) {
			visited[i] = 0;
		}
		adjMatrix = new int[size][size];
		weightMatrix = new int[size][size];
	}
```