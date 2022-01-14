# Selection sort
Selection sort is a comparison sorting algorithm. It is faster than bubble sort and simple to implement.

## Time complexity (N : the number of elements)
> (N-1) + (N-2) + (N-3) + ... + 1 -> the sum of arithmetic series : [(N-1){2(N-1) + (N-1-1) * -1}] / 2 = **O(n^2)**

~~~c++
#include <iostream>
using namespace std;

void print_array(int* arr, int length) {
	for (int i = 0; i < length; i++)
		cout << arr[i] << " ";
	cout << "\n";
}

void selection_sort(int* arr, int length) {
	for (int i = 0; i < length - 1; i++) {
    // Look for the minimum from index i to the last index
		int min = i;
		for (int j = i + 1; j < length; j++)
			if (arr[j] < arr[min])
				min = j;
		//-----
		swap(arr[i], arr[min]); // Put the minimum in index i
		print_array(arr, length); // Show the process
	}
}

void main() {
	int arr[] = { 5,4,3,2,1 };
	int length = sizeof(arr) / sizeof(int);
	printf("Elements to sort : "); print_array(arr, length);
	selection_sort(arr, length);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149547901-8ea63e8e-81b0-4cda-8e16-53b023ba928a.png)
