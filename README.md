// sorting-visualizer
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define SIZE 10 // Change SIZE for larger arrays

// Function to print the array (used for visualization)
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Forward declaration of partition function
int partition(int arr[], int low, int high);

// Quick Sort Algorithm
void quickSort(int arr[], int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high); 
        // Recursively sorting the two sub-arrays
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Partition function that selects a pivot and arranges elements
// so that all elements smaller than the pivot are on the left,
// and all elements greater than the pivot are on the right.
int partition(int arr[], int low, int high) {
    int pivot = arr[high];  // Choosing the last element as the pivot
    int i = low - 1;        // Index for the smaller element
  // Loop through the array, moving smaller elements to the left
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++; // Increment the index of smaller element
            // Swap arr[i] and arr[j]
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }

   // Swap the pivot element with the element at i+1
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;

   // Print the array after each partition operation (for visualization)
    printf("Array after partitioning with pivot %d:\n", pivot);
    printArray(arr, SIZE);

   return i + 1; // Return the partition index
}

// Function to generate random numbers
void generateRandomArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] = rand() % 100 + 1; // Random numbers between 1 and 100
    }
}

int main() {
    srand(time(NULL)); // Seed the random number generator
    int arr[SIZE];

   // Generate a random array of integers
    generateRandomArray(arr, SIZE);

   printf("Original Array:\n");
    printArray(arr, SIZE);

   // Call Quick Sort
    printf("\nSorting Process using Quick Sort:\n");
    quickSort(arr, 0, SIZE - 1);

  printf("\nSorted Array:\n");
    printArray(arr, SIZE);

   return 0;
}

