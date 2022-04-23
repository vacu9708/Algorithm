# split()

~~~C++
#include <iostream>
#include <list>
using namespace std;

void split(string str, char delimiter, list<string>& container) {
	int start = 0, length = str.length();
	for (int i = 0; i < length; i++)
		if (str[i] == delimiter) { // If the delimiter was found, put the word into list.
			container.push_back(str.substr(start, i - start));
			start = i + 1; // To find the next word
		}

	container.push_back(str.substr(start, length - start)); // Last element
}

int main() {
	list<string> container;
	string str = "apple/grape/strawberry";
	cout << "Split (" << str << ")\n";
	split("apple/grape/strawberry", '/', container);
	for (auto i = container.begin(); i != container.end(); i++)
		cout << *i << "\n";
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/148947913-09404c57-432f-4dec-8dcf-d7a2faa47e4b.png)
