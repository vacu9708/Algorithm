# Goldbach's conjecture
>Goldbach's conjecture : All even numbers over 2 can be expressed as the sum of 2 prime numbers.<br>
>Sieve of Eratosthenes : A method to find prime numbers fast.

### [ref: the symmetry of divisors instead of sieve](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/Programmers/level2/k%EC%A7%84%EC%88%98%EC%97%90%EC%84%9C%20%EC%86%8C%EC%88%98%20%EA%B0%9C%EC%88%98%20%EA%B5%AC%ED%95%98%EA%B8%B0.md)

~~~c++
#include <iostream>
#include <math.h>

char not_prime[10001]; // Can store prime numbers upto 10000. If it's is_prime instead, all the elements have to be initialized to [true]

void prime_number_sieve(int max) {
    for (int i = 2; i*i <= max; i++) { // because numbers before i*i have already been dealt with
        if (not_prime[i] == true) // If i has been removed, then the multiples of i have also been removed earlier
            continue;
        for (int j = i; i*j <= max; j++) // i*j<=max -> j<=max/i
            not_prime[i * j] = true;
    }
}


void goldbachs_conjecture(int target_number) {
    if (!(target_number > 2) || target_number % 2 != 0) { // If n is not over 2 or an even number, goldbach's conjecture is not valid.
        printf("n is not over 2 or it's not an even number");
        return;
    }

    // Find all i's and j's that satisfy (i + j == target_number)
    for (int i = 2; i <= (target_number / 2); i++) {
        if (not_prime[i] == true) // Continue if it's not a prime number
            continue;
        for (int j = 2; j <= (target_number - i); j++) {
            if (not_prime[j] == true)
                continue;
            if (i + j == target_number) // Print a case that satisfy goldbach's conjecture, that is, print a goldbach number
                printf("%d + %d = %d\n", i, j, target_number);
        }
    }
    //-----
}

int main() {
    prime_number_sieve(10000);
    int target_number;
    printf("Input : ");
    scanf_s("%d", &target_number);
    goldbachs_conjecture(target_number);
    return 0;
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149280363-3c1be358-e784-41c8-92a4-5c1b739f87ab.png)
