# Permutation and combination

~~~c++
#include <iostream>
using namespace std;

char set[] = { 'a','b','c','d' };
int r = 3; // the number of elements to arrange
 
class Permutation_without_repetition {
	char* a_case = new char[r];
	int n_of_cases = 0; // number of cases
	bool visited[4];
public:
	Permutation_without_repetition() {
		DFS(0);
		delete[] a_case;
		printf("\n");
	}

	void DFS(int level) {
		if (level == r) {
			n_of_cases++;
			for (int i = 0; i < r; i++)
				printf("%c ", *(a_case + i));
			printf("/ Number of cases : %d\n", n_of_cases);
			return;
		}

		for (int i = 0; i < sizeof(set); i++)
			if (!visited[i]) {
				visited[i] = true;
				a_case[level] = set[i];
				DFS(level + 1);
				visited[i] = false;
			}
	}
};

class Permutation_with_repetition {
	int n_of_cases = 0;
	char* a_case = new char[r];
public:
	Permutation_with_repetition() {
		DFS(0);
		delete[] a_case;
		printf("\n");
	}

	void DFS(int level) {
		if (level == r) {
			n_of_cases++;
			for (int i = 0; i < r; i++)
				printf("%c ", *(a_case + i));
			printf("/ Number of cases : %d\n", n_of_cases);
			return;
		}

		for (int i = 0; i < sizeof(set); i++) {
			a_case[level] = set[i];
			DFS(level + 1);
		}
	}
};

class Combination_without_repetition {
	int n_of_cases = 0;
	char* a_case = new char[r];
public:
	Combination_without_repetition() {
		DFS(0, 0);
		delete[] a_case;
		printf("\n");
	}

	void DFS(int level, int start_index) {
		if (level == r) {
			n_of_cases++;
			for (int i = 0; i < r; i++)
				printf("%c ", *(a_case + i));
			printf("/ Number of cases : %d\n", n_of_cases);
			return;
		}

		for (int i = start_index; i < sizeof(set); i++) {
			a_case[level] = set[i];
			DFS(level + 1, i + 1);
		}
	}
};


class Combination_with_repetition {
	int n_of_cases = 0;
	char* a_case = new char[r];
public:
	Combination_with_repetition() {
		DFS(0, 0);
		delete[] a_case;
		printf("\n");
	}

	void DFS(int level, int start_index) {
		if (level == r) {
			n_of_cases++;
			for (int i = 0; i < r; i++)
				printf("%c ", *(a_case + 1));
			printf("/ Number of cases : %d\n", n_of_cases);
			return;
		}

		for (int i = start_index; i < sizeof(set); i++) {
			a_case[level] = set[i];
			DFS(level + 1, i);
		}
	}
};

/* A list can be used to print cases like this instead of an array.
class Combination_without_repetition {
	int n_of_cases = 0;
	list<char> a_case;
public:
	Combination_without_repetition() {
		DFS(0, 0);
		printf("\n");
	}

	void DFS(int level, int start_index) {
		if (level == r) {
			n_of_cases++;
			for (auto i = a_case.begin(); i != a_case.end(); i++)
				printf("%c ", *i);
			printf("/ Number of cases : %d\n", n_of_cases);
			return;
		}

		for (int i = start_index; i < sizeof(set); i++) {
			a_case.push_back(set[i]);
			DFS(level + 1, i + 1);
			a_case.pop_back();
		}
	}
};*/

int main() {
	printf("-----Permutation_without_repetition\n");
	Permutation_without_repetition a;
	printf("-----Permutation_with_repetition\n");
	Permutation_with_repetition b;
	printf("-----Combination_without_repetition\n");
	Combination_without_repetition c;
	printf("-----Combination_with_repetition\n");
	Combination_with_repetition d;
}
~~~

## Output (Arranging a set {a, b, c, d} when r = 3)

![Untitled](https://user-images.githubusercontent.com/67142421/149171691-ab7b9964-9d40-452f-8b23-a05a0bddf0ac.png)

![Untitled](https://user-images.githubusercontent.com/67142421/149171860-5d313925-2cc4-4238-b230-203a09e0dfbd.png)

![Untitled](https://user-images.githubusercontent.com/67142421/149171934-93f9e640-2411-4c44-a7c4-696a14820acc.png)

