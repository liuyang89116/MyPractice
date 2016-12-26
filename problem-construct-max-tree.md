# Problem: Construct Max Tree

这道题目 LeetCode 没有，LintCode 不对外开放。但这道题目非常地经典。

##题目
Given an integer array with no duplicates. A max tree building on this array is defined as follow:
* The root is the maximum number in the array
* The left subtree and right subtree are the max trees of the subarray divided by the root number.  
Construct the max tree by the given array.  
**Example**  
Given [2, 5, 6, 0, 3, 1], the max tree is  

```
               6

             /    \

           5       3

         /        /  \

       2         0     1
```
-----------
##思路
* 这种树叫做笛卡尔树（Cartesian tree）。直接递归建树的话复杂度最差会退化到`O(n^2)`。经典建树方法，用到的是单调堆栈。我们堆栈里存放的树，只有左子树，没有右子树，且根节点最大。
* (1) 如果新来一个数，比堆栈顶的树根的数小，则把这个数作为一个单独的节点压入堆栈。
* (2) 否则，不断从堆栈里弹出树，新弹出的树以旧弹出的树为右子树，连接起来，直到目前堆栈顶的树根的数大于新来的数。然后，弹出的那些数，已经形成了一个新的树，这个树作为新节点的左子树，把这个新树压入堆栈。
* (3) **这样的堆栈是单调的**，越靠近堆栈顶的数越小。最后还要按照（2）的方法，把所有树弹出来，每个旧树作为新树的右子树。
------
##复杂度
* Time: `O(n)`

--------


```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
	/**
	* @param A: Given an integer array with no duplicates.
	* @return: The root of max tree.
	*/
	public TreeNode maxTree(int[] nodes) {
		if (nodes == null || nodes.length == 0) {
			return null;
		}

		Stack<TreeNode> stack = new Stack<TreeNode>();
		stack.push(new TreeNode(nodes[0]));
		for (int i = 1; i < nodes.length; i++) {
			if (nodes[i] <= stack.peek().val()) {
				stack.push(new TreeNode(nodes[i]));
			} else {
				TreeNode n1 = stack.pop();
				while (!stack.isEmpty() && stack.peek().val < nodes[i]) {
					TreeNode n2 = stack.pop();
					n2.right = n1;
					n1 = n2;
				}
				TreeNode node = new TreeNode(nodes[i]);
				node.left = n1;
				stack.push(node);
			}
		}

		TreeNode root = stack.pop();
		while (!stack.isEmpty()) {
			stack.peek().right = root;
			root = stack.pop();
		}

		return root;
	}
}
```


















