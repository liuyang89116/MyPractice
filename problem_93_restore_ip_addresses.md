# Problem 93: Restore IP Addresses


> https://leetcode.com/problems/restore-ip-addresses/

----------------------------------------------------------------

这道题很多的注意的地方，这也是刷题的意义所在：把中等题目完全掌握就没有什么问题了。

---------------------------------------------------------------

##思路
集合问题的一个统一的思路就是：
* 创建一个result的ArrayList， 一个单独的list， 待操作的字符串， starting index
* 首先想好return条件，然后有结果就加到result里面
* 而真正“结果”的产生，依靠于不停地循环，调用自己本身


-----------------------------------------------------------------

```java
public class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> result =  new ArrayList<String>();
        List<String> list = new ArrayList<String>();

        if (s.length() < 4 || s.length() > 12) {
            return result;
        }
        helper(result, list, s, 0);
        return result;
    }

    private void helper(List<String> result, List<String> list, String s, int index) {
        if (list.size() == 4) {
            if (index != s.length()) {
                return;
            }
            StringBuilder sb = new StringBuilder();
            for (String tmp : list) {
                sb.append(tmp);
                sb.append(".");
            }
            sb.deleteCharAt(sb.length() - 1);
            result.add(sb.toString());
        }

        for (int i = index; i < s.length() && i < index + 3; i++) {
            String tmp = s.substring(index, i + 1);
            if (isValid(tmp)) {
                list.add(tmp);
                helper(result, list, s, i + 1);
                list.remove(list.size() - 1);
            }
        }
    }

    private boolean isValid(String s) {
        if (s.charAt(0) == '0') {
            return s.equals("0");
        }
        int num = Integer.valueOf(s);
        return num > 0 && num <= 255;
    }
}
```
##易错点

1. 第一个corner case
   ```java
   if (s.length() < 4 || s.length() > 12) {
       return result;
   }
   ```
   首先排除掉过短或过长的字符串
2. 


