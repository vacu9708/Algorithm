~~~c++
#include <iostream>
#include <vector>
using namespace std;

void print_array(vector<int> arr) {
	for (int i = 0; i < arr.size(); i++)
		cout << arr[i] << ' ';
}

int lis(vector<int> arr, int n)
{
	vector<int> memo(n); // Longest lengths of subsequences
	memo[0] = 1;

	for (int i = 1; i < n; i++) { // Last index of subsequences
		memo[i] = 1; // Initialize the length of subsequence
		for (int j = 0; j < i; j++)
			if (arr[i] > arr[j] && memo[i] < memo[j] + 1) {
				printf("i: %d j: %d / ", i, j); print_array(memo); printf(" -> ");
				memo[i] = memo[j] + 1;
				print_array(memo); printf("\n");
			}
	}

	// Return maximum value in memo[]
	int max_i = 0;
	for(int i=1; i<n; i++){
		if (memo[i] > memo[max_i])
			max_i = i;
	}
	return memo[max_i];
}

/* Driver program to test above function */
int main()
{
	vector<int> arr = { 10,20,10,30,20,50 };
	int n = arr.size();
	printf("Length of lis is %d\n", lis(arr, n));

	return 0;
}
~~~
