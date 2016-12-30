# Problem: Construct BST from given preorder traversal

* 这是 Facebook 的一道面试题，这个贴子讲得还行。
> http://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/

-----------
##思路
* 这道题的思路和上一题是一样的，就是通过 preorder 的序列和 BST 的性质来确定一个 Tree
* 我们可以看出来，第一个元素肯定是一个根，那么我们找下一个比目前的根大的元素，那么从它开始就是右子树，左边的就是左子树。然后用递归构建整个 Tree。
* 递归的退出条件：`start == end`，说明已经是叶子了，直接返回就行

-------------
##复杂度
* Time: `O(n)`，遍历整个数组

-----------


```java
/**
 * Created by yang on 12/29/16.
 */
public class PreorderToBST {
    // TreeNode class
    public static class TreeNode {
        int val;
        TreeNode left, right;

        TreeNode(int x) {
            this.val = x;
        }
    }

    // convert function
    public static TreeNode convertBST(int[] preorder) {
        return helper(preorder, 0, preorder.length - 1);
    }

    // helper function, call recursively
    private static TreeNode helper(int[] preorder, int start, int end) {
        if (start == end) {
            TreeNode node = new TreeNode(preorder[start]);
            return node;
        }
        int rootVal = preorder[start];
        int rootIndex = findIndex(preorder, rootVal, start, end);

        TreeNode root = new TreeNode(rootVal);
        root.left = helper(preorder, start + 1, rootIndex - 1);
        root.right = helper(preorder, rootIndex, end);

        return root;
    }

    // find index
    private static int findIndex(int[] preorder, int rootVal, int start, int end) {
        for (int i = start; i <= end; i++) {
            if (preorder[i] > rootVal) {
                return i;
            }
        }

        return -1;
    }

    // print function
    private static void printTree(TreeNode root) {
        if (root == null) {
            return;
        }
        System.out.print(root.val + " ");
        printTree(root.left);
        printTree(root.right);
    }

    // test, main function
    public static void main(String[] args) {
        int[] preorder = new int[]{6, 4, 3, 5, 10, 7, 11};
        TreeNode root = convertBST(preorder);
        System.out.println("Print preorder: ");
        printTree(root);
    }

}


```

