**The Longest Increasing Subsequence (LIS)** problem is to find the length of the longest subsequence of a given sequence such that all elements of the subsequence are sorted in increasing order. For example, the LIS of {10, 22, 9, 33, 21, 50, 41, 60, 80} is {10, 22, 33, 50, 60, 80} and its length is 6. 

~~~c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

void print_list(vector<int> arr) {
	for (int i = 0; i < arr.size(); i++)
		cout << arr[i] << ' ';
}

int LIS_n_squared(vector<int> arr)
{
	int n = arr.size();
	vector<int> memos(n); // Longest length of subsequences. Each index of memos is the last index of LIS
	memos[0] = 1;

	for (int i = 1; i < n; i++) { // LIS whose last index is i
		memos[i] = 1; // Initialize the length of the LIS
		for (int j = 0; j < i; j++) // Previously found LIS whose last index is j
			if (arr[i] > arr[j] && memos[j] + 1 > memos[i]) { // Increasing sequence && adding the [j] LIS makes the current subsequence longer
				printf("i: %d j: %d / ", i, j); print_list(memos); printf(" -> "); // Show the process
				memos[i] = memos[j] + 1;
				print_list(memos); printf("\n"); // Show the process
			}
	}

	// Return the length of LIS
	int max_i = 0;
	for (int i = 1; i < n; i++) {
		if (memos[i] > memos[max_i])
			max_i = i;
	}
	return memos[max_i];
}

int LIS_nlogn(vector<int> arr) { // Faster using binary search
	int n = arr.size();
	const int INF = 1e3;
	vector<int> memos(n + 1, INF);
	memos[0] = -INF;

	for (int i = 0; i < n; i++) {
		int j = lower_bound(memos.begin(), memos.end(), arr[i]) - memos.begin(); // binary search
		if (memos[j - 1] < arr[i] && arr[i] < memos[j]) { // Increasing sequence && a longer sequence is made
			printf("i: %d j: %d / ", i, j); print_list(memos); printf(" -> "); // Show the process
			memos[j] = arr[i];
			print_list(memos); printf("\n"); // Show the process
		}
	}

	int answer = 0;
	for (int i = 1; i < n; i++) {
		if (memos[i] < INF)
			answer = i;
	}
	return answer;
}

int main() // test code
{
	vector<int> arr = { 10,20,10,30,20,50 };
	int n = arr.size();
	printf("Length of LIS is %d\n\n", LIS_nlogn(arr));
	printf("Length of LIS is %d\n", LIS_n_squared(arr));
	return 0;
}
~~~
## Output
### DP
![image](https://user-images.githubusercontent.com/67142421/176540948-ff1a20de-2d06-41e9-ac4f-bbda6f2e157d.png)

### DP with binary search
![image](https://user-images.githubusercontent.com/67142421/176553448-08e0f20d-4904-4f29-a1a3-e7f30705e82f.png)
