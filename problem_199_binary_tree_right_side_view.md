# Problem 199: Binary Tree Right Side View


> https://leetcode.com/problems/binary-tree-right-side-view/

-----------
##思路
* 这道题其实就是在 BFS 遍历的基础上稍加改变：只存每个 level 最有边的那个数
* 怎么实现这个过程呢？ 可以用 currIndex 标记当前的 node 的 index;用 nextIndex 标记下一个 node 的index
* 每次初始的时候，currIndex > 0， nextIndex = 0。这样做是因为每一个 level 上会有很多 node，当 currIndex 为 0 的时候，我们知道这是最后一个 node 了，可以存他了。 
* nextIndex 用来记下下一个 level 里有多少个 nodes，方便给下一次的 currIndex 赋值

------------
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> rst = new ArrayList<Integer>();
        if (root == null) {
            return rst;
        }
        
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        int currIndex = 1, nextIndex = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode currNode = queue.poll();
                currIndex--;
                if (currIndex == 0) {
                    rst.add(currNode.val);
                }
                if (currNode.left != null) {
                    queue.offer(currNode.left);
                    nextIndex++;
                }
                if (currNode.right != null) {
                    queue.offer(currNode.right);
                    nextIndex++;
                }
                if (currIndex == 0) {
                    currIndex = nextIndex;
                    nextIndex = 0;
                }
            }
        }
        
        return rst;
    }
}
```

------------
##易错点
1. 如果是求 left side view 呢？
```java
if (nextIndex == 0) {
       rst.add(currNode.val);
}
```
只需要做这一个改动。




















