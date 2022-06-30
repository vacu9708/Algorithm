# Basics of bit manipulation
* **Changing i'th bit to 1** : use OR.<br>
Ex) 10101 | 1 << 3 makes 11101 because 1 << 3 is 1000.
* **Changing i'th bit to 0** : use AND and NOT.<br>
Ex) 11101 & ~1 << 3 makes 10101 because ~1 << 3 10111, so it becomes 11101 & 10111.
* **Getting i'th bit** : use AND.<br>
Ex) 3rd bit of 10101 = 10101 & (1 << 3) = 10101 & 01000 → 0<br>
Ex) 4th bit of 10101 10101 & (1 << 4) = 10101 & 10000 → 10000

# Bit manipulation problem
>Write a program that gets 4 inputs of characters and stores them in an unsigned int type variable.<br>
>The first character is stored from bit 0 to bit 7. The second character is stored from bit 8 to bit 15.<br>
>The third character is stored from bit 16 to bit 23. The fourth character is stored from bit 24 to bit 31.<br>
>Print the result as a hexadecimal number.<br>

~~~c++
#include<iostream>
using namespace std;

void foo() {
	unsigned int storage = 0;
	char a, b, c, d;
	//scanf("%c %c %c %c",&a[0],&a[1*4],&a[2*4],&a[3*4]);

	cout << "First character : ";
	cin >> a;
	cout << "Second character : ";
	cin >> b;
	cout << "Third character : ";
	cin >> c;
	cout << "Fourth character : ";
	cin >> d;

	storage |= a;
	storage |= b << 8;
	storage |= c << 8 * 2;
	storage |= d << 8 * 3;
	printf("%X", storage);
	//cout << hex; cout << storage;
}


int main(void) {
	foo();
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149675756-b483945d-a1af-4bff-bd24-312a7a9ba425.png)

