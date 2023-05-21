# Knapsack problem
>A thief has a knapsack of given capacity, and he wishes to maximize the profit with available valuables. What should he do?

# 0-1 knapsack problem (true or false cases, take or not)
>Item boxes cannot be opened which means the items in them cannot be divided to put in the knapsack.<br>
>We either take the whole item box or don’t take it. 

### Items to put in the knapsack and the max weight of the knapsack in this code
![image](https://user-images.githubusercontent.com/67142421/149814653-891bdeab-0a10-4480-8895-0b7c3c13cd7a.png)

## Finding only the biggest profit(DP)
~~~c++
#include <iostream>
#include <vector>

using namespace std;

void knapsack() {
	int max_weight = 15;
	vector<int> weights = { 12,1,4,1,2 };
	vector<int> values = { 4,2,10,1,2 };
	vector<int> memo(max_weight + 1); // All possible full weights: memo[knapsack_weight]=value

	for (int i = 0; i < weights.size(); i++){
		for (int j = max_weight; j >= 1; j--){//for (int j = 1; j <= max_weight; j++) // doesn't work because it's previous solutions that have to be used.
			if (weights[i] > j) // Current item exceeded full weight
                break;
            memo[j] = max(memo[j], memo[j - weights[i]] + values[i]); // Make use of a previous solution
            // Print result
            for (int i = 1; i <= max_weight; i++) printf("%d ",memo[i]);
            cout << "\n";
        }
        printf("%d-----\n",i);
    }
        
	printf("%d", memo[max_weight]);
}

int main() {
	knapsack();
}
~~~

## Output
15

# Fractional knapsack problem (Greedy approach)
>In Fractional Knapsack, we can open item boxes and divide them for maximizing the total value of knapsack.

### Items to put in the knapsack and the max weight of the knapsack in this code
![image](https://user-images.githubusercontent.com/67142421/149818631-20b8c7a4-f19e-4381-a221-adf11571add6.png)

~~~c++
#include <iostream>
#include <vector>
#include <algorithm> // For greedy approach

using namespace std;

class Value_per_weight {
public:
	double value_per_weight;
	short original_index;

	bool operator>(Value_per_weight a) {
		return value_per_weight > a.value_per_weight;
	}
};

const short number_of_items = 5;
vector<double> item_weights = { 12, 1, 4, 1, 2 };
vector<double> item_values = { 4, 2, 10, 1, 2 };
vector<Value_per_weight> values_per_weight(number_of_items);
vector<short> items_in_bag(number_of_items); // kg

void print_result() {
	int total_weight = 0;
	cout << "A B C D E\n";
	for (int i = 0; i < number_of_items; i++) {
		cout << items_in_bag[i] << " ";
		total_weight += items_in_bag[values_per_weight[i].original_index] * values_per_weight[i].value_per_weight;
	}
	cout << "\nTotal weight : " << total_weight;
}

void knapsack_greedy() {
	int sum_of_weights = 0, max_weight = 15;

	// Calculate value per weight and sort so that items with higher value per weight is in front
	for (int i = 0; i < number_of_items; i++) {
		values_per_weight[i].value_per_weight = item_values[i] / item_weights[i];
		values_per_weight[i].original_index = i;
	}
	sort(values_per_weight.begin(), values_per_weight.end(), [](Value_per_weight a, Value_per_weight b) {return a > b;});
	//------
	// Put items (that have been sorted in order of higher value per weight) in bag
	for (int i = 0; i < number_of_items; i++)
		while (items_in_bag[values_per_weight[i].original_index] + 1 <= item_weights[values_per_weight[i].original_index] && sum_of_weights + 1 <= max_weight) {
			items_in_bag[values_per_weight[i].original_index]++;
			sum_of_weights++;
		}
	//-----
	print_result();
}

int main() {
	knapsack_greedy();
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/149819785-fc363e2c-9644-4670-b20e-cf2b6d5a8055.png)

## Finding the best way to put items in a knapsack to get the biggest profit (Backtracking method)
~~~c++
#include <iostream>
#include <vector>

using namespace std;

unsigned int how_many_items = 5, max_weight = 15, biggest_profit = 0;
vector<bool> truth_table(how_many_items), answer(how_many_items);
vector<int> item_weights = { 12, 1, 4, 1, 2 }; // kg
vector<int> item_values = { 4, 2, 10, 1, 2 }; // $

void knapsack_backtracking(int level, int sum_of_weights, int sum_of_values) { // level : Level of tree, item index
	if (level == how_many_items) { // In the last level of tree, all the items have been checked, so terminate
		if (sum_of_values > biggest_profit) { // If a new sum of values is better than the biggest value, update the answer
			biggest_profit = sum_of_values;
			for (int i = 0; i < how_many_items; i++)
				answer[i] = truth_table[i];
		}

		return;
	}

	for (int i = 0; i <= 1; i++) { // DFS on a tree
		truth_table[level] = i;
		if (i == 1) { // If the item in this level is to be put in the knapsack
			// If the sum of weights exceeds max weight, nodes from the current node are useless, so cut the branch for backtracking.
			if (sum_of_weights + item_weights[level] > max_weight)
				return;

			// Update information in the parameters.
			knapsack_backtracking(level + 1, sum_of_weights + item_weights[level], sum_of_values + item_values[level]);
		}
		else // If the item in this level is not to be put in the knapsack, go to the next level without adding the item.
			knapsack_backtracking(level + 1, sum_of_weights, sum_of_values);
	}
}

void print_answer() {
	printf("A B C D E\n");
	for (int i = 0; i < how_many_items; i++)
		printf("%d ", answer[i] == true ? 1 : 0);
	printf("\nBiggest profit : %d\n", biggest_profit);

}

int main() {
	/* Manual input
	cin >> how_many_items >> max_weight;
	item_weights.resize(how_many_items);
	item_values.resize(how_many_items);
	for (int i = 0; i < how_many_items; i++)
		cin >> item_weights[i] >> item_values[i];*/

	knapsack_backtracking(0, 0, 0);
	print_answer();
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/149814608-fc4dc878-7669-4fd7-a1e6-82b89d38df67.png)
