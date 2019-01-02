# Problem 98: Validate Binary Search Tree

> [https://leetcode.com/problems/validate-binary-search-tree/](https://leetcode.com/problems/validate-binary-search-tree/)

---

## 思路

* 这道题很有代表性。一种方式就是利用 iterative 的方法做，另一种就是 recursion 的方法。

---

* **Solution 1**: Iterative 
* 这是可以解决一类问题的必杀手段。大体的思路就是：利用一个 stack 来储存元素，然后利用 inorder \(左-根-右\) 的顺序遍历整个 tree，继而得到答案。  
  这篇文章讲得很好！
  > [https://discuss.leetcode.com/topic/46016/learn-one-iterative-inorder-traversal-apply-it-to-multiple-tree-questions-java-solution/2](https://discuss.leetcode.com/topic/46016/learn-one-iterative-inorder-traversal-apply-it-to-multiple-tree-questions-java-solution/2)

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
    public boolean isValidBST(TreeNode root) {
        if (root == null) {
            return true;
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode prev = null;
        while (root != null || !stack.isEmpty()) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            if (prev != null && prev.val >= root.val) return false;
            prev = root;
            root = root.right;
        }

        return true;
    }
}
```

---

* **Solution 2**: 递归

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
    public boolean isValidBST(TreeNode root) {
        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean helper(TreeNode root, long minVal, long maxVal) {
        if (root == null) return true;
        if (root.val <= minVal || root.val >= maxVal) return false;
        return helper(root.left, minVal, root.val) && helper(root.right, root.val, maxVal);
    }
}
```

---

* **Solution 3**: 分治
* 分治思想，有几个点很容易出错;
* 这里要维护几个不同的值：min, max 和 is\_bst，所以直接创立一个 ResultType 的类是比较方便的
* 关键点：左边的最大要小于root，右边的最小要小于root。这样才能成为一个 binary search tree.

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
    public class ResultType {
        boolean is_bst;
        int min, max;

        public ResultType(boolean is_bst, int max, int min) {
            this.is_bst = is_bst;
            this.max = max;
            this.min = min;
        }
    }

    public boolean isValidBST(TreeNode root) {
        ResultType result = validateHelper(root);
        return result.is_bst;
    }

    private ResultType validateHelper(TreeNode root) {
        if (root == null) {
            return new ResultType(true, Integer.MIN_VALUE, Integer.MAX_VALUE);
        }

        ResultType left = validateHelper(root.left);
        ResultType right = validateHelper(root.right);

        if (!left.is_bst || !right.is_bst) {
            return new ResultType(false, 0, 0);
        }
        if (root.left != null && left.max >= root.val || root.right != null && right.min <= root.val) {
            return new ResultType(false, 0, 0);
        }

        int min = Math.min(root.val, left.min);
        int max = Math.max(root.val, right.max);

        return new ResultType(true, max, min);

    }
}
```

---

## 易错点

1. root为空的情况。
   ```java
   if (root == null) {
       return new ResultType(true, Integer.MIN_VALUE, Integer.MAX_VALUE);
   }
   ```
2. 这里的 min 和 max 跟 ResultType 里正好是相反的！原因是为了能不停地迭代，要判断 max，那开始就设成 min，这样能不停地往下走。
3. root 为空，不代表整个树不是搜索树，所以空结点要返回一个 true；另外一方面，这个空节点的最大最小值不能影响整个树的结构，所以我们把最小值设成最大，最大值设成最小。

4. 条件判断，**非常易错**

   ```java
   if (root.left != null && left.max 便便>= root.val || root.right != null && right.min <= root.val) {
       return new ResultType(false, 0, 0);
   }
   ```

   注意看这里是`root.left != null`和`left.max >= root.val`！  
   而我错就错在写成了`left.max >= root.val`！这种情况下，当 left 本身为空的时候，直接就会出错。

5. **指代对象不同**
   ```java
   if (root.left != null && left.max 便便>= root.val || root.right != null && right.min <= root.val) {
       return new ResultType(false, 0, 0);
   }
   ```

   这里是`root.left`，和`left`是**两个东西**！  
   `left`指的是 ResultType；而`root.left`是判断树的左边有没有东西！



