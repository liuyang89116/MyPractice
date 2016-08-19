# Problem 88: Merge Sorted Array


> https://leetcode.com/problems/merge-sorted-array/

------
##思路
* 因为我们没有额外的一个数组来单独存放最后的结果，所以我们不能从头到尾这么来扫一遍数组，因为开头的元素对于 nums1 来说是一个萝卜一个坑
* 但是，我们可以反其道而行之，就是**从后往前来存储元素！**

-------------
```java
public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;
        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }
        while (i >= 0) {
            nums1[k--] = nums1[i--];
        } 
        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }
    }
}
```
-----
##易错点
1. 对于表达方式的熟悉
```nums1[k--] = nums1[i--]```
```nums[i--]```是```nums[i]```先赋值再```i--```；同理```nums[k--]```是```nums[k]```先接到值，然后再```k--```。 

2. 这里相当于是，
```java
nums1[k] = nums1[i];
i--;
k--;
```
3. 最后对剩余元素的处理
```java
while (i >= 0) {
       nums1[k--] = nums1[i--];
} 
while (j >= 0) {
       nums1[k--] = nums2[j--];
}
```
对比LinkedList当之，我们最后用的是```if```语句，这是因为LinkedList可以直接通过 head 把剩下的字串直接存好。Array得通过while循环一个一个存。



























