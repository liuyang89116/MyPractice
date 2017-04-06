# Problem 126: Word Ladder II

> https://leetcode.com/problems/word-ladder-ii/\#/description

------

## 思路

> https://discuss.leetcode.com/topic/27504/my-concise-java-solution-based-on-bfs-and-dfs

这个讲解不错！

* 这道题是上一题的延伸，要寻找所有的最短梯子的解，而上一题只要得出最短的 length 长度就可以了。
* 可以用 bfs + dfs 的方式来得出所有的解。这里用 distance 记录所有的元素从 beginWord 出发的距离，这样，我们可以先用 bfs 找出最短长度，然后不断地找剩下的 word，根据 distance 来 match

----------------

```java
public class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        List<String> path = new ArrayList<>();
        List<List<String>> rst = new ArrayList<>();
        Set<String> dict = new HashSet<String>(wordList);
        Map<String, List<String>> nodeNeighbors = new HashMap<>();
        Map<String, Integer> distance = new HashMap<>();
        
        dict.add(beginWord);
        bfs(beginWord, endWord, dict, nodeNeighbors, distance);
        dfs(beginWord, endWord, dict, nodeNeighbors, distance, path, rst);
        
        return rst;
    }
    
    private void bfs(String beginWord, String endWord, Set<String>dict, Map<String, List<String>> nodeNeighbors, Map<String, Integer> distance) {
        for (String s : dict) {
            nodeNeighbors.put(s, new ArrayList<>());
        }
        
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        distance.put(beginWord, 0);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            boolean isFinish = false;
            for (int i = 0; i < size; i++) {
                String word = queue.poll();
                int curDistance = distance.get(word);
                List<String> neighbors = getNeighbors(word, dict);
                
                for (String neighbor : neighbors) {
                    nodeNeighbors.get(word).add(neighbor);
                    if (!distance.containsKey(neighbor)) {
                        distance.put(neighbor, curDistance + 1);
                        if (neighbor.equals(endWord)) {
                            isFinish = true;
                        } else {
                            queue.offer(neighbor);
                        }
                    }
                }
            }
            
            if (isFinish) break;
        }
    }
    
    private void dfs(String currWord, String endWord, Set<String>dict, Map<String, List<String>> nodeNeighbors, Map<String, Integer> distance, List<String> path, List<List<String>> rst) {
        path.add(currWord);
        if (currWord.equals(endWord)) {
            rst.add(new ArrayList<String>(path));
        } else {
            for (String nextWord : nodeNeighbors.get(currWord)) {
                if (distance.get(nextWord) == distance.get(currWord) + 1) {
                    dfs(nextWord, endWord, dict, nodeNeighbors, distance, path, rst);
                }
            }
        }
        path.remove(path.size() - 1);
    }
    
    private List<String> getNeighbors(String word, Set<String> dict) {
        List<String> neighbors = new ArrayList<>();
        
        for (int i = 0; i < word.length(); i++) {
            for (char c = 'a'; c <= 'z'; c++) {
                if (c == word.charAt(i)) continue;
                
                String neighbor = replace(word, i, c);
                if (dict.contains(neighbor)) {
                    neighbors.add(neighbor);
                }
            }
        }
        
        return neighbors;
    }
    
    private String replace(String word, int index, char c) {
        char[] arr = word.toCharArray();
        arr[index] = c;
        return new String(arr);
    }
}



```



