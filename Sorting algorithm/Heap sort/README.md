# Heap sort
>Heapsort is a comparison-based sorting algorithm using the characteristic of *Heap* that the first elemenet is the biggest or smallest. Heapsort can be thought of as an improved selection sort in that maxima or minima are looked for and then they are moved like in selection sort.

## Process (ascending order)
> 1. Max heapify
> 2. Move the 1st element which is the biggest value to the far right except already-done elements

## Features
- **Unstable** like selection sort
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

void print(vector<int>& heap_tree) {
	int tree_size = heap_tree.size();
	for (int i = 0; i < tree_size; i++)
		cout << heap_tree[i] << " ";
	cout << "\n";
}

void max_heapify(vector<int>& heap_tree, int curr, int upto) {
    int left = curr*2+1, right = curr*2+2; // children
    int biggest = curr;
    // If child is larger than parent, swap parent and child
    if (left <= upto && heap_tree[left] > heap_tree[biggest])
        biggest=left;
    if (right <= upto && heap_tree[right] > heap_tree[biggest])
        biggest=right;
    if (biggest != curr) {
        swap(heap_tree[biggest], heap_tree[curr]);
        max_heapify(heap_tree, biggest, upto);
    }
}

void heapify_all(vector<int>& heap_tree){
    for (int i = (heap_tree.size()-2)/2; i >= 0; i--) // from last child's parent
        max_heapify(heap_tree, i, heap_tree.size()-1);
}


void heap_sort(vector<int>& heap_tree) {
	// Heapify from the last parent
	for (int i = heap_tree.size() - 1; i > 0; i--) {
		swap(heap_tree[0], heap_tree[i]); // Move the biggest to the right
		printf("---Swap the root with index (%d)\n", i); print(heap_tree);
		max_heapify(heap_tree, 0, i - 1);
		printf("---Heapify up to index (%d)\n", i - 1); print(heap_tree);
	}
}

int main() {
	vector<int> heap_tree = { 3,1,5,4,2 };
	printf("Elements to sort: "); print(heap_tree);
	heapify_all(heap_tree);
    	printf("Heap tree: "); print(heap_tree);
	heap_sort(heap_tree);
}
~~~

## Output
![image](https://github.com/vacu9708/Algorithm/assets/67142421/1acb38bc-3ec3-4ba8-95b7-f5d5711c3e46)
