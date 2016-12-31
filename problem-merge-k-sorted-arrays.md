# Problem: Merge K sorted Arrays

> Given k sorted integer arrays, merge them into one sorted array. Do it in O(N log k).N is the total number of integers.k is the number of arrays.

``` 
Example  
Given 3 sorted arrays:   
[ 
  [1, 3, 5, 7],
  [2, 4, 6],
  [0, 8, 9, 10, 11]
]
return [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11].
Challenge

Tags：Heap Priority Queue
```

-----------
##思路
* 思路和上面一题一样，都是利用 Heap 来解决。
* 这里的 trick 是： 对于 LinkedList 我们可以有 pointer 来把当前元素之后剩下的元素 push 进去，但是对于 array 该怎么办呢？
* 我们自己创建一个 class Node，这个 node 有 val，row， pos 三个属性，这样就标记了它的值，第几行，第几个元素，从而实现 merge

--------
##复杂度
* Time： `O(n log K)`

---------


```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.PriorityQueue;

/**
 * Created by yang on 12/31/16.
 */
public class Solution {
    // node class, used to "linked" each array
    public static class Node {
        int val, row, pos;

        public Node(int val, int row, int pos) {
            this.val = val;
            this.row = row;
            this.pos = pos;
        }
    }

    // sort K arrays
    public static List<Integer> mergeKSortedArrays(int[][] arrays) {
        List<Integer> rst = new ArrayList<>();
        if (arrays == null || arrays.length == 0) {
            return rst;
        }

        PriorityQueue<Node> pq = new PriorityQueue<>(arrays.length, new Comparator<Node>() {
            @Override
            public int compare(Node o1, Node o2) {
                return o1.val - o2.val;
            }
        });

        for (int i = 0; i < arrays.length; i++) {
            if (arrays[i].length == 0) continue;
            Node newNode = new Node(arrays[i][0], i, 0);
            pq.offer(newNode);
        }
        while (!pq.isEmpty()) {
            Node num = pq.poll();
            rst.add(num.val);
            if (num.pos < arrays[num.row].length - 1) {
                pq.offer(new Node(arrays[num.row][num.pos + 1], num.row, num.pos + 1));
            }
        }

        return rst;
    }

    public static void main(String[] args) {
        int[] arr1 = new int[]{1, 3, 5, 7};
        int[] arr2 = new int[]{2, 4, 6};
        int[] arr3 = new int[]{0, 8, 10, 12};
        int[][] arr = new int[][]{arr1, arr2, arr3};

        List<Integer> rst = mergeKSortedArrays(arr);
        for (int num : rst) {
            System.out.print(num + " ");
        }
    }
}



```

