# Bubble sort
Bubble sort is simple to implement but is the slowest of other sorting algorithms

## Time complexity
> N = the number of elements to sort.
> In the first iteration of the first loop, N-1 of comparison is conducted >> In the 2nd iteration, N-2 >> N-3 ... 2 ... 1
> (N-1)+(N-2)+(N-3)+...+2+1 >> By the sum of arithmetical series : ![image](https://user-images.githubusercontent.com/67142421/149508649-d1d4efed-9e65-4b85-bff7-7a851a2dadff.png)
> 
> Time complexity : **O(n^2)**

## Working process
![image](https://user-images.githubusercontent.com/67142421/149490296-a057ecca-c8ec-44c6-b3fc-603a0dcd7031.png)

~~~c++
#include <iostream>
using namespace std;

int arr[] = { 5,4,3,2,1 };
int length = sizeof(arr) / sizeof(int);

void print_array() {
	for (int i = 0; i < length; i++)
		cout << arr[i] << " ";
	cout << "\n";
}

void swap(int* first, int* second) {
	int temp = *first;
	*first = *second;
	*second = temp;
}

void bubble_sort() {
	int tmp = 0;
	for (int i = 1; i < length; i++) { // Stack numbers from the far right in ascending order
		print_array(); // Show the process
		for (int j = 0; j < length - i; j++) {
			if (arr[j] > arr[j + 1])
				swap(arr[j], arr[j + 1]);
		}
	}
	printf("Sorted array : "); print_array(); // Show the result
}

void main() {
	bubble_sort();
}
~~~

## Compile and run
Sort 5 4 3 2 1
![Untitled](https://user-images.githubusercontent.com/67142421/149509160-b5323404-3059-4bc6-8535-d1da481906ac.png)
