# Heap sort
>Heapsort is a comparison-based sorting algorithm using the characteristic of *Heap* that the first elemenet is the biggest or smallest. Heapsort can be thought of as an improved selection sort in that maxima or minima are looked for and then they are moved like in selection sort.

## Process (ascending order)
> 1. Max heapify
> 2. Move the root which is the biggest value to the far right except sorted elements in ascending order
> 3. Repeat this process

## Features
- Unstable like selection sort
- Theoretically the best but in reality not that good because it is not cache-friendly

## Time complexity
* Let the number of elements be N
* Heapifying : log(N)<br>
>N times of heapifying are needed in each swap<br>
>log(N) + log(N-1) + log(N-2) + ... = **O(NlogN)**

~~~c++
#include <iostream>
#include <vector>
using namespace std;

void print_elements(vector<int>& heap_tree) {
	int tree_size = heap_tree.size();
	for (int i = 0; i < tree_size; i++)
		cout << heap_tree[i] << " ";
	cout << "\n";
}

void heapify(vector<int>& heap_tree, int parent_index, int heapify_upto) {
	int tree_size = heap_tree.size();
	int left_child = 2 * parent_index + 1, right_child = 2 * parent_index + 2;

	if (left_child <= heapify_upto && heap_tree[left_child] > heap_tree[parent_index]) {
		heapify(heap_tree, left_child, heapify_upto);
		swap(heap_tree[parent_index], heap_tree[left_child]);
	}
	if (right_child <= heapify_upto && heap_tree[right_child] > heap_tree[parent_index]) {
		heapify(heap_tree, right_child, heapify_upto);
		swap(heap_tree[parent_index], heap_tree[right_child]);
	}
}

void heap_sort(vector<int>& heap_tree) {
	int tree_size = heap_tree.size();
	printf("---Heapify\n");
	// Heapify from the last parent ( (child+1) / 2 - 1 is its parent)
	for (int i = 0; i <= tree_size / 2 - 1; i++) {
		heapify(heap_tree, i, tree_size - 1);
		print_elements(heap_tree); // Show the process
	}
	cout << "-----\n\n";
	//-----
	for (int i = tree_size - 1; i > 0; i--) {
		cout << "---Swap the root with index (" << i << ")\n"; // Show the process
		swap(heap_tree[0], heap_tree[i]); // Move the root which is the biggest value except sorted elements to the right in ascending order
		print_elements(heap_tree);

		printf("---Heapify up to index (%d)\n", i - 1); // Show the process
		heapify(heap_tree, 0, i - 1);
		print_elements(heap_tree);
	}
}

int main() {
	vector<int> heap_tree = { 3,1,5,4,2 };
	printf("Elements to sort: "); print_elements(heap_tree);

	heap_sort(heap_tree);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149524068-2f7a71f0-cdd4-49ff-8df2-255f4359818a.png)
