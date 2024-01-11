# Insertion sort
![image](https://github.com/vacu9708/Algorithm/assets/67142421/c8505341-4292-4dab-bcc3-96d3d23af9b0)

A **stable** sorting algorithm to the extent of being used as part of other sorting algorithms because in the best case, it is very fast with the time complexity **O(n)**.<br>
It is repeated to sort sublists, and sorted sublists are skipped.<br>

## Time complexity
- **Best case**
  >Elements that are already sorted (1 2 3 4 5)<br>
  >Only the outer loop is carried out (n-1) times.<br>
  > ### -> O(n)
- **Worst case**
  >Elements that are not sorted at all : (5 4 3 2 1)<br>
  >2 + 3 + 4 + ... + N-1 + N = ![image](https://user-images.githubusercontent.com/67142421/149545993-042d9d32-351e-4220-99a2-2ea2d31a8d04.png) 
  >### -> O(n^2)
- **Linked list**: is a data structure where insertion is fast, which means the insertion sort is good for linked lists.

~~~c++
#include <stdio.h>
#include <string.h>

void InsertionSort(int DataSet[], int Length)
{
    int i=0, j=0, value=0;

    for(i=1; i<Length; i++)
    {
	// If this sublist is already sorted
        if(DataSet[i-1] <= DataSet[i])
            continue;
	// Else, insert the value
        value = DataSet[i];
        for(j=0; j<i; j++)
        {
            if(DataSet[j] > value)
            {   // Insertion
                memmove(&DataSet[j+1], &DataSet[j], sizeof(DataSet[0])*(i-j));
                DataSet[j] = value;
                break;
            }
        }
    }
}

int main(void)
{
    int DataSet[] = {6, 4, 2, 3, 1, 5};
    int Length = sizeof DataSet / sizeof DataSet[0];
    int i = 0;

    InsertionSort(DataSet, Length);

    for(i=0; i<Length; i++)
        printf("%d ", DataSet[i]);

    printf("\n");

    return 0;
}
~~~

### Old code
~~~c++
#include <iostream>
using namespace std;

void print_array(int* arr, int length) {
	for (int i = 0; i < length; i++)
		cout << arr[i] << " ";
	cout << "\n";
}

void insertion_sort1(int arr[], int length) { // Using while-loop
	for (int i = 1; i < length; i++) {
		// Sort the sublist in ascending order
		for (int j = i; j > 0 && arr[j-1] > arr[j]; j--) {
			swap(arr[j], arr[j - 1]);
			print_array(arr, length); // Show the process
		}
		printf("-----A pass finished\n");
	}
}
void insertion_sort2(int* arr, int length) {
	int j, key;
	for (int i = 1; i < length; i++) { // i : the index of key
		key = arr[i];
		for (j = i - 1; j >= 0 && arr[j] > key; j--) {// Sort a sublist up to index i. The sublist up to index i - 1 has already been sorted.
			arr[j + 1] = arr[j];
			print_array(arr, length); // Show the process
		}
		arr[j + 1] = key;
		print_array(arr, length); printf("-----A pass finished\n");
	}
}

int main() {
	int arr[] = { 5,4,3,2,1 };
	int length = sizeof(arr) / sizeof(arr[0]);
	printf("Elements to sort : "); print_array(arr, length); printf("\n");
	insertion_sort1(arr, length);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149538271-30537d3e-790f-44d9-bc1a-056e43916857.png)
