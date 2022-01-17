# Adding very large numbers

~~~c++
#include <iostream>
#include <vector>
using namespace std;
#define BUFFER_LENGTH 111

void sum_of_big_numbers(string num1, string num2) {
	// Put numbers into buffers in order to match the digit positions to calculate
	vector<char> buffer1(BUFFER_LENGTH, '0'), buffer2(BUFFER_LENGTH, '0');
	int buffer1_index = BUFFER_LENGTH - 1, buffer2_index = BUFFER_LENGTH - 1;

	int from1 = num1.size() - 1;
	while (from1 >= 0)
		buffer1[buffer1_index--] = num1[from1--];

	int from2 = num2.size() - 1;
	while (from2 >= 0)
		buffer2[buffer2_index--] = num2[from2--];
	//-----
	// Calculate
	int calculation_index = BUFFER_LENGTH - 1, sum_of_a_digit = 0, carry = 0;
	char sum[BUFFER_LENGTH];
	while (calculation_index > buffer1_index || calculation_index > buffer2_index) {
		sum_of_a_digit = ( (buffer1[calculation_index] - '0') + (buffer2[calculation_index] - '0') ) + carry; // minus '0' is equals to atoi()
		sum[calculation_index--] = (sum_of_a_digit % 10) + '0'; // plus '0' is equal to [int to ASCII];
		carry = sum_of_a_digit / 10;
	}
	if (carry != 0) // If there's a remaining carry
		sum[calculation_index--] = carry + '0';
	//-----
	// Print
	cout << num1 << " + " << num2 << " = ";
	for (int i = calculation_index + 1; i < BUFFER_LENGTH; i++)
		printf("%c", sum[i]);
		//cout << sum[i];
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
![image](https://user-images.githubusercontent.com/67142421/149729919-343de98f-1b4f-44dc-966c-3d3b60cdcdea.png)
