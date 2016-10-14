# Problem 345: Reverse Vowels of a String


> https://leetcode.com/problems/reverse-vowels-of-a-string/

---------------
##思路
* 这道题在时间复杂度上有要求
* 我们用一个数组来记录元音的位置，然后在第二次访问的时候，交换元音的位置

-------------------------------------------------------
```java
public class Solution {
    public String reverseVowels(String s) {
        HashSet<Character> hs = new HashSet<Character>();
        hs.add('a');
        hs.add('e');
        hs.add('i');
        hs.add('o');
        hs.add('u');
        hs.add('A');
        hs.add('E');
        hs.add('I');
        hs.add('O');
        hs.add('U');

        int[] pos = new int[s.length()];   //record vowel character position
        int count = 0;                   //record vowel number
        for (int i = 0; i < s.length(); i++) {
            if (hs.contains(s.charAt(i))) {
                pos[count] = i;
                count++;
            }
        }

        char[] ans = s.toCharArray();
        for (int i = 0; i < count; i++) {
            ans[pos[i]] = s.charAt(pos[count - 1 - i]);
        }

        return String.valueOf(ans);
    }
}
```
```java
／*
  这个解法是正确的，但是在时间复杂度上不行，太麻烦了
*/
public class Solution {
    public String reverseVowels(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }
        
        HashSet<Character> set = new HashSet<Character>();
        set.add('a');
        set.add('e');
        set.add('i');
        set.add('o');
        set.add('u');
        set.add('A');
        set.add('E');
        set.add('I');
        set.add('O');
        set.add('U');
        
        int left = 0, right = s.length() - 1;
        while (left < right) {
            while (left < right && !set.contains(s.charAt(left))) left++;
            while (right > left && !set.contains(s.charAt(right))) right--;
            s = swap(s, left, right);
            left++;
            right--;
        }
        
        return s;
    }
    
    private String swap(String s, int left, int right) {
        char[] arr = s.toCharArray();
        char tmp = arr[left];
        arr[left] = arr[right];
        arr[right] = tmp;
        
        String str = new String(arr);
        
        return str;
    }
    
}
```
---------------------------

## 易错点
1. HashSet是去重复的有利手段；HashMap则是用来储存键值对的;
2. 思路：
   用count来记录元音元素；用一个数组pos来记录他们的位置
   ```java
   if (hs.contains(s.charAt(i))) {
          pos[count] = i;
          count++;
   }
   ```
3. length方法

|data structure|方法|描述|
| --| -- | -- |
|Array| s.length | 没括号 |
| String |s.length() |有括号 |
|List|s.size()|有括号|



4.**String转Array**
```char[] ans = s.toCharArray();```

5.**Array转String**
```
String.valueOf(ans);
```

6.互换元素的index关系
 ```ans[pos[i]] = s.charAt(pos[count - 1 - i]);```

