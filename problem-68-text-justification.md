# Problem 68: Text Justification

> https://leetcode.com/problems/text-justification/

------------
##思路
* String 里面的难题，能把这个折腾明白，String 里的题基本就差不多了。
* 这道题属于纯粹的字符串操作，要把一串单词安排成多行限定长度的字符串。主要**难点**在于空格的安排，首先每个单词之间必须有空格隔开，而当当前行放不下更多的 单词并且字符又不能填满长度 L 时，我们要把空格均匀的填充在单词之间。如果剩余的空格量刚好是间隔倍数那么就均匀分配即可，否则还必须把多的一个空格放到前面的间隔里面。
* 实现中我们维护一个 count 计数记录当前长度，超过之后我们计算共同的空格量以及多出一个的空格量，然后将当行字符串构造出来。
* 最后一个细节就是最后一行不需要均匀分配空格，句尾留空就可以，所以要单独处理一下。

----------
##复杂度
时间上我们需要**扫描单词一遍**，然后在找到行尾的时候再扫描一遍当前行的单词，不过总体每个单词不会被访问超过两遍，所以总体时间复杂度是`O(n)`。而空间复杂度则是结果的大小（跟单词数量和长度有关，不能准确定义，如果知道最后行数 r，则是`O(r*L)`）。

--------------



```java
public class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> rst = new ArrayList<>();
        if (words == null || words.length == 0) {
            return rst;
        }
        // count 是上一次计算的单词的长度，last 是记录下一个单词的开始
        int count = 0, last = 0;
        for (int i = 0; i < words.length; i++) {
            // words[i].length() 是尝试放当前的单词
            // (i - last) 是这一行单词之间的间隔个数
            // 它们的和用来判断这个单词放在这里是否会超过 L
            if (count + words[i].length() + (i - last) > maxWidth) {
                int numOfSpace = 0;
                int extraSpace = 0;
                // 因为 words[i] 尝试失败了，所以间隔数减去 1
                if (i - last - 1 > 0) { // 计算要放几个 space 以及是否需要 extra space
                    numOfSpace = (maxWidth - count) / (i - last - 1);
                    extraSpace = (maxWidth - count) % (i - last - 1);
                }
                StringBuilder sb = new StringBuilder();
                for (int j = last; j < i; j++) {
                    sb.append(words[j]);
                    if (j < i - 1) { // words[i - 1] 之后就不用填空格了，所以这里是 j < i - 1
                        for (int k = 0; k < numOfSpace; k++) {
                            sb.append(" ");
                        }
                        if (extraSpace > 0) {
                            sb.append(" ");
                        }
                        extraSpace--;
                    }
                }
                
                // 这个 for loop 用来处理只有一个单词还没有填满一行的情况
                for (int j = sb.length(); j < maxWidth; j++) {
                    sb.append(" ");
                }
                
                rst.add(sb.toString());
                count = 0;
                last = i; // 下一个单词的开始
            }
            
            count += words[i].length();
        }
        
        // 单独处理最后一行
        StringBuilder sb = new StringBuilder();
        for (int i = last; i < words.length; i++) {
            sb.append(words[i]);
            if (sb.length() < maxWidth) {
                sb.append(" ");
            }
        }
        for (int i = sb.length(); i < maxWidth; i++) {
            sb.append(" ");
        }
        
        rst.add(sb.toString());
        
        return rst;
    }
}
```

-------
##其他解法
* 还可以用 dynamic programming 来做，这里这个视频讲解很好
> https://www.youtube.com/watch?v=RORuwHiblPc

* 这里是代码
> https://github.com/mission-peace/interview/blob/master/src/com/interview/linklist/CopyLinkListWIthArbitPointer.java

* 不过这个时空复杂度是 `O(n^2)`





































