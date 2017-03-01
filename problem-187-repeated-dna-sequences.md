# Problem 187: Repeated DNA Sequences

> https://leetcode.com/problems/repeated-dna-sequences/?tab=Description

------

## 思路

* 这道题是在求不止一次重复的 substring。我们可以用两个 hashset 来维护这个结果
* 用一个 testSet 来判断以前加过此元素没有。根据他的返回值，来判断是否要加入此元素进入 rstSet
* 最后把这个 rstSet 的结果都加入到 rst 的 list 里面

-------------

```java
public class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        List<String> rst = new ArrayList<String>();
        if (s == null || s.length() < 10) return rst;
        
        Set<String> testSet = new HashSet<String>();
        Set<String> rstSet = new HashSet<String>();
        for (int i = 0; i <= s.length() - 10; i++) {
            String str = s.substring(i, i + 10);
            if (!testSet.add(str)) {
                rstSet.add(str);
            }
        }
        rst.addAll(rstSet);
        
        return rst;
    }
}
```





