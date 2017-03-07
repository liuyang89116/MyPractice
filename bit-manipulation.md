# Bit Manipulation

> [https://discuss.leetcode.com/topic/50315/a-summary-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently](https://discuss.leetcode.com/topic/50315/a-summary-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently)

* 这个帖子讲得非常好！

---------

## 基本操作总结

* Set union `A | B`
* Set intersection `A & B`
* Set subtraction `A & ~B`
* Set negation `ALL_BITS ^ A` or `~A`
* Set bit `A |= 1 << bit`
* Clear bit `A &= ~(1 << bit)`
* Test bit `(A & 1 << bit) != 0`
* Extract last bit `A &-A` or `A & ~(A - 1)` or `x ^ (x & (x-1))`
* Remove last bit `A & (A-1)`
* Get all 1-bits `~0`











--------

## XOR \(^\) tricks

* XOR 主要用来剔除掉**偶数个的相同元素**，而生下来单独存在的元素
* 特性： 

\(1\) 恒等律：`A ^ 0 = A`

\(2\) 归零律:  `A ^ A = 0`

相同的元素互相抵消；任何元素与 0 异或得到本身。

### eg1: 不使用其他空间，交换两个值

```
a = a ^ b;    
b = a ^ b;   // b = a ^ b = a ^ b ^ b = a ^ 0 = a
a = a ^ b;   // a = a ^ a ^ b = b
```

### eg2: Missing Number

> Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array. For example, Given nums = \[0, 1, 3\] return 2. \(Of course, you can do this by math.\)

```java
public class Solution {
    public int missingNumber(int[] nums) {
        int index = 0, xor = 0;
        for (int i = 0; i < nums.length; i++) {
            xor ^= index ^ nums[i];
            index++;
        }

        return xor ^ index;
    }
}
```

---

## AND \(&\) tricks

* selecting certain bits
* reverse the bits in integer

### eg1: BITWISE AND OF NUMBERS RANGE

```java
public class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        if (m == 0) return 0;

        int count = 0;
        while (m != n) {
            m >>= 1;
            n >>= 1;
            count++;
        }

        return m << count;
    }
}
```

### eg2: NUMBER OF 1 BITS

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            count += (n & 1);
            n = n >>> 1;
        }

        return count;
    }
}
```

---

## OR \(\|\) trick

* Keep as many 1-bits as possible

## eg1: Find Largest power of 2

> Find the largest power of 2 \(most significant bit in binary form\), which is less than or equal to the given number N.

```java
long largest_power(long N) {
    //changing all right side bits to 1.
    N = N | (N>>1);
    N = N | (N>>2);
    N = N | (N>>4);
    N = N | (N>>8);
    N = N | (N>>16);
    return (N+1)>>1;
}
```

## eg2: REVERSE BITS

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int rst = 0;
        for (int i = 0; i < 32; i++) {
            rst += (n & 1);
            n >>>= 1;
            if (i < 31) rst <<= 1;
        }

        return rst;
    }
}
```



