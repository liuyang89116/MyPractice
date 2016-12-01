# Problem 91: Decode Ways

>https://leetcode.com/problems/decode-ways/

-----------
##思路
* 和 word ladder 类似的一个 dp 题目
* 单个的数字只要不是 0 就对应一种方法；两位数的时候，考虑首位数字是否为 0

----------
```java
public class Solution {
    public int numDecodings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
    
        int[] nums = new int[s.length() + 1];
        nums[0] = 1;
        nums[1] = s.charAt(0) == '0' ? 0 : 1;
        for (int i = 2; i <= s.length(); i++) {
            if (s.charAt(i - 1) != '0') {
                nums[i] = nums[i - 1];
            }
            
            // 得到两位数的方法
            int twoDigits = (s.charAt(i - 2) - '0') * 10 + (s.charAt(i - 1) - '0');
            if (twoDigits >= 10 && twoDigits <= 26) {
                nums[i] += nums[i - 2];
            }
        }
        
        return nums[s.length()];
    }
}
```
--------
##易错点
1. String s 和数组 nums 的 index 正好错一位  
比如 s.charAt(0) 对应的其实是 nums[1] 
```java
if (s.charAt(i - 1) != '0') {
         nums[i] = nums[i - 1];
}
```
2. 循环的 upper bound
```java
for (int i = 2; i <= s.length(); i++)
```
之前写的是
```java
for (int i = 2; i <= nums.length; i++)
```
就这么一个小细节，就会导致结果的越界。
**非常容易出错，第二次写的时候，又在这里错了！**
3. 注意 charAt() 方法
```java
nums[1] = s.charAt(0) == '0' ? 0 : 1;
```
写成了
```java
nums[1] = s.charAt(0) == 0 ? 0 : 1;
```
少了引号，但是 compiler 是不会报错的。



















