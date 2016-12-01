# Problem 208: Implement Trie (Prefix Tree)

> https://leetcode.com/problems/implement-trie-prefix-tree/

----------
##思路
* 首先要理清 trie 的基本结构：当前的字符 c；c 后面的 children；已经标记是否为一个单词的末尾 endWord。其中 children 可以用 HashMap 来存储。
* insert 和 search 的过程类似于“顺藤摸瓜”：把待查找的字符串 word 打散成 array，然后顺着每一个字符查找添加。
* 注意一定要在这个过程中更新当前 node 和 children

-------------------
```java
class TrieNode {
    char c;
    HashMap<Character, TrieNode> children = new HashMap<Character, TrieNode>();
    boolean endWord;
    
    public TrieNode() {
        children = new HashMap<Character, TrieNode>();
        endWord = false;
    }
    
    public TrieNode(char c) {
        this.c = c;
        children = new HashMap<Character, TrieNode>();
        endWord = false;
    }
    
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) {
        TrieNode node = root;
        HashMap<Character, TrieNode> children = root.children;
        char[] arr = word.toCharArray();
        for (int i = 0; i < arr.length; i++) {
            char c = arr[i];
            if (children.containsKey(c)) {
                node = children.get(c);
            } else {
                TrieNode newNode = new TrieNode(c);
                children.put(c, newNode);
                node = newNode;
            }
            children = node.children;
            if (i == word.length() - 1) {
                node.endWord = true;
            }
        }
        
    }

    // Returns if the word is in the trie.
    public boolean search(String word) {
        if (searchWordPos(word) == null) {
            return false;
        } else if (searchWordPos(word).endWord) {
            return true;
        } else {
            return false;
        }
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        if (searchWordPos(prefix) == null) {
            return false;
        } else {
            return true;
        }
    }
    
    
    private TrieNode searchWordPos(String s) {
        char[] arr = s.toCharArray();
        TrieNode node = null;
        HashMap<Character, TrieNode> children = root.children;
        for (int i = 0; i < arr.length; i++) {
            char c = arr[i];
            if (children.containsKey(c)) {
                node = children.get(c);
                children = node.children;
            } else {
                return null;
            }
        }
        
        return node;
    }
    
}

// Your Trie object will be instantiated and called as such:
// Trie trie = new Trie();
// trie.insert("somestring");
// trie.search("key");
```
-------
##易错点
1. 更新 children
```java
if (children.containsKey(c)) {
      node = children.get(c);
      children = node.children;
} else {
      return null;
}
```

















