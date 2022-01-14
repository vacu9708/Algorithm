# BFS
## Depth First Search VS Breadth First Search
![image](https://user-images.githubusercontent.com/67142421/149474909-755eb088-f437-48c2-8e98-e9d0f4f2ea5f.png)

## The searching order of DFS and BFS
![image](https://user-images.githubusercontent.com/67142421/149474919-bd949f3b-17ae-4d10-a222-729a023e1e64.png)

## The graph for searching in this code
![Graph for searching](https://user-images.githubusercontent.com/67142421/149483978-c3e83d9d-6a24-4fd5-b951-49bc34a4b409.png)

## Using adjacent list
~~~c++
#include <iostream>
#include <vector>
using namespace std;

#define GRAPH_LENGTH 10 // The number of vertices

void insert_edge(vector<vector<int>>& graph, int start, int end) {
	graph[start].push_back(end);
	graph[end].push_back(start);
}

void print_graph(vector<vector<int>>& graph) {
	for (int i = 0; i < GRAPH_LENGTH; i++) {
		cout << i << " : { ";
		for (int j = 0; j < GRAPH_LENGTH; j++)
			cout << graph[i][j] << " ";
		cout << "}\n";
	}
}

int queue[GRAPH_LENGTH];
int front = 0, rear = 0;
void enQ(int data) {
	rear = (rear + 1) % GRAPH_LENGTH; // If it's the last index go to index 0, else index++
	queue[rear] = data;
}

int deQ() {
	front = (front + 1) % GRAPH_LENGTH;
	return queue[front];
}

bool visited[GRAPH_LENGTH] = { false, };
void BFS(vector<vector<int>>& graph, int vertex) {
	visited[vertex] = true;
	cout << vertex << " -> ";
	enQ(vertex); // Record the vertices to search from later while searching

	while (front != rear) { // While the queue isn't empty
		vertex = deQ(); // Search from the vertex that was visited the earliest
		for (auto i : graph[vertex]) // Search for the vertices not visited
			if (visited[i] == false) {
				visited[i] = true;
				cout << i << " -> ";
				enQ(i);
			}
	}
}

int main() {
	// A : 0 | B : 1 | C : 2 | D : 3 | S : 4
	vector<vector<int>> graph(GRAPH_LENGTH);
	insert_edge(graph, 0, 1);
	insert_edge(graph, 1, 2);
	insert_edge(graph, 1, 3);
	insert_edge(graph, 2, 4);
	insert_edge(graph, 3, 4);
	insert_edge(graph, 3, 5);
	insert_edge(graph, 5, 6);
	insert_edge(graph, 5, 7);
	insert_edge(graph, 6, 7);
	insert_edge(graph, 7, 8);
	insert_edge(graph, 7, 9);
	print_graph(graph);
	BFS(graph, 3);
}
~~~

## Using adjacent matrix
~~~c++
#include <iostream>
using namespace std;

#define GRAPH_LENGTH 10

void insert_edge(int adj_matrix[][GRAPH_LENGTH], int start, int end) {
	adj_matrix[start][end] = 1;
	adj_matrix[end][start] = 1;
}

void print_adj_matrix(int adj_matrix[][GRAPH_LENGTH]) {
	for (int i = 0; i < GRAPH_LENGTH; i++) {
		for (int j = 0; j < GRAPH_LENGTH; j++)
			cout << adj_matrix[i][j] << "  ";
		cout << "\n";
	}
}

int queue[GRAPH_LENGTH];
int front = 0, rear = 0;
void enQ(int data) {
	rear = (rear + 1) % GRAPH_LENGTH;
	queue[rear] = data;
}

int deQ() {
	front = (front + 1) % GRAPH_LENGTH;
	return queue[front];

}

bool visited[GRAPH_LENGTH] = { false, };
void BFS(int adj_matrix[][GRAPH_LENGTH], int vertex) {
	visited[vertex] = true;
	cout << vertex << " ";
	enQ(vertex);

	while (front != rear) {
		vertex = deQ();
		for (int i = 0; i < GRAPH_LENGTH; i++)
			if (adj_matrix[vertex][i] && !visited[i]) {
				visited[i] = true;
				cout << i << " ";
				enQ(i);
			}
	}
}
~~~
					     
## Result
![Untitled](https://user-images.githubusercontent.com/67142421/149474554-3e1df771-97f9-4e95-ae90-68bd2bc2ca16.png)
