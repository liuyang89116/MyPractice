# Problem: Backpack III

> Given n kind of items with size Ai and value Vi( each item has an infinite number available) and a backpack with size m. What's the maximum value can you put into the backpack?
Notice
You cannot divide item into small pieces and the total size of items you choose should smaller or equal to m.
Example
Given 4 items with size [2, 3, 5, 7] and value [1, 5, 2, 4], and a backpack with size 10. The maximum value is 15.

------
##思路
* 这道题的变化是：每个 item 可以重复选取
* 所以内层遍历 i 的时候从小到大遍历，这样物品可以重复选取。比如一开始在j的时候取了i，然后随着j的增大，在j'的时候又取了i，而恰好j = j' - A[i]，在这种情况下i就被重复选取。如果从大往小遍历则所有物品只能取一次，所以II中是从大往小遍历。
* 因此**可以重复取元素则背包容量从小到大遍历**，**反之从大到小遍历**。

------


```java
public class Solution {
    /**
     * @param A an integer array
     * @param V an integer array
     * @param m an integer
     * @return an array
     */
    public int backPackIII(int[] A, int[] V, int m) {
        // Write your code here
        int n = A.length;
        int[] dp = new int[m + 1];

        for(int j = 0; j < n; j++){
            for(int i = A[j]; i <= m; i++){
            //对于当前物品 j，若 i 从小到大的话，很可能在 i 之前的 i - A[j] 时已经放过第 j 件物品了，在 i 时再放就是重复放入；若 i 从大到小，则 i 之前的所有情况都没有更新过，不可能放过第 j 件物品，所以不会重复放入。
                if(dp[i] < dp[i - A[j]] + V[j]){
                   dp[i] = dp[i - A[j]] + V[j];
                }
            }
        }

        return dp[m];
    }
}
```

