# Problem 274: H-Index

> https://leetcode.com/problems/h-index/\#/description

--------

## 思路

* 首先应该搞清 h-index 的含义：不少于 h 篇的文章，引用次数大于等于 h。从这个定义也可以看出来：h &gt;= n，因为 h 不可能比篇数还大
* 用一个额外的 arr 来记录对应的大于 i 的引用的文章的篇数，最后倒着遍历就可以得到 h - index

--------

```java
public class Solution {
    public int hIndex(int[] citations) {
        if (citations == null || citations.length == 0) return 0;
        
        int n = citations.length;
        int[] arr = new int[n + 1];
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (citations[i] >= n) {
                arr[n]++;
            } else {
                arr[citations[i]]++;
            }
        }
        
        for (int i = n; i >= 0; i--) {
            count += arr[i];
            if (count >= i) return i;
        }
        
        return 0;
    }
}
```





