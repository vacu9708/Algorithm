# Permutation and combination

>DFS(Depth First Search) is used to find the number of cases.

~~~c++
#include <iostream>
using namespace std;

char set[] = { 'a','b','c','d' };
int r = 3; // the number of elements to arrange

//-----Permutation_without_repetition
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
//-----
//-----Permutation_with_repetition
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
//-----
//-----Combination_without_repetition
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
			
		// If a_case[i] has already been sorted chosen, it cannot be chosen again in the next recursion because
		// cases where only the order is different with the same elements are considered one in combination.
		for (int i = start_index; i < sizeof(set); i++) {
			a_case[level] = set[i];
			DFS(level + 1, i + 1);
		}
	}
};
//-----
//-----Combination_with_repetition
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
				printf("%c ", *(a_case + i));
			printf("/ Number of cases : %d\n", n_of_cases);
			return;
		}

		for (int i = start_index; i < sizeof(set); i++) {
			a_case[level] = set[i];
			DFS(level + 1, i);
		}
	}
};
//-----

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
![image](https://user-images.githubusercontent.com/67142421/149829768-1ee5598a-a045-4521-a626-5af6ff23c77d.png)
