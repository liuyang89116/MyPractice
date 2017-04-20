# Problem 315: Count of Smaller Numbers After Self

> https://leetcode.com/problems/count-of-smaller-numbers-after-self/\#/description

-----------

## 思路

> https://discuss.leetcode.com/topic/31405/9ms-short-java-bst-solution-get-answer-when-building-bst

这个讲解不错！

* 这个 BST 的结构设计地很巧妙，利用 BST 来解决实际问题。用 dup 来统计重复元素；sum 来统计小于它的元素个数；val 代表元素的值
* 然后用一个 array rst 来统计符合条件的结果的个数，最后转换成 list 输出
* insert\(\) 这个方法很巧妙，涵盖了各种情况

------

```java
public class Solution {
    class TreeNode {
        TreeNode left, right;
        int val, sum, dup = 1;
        public TreeNode (int val, int sum) {
            this.val = val;
            this.sum = sum;
        }
        
    }
    public List<Integer> countSmaller(int[] nums) {
        Integer[] rst = new Integer[nums.length];
        TreeNode root = null;
        for (int i = nums.length - 1; i >= 0; i--) {
            root = insert(nums[i], root, i, 0, rst);
        }
        
        return Arrays.asList(rst);
    }
    
    private TreeNode insert(int num, TreeNode node, int index, int prevSum, Integer[] rst) {
        if (node == null) {
            node = new TreeNode(num, 0);
            rst[index] = prevSum;
        } else if (num == node.val) {
            node.dup++;
            rst[index] = prevSum + node.sum;
        } else if (num < node.val) {
            node.sum++;
            node.left = insert(num, node.left, index, prevSum, rst);
        } else {
            node.right = insert(num, node.right, index, prevSum + node.dup + node.sum, rst);
        }
        
        return node;
    }    
    
}


```





