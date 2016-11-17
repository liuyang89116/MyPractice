# Problem 211: Add and Search Word - Data structure design

##思路
* 这道题是考察 trie 的经典题目
* 首先，构造一个 TrieNode 的 class，里面存放两个信息，一个是他的子结点，第二个是 flag，判断是否是一个单词的最末尾
* 添加单词的时候，不断更新 curr 指针的位置，在最后一个指针的时候标记为 endWord
* find 函数很重要，index 用来标记从什么地方开始搜索。搜索成功的退出条件是 index 等于 word 的长度。

-------------------------
```java
class TrieNode {
    public TrieNode[] children;
    public boolean endWord;
    
    public TrieNode() {
        children = new TrieNode[26];
        endWord = false;
    }
}

public class WordDictionary {
    private TrieNode root;
    
    public WordDictionary() {
        root = new TrieNode();
    }
    
    // Adds a word into the data structure.
    public void addWord(String word) {
        TrieNode curr = root;
        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            if (curr.children[c - 'a'] == null) {
                curr.children[c - 'a'] = new TrieNode();
            }
            curr = curr.children[c - 'a'];
        }
        curr.endWord = true;
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        return find(word, 0, root);
    }
    
    public boolean find(String word, int index, TrieNode curr) {
        if (index == word.length()) {
            return curr.endWord;
        }
        
        char c = word.charAt(index);
        if (c == '.') {
            for (int i = 0; i < 26; i++) {
                if (curr.children[i] != null) {
                    if (find(word, index + 1, curr.children[i])) {
                        return true;
                    }
                }
            }
            return false;
        } else if (curr.children[c - 'a'] != null) {
            return find(word, index + 1, curr.children[c - 'a']);
        } else {
            return false;
        }
         
    }
    
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```
--------
##易错点

1. 设立 curr 指针
```java
TrieNode curr = root;
```
因为这个 curr 可以不断更新每个词的位置，直接操作 root 的话会影响后面的结果
2. 理解递归函数的意义
```java
if (find(word, index + 1, curr.children[i]))
```
这是在遇到 '.' 的时候，下一步是在 curr 的 children 下面继续寻找
```java
find(word, index + 1, curr.children[c - 'a']);
```
这是在定位到相应的字符时，下一步在这个字符的后面继续操作。


















