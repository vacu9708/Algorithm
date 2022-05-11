# Adding very large numbers
>Very large numbers can't be calculated in a normal way because the size of regular variable types is limited.
>They can be calculated by using string containers.

~~~c++
#include <iostream>
#include <vector>
using namespace std;
#define BUFFER_LENGTH 111

void sum_of_big_numbers(string num1, string num2) {
	// Put numbers into buffers in order to match the digit positions to calculate
	vector<char> buffer1(BUFFER_LENGTH, '0'), buffer2(BUFFER_LENGTH, '0');
	int buffer1_index = BUFFER_LENGTH - 1, buffer2_index = BUFFER_LENGTH - 1;

	int num1_i = num1.size() - 1;
	while (from1 >= 0)
		buffer1[buffer1_index--] = num1[num1_i--];

	int num2_i = num2.size() - 1;
	while (from2 >= 0)
		buffer2[buffer2_index--] = num2[num2_i--];
	//-----
	// Calculate
	int calculation_index = BUFFER_LENGTH - 1, sum_of_a_digit = 0, carry = 0;
	char sum[BUFFER_LENGTH];
	while (calculation_index > buffer1_index || calculation_index > buffer2_index) {
		sum_of_a_digit = ((buffer1[calculation_index] - '0') + (buffer2[calculation_index] - '0')) + carry; // minus '0' is equals to atoi()
		sum[calculation_index--] = (sum_of_a_digit % 10) + '0'; // plus '0' is equal to [int to ASCII];
		carry = sum_of_a_digit / 10;
	}
	if (carry != 0) // If there's a remaining carry, add it
		sum[calculation_index--] = carry + '0';
	//-----
	// Print
	printf("=\n");
	for (int i = calculation_index + 1; i < BUFFER_LENGTH; i++)
		printf("%c", sum[i]);
	//-----
//-----
}

int main() {
	string a, b;
	printf("Enter 2 numbers : \n");
	cin >> a;
	cout << "+\n";
	cin >> b;
	sum_of_big_numbers(a, b);
	cout << "\n";
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/149763064-7455699b-7041-4b56-ba9a-5c40d11bf880.png)
