# Insertion sort
>A **stable** sorting algorithm to the extent of being used as part of other sorting algorithms because in the best case, it is very fast with the time complexity **O(n)**.

## Time complexity
- **Best case**
  >Elements that are already sorted (1 2 3 4 5)
  >Only the outer loop is carried out (n-1) times.
  > ### -> O(n)
- **Worst case**
  >Elements that are not sorted at all : (5 4 3 2 1)
  >
  >2 + 3 + 4 + ... + N-1 + N = ![image](https://user-images.githubusercontent.com/67142421/149545993-042d9d32-351e-4220-99a2-2ea2d31a8d04.png) 
  >### -> O(n^2)


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
