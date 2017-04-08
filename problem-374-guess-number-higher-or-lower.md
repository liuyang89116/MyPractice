# Problem 374: Guess Number Higher or Lower

> https://leetcode.com/problems/guess-number-higher-or-lower/\#/description

---------

## 思路

* 常规题目，只是用一个 API 做了一些掩饰而已

--------

```
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int start = 1, end = n, mid;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            int guessRst = guess(mid);
            if (guessRst == 0) {
                return mid;
            } else if (guessRst == - 1) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (guess(start) == 0) {
            return start;
        } else {
            return end;
        }    
    }
}
```



