# Problem 255: Verify Preorder Sequence in Binary Search Tree

> https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/

----------
![](/assets/255.png)

---------
##思路
![](/assets/verifyPreorder.png)
* 先看上面这个最简单的例子，一个是 BST tree，一个是 preorder 的序列，这俩基本上就可以完全地确定一个 tree。
* 观察 preorder 序列，当 curr node 比上一个 node 小的时候，我们可以确定目前我们在上一个 node 的左子树下面。反之如果变大的话，就在右子树。
* 我们可以用一个 stack 来维护这一过程。

------------
* Stack 来解，时间复杂度 ：`O(n)`，空间复杂度： `O(n)`

```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        if (preorder == null || preorder.length == 0) {
            return true;
        }
        
        Stack<Integer> stack = new Stack<Integer>();
        int low = Integer.MIN_VALUE;
        for (int node : preorder) {
            if (node < low) {
                return false;
            }
            
            while (!stack.isEmpty() && node > stack.peek()) {
                low = stack.pop();
            }
            stack.push(node);
        }
        
        return true;
    }
}
```

* 优化：重复利用原来的数组，额外空间复杂度为 `O(1)`


```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        if (preorder == null || preorder.length == 0) {
            return true;
        }
        
        int low = Integer.MIN_VALUE;
        int i = -1;
        for (int node : preorder) {
            if (node < low) {
                return false;
            }
            
            while (i >= 0 && node > preorder[i]) {
                low = preorder[i--];
            }
            preorder[++i] = node;
        }
        
        return true;
    }
}
```
----------


