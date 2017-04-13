



# Problem 241: Different Ways to Add Parentheses

> https://leetcode.com/problems/different-ways-to-add-parentheses/\#/description

------

## 思路

* 通过遍历，定位每一个符号，然后把符号左右一分为二。
* 分别递归左右两部分，然后合并最后的解
* 如果没有数字被加进 list 里，最后把 input 放进来

---------

```java
public class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        List<Integer> rst = new ArrayList<>();
        for (int i = 0; i < input.length(); i++) {
            char sign = input.charAt(i);
            if (sign == '+' || sign == '-' || sign == '*') {
                String first = input.substring(0, i);
                String second = input.substring(i + 1);
                List<Integer> firstList = diffWaysToCompute(first);
                List<Integer> secondList = diffWaysToCompute(second);
                for (Integer num1 : firstList) {
                    for (Integer num2 : secondList) {
                        int num = 0;
                        switch(sign) {
                            case '+': num = num1 + num2;
                                break;
                            case '-': num = num1 - num2;
                                break;
                            case '*': num = num1 * num2;
                                break;
                        }
                        rst.add(num);
                    }
                }
            }
        }
        
        if (rst.size() == 0) rst.add(Integer.valueOf(input));
        
        return rst;
    }
}
```

# 



