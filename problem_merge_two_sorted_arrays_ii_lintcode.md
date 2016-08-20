# Problem: Merge Two Sorted Arrays II (LintCode)


> http://www.lintcode.com/en/problem/merge-two-sorted-arrays/

---------------
##思路

* 这道题比之前的其实要简单，上一道题目是“in place”的移动，这个有第三个数组来存储结果，反而简单

----
```java
class Solution {
    /**
     * @param A and B: sorted integer array A and B.
     * @return: A new sorted integer array
     */
    public int[] mergeSortedArray(int[] A, int[] B) {
        int m = A.length;
        int n = B.length;
        int[] sortArr = new int[m + n];
        int i = 0, j = 0, k = 0; 
        while (i < m && j < n) {
            if (A[i] < B[j]) {
                sortArr[k++] = A[i++];
            } else {
                sortArr[k++] = B[j++];
            }
        }
        while (i < m) {
            sortArr[k++] = A[i++];
        }
        while (j < n) {
            sortArr[k++] = B[j++];
        }
        
        return sortArr;
    }
}
```
