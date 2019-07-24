```java
package sort.heap_sort;

public class HeapSort2 {

    public void sort(int arr[]) {
        int n = arr.length;
        for (int i = n/2 - 1; i >=0; i--) {
            heapify(arr, n, i);
        }

        for (int i = n-1; i >= 0; i--) {
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            heapify(arr, i, 0);
        }
    }

    public void heapify(int arr[], int n, int i) {
        int largest = i;
        int left = i/2 + 1;
        int right = i/2 + 2;

        if (left < n && arr[left] > arr[largest])
            largest = left;

        if (right < n && arr[right] > arr[largest])
            largest = right;

        if (largest != i) {
            int temp = arr[largest];
            arr[largest] = arr[i];
            arr[i] = temp;

            heapify(arr, n, largest);
        }
    }

    public static void printArray(int arr[]) {
        int n = arr.length;
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int arr[] = {12, 11, 13, 5, 6, 7};
        HeapSort2 hs = new HeapSort2();
        hs.sort(arr);
        printArray(arr);
    }
}

```

