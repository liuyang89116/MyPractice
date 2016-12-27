# Problem 295: Find Median from Data Streamf

> https://leetcode.com/problems/find-median-from-data-stream/

----------
##思路
* 这道题十分巧妙。要想得到中位数，那么我们可以把一串数从中间一劈为二，如果左右的个数相同，那么左边右边加起来除以二；如果不相等，那么取右边的（因为默认右边多）
* 左边最大堆，右边最小堆。维持最大堆的时候，add 一个负数就可以了。

------------------
```java
public class MedianFinder {
    
    Queue<Integer> left = new PriorityQueue<Integer>();
    Queue<Integer> right = new PriorityQueue<Integer>();

    // Adds a number into the data structure.
    public void addNum(int num) {
        right.offer(num);
        left.offer(-right.poll());
        if (left.size() > right.size()) {
            right.add(-left.poll());
        }
    }

    // Returns the median of current data stream
    public double findMedian() {
        if (right.size() > left.size()) {
            return (double) right.peek();
        } else {
            return (double) (right.peek() - left.peek()) / 2;
        }
    }
};

// Your MedianFinder object will be instantiated and called as such:
// MedianFinder mf = new MedianFinder();
// mf.addNum(1);
// mf.findMedian();
```
-----
##易错点
1. Queue 的操作  
**offer() / poll()**  
联想 Stack 的操作：  
push() / pop()  

































