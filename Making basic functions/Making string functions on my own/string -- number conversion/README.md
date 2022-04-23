# String <-> number conversion

## C++ style

~~~C++
#include <iostream>
using namespace std;

string my_to_string(int number) {
	string num_string = "";
	char a_digit = 0;
	while (number > 0) {
		a_digit = (number % 10) + '0'; // Getting the first digit
		num_string = a_digit + num_string;
		number /= 10; // Get rid of the first digit
	}
	return num_string;
}

int string_to_int(string str) {
	int end_of_string = str.length() - 1, coefficient = 1, container = 0;
	for (int i = end_of_string; i >= 0; i--) {
		container += (str[i] - '0') * coefficient;
		coefficient *= 10;
	}
	return container;
}

int main() {
	cout << my_to_string(12345) << "\n";
	cout << string_to_int("12345");
}
~~~



## C language style

~~~C++
#include <iostream>
using namespace std;

char container[1111] = "";

void my_to_string(int number, int length) {
	string num_string = "";
	char a_digit = 0;
	int index = length - 1;
	while (number > 0) {
		a_digit = (number % 10) + '0';
		container[index--] = a_digit;
		number /= 10;
	}

}

int main() {
	int length = sizeof(container);
	my_to_string(123456789, length);
	for (int i = 0; i < length; i++)
		printf("%c", container[i]);
}
~~~
