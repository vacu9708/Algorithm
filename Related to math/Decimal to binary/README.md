# Decimal number to binary

## How it works
![image](https://user-images.githubusercontent.com/67142421/149515479-f171e1a1-fa84-42bf-b752-562597df22e6.png)


~~~c++
#include <iostream>
#include <string>
using namespace std;

void decimal_number_to_binary1(int decimal_number) { // // Using a string. The simplest
    string binary = "";
    int a_digit = 0, how_many_one = 0;
    while (decimal_number > 0) {
        a_digit = decimal_number % 2;
        binary = to_string(a_digit) + binary;
        decimal_number /= 2;

        if (a_digit == 1) // Counting the number of 1
            how_many_one++;
    }

    cout << "Binary : " << binary << "\n";
    printf("Count : %d\n", how_many_one);
}

void decimal_number_to_binary2(int decimal_number) { // Using an int variable to store the binary
    char a_digit;
    long long int coefficient = 1, binary = 0;
    int how_many_one = 0;
    while (decimal_number > 0) {
        a_digit = decimal_number % 2;
        binary += a_digit * coefficient;
        decimal_number >>= 1; // One bit shift to the right is equal to dividing with 2
        coefficient *= 10;

        if (a_digit == 1) // Counting the number of 1
            how_many_one++;
    }

    printf("Binary : %d\n", binary);
    printf("Count : %d\n", how_many_one);
}

void decimal_number_to_binary3(int decimal_number) { // Using a char array to store binary(string of C language style)
    char a_digit;
    long long int index = 0;
    char binary[111] = "";
    int how_many_one = 0;
    while (decimal_number > 0) {
        a_digit = decimal_number % 2;
        binary[index] = a_digit + '0'; //int to ASCII
        decimal_number >>= 1; // One bit shift to the right is equal to dividing with 2
        index++;

        if (a_digit == 1) // Counting the number of 1
            how_many_one += 1;
    }

    printf("Binary : ");
    for (int i = index - 1; i >= 0; i--) //Print from the last index of the array
        printf("%c", binary[i]);
    printf("\nCount : %d\n", how_many_one);
}

void decimal_fraction_to_binary1(double decimal_fraction) { // Decimal fraction to binary
    string binary = "0.";
    while (decimal_fraction > 0) {
        decimal_fraction *= 2;
        binary += to_string((int)decimal_fraction--);
    }

    cout << "Binary : " << binary << "\n";
}

/* This doesn't work because the calculation of decimal fraction of computers is inaccurate
void decimal_fraction_to_binary2(double decimal_fraction) {
    double i = 0.1;
    double binary = 0;
    while (decimal_fraction > 0) {
        decimal_fraction *= 2;
        if (decimal_fraction >= 1) {
            binary += i;
            decimal_fraction--;
        }
        i *= 0.1;
    }
    cout << binary << "\n";
}*/

int main() {
    cout.precision(33);
    int decimal_number = 123;
    printf("Decimal number : %d >>\n", decimal_number);
    decimal_number_to_binary1(123);
    decimal_number_to_binary2(123);
    decimal_number_to_binary3(123);

    double decimal_fraction = 0.875;
    printf("\nDecimal fraction : %lf >> ", decimal_fraction);
    decimal_fraction_to_binary1(decimal_fraction);
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149196508-d6d725fe-ee60-488e-afac-5b66357785f3.png)
