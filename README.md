# DSA-K-Way-Merge-C
# DSA Assignment - K-Way Merge using Min Heap and Pairwise Merging

## Problem Statement
A financial system receives three already sorted transaction lists:
- L1 = [10, 30, 50, 70]
- L2 = [20, 40, 60, 80]
- L3 = [15, 35, 55, 75]

## C Program Implementation (Min Heap K-Way Merge)

```c
#include <stdio.h>
#include <stdlib.h>

struct MinHeapNode {
    int element;
    int i;
    int j;
};

void swap(struct MinHeapNode* a, struct MinHeapNode* b) {
    struct MinHeapNode temp = *a;
    *a = *b;
    *b = temp;
}

void minHeapify(struct MinHeapNode arr[], int i, int heapSize) {
    int smallest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < heapSize && arr[left].element < arr[smallest].element)
        smallest = left;

    if (right < heapSize && arr[right].element < arr[smallest].element)
        smallest = right;

    if (smallest != i) {
        swap(&arr[i], &arr[smallest]);
        minHeapify(arr, smallest, heapSize);
    }
}

void kWayMerge(int arr[][4], int k, int n, int output[]) {
    struct MinHeapNode* harr = (struct MinHeapNode*)malloc(k * sizeof(struct MinHeapNode));
    int initial_heap_size = 0;

    for (int i = 0; i < k; i++) {
        if (n > 0) {
            harr[i].element = arr[i][0];
            harr[i].i = i;
            harr[i].j = 1;
            initial_heap_size++;
        }
    }

    for (int i = (initial_heap_size - 1) / 2; i >= 0; i--)
        minHeapify(harr, i, initial_heap_size);

    int count = 0;
    while (initial_heap_size > 0) {
        struct MinHeapNode root = harr[0];
        output[count++] = root.element;

        if (root.j < n) {
            harr[0].element = arr[root.i][root.j];
            harr[0].j = root.j + 1;
        } else {
            harr[0] = harr[initial_heap_size - 1];
            initial_heap_size--;
        }
        minHeapify(harr, 0, initial_heap_size);
    }
    free(harr);
}

int main() {
    int k = 3;
    int n = 4;
    int L[3][4] = {
        {10, 30, 50, 70},
        {20, 40, 60, 80},
        {15, 35, 55, 75}
    };

    int output[12];
    kWayMerge(L, k, n, output);

    printf("--- K-Way Merge using Min Heap ---\nMerged Output: ");
    for (int i = 0; i < k * n; i++) {
        printf("%d ", output[i]);
    }
    printf("\n");
    return 0;
}





# DSA Assignment - K-Way Merge using Min Heap and Pairwise Merging

## Project Structure
- **README.md**: Contains problem statement, documentation, and implementation code.
- **ANALYSIS.md**: Contains the performance analysis, time complexity, and comparison between Min Heap and Pairwise Merging.

## Data Structures Used
- **Min Heap**: Used for efficient K-Way merging by keeping track of the minimum elements from each sorted list.
- **Arrays**: Used to store the input transaction lists and the final merged output.

## How to Build and Run
1. Clone or download the repository.
2. Open a terminal/command prompt in the project folder.
3. Compile the C program using GCC:
   ```bash
   gcc minheap.c -o minheap




## Trace Table & Execution Steps
- **Step 1:** Initialize Min Heap with the first element of each of the $K$ sorted lists.
- **Step 2:** Extract the minimum element from the heap and store it in the output array.
- **Step 3:** Insert the next element from the same list into the heap and heapify.
- **Step 4:** Repeat until all elements are processed.

## Comparison Table / Performance Analysis
| Approach | Heap Size | Time Complexity | Space Complexity |
| :--- | :--- | :--- | :--- |
| **Min Heap K-Way Merge** | $K$ | $O(N \log K)$ | $O(K)$ |
| **Pairwise Merging** | None (0) | $O(N \times K)$ | $O(N)$ |
