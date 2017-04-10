# Problem 179: Largest Number

> https://leetcode.com/problems/largest-number/\#/description

----------

## 思路

* 这道题的核心思想就是：有两个 String `str1 = "23"`, `str2 = "65"`，他们的组合可能是 `str1 + str2 : "2365"` 或者 `str2 + str1 : "6523"`。
* 所以我们可以用一个 comparator 来比较这两种连接方式。
* 注意我们是用 reverse 的 order 来排序的，因为最后是 append 从大到小的 string

----------

```java
public class Solution {
    public String largestNumber(int[] nums) {
        if (nums == null || nums.length == 0) return "0";
        
        String[] strArr = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            strArr[i] = String.valueOf(nums[i]);
        }
        Arrays.sort(strArr, new Comparator<String>(){
            public int compare(String str1, String str2) {
                String s1 = str1 + str2;
                String s2 = str2 + str1;
                return s2.compareTo(s1);
            }
        });
        
        StringBuilder sb = new StringBuilder();
        for (String s : strArr) {
            sb.append(s);
        }
        if (strArr[0].charAt(0) == '0') return "0";
        
        return sb.toString();
    }
}
```



