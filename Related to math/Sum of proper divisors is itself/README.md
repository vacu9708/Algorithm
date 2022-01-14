# Find how many numbers in a certain range have the sum of their proper divisors as itself

~~~C++
#include <iostream>
using namespace std;

void sum_of_proper_divisors_is_itself(int range) {
	int count = 0, sum_of_divisors = 0;
	for (int i = 4; i <= range; i++) {
		sum_of_divisors = 0;
		// First, find the sum of divisors.
		for (int j = 1; j <= i / 2; j++) { // j : divisors
			if (i % j == 0) // It means j is a divisor of i if the remainder is 0.
				sum_of_divisors += j;
		}
		//-----
		if (sum_of_divisors == i) { // If the sum of the divisors is itself, it's included in the answer.
			cout << i << " ";
			count++;
		}
	}
	cout << "\nTotal number : " << count; // The total number of numbers that have the sum of their proper divisors as itself
}

int main() {
	int range = 1000;
	printf("Answer up to (%d) : ", range);
	sum_of_proper_divisors_is_itself(range);
~~~
# Output
![Untitled](https://user-images.githubusercontent.com/67142421/148955468-7b492554-257a-457a-b61d-66da983480c4.png)
