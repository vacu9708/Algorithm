**The Longest Increasing Subsequence (LIS)** problem is to find the length of the longest subsequence of a given sequence such that all elements of the subsequence are sorted in increasing order. For example, the length of LIS for {10, 22, 9, 33, 21, 50, 41, 60, 80} is 6 and LIS is {10, 22, 33, 50, 60, 80}. 

~~~c++
#include <iostream>
#include <vector>
using namespace std;

void print_list(vector<int> arr) {
	for (int i = 0; i < arr.size(); i++)
		cout << arr[i] << ' ';
}

int lis(vector<int> arr, int n)
{
	vector<int> memo(n); // Longest lengths of subsequences
	memo[0] = 1;

	for (int i = 1; i < n; i++) { // Last index of subsequences
		memo[i] = 1; // Initialize the length of a subsequence
		for (int j = 0; j < i; j++)
			if (arr[i] > arr[j] && memo[j] + 1 > memo[i]) { // Increasing && adding the [j] subsequence makes the current subsequence longer
				printf("i: %d j: %d / ", i, j); print_list(memo); printf(" -> "); // To see the process
				memo[i] = memo[j] + 1;
				print_list(memo); printf("\n"); // To see the process
			}
	}

	// Return the length of LIS
	int max_i = 0;
	for(int i=1; i<n; i++){
		if (memo[i] > memo[max_i])
			max_i = i;
	}
	return memo[max_i];
}

int main() // test code
{
	vector<int> arr = { 10,20,10,30,20,50 };
	int n = arr.size();
	printf("Length of LIS is %d\n", lis(arr, n));

	return 0;
}
~~~
