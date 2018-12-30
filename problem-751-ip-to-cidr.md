# Problem 751: IP to CIDR

> [https://leetcode.com/problems/ip-to-cidr/](https://leetcode.com/problems/ip-to-cidr/)

![](/assets/751.png)

---

## 思路：

1. 这道题很难读懂，不知道为什么算是一道简单题。大概的意思是对一个 ip address，取前面的一串为 prefix，后面的数字为对应这个 prefix 的 id。这个帖子有助于理解题目：

   > [https://leetcode.com/problems/ip-to-cidr/discuss/151348/Java-Solution-with-Very-Detailed-Explanation-8ms](https://leetcode.com/problems/ip-to-cidr/discuss/151348/Java-Solution-with-Very-Detailed-Explanation-8ms)
   >
   > [https://blog.csdn.net/qq\_32832023/article/details/78891298](https://blog.csdn.net/qq_32832023/article/details/78891298)

2. 首先把一个 ip address 表示成十进制的数

```java
for (int i = 0; i < ips.length; i++) {
    num = num * 256 + Integer.parseInt(ips[i]);
}
```

1. 理解 `x & -x` 的含义：取从右往左第一个为 1 的那一位（取最低位的 1 ）。为什么要做这个操作呢？比如我们有一个 ip：`111111 101001 111000` 最后三位都是 0， 也就是说之前的可以作为 prefix，后面三位可以组成不同的 hosts。同时，我们也可以得出：如果是奇数，那么只可以有一个 id 可以用，因为奇数最后一位肯定是 1，后面没有 0 了。

2. `(int) (num & 255)` 求出后 8 位数的十进制表示

---

```java
class Solution {
    public List<String> ipToCIDR(String ip, int n) {
        List<String> rst = new ArrayList<>();
        
        String[] ips = ip.split("\\.");
        long num = 0;
        for (int i = 0; i < ips.length; i++) {
            num = num * 256 + Integer.parseInt(ips[i]);
        }
        
        while (n > 0) {
            long step = num & -num;
            
            while (step > n) step /= 2;
            rst.add(toIpString(num, step));
            num += step;
            n -= step;
        }
        
        return rst;
    }
    
    private String toIpString(long num, long step) {
        int[] blocks = new int[4];
        
        blocks[0] = (int) (num & 255);
        num >>= 8;
        blocks[1] = (int) (num & 255);
        num >>= 8;
        blocks[2] = (int) (num & 255);
        num >>= 8;
        blocks[3] = (int) (num & 255);
        num >>= 8;
        
        int count = 0;
        while (step > 0) {
            count++;
            step /= 2;
        }
        
        return blocks[3] + "." + blocks[2] + "." + blocks[1] + "." + blocks[0] + "/" + (33 - count);
    }
}
```



