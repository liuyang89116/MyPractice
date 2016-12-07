# Find all the peak and valley

tags: tag1, tag2, tag3 is here
> 技术面试 一个数组 A[i + 1] = A +/- 1; 找出有所有 peek 和 valley 的坐标

------------
##思路
* 直观地想就是过一遍用 $$ O(n) $$ 的时间，维护一个最大值和最小值
* 优化：  
优化方法是 binary search。每次找出一个数就看一下它是不是 peek 或者 valley。是的话 就加入 result 里面，然后检查 mid - start == Math.abs(A[mid] - A[start])，排除这一段全部上升或下降的可能。

