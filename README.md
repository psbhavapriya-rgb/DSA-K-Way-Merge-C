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
#define K 3
#define SIZE 4 #define TOTAL (K * SIZE)
typedef struct {     int value;     int list;     int index; } HeapNode;
typedef struct {     HeapNode arr[K];     int size; } MinHeap;
void swap(HeapNode *a, HeapNode *b) {
    HeapNode temp = *a;
    *a = *b;
    *b = temp; }
void heapifyDown(MinHeap *heap, int i, int *comparisons) {     while (1)     {         int smallest = i;         int left = 2 * i + 1;         int right = 2 * i + 2;
        if (left < heap->size)         {             (*comparisons)++;             if (heap->arr[left].value < heap->arr[smallest].value)                 smallest = left;         }
        if (right < heap->size)         {             (*comparisons)++;
            if (heap->arr[right].value < heap->arr[smallest].value)                 smallest = right;         }
        if (smallest == i)             break;
        swap(&heap->arr[i], &heap->arr[smallest]);         i = smallest;     } }
void insertHeap(MinHeap *heap, HeapNode node) {     int i = heap->size;     heap->arr[i] = node;     heap->size++;
    while (i > 0)     {
        int parent = (i - 1) / 2;
        if (heap->arr[parent].value <= heap->arr[i].value)             break;
        swap(&heap->arr[parent], &heap->arr[i]);         i = parent;     }
}
HeapNode removeMin(MinHeap *heap, int *comparisons)
{     HeapNode minNode = heap->arr[0];
    heap->size--;
    if (heap->size > 0)     {         heap->arr[0] = heap->arr[heap->size];         heapifyDown(heap, 0, comparisons);     }
    return minNode; }
void printHeap(MinHeap *heap) {     printf("[ ");
    for (int i = 0; i < heap->size; i++)         printf("%d ", heap->arr[i].value);
    printf("]"); }
void kWayMerge(int lists[K][SIZE]) {     MinHeap heap;     heap.size = 0;
    int comparisons = 0;     int output[TOTAL];     int count = 0;
    for (int i = 0; i < K; i++)     {         HeapNode node;
        node.value = lists[i][0];         node.list = i;         node.index = 0;
        insertHeap(&heap, node);     }
    printf("\n====================================\n");     printf(" K-WAY MERGE USING MIN HEAP\n");     printf("====================================\n");
    printf("Initial Heap: ");     printHeap(&heap);     printf("\n\n");
    while (heap.size > 0)     {         HeapNode minNode = removeMin(&heap, &comparisons);
        output[count] = minNode.value;         count++;
        if (minNode.index + 1 < SIZE)         {             HeapNode nextNode;
            nextNode.list = minNode.list;             nextNode.index = minNode.index + 1;             nextNode.value = lists[minNode.list][nextNode.index];
            insertHeap(&heap, nextNode);         }
        printf("Step %2d : Deleted %d\tHeap = ",                count, minNode.value);         printHeap(&heap);         printf("\n");     }
    printf("\nFinal K-Way Output:\n");     for (int i = 0; i < TOTAL; i++)         printf("%d ", output[i]);
    printf("\n");     printf("Heap Comparisons = %d\n", comparisons); }
int main() {     int lists[K][SIZE] = {         {10, 30, 50, 70},
        {20, 40, 60, 80},
        {15, 35, 55, 75}     };
    printf("====================================\n");     printf(" SORTED TRANSACTION LISTS\n");     printf("====================================\n");
    printf("L1 : 10 30 50 70\n");     printf("L2 : 20 40 60 80\n");     printf("L3 : 15 35 55 75\n");
    kWayMerge(lists);
    return 0;
}
OUTPUT
====================================
 SORTED TRANSACTION LISTS
====================================
L1 : 10 30 50 70
L2 : 20 40 60 80
L3 : 15 35 55 75
====================================
 K-WAY MERGE USING MIN HEAP
====================================
Initial Heap: [ 10 20 15 ]
Step  1 : Deleted 10    Heap = [ 15 20 30 ]
Step  2 : Deleted 15    Heap = [ 20 30 35 ]
Step  3 : Deleted 20    Heap = [ 30 35 40 ]
Step  4 : Deleted 30    Heap = [ 35 40 50 ]
Step  5 : Deleted 35    Heap = [ 40 50 55 ]
Step  6 : Deleted 40    Heap = [ 50 55 60 ]
Step  7 : Deleted 50    Heap = [ 55 60 70 ]
Step  8 : Deleted 55    Heap = [ 60 70 75 ]
Step  9 : Deleted 60    Heap = [ 70 75 80 ]
Step 10 : Deleted 70    Heap = [ 75 80 ]
Step 11 : Deleted 75    Heap = [ 80 ]
Step 12 : Deleted 80    Heap = [ ]
Final K-Way Output:
10 15 20 30 35 40 50 55 60 70 75 80
Heap Comparisons = 18




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
| **Min Heap K-Way Merge** | K | O(N log K) | O(K) |
| **Pairwise Merging** | None (0) | O(N * K) | O(N) |
