# Calculating a remainder
~~~c++
#include <stdio.h>

int mod(int numerator, int denominator) {
	int quotient = 0;

	while (1) {
		quotient++;
		if (denominator * quotient > numerator) {
			quotient--;
			return numerator - denominator * quotient; // remainder
		}
	}
}

int mod2(int numerator, int denominator) { // Only with addition
	int denominator_times_quotient = 0;

	while (1) {
		denominator_times_quotient += denominator;
		if (denominator_times_quotient > numerator) {
			denominator_times_quotient -= denominator;
			return numerator - denominator_times_quotient; // remainder
		}
	}
}


int main() {
	int numerator = 7, denominator = 4;
	printf("%d mod %d : \n", numerator, denominator);
	printf("Remainder : %d\n", mod(numerator, denominator));
	printf("Remainder : %d\n", mod2(numerator, denominator));
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149187384-65bb2fe7-7c5a-43e7-922d-0f9cd0736383.png)
