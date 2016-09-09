# Problem 60: Permutation Sequence

> https://leetcode.com/problems/permutation-sequence/

---------
##思路
* 基本的思路: 
1） For n numbers, permutations can be divided into n groups with (n - 1)! elements in each group. 2） Thus, k / (n - 1)! is the group index among the current n (to be) sorted groups；3） and k % (n - 1)! is the sequence number k for next iteration.    
* 这个讲解不错
>https://github.com/liuyang89116/LeetCode-1/blob/master/Backtracking/Permutation%20Sequence.java

------------
```java
public class Solution {
    public String getPermutation(int n, int k) {
        LinkedList<Integer> list = new LinkedList<Integer>();
        for (int i = 1; i <= n; i++) {
            list.add(i);
        }
        int fact = 1;
        for (int i = 2; i <= n; i++) {
            fact *= i;
        }
        
        StringBuilder sb = new StringBuilder();
        for (k--; n > 0; n--) {
            fact /= n;
            sb.append(list.remove(k / fact));
            k %= fact;
        }
        
        return sb.toString();
        
    }
}
```
----
##易错点

1. 用 LinkedList 把元素存好，然后一个一个地取出来
2. for 循环 k-- 相当于是 k = k - 1;
```java
for (k--; n > 0; n--) {
          fact /= n;
          sb.append(list.remove(k / fact));
          k %= fact;
}
```
























