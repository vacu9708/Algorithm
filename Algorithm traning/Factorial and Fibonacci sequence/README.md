# Recursive method
## When to use?
>A recursive method takes a lot of stack memory, so it should be used only when it is complex to write regular iterative code.
* Used when the answer can be found by solving the problem that is a level below. For example, if you know 4!, you can find 5!. Tower of hanoi is included in this example.
* Used for searching a graph such as DFS, BFS. (The main use)

## Recursive methods and a regular iterative method
~~~c++
int factorial_recursive1(int n) {
	if (n=1)
		return 1;
    
	return n*factorial(n - 1);	
}

int factorial_recursive2(int n) {
	if (n > 1)
		return n*factorial(n - 1);
	else
		return 1;
}

int factorial_loop(int n) {
    int result=1;
    for(int i=n; i>0; i--)
        result*=i;
        
    return result;
}

int main() {
  cout << factorial_recursive1(4) << '\n';
  cout << factorial_loop(4) << '\n';
}
~~~

## Output
24<br>
24

# Fibonacci sequence
>The Fibonacci sequence is the series of numbers where each number is the sum of the two preceding numbers.<br>
1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, ...

## A recursive method and regular iterative methods
* **Recursive fibonacci** : **O(n^2)** because values that have already been calculated are calculated again. 
![image](https://user-images.githubusercontent.com/67142421/178239230-18553100-0f4a-49d6-a34e-4ca265f1aaa2.png)

* **DP and iterative fibonacci** : **O(n)**
~~~python
def fibonacci_loop1(n):
    fibonacci_sequence = [1,1]
    for i in range(2, n + 1):
        fibonacci_sequence.append(fibonacci_sequence[i - 1] + fibonacci_sequence[i - 2])
        
    return fibonacci_sequence[n]
    '''
    for i in range(n + 1): # Print the terms
        print("index",i,":",fibonacci_sequence[i])
    '''

def fibonacci_loop2(n):
    a, b = 1, 1 # 0th and 1st term
    for i in range(n - 1):
        a, b = b, a + b

    return b

def fibonacci_recursive(n):
    if n <= 1:
        return 1 
    
    return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
    
print(fibonacci_loop1(5));
print(fibonacci_loop2(5));
print(fibonacci_recursive(5));
~~~
## Output
8<br>
8<br>
8

## Using dynamic programming

~~~c++
#include<iostream>
using namespace std;

int memo[100]{ 1,1 };
int fibonacci(unsigned int n) {
    if (memo[n] != 0) // If memo[n] is availale, use it in order not to repeat the same operation.
        return memo[n];

    memo[n] = fibonacci(n - 1) + fibonacci(n - 2); // Top-down
}

void main() {
    fibonacci(5);
    for (int i = 0; i <= 5; i++)
        cout << "Index " << i << " : " << memo[i] << "\n";
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/149926604-5ea07991-3061-41ae-bedd-fa8e0f93ed1e.png)

Memoization : taking advantage of previous results
Dynamic programming : solving a problem by breaking it down into subproblems
