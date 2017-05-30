# Problem 425: Word Squares

> [https://leetcode.com/problems/word-squares/\#/description](https://leetcode.com/problems/word-squares/#/description)

---

![](/assets/425_1.png)![](/assets/425_2.png)![](/assets/425_3.png)



-------

## 思路

* 这是一道用 trie 的 prefix 来处理的题目，这个讲解非常好。

> https://discuss.leetcode.com/topic/63516/explained-my-java-solution-using-trie-126ms-16-16



-------

```java
public class Solution {
    class TrieNode {
        List<String> startWith;
        TrieNode[] children;
        
        public TrieNode() {
            startWith = new ArrayList<>();
            children = new TrieNode[26];
        }
    }
    
    class Trie {
        TrieNode root;
        
        public Trie(String[] words) {
            root = new TrieNode();
            for (String word : words) {
                TrieNode cur = root;
                for (char c : word.toCharArray()) {
                    int index = c - 'a';
                    if (cur.children[index] == null) cur.children[index] = new TrieNode();
                    cur.children[index].startWith.add(word);
                    cur = cur.children[index];
                }
            }
        }
        
        public List<String> findByPrefix(String prefix) {
            List<String> rst = new ArrayList<>();
            TrieNode cur = root;
            for (char c : prefix.toCharArray()) {
                int index = c - 'a';
                if (cur.children[index] == null) return rst;
                cur = cur.children[index];
            }
            rst.addAll(cur.startWith);
            return rst;
        }
    }
    
    public List<List<String>> wordSquares(String[] words) {
        List<List<String>> rst = new ArrayList<>();
        if (words == null || words.length == 0) return rst;
        int len = words[0].length();
        Trie trie = new Trie(words);
        List<String> rstBuilder = new ArrayList<>();
        for (String word : words) {
            rstBuilder.add(word);
            search(len, trie, rstBuilder, rst);
            rstBuilder.remove(rstBuilder.size() - 1);
        }
        return rst;
    }
    
    private void search(int len, Trie trie, List<String> rstBuilder, List<List<String>> rst) {
        if (rstBuilder.size() == len) {
            rst.add(new ArrayList<>(rstBuilder));
            return;
        }
        int index = rstBuilder.size();
        StringBuilder prefixBuilder = new StringBuilder();
        for (String s : rstBuilder) {
            prefixBuilder.append(s.charAt(index));
        }
        List<String> startWith = trie.findByPrefix(prefixBuilder.toString());
        for (String sw : startWith) {
            rstBuilder.add(sw);
            search(len, trie, rstBuilder, rst);
            rstBuilder.remove(rstBuilder.size() - 1);
        }
    }
}



```



