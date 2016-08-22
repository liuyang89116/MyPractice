# Problem 229: Majority Element II


> https://leetcode.com/problems/majority-element-ii/

-----------
##思路
* 和上一道题目是类似的。只不过要达到1/3,我们得需要两个candidate来标记
* 还有一个**难点**就是，当我们确定了这两个candidate值以后，我们是不知道他们的实际count数的，因为中间经过了抵消。所以我们再循环一次看一下count数就好了

----------
```java
public class Solution {
    public List<Integer> majorityElement(int[] nums) {
        List<Integer> result = new ArrayList<Integer>();
        if (nums == null || nums.length == 0) {
            return result;
        }
        
        int candidate1 = -1; 
        int candidate2 = -1;
        int count1 = 0, count2 = 0;
        for (int i = 0; i < nums.length; i++) {
            if (candidate1 == nums[i]) {
                count1++;
            } else if (candidate2 == nums[i]) {
                count2++;
            } else if (count1 == 0) {
                candidate1 = nums[i];
                count1++;
            } else if (count2 == 0) {
                candidate2 = nums[i];
                count2++;
            } else {
                count1--;
                count2--;
            }
        }
        
        count1 = 0;
        count2 = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == candidate1) {
                count1++;
            }
            if (nums[i] == candidate2) {
                count2++;
            }
        }
        
        if (count1 > nums.length / 3) {
            result.add(candidate1);
        }
        if (count2 > nums.length / 3) {
            result.add(candidate2);
        }
        
        return result;
    }
}

```
##易错点

1. 循环的顺序
```java
for (int i = 0; i < nums.length; i++) {
        if (candidate1 == nums[i]) {
            count1++;
        } else if (candidate2 == nums[i]) {
            count2++;
        } else if (count1 == 0) {
            candidate1 = nums[i];
            count1++;
        } else if (count2 == 0) {
            candidate2 = nums[i];
            count2++;
        } else {
            count1--;
            count2--;
        }
}        
```
为什么要先比较candidate1和candidate2的值呢？为什么不先check两个count1，count2的值呢？
**原因**就是：因为这里有两个数，当出现这样的例子时```[2, 2]```我们返回的应该是一个```[2]```，如果先check count数，返回的结果会成为```[2, 2]```

2. 两条语句写一行有时会报错
































