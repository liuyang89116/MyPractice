# Bubble Sort

##思路
核心：**冒泡**，持续比较相邻元素，大的挪到后面，因此大的会逐步往后挪，故称之为冒泡。

![](bubble_sort.gif)

##复杂度分析
**Best**: $$\Omega (n)$$  
**Worst**: $$O(n^2)$$  
**Average**: $$\Theta(n^2)$$

------------------
```java
package bubbleSort;

public class BubbleSort {
	public static void main(String[] args) {
		int[] unsortedArr = new int[] { 6, 5, 3, 1, 8, 7, 2, 4 };
		bubbleSort(unsortedArr);
		System.out.println("After Sort: ");
		printArr(unsortedArr);
	}

	private static void bubbleSort(int[] arr) {
		int len = arr.length;
		for (int i = 0; i < len; i++) {
			printArr(arr);
			System.out.println();
			for (int j = 1; j < len - i; j++) {
				if (arr[j - 1] > arr[j]) {
					swap(arr, j - 1, j);
				}
			}
		}
	}

	private static void swap(int[] arr, int i, int j) {
		int tmp = arr[i];
		arr[i] = arr[j];
		arr[j] = tmp;
	}

	private static void printArr(int[] arr) {
		for (Integer num : arr) {
			System.out.print(num + " ");
		}
	}
}

```