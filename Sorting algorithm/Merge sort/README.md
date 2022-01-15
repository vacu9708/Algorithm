# Merge sort
>Merge sort is a comparison-based sorting algorithm which is one of the most efficient sorting algorithms. It is one of *Divide and conquer algorithms*.<br>

![image](https://user-images.githubusercontent.com/67142421/149567895-7ef189fb-abcd-4430-bf6a-5cef1dd9ea8f.png)

## Characteristics
* Merge sort is a stable sort, which means that the order of equal elements is maintain their original positions in the input and output.
* Its speed is not influenced by how elements are arranged before sorting, in other words, in all cases the time complexity is **O(nlogn)**
>Because of these strengths, merge sort runs stably in any situation.

## Time complexity
![image](https://user-images.githubusercontent.com/67142421/149573847-f3907973-8d7b-473f-aa43-cdc9507d4838.png)

>The way of calculating the time complexity of Merge sort is derives from the principle of calculating that of Binary search.<br>
>In each recursive iteration, the number of elements decreases to half. If the last level of the recursion tree is L, the total number of trials is cn * (L+1)<br>
>As written in [my binary search page](https://github.com/vacu9708/Algorithm/tree/main/Searching%20algorithm/Binary%20search), L is log(N). 
>Therefore, the time complexity of merge sort is **O(nlogn)**

~~~c++
#include <iostream>
#include <vector>
using namespace std;

void print_elements(vector<int>& list) {
	int list_size = list.size();
	for (int i = 0; i < list_size; i++)
		cout << list[i] << " ";
	printf("\n");
}

void sort(vector<int>& list, vector<int>& temp, int left, int mid, int right) { // Sort elements in ascending order
	// First half and second half have already been sorted.
	int i = left, j = mid + 1, temp_index = left; // i : index in 1st half / j : index in 2nd half
	while (i <= mid && j <= right) { // While i and j are within 1st half and 2nd half each
		if (list[i] < list[j])
			temp[temp_index++] = list[i++];
		else if (list[j] < list[i])
			temp[temp_index++] = list[j++];
	}
	// Pick up the remaining elements and put them in temp
	while (i <= mid) // Copy the remaining elements of first half, if there are any
		temp[temp_index++] = list[i++];
	while (j <= right) // Copy the remaining elements of second half, if there are any
		temp[temp_index++] = list[j++];
	//-----
	for (int i = left; i <= right; i++) // Copy temp list to original list
		list[i] = temp[i];

	// Show the process
	if (right - left == list.size() - 1) // The last procedure
		printf("-----Merge!\n");
	print_elements(list);
	//-----
}

void merge_sort(vector<int>& list, vector<int>& temp, int left, int right) {
	if (left == right) // Termination condition(base case) of recursion
		return;

	int mid = (left + right) / 2;
	merge_sort(list, temp, left, mid);
	merge_sort(list, temp, mid + 1, right);
	sort(list, temp, left, mid, right);
}

int main(void) {
	vector<int> list = { 8,7,6,5,4,3,2,1 };
	vector<int> temp(list.size()); // Essential for merge sort
	printf("Elements to sort : "); print_elements(list);
	merge_sort(list, temp, 0, list.size() - 1);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149567500-2f875e4e-c74e-4f25-b498-3ec84f0937b2.png)
