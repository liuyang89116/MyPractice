# Selection Sort

##思路
不断地选择剩余元素中的最小者。  
* 找到数组中最小元素并将其和数组第一个元素交换位置。
* 在剩下的元素中找到最小元素并将其与数组第二个元素交换，直至整个数组排序。

![](selection_sort.gif)

##复杂度分析
**Best**： $$\Omega(n^2)$$  
**Worst**: $$O(n^2)$$    
**Average**: $$\Theta(n^2)$$

---------------------
```java
package selectionSort;

public class SelectionSort {
	public static void main(String[] args) {
		int[] unsortedArray = new int[] { 8, 5, 2, 6, 9, 3, 1, 4, 0, 7 };
		selectionSort(unsortedArray);
		System.out.println("After Sort: ");
		printArr(unsortedArray);
	}

	private static void selectionSort(int[] arr) {
		int len = arr.length;
		for (int i = 0; i < len; i++) {
			printArr(arr);
			System.out.println();
			int minIndex = i;
			for (int j = i; j < len; j++) {
				if (arr[j] < arr[minIndex]) {
					minIndex = j;
				}
			}
			swap(arr, minIndex, i);
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