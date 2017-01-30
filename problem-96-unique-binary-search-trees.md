# Problem 96: Unique Binary Search Trees

> https://leetcode.com/problems/unique-binary-search-trees/

-----
##思路
* 这个讲解不错
> https://discuss.leetcode.com/topic/8398/dp-solution-in-6-lines-with-explanation-f-i-n-g-i-1-g-n-i/2
* 我们先定义两个方程：
```
dp(n): the number of unique BST for a sequence of length n
```
```
f(i, n), 1 <= i <= n: the number of unique BST, 
where the number i is the root of BST, 
and the sequence ranges from 1 to n.
```
所以显而易见，
```
dp(n) = f(1, n) + f(2, n) + ... + f(n, n)
```
* 求 f(i, n)
> Given a sequence 1…n, we pick a number i out of the sequence as the root, then the number of unique BST with the specified root F(i), is the cartesian product of the number of BST for its left and right subtrees. 
For example, F(3, 7): the number of unique BST tree with number 3 as its root. To construct an unique BST out of the entire sequence [1, 2, 3, 4, 5, 6, 7] with 3 as the root, which is to say, we need to construct an unique BST out of its left subsequence [1, 2] and another BST out of the right subsequence [4, 5, 6, 7], and then combine them together (i.e. cartesian product). The tricky part is that we could consider the number of unique BST out of sequence [1,2] as dp(2), and the number of of unique BST out of sequence [4, 5, 6, 7] as dp(4). Therefore, F(3,7) = dp(2) * dp(4).
* 从上面的讲解可以看出，f(i, n) 的通项公式
```
f(i, n) = dp(i - 1) * dp(n - i)
```
* 结合上面两个式子，可以看出
```
dp(n) = dp(0) * dp(n - 1) + dp(1) * dp(n - 2) + ... + dp(n - 1) * dp(0)
```

------


```java
public class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                dp[i] += dp[j - 1] * dp[i - j];
            }
        }
        
        return dp[n];
    }
}
```






