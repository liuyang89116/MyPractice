# Problem 449: Serialize and Deserialize BST

> https://leetcode.com/problems/serialize-and-deserialize-bst/\#/description

---------

## 思路

> https://discuss.leetcode.com/topic/66651/java-preorder-queue-solution

这个讲解很好！

* 首先用 preorder 把 tree 压入 string
* decode 的时候用分隔符把 nodes parse 开来。用一个 smallerQueue 存左子树，剩下的就是右子树，最后 recurse build 整个 tree

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
        if (root == null) return null;
        StringBuilder sb = new StringBuilder();
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            sb.append(node.val).append(",");
            if (node.right != null) stack.push(node.right);
            if (node.left != null) stack.push(node.left);
        }
        
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null || data.length() == 0) return null;
        
        String[] arr = data.split(",");
        Queue<Integer> queue = new LinkedList<>();
        for (String val : arr) {
            queue.offer(Integer.parseInt(val));
        }
        
        return buildTree(queue);
    }
    
    private TreeNode buildTree(Queue<Integer> queue) {
        if (queue.isEmpty()) return null;
        
        TreeNode root = new TreeNode(queue.poll());
        Queue<Integer> smallerQueue = new LinkedList<>();
        while (!queue.isEmpty() && queue.peek() < root.val) smallerQueue.offer(queue.poll());
        
        root.left = buildTree(smallerQueue);
        root.right = buildTree(queue);
        
        return root;
    }
    
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```



