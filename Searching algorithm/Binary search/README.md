# Binary search
>Binary search is an efficient algorithm for finding an item from a sorted list of items.<br>
>It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one.

## How it works
![image](https://user-images.githubusercontent.com/67142421/149464404-17ab5222-a2bd-4f2a-9d0f-5ddf522979bc.png)


## Calculating the time complexity of Binary search
![KakaoTalk_20220114_155140537](https://user-images.githubusercontent.com/67142421/149464207-65f6178f-91bc-4c5a-9982-4d3da5a8ddd1.jpg)

~~~c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

string binary_search(vector<int>& vector, int target) {
	int left = 0, right = vector.size() - 1;
	while (left <= right) {
		int mid = (left + right) / 2;
		if (target == vector[mid])
			return "At index (" + to_string(mid) + ") found";
		else if (target < vector[mid])
			right = mid - 1;
		else if (target > vector[mid])
			left = mid + 1;
	}
	return "Not found";
}

void insert_in_order(vector<int>& vector, int data) {
	if (vector.empty())
		vector.push_back(data);
	else {
		int i = 0, vector_size = vector.size();
		// Look for the location to insert
		for (i = 0; i < vector_size; i++)
			if (data < vector[i])
				break;
		//-----
		vector.insert(vector.begin() + i, data);
	}
}

void print_vector(vector<int>& vector) {
	for (auto i : vector)
		cout << i << " ";
	cout << endl;
}

int main() {
	vector<int> vector = { 1,3,5,7 };
	print_vector(vector);
	cout << "Search (2) -> " << binary_search(vector, 2) << endl;
	cout << "Insert (2) -> "; insert_in_order(vector, 2);
	print_vector(vector);
	cout << "Search (2) -> " << binary_search(vector, 2) << endl;
	cout << "Erase at index (2) -> "; vector.erase(vector.begin() + 2);
	print_vector(vector);
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149461539-54a393b2-eb89-4fd0-9bd2-2e84cbb2e145.png)
