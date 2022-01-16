# Checking if two strings are anagrams

~~~c++
#include <iostream>
#include <string>
using namespace std;

void is_anagram(string s1, string s2)
{
	bool done[111] = { 0, }; //To check if a letter has already been done
	if (s1.length() != s2.length()) {
		cout << "Result : not anagram(different length)";
		return;
	}

	for (int i = 0; i < s1.length(); i++)
		for (int j = 0; j < s2.length(); j++) {
			if (done[j] == 1) // Skip if the letter's already done
				continue;
			if (s1[i] == s2[j]) { // Was the same letter found?
				done[j] = 1;
				break;
			}
			if (j >= s2.length() - 1) { // If it's the final index when both letters are diferent
				cout << "Result : not anagram ";
				return;
			}
		}
	cout << "Result : They are anagrams";
}

int main() {
	string s1, s2;
	cout << "first word : ";
	cin >> s1;
	cout << "second word : ";
	cin >> s2;
	is_anagram(s1, s2);
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/149676597-2b8f3d83-602c-46ee-a141-4ba5953e79e7.png)

![image](https://user-images.githubusercontent.com/67142421/149676623-db1474b1-7616-4850-a829-fa24ab360c73.png)

![image](https://user-images.githubusercontent.com/67142421/149676635-26d8762b-ca47-4100-86a0-9992cb6cacca.png)

