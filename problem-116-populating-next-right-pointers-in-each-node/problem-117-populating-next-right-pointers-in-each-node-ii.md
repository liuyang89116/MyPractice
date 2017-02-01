# Problem 117: Populating Next Right Pointers in Each Node II

> https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/

-----
##思路
* 这道题不是 perfect tree 了，不能再用简单的 recursion 来解决，所以我们要用 iterative 的方法遍历整个 tree
* 总的思路就是先挂左边的结点，然后再挂右边的结点，这里用一个 dummy node 来 maintain 所有的结点顺序。
