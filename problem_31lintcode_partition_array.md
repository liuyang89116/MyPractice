

# Problem: Partition Array (LintCode)


> http://www.lintcode.com/en/problem/partition-array/

------------------------------------------------------------
##思路
* 这道题就是一个Quick Sort的题目。
* 其实理解这道题的题目本身就花了些时间

> Given an array nums of integers and an int k, partition the array (i.e move the elements in "nums") such that:
All elements < k are moved to the left;
All elements >= k are moved to the right

实际上是要进行*原位排序！*根据target元素，把数组分成两大块儿。（不需要对每个元素的相对位置都排序，只是分两大块）

* 说到底，思路本身其实就是设置连个指针，一头一尾。当“头大尾小”的情况发生时，首尾对调。其他情况则按兵不动，一直等到首尾都满足。
* 这是一个for循环嵌套while循环的例子，值得好好掌握

--------------------------------------------------------------------
```java
public class Solution {
    /**
     *@param nums: The integer array you should partition
     *@param k: As description
     *return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int i = 0;
        int j = nums.length - 1;
        for (; i <= j; i++) {
            if (nums[i] < k) {
                continue;
            }

            while (i <= j && nums[j] >= k) {
                j--;
            }

            if (i <= j) {
                int tmp = nums[i];
                nums[i] = nums[j];
                nums[j] = tmp;
                j--;
            }

        }
        return j + 1;
    }
}
```
##易错点
1. for循环缺省表达
   ```java
   int i = 0;
   for (; i <= j; i++) {
   
   }
   ```
2. 先变```i```（头指针），再变```j```（尾指针）
3. index细节
   ```java
   return j + 1;
   ```




