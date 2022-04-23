# Basic string functions

~~~C++
#include <iostream>

void my_scanf(char* container)
{
	printf("Put a string : ");
	char character;
	unsigned int index = 0;
	char* str = new char[1], * new_str = NULL;

	while (1) {
		character = getchar();

		if (character == '\n') { // Finish if a new line was begun
			str[index] = '\0'; // End of string
			
			for (int i = 0; i <= index; i++) // Put the entered string into the container
				*(container + i) = *(str + i);

			delete[] str;
			return;
		}

		str[index] = character;

		// Reallocation for the next character
		new_str = new char[index + 2];
		for (int i = 0; i <= index; i++)
			*(new_str + i) = *(str + i);
		delete[] str;
		str = new_str;
		//-----
		index++;
	}
}

int length(char* string) { // Function to measure the length of a string
	unsigned int length = 0;
	while (1)
		if (string[length] == '\0')
			break;
		else
			length++;

	return length;
}

void copy(char* from, char to[]) { // Function to copy a string
	int i = 0;
	while (1) {
		to[i] = from[i];

		if (to[i] == '\0')
			return;

		i++;
	}
}

int main() {
	char container[111];
	my_scanf(container);
	printf("Entered string : %s\n", container);
	printf("Length : %d\n", length(container));
	char to[111];
	copy(container, to);
	printf("Copied string : %s\n", to);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/148942870-01a381e0-235d-4402-a2c1-e876ec54c69b.png)
