# Slicing

~~~c++
#include <iostream>
#include <vector>
using namespace std;

vector<int> slice(vector<int> list, int start, int end, int jump) {
	int new_list_size = ceil((end - start) / double(jump));
	vector<int> new_list(new_list_size);
	int new_i = 0;
	for (int old_i = start; old_i < end; old_i += jump) {
		new_list[new_i] = list[old_i];
		new_i++;
	}
	return new_list;
}

int main() {
	vector<int> list = { 0,1,2,3,4,5,6 };
	list = slice(list, 1, list.size(), 2);
	for (int i = 0; i < list.size(); i++)
		printf("%d ", list[i]);
}
~~~

## Input
list = {0,1,2,3,4,5,6};<br>
slice(list, 1, list.size(), 2);

## Output
### 1 3 5
