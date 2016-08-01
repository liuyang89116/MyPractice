# test

```java
   /**
	 * This is the main function to implement DFS algorithm.
	 * 
	 * Also we use it to check the connectivity of the graph
	 * 
	 */
	public boolean dfs(int rootNode) {
		// check whether input value is valid
		if (rootNode > nodeList.length) {
			System.out.println("The index of the starting node should be less the length of nodeList.");
			return false;
		}
		int count = 0; // record the connected elements

		Stack<Integer> stack = new Stack<Integer>();
		stack.push(nodeList[rootNode]);
		visited[rootNode] = 1;
		// System.out.println("===========================================");
		// System.out.println("The connected graph elements are: ");
		// printNode(nodeList[rootNode]);
		count++;
		while (!stack.isEmpty()) {
			int currentIndex = getIndex(stack.peek());
			int childIndex = getNext(currentIndex);
			while (childIndex != -1) {
				visited[childIndex] = 1;
				// printNode(nodeList[childIndex]);
				count++;
				stack.push(nodeList[childIndex]);
				childIndex = getNext(childIndex);
			}
			stack.pop();
		}

		// check whether the graph is connected or not. if the count number
		// equals to the number of nodes, then they are connected. otherwise
		// they are not
		if (count == nodeList.length) {
			// System.out.println("True. The graph is connected.");
			return true;
		} else {
			// System.out.println("False. The graph is not connected.");
			return false;
		}

	}
```