# DFS
## Depth First Search VS Breadth First Search
![image](https://user-images.githubusercontent.com/67142421/149474909-755eb088-f437-48c2-8e98-e9d0f4f2ea5f.png)

## The searching order of DFS and BFS
![image](https://user-images.githubusercontent.com/67142421/149474919-bd949f3b-17ae-4d10-a222-729a023e1e64.png)

## The graph for searching in this code
![Graph for searching](https://user-images.githubusercontent.com/67142421/149482856-ba8dcc40-4928-4a6a-bef6-782ad4778e2a.png)

## Using adjacent list
~~~c++
#include <iostream>
#include <vector>
using namespace std;

const char GRAPH_SIZE = 10;
vector<vector<int>> graph(GRAPH_SIZE);

void add_edge(int start, int end) {
	graph[start].push_back(end);
	graph[end].push_back(start);
}

vector<bool> visited(GRAPH_SIZE, false);
void DFS(int vertex) {
	visited[vertex] = true; // Visit
	cout << vertex << " -> ";

	for (auto i : graph[vertex]) // Search for vertices not visited
		if (!visited[i])
			DFS(i);
}

int main() {
	add_edge(0, 1);
	add_edge(1, 2);
	add_edge(1, 3);
	add_edge(2, 4);
	add_edge(3, 4);
	add_edge(3, 5);
	add_edge(5, 6);
	add_edge(5, 7);
	add_edge(6, 7);
	add_edge(7, 8);
	add_edge(7, 9);
	cout << "Searchng : ";
	DFS(3);
}
~~~

## Using adjacent matrix
~~~c++
#include <iostream>
using namespace std;

const char GRAPH_SIZE = 10;
bool adj_matrix[GRAPH_SIZE][GRAPH_SIZE] = { 0, };

void add_edge(int start, int end) {
	adj_matrix[start][end] = 1;
	adj_matrix[end][start] = 1;
}

void print_adj_matrix() {
	for (int i = 0; i < GRAPH_SIZE; i++) {
		for (int j = 0; j < GRAPH_SIZE; j++)
			cout << adj_matrix[i][j] << "  ";
		cout << "\n";
	}
}

bool visited[GRAPH_SIZE] = { false, };

void DFS(int vertex) {
	visited[vertex] = true; // Visit
	cout << vertex << " -> ";

	for (int i = 0; i < GRAPH_SIZE; i++)
		if (adj_matrix[vertex][i] && !visited[i]) // Search for vertices not visited
			DFS(i);
}

int main() {
	add_edge(0, 1);
	add_edge(1, 2);
	add_edge(1, 3);
	add_edge(2, 4);
	add_edge(3, 4);
	add_edge(3, 5);
	add_edge(5, 6);
	add_edge(5, 7);
	add_edge(6, 7);
	add_edge(7, 8);
	add_edge(7, 9);
	print_adj_matrix();
	DFS(3);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149482085-dc2c4135-8928-499e-9ba3-7ed7aa621311.png)
