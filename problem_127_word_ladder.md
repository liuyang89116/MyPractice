# Problem 127:  Word Ladder

> [https://leetcode.com/problems/word-ladder/](https://leetcode.com/problems/word-ladder/)

---

## 思路

* 这道题做了一些改动，在之前的时候，parameter 是 Set，这里改成了 List。其实 list 也可以用来检查元素是否在其中，但是效率比 set 慢很多，最后的一些 test case 会过不去。
* 这道题用 BFS 搜索，找到第一个元素，然后依次替换每一个字母，看是否在字典里
* 用 queue 来实现 BFS，遍历每一个元素。
* 用一个 HashSet 来 track 是否访问过此元素
* 每一次找 nextWord 都是对当前的 word 做一个改动 

---

```java
public class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if (wordList == null) {
            return 0;
        }
        if (beginWord.equals(endWord)) {
            return 1;
        }

        Set<String> wordSet = new HashSet<String>();
        for (String s : wordList) {
            wordSet.add(s);
        }

        HashSet<String> visited = new HashSet<String>();
        Queue<String> queue = new LinkedList<String>();
        visited.add(beginWord);
        queue.offer(beginWord);

        int count = 1;
        while (!queue.isEmpty()) {
            count++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String word = queue.poll();
                for (String nextWord : getNextWord(word, wordSet)) {
                    if (visited.contains(nextWord)) continue;

                    if (nextWord.equals(endWord)) {
                        return count;
                    }
                    visited.add(nextWord);
                    queue.offer(nextWord);
                }
            }
        } 

        return 0;
    }

    private ArrayList<String> getNextWord(String word, Set<String> wordSet) {
        ArrayList<String> nextWordList = new ArrayList<String>();
        for (char c = 'a'; c <= 'z'; c++) {
            for (int i = 0; i < word.length(); i++) {
                if (c == word.charAt(i)) continue;

                String nextWord = replace(word, i, c);
                if (wordSet.contains(nextWord)) {
                    nextWordList.add(nextWord);
                }
            }
        }

        return nextWordList;
    }

    private String replace(String word, int index, char c) {
        char[] arr = word.toCharArray();
        arr[index] = c;

        return new String(arr);
    }

}
```

---

## 易错点

1.先把首位两个字母加到字典里去，而不是加到 HashSet

```java
wordList.add(beginWord);
wordList.add(endWord);
```

2. char 也可以循环

```java
for (char c = 'a'; c <= 'z'; c++) {
     for (int i = 0; i < word.length(); i++) {
           if (c == word.charAt(i)) {
                continue;
           }
           String nextWord = replace(word, i, c);
           if (wordList.contains(nextWord)) {
                nextWordList.add(nextWord);
           }
      }
}
```

3. 注意是 equals 方法比较，而不是 “==”

```java
if (nextWord.equals(endWord)) {
    return count;
}
```



