# Merge sort
>Merge sort is a comparison-based sorting algorithm that takes **O(nlogn)** time which is one of the most efficient sorting algorithms. It is one of *Divide and conquer algorithms*.<br>

![image](https://user-images.githubusercontent.com/67142421/149567895-7ef189fb-abcd-4430-bf6a-5cef1dd9ea8f.png)

## Characteristics
* Merge sort is a stable sort, which means that the order of equal elements is maintained
* Its speed is not influenced by how elements are arranged before sorting, in other words, in all cases the time complexity is **O(nlogn)**
>Due to these strengths, merge sort runs stably in any situation.

## Time complexity
![image](https://user-images.githubusercontent.com/67142421/234135296-56675120-907a-431b-93ae-b7dfc1cc95f2.png)

>In each recursive iteration, the number of elements decreases to half. If the last level of the recursion tree is is log(N) as written in [Binary search](https://github.com/vacu9708/Algorithm/tree/main/Searching%20algorithm/Binary%20search).<br>
>The last level of the tree is reached N times. Therefore, the time complexity of merge sort is **O(NlogN)**

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

void merge_sort(vector<int>& list, vector<int>& temp, int left, int right) {
	if (left == right)
		return;

	int mid = (left + right) / 2;
	merge_sort(list, temp, left, mid);
	merge_sort(list, temp, mid + 1, right);

	int i = left, j = mid + 1, temp_i = left; // i : pointer in 1st half / j : pointer in 2nd half
	// While i is within 1st half and j within 2nd half
	while (i <= mid && j <= right) {
		if (list[i] < list[j])
			temp[temp_i++] = list[i++];
		else
			temp[temp_i++] = list[j++];
	}
	// Copy the remaining elements into temp
	while (i <= mid) 
		temp[temp_i++] = list[i++];
	while (j <= right)
		temp[temp_i++] = list[j++];
	// Copy temp list to original list(Merge)
	for (int i = left; i <= right; i++)
		list[i] = temp[i];

	// Show the process
	//if (right - left == list.size() - 1) // The last procedure
		//printf("-----Merge!\n");
}

int main(void) {
	vector<int> list = { 8,7,6,5,4,3,2,1 };
	vector<int> temp(list.size()); // Essential for merge sort
	printf("Elements to sort : "); print_elements(list);
	merge_sort(list, temp, 0, list.size() - 1);
	print_elements(list);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149567500-2f875e4e-c74e-4f25-b498-3ec84f0937b2.png)
