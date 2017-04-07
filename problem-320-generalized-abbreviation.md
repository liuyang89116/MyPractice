# Problem 320: Generalized Abbreviation

> [https://leetcode.com/problems/generalized-abbreviation/\#/description](https://leetcode.com/problems/generalized-abbreviation/#/description)

---

![](/assets/320.png)

---

## 思路

* 对每个 character 来说，有两种情况：取或者不取。

* 对于每个 dfs，也有两种情况：count 增加，或者从 0  开始。

---------

```java
public class Solution {
    public List<String> generateAbbreviations(String word) {
        List<String> rst = new ArrayList<>();
        dfs(word, "", 0, 0, rst);
        
        return rst;
    }
    
    private void dfs(String word, String cur, int pos, int count, List<String> rst) {
        if (pos == word.length()) {
            if (count > 0) cur += count;
            rst.add(cur);
            return;
        } 
            
        dfs(word, cur, pos + 1, count + 1, rst);
        dfs(word, cur + (count > 0 ? count : "") + word.charAt(pos), pos + 1, 0, rst);
    }
}
```



