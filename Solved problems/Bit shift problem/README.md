# Bit shift
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

