# Selection sort
>**Unstable** sorting algorithm. It is faster than bubble sort and simple to implement.

## Working process
1. Look for the minimum
2. Place the found minimum from the far left to the right.

## Time complexity (N : the number of elements)
> (N-1) + (N-2) + (N-3) + ... + 1 -> the sum of arithmetic series : [(N-1){2(N-1) + (N-1-1) * -1}] / 2 => **O(n^2)**

~~~c++
#include <iostream>
using namespace std;

void print_array(int* arr, int length) {
	for (int i = 0; i < length; i++)
		cout << arr[i] << " ";
	cout << "\n";
}

void insertion_sort1(int arr[], int length) { // Using while-loop
	for (int i = 0; i < length - 1; i++) {//Sort the sublists in ascending order
		for (int j = i + 1; j > 0 && arr[j] < arr[j - 1]; j--) {
			swap(arr[j], arr[j - 1]);
			print_array(arr, length); // Show the process
		}
		printf("-----A pass finished\n");
	}
}
void insertion_sort2(int* arr, int length) { // Sort the elements by sorting the sublists in ascending order
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
![Untitled](https://user-images.githubusercontent.com/67142421/149547901-8ea63e8e-81b0-4cda-8e16-53b023ba928a.png)
