# Problem 297: Serialize and Deserialize Binary Tree

> https://leetcode.com/problems/serialize-and-deserialize-binary-tree/

---------
##思路
这篇分析得很好
> http://blog.csdn.net/ljiabin/article/details/49474445

* 序列化比较容易，我们做一个层次遍历就好，空的地方用 null 表示，稍微不同的地方是题目中示例得到的结果是 "[1,2,3,null,null,4,5,null,null,null,null,]" ，即 4 和 5 的两个空节点我们也存了下来。
* 反序列化时，我们根据都好分割得到每个节点。需要注意的是，反序列化时如何寻找父节点与子节点的对应关系，我们知道在数组中，如果满二叉树（或完全二叉树）的父节点下标是 i，那么其左右孩子的下标分别为 `2*i + 1` 和 `2*i + 2`，但是这里并不一定是满二叉树（或完全二叉树），所以这个对应关系需要稍作修改。如下面这个例子：序列化结果为[5,4,7,3,null,2,null,-1,null,9,null,null,null,null,null,]。
```
       5
      / \
     4   7
    /   /
   3   2
  /   /
 -1  9
```
其中，节点 2 的下标是 5，可它的左孩子 9 的下标为 9，并不是 `2 * i + 1 = 11`，原因在于 前面有个 null 节点，这个 null 节点没有左右孩子，所以后面的节点下标都提前了2。所以我们只需要记录每个节点前有多少个 null 节点，就可以找出该节点的孩子在哪里了，其左右孩子分别为 **`2 *(i-num) + 1`** 和 **`2  *  (i-num)+ 2`**（num为当前节点之前 null 节点的个数）。

----------



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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (node == null) {
                sb.append("null,");
            } else {
                sb.append(node.val + ",");
                queue.offer(node.left);
                queue.offer(node.right);
            }
        }
        
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null || data.length() == 0) {
            return null;
        }
        
        String[] vals = data.split(",");
        int[] nums = new int[vals.length];  // store num of "null"
        TreeNode[] nodes = new TreeNode[vals.length];
        for (int i = 0; i < vals.length; i++) {
            if (i > 0) {
                nums[i] = nums[i - 1];
            }
            if (vals[i].equals("null")) {
                nodes[i] = null;
                nums[i]++;
            } else {
                nodes[i] = new TreeNode(Integer.parseInt(vals[i]));
            }
        }
        
        for (int i = 0; i < vals.length; i++) {
            if (nodes[i] == null) continue;
            nodes[i].left = nodes[2 * (i - nums[i]) + 1];
            nodes[i].right = nodes[2 * (i - nums[i]) + 2];
        }
        
        return nodes[0];
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));


```

