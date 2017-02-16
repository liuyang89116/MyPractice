# Problem 140: Word Break II

> https://leetcode.com/problems/word-break-ii/

--------------
##思路
* 用一个 HashMap 来 maintain `<Index, 与此 index 对应的 wordList>`，这样的话，如果后面的元素需要调出指定的 index 的时候，可以迅速从 map 里寻找，不需要再重新计算。
* 每次都用 substring 函数来得出一个一个临时的 tmp 单词，然后去 map 里去比对。如果 map 里有，直接调出来；如果没有，再执行一次 helper 函数。
* 记得先把字典从 list 转成 set，便于查找。

---------


```java
public class Solution {
    HashMap<Integer, List<String>> map = new HashMap<Integer, List<String>>();
    
    public List<String> wordBreak(String s, List<String> wordDict) {
        Set<String> wordSet = new HashSet<String>();
        for (String word : wordDict) {
            wordSet.add(word);
        }
        int maxLength = findMaxLength(wordSet);
        
        return helper(s, wordSet, 0, maxLength);
    }
    
    private List<String> helper(String s, Set<String> wordSet, int index, int maxLength) {
        List<String> wordList = new ArrayList<String>();
        if (index == s.length()) {
            wordList.add("");
            return wordList;
        }
        
        for (int i = index + 1; i <= index + maxLength && i <= s.length(); i++) {
            String tmp = s.substring(index, i);
            if (wordSet.contains(tmp)) {
                List<String> tmpList;
                if (map.containsKey(i)) {
                    tmpList = map.get(i);
                } else {
                    tmpList = helper(s, wordSet, i, maxLength);
                }
                
                for (String word : tmpList) {
                    wordList.add(tmp + (word.equals("") ? "" : " ") + word);
                }
            }
        }
        map.put(index, wordList);
        
        return wordList;
    }
    
    
    private int findMaxLength(Set<String> wordSet) {
        int maxLength = 0;
        for (String word : wordSet) {
            maxLength = Math.max(maxLength, word.length());
        }
        
        return maxLength;
    }
}
```

