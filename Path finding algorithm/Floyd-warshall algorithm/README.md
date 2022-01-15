# Floyd-warshal algorithm
>Floyd warshal algorithm is for finding shortest paths like Dijikstra's algorithm. But in contrast to Dijikstra's algorithm, floyd-warshal algorithm finds all shortest distances and paths between every pair of vertices.

~~~c++
#include <iostream>
#include <list>
using namespace std;

int INF = 987654321;
const int GRAPH_SIZE = 10;
int graph[GRAPH_SIZE][GRAPH_SIZE];

void add_edge(int vertex1, int vertex2, int weight) {
	graph[vertex1][vertex2] = weight;
	graph[vertex2][vertex1] = weight;
}

void floyd_warshall() {
	int weight_table[GRAPH_SIZE][GRAPH_SIZE];
	list<int> shortest_paths[GRAPH_SIZE][GRAPH_SIZE];

	// Initialize the solution matrix and shortest paths.
	for (int from = 0; from < GRAPH_SIZE; from++)
		for (int to = 0; to < GRAPH_SIZE; to++) {
			weight_table[from][to] = graph[from][to];
			shortest_paths[from][to].push_back(from);
			if (graph[from][to] != INF && graph[from][to] != 0)
				shortest_paths[from][to].push_back(to);
		}

	// Update
	for (int through = 0; through < GRAPH_SIZE; through++) // intermediate vertices
		for (int from = 0; from < GRAPH_SIZE; from++) // source vertices
			for (int to = 0; to < GRAPH_SIZE; to++) { // destination vertices
				int weight_of_new_path = weight_table[from][through] + weight_table[through][to]; // new path
				if (weight_of_new_path < weight_table[from][to]) { // Update if the new path is better than the old path
					weight_table[from][to] = weight_of_new_path;

					shortest_paths[from][to] = shortest_paths[from][through];
					auto crawler = shortest_paths[through][to].begin(); crawler++;
					for (auto i = crawler; i != shortest_paths[through][to].end(); i++)
						shortest_paths[from][to].push_back(*i);
				}
			}

	// Print
	printf("-----Weight table\n");
	for (int i = 0; i < GRAPH_SIZE; i++) {
		for (int j = 0; j < GRAPH_SIZE; j++)
			printf("%3d ", weight_table[i][j]);
		printf("\n");
	}

	printf("\n\n-----Shortest paths\n");
	for (int from = 0; from < GRAPH_SIZE; from++)
		for (int to = 0; to < GRAPH_SIZE; to++) {
			if (from == to)
				continue;

			cout << "From " << from << " to " << to << " : ";
			auto i = shortest_paths[from][to].begin();
			while (true) {
				cout << *i;
				i++;
				if (i != shortest_paths[from][to].end())
					printf(" -> ");
				else {
					printf("\n");
					break;
				}
			}
		}
}

int main() {
	for (int i = 0; i < GRAPH_SIZE; i++)
		for (int j = 0; j < GRAPH_SIZE; j++)
			i == j ? graph[i][j] = 0 : graph[i][j] = INF;

	add_edge(0, 1, 5);
	add_edge(1, 2, 5);
	add_edge(0, 2, 6);
	add_edge(0, 9, 14);
	add_edge(0, 8, 7);
	add_edge(8, 9, 15);
	add_edge(8, 7, 8);
	add_edge(1, 3, 4);
	add_edge(3, 2, 3);
	add_edge(3, 4, 6);
	add_edge(2, 4, 10);
	add_edge(4, 5, 8);
	add_edge(2, 5, 11);
	add_edge(2, 9, 5);
	add_edge(9, 5, 6);
	add_edge(9, 6, 4);
	add_edge(5, 6, 7);
	add_edge(7, 6, 3);

	floyd_warshall();
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149640346-665bb8e6-ef58-47a4-ba63-1fb72bef4aeb.png)