<img src="https://user-images.githubusercontent.com/67142421/177835491-441dc710-f04e-40dc-bb68-42b17319adff.png" width=640 height=400>

# Coin change
>Find the way to use the fewest coins to make target money with given coins.
>We have $1, $5, $12 and have to make $15 with the given coins. There are 33 coins for each coin.

## Back tracking method
~~~c++
#include <iostream>
#include <vector>

using namespace std;

int target_money = 15, n_of_coin_type = 3, min_n_of_coins = 987654321;
vector<int> values_of_coins = { 1,5,12 }, numbers_of_remaining_coins = { 33,33,33 }, best_case(n_of_coin_type);

void backtracking(int start_index, int sum_of_coins, int n_of_coins_used, vector<int> a_case, vector<int> numbers_of_remaining_coins) {
	if (sum_of_coins == target_money) {
		if (n_of_coins_used < min_n_of_coins) {
			min_n_of_coins = n_of_coins_used;
			for (int i = 0; i < n_of_coin_type; i++)
				best_case[i] = a_case[i];
		}
		return;
	}
	else if (sum_of_coins > target_money)
		return;

	for (int i = start_index; i < n_of_coin_type; i++) { // Combination with repetition
		if (numbers_of_remaining_coins[i] == 0) // Use other coins if one of the coins has run out
			continue;

		numbers_of_remaining_coins[i]--;
		a_case[i]++;
		n_of_coins_used++;
		// Store the number of coins used and sum of coins upto the previous cases in the parameters
		backtracking(i, sum_of_coins + values_of_coins[i], n_of_coins_used, a_case, numbers_of_remaining_coins);
		numbers_of_remaining_coins[i]++; // Recover the changed information for the next coin
		a_case[i]--;
		n_of_coins_used--;
		//-----
	}
}

void print_answer() {
	printf("Coins used : ");
	for (auto i : best_case)
		cout << i << " ";
	printf("/ Numbers of coins used : %d\n", min_n_of_coins);
}

int main() {
	/* Putting values in the variables manually
	cin >> target_money;
	cin >> n_of_coin_type;
	values_of_coins.resize(n_of_coin_type);
	numbers_of_remaining_coins.resize(n_of_coin_type);
	a_case.resize(n_of_coin_type);

	for (int i = 0; i < n_of_coin_type; i++)
		cin >> values_of_coins[i] >> numbers_of_remaining_coins[i];*/

	backtracking(0, 0, 0, best_case, numbers_of_remaining_coins);
	print_answer();
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/149828518-619a0090-676e-43ac-bcd4-05c58bd9676e.png)

## Dynamic programming(the fastest)
>Only finding the minimum number of coins needed to make target money without finding what coins are used

~~~c++
// Finding the minimum number of coins needed to make target money
// Dynamic programming (The solution is always the most efficient)

#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

#define INF 98765
int memo[100001];
int target_money = 15, n_of_coin_type = 2;
vector<int> coins = { 5, 2 };

//int solution_recursion(int target_money) { // Works well but ineffective
//	if (target_money == 2 || target_money == 5)
//		return 1;
//	if (target_money == 0)
//		return 0;
//	if (target_money < 2)
//		return INF;
//
//	return min(solution(target_money - 2), solution(target_money - 5)) + 1;
//}

void solution(int target_money) {
	// Initialization
	for (int i = 0; i <= target_money; i++)
		memo[i] = INF;
	memo[0] = 0, memo[2] = 1, memo[5] = 1;
	//-----

	for (int i = 0; i < coins.size(); i++)
		for (int j = coins[i]; j <= target_money; j++) {
			memo[j] = min(memo[j], memo[j - coins[i]] + 1);

			for (int i = 0; i <= target_money; i++) // For debugging
				cout << memo[i] << " ";
			cout << "\n";
		}

	//for (int i = 0; i < coins.size(); i++) // Doesn't work
	//	for (int j = target_money; j >= coins[i]; j--) {
	//		memo[j] = min(memo[j], memo[j - coins[i]] + 1);
	//			
	//		for (int i = 0; i <= target_money; i++) // Checking the memo for dynamic programming
	//			cout << memo[i] << " ";
	//		cout << "\n";
	//	}
}

int main() {
	/* Manual input
	cin >> target_money;
	cin >> n_of_coin_type;
	for (int i = 0; i < n_of_coin_type; i++)
		cin >> coins[i];*/

	solution(target_money);
	printf("%d", memo[target_money] == INF ? -1 : memo[target_money]);

	//int answer = solution(target_money); // Recursvie solution(doesn't work)
	//printf("%d", answer == INF + 1 ? -1 : answer);
}
~~~

## Output (Target money : 15, coins = {5, 2})
3
