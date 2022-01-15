# Quick sort
>Quick sort is the most effective sorting algorithm that takes **O(nlog(n)) time** on average.<br>
>It is one of *Divide and conquer* algorithms.

## Characteristics
* It can't preserve the elements with the same value. In other words, the order of elements with the same value can be changed.
* In the worst case where the worst pivot is selected, **O(n^2)** time might be taken. This problem can be solved by using a random pivot.
* A list is divided into sublists and they are sorted. This process is repeated. 
* There are only elements smaller than or equal to pivot on the left of a dividing index and only elements bigger than or equal to pivot on the right of a dividng index.

## Working process (ascending order)
1. A pivot is selected and moved to the first index.
2. "i" starts searching for elements bigger than the pivot from the first index and "j" starts searching for elements smaller than the pivot from the last index.
   All the elements of "i" bigger than the pivot and all the elements of "j" smaller than the pivot are swapped
   In this process, only elements smaller than or equal to pivot remain on the left of "i" and only elements bigger than or equal to the pivot remain on the right of "j"
3. Once "i" is not on the left of "j", swap "j", which is smaller than or equal to the pivot, and the start index(which is a pivot) 
   because "j" is going to be a dividing index and there have to be only elements smaller than the dividing number on the left of it.

~~~c++
#include <iostream>
#include <vector>
#include <random>
using namespace std;

int random_integer(int min, int max) {
    random_device seed; // Generate a random seed
    mt19937_64 mersenne(seed());
    uniform_int_distribution<> random(min, max);
    return random(mersenne);
}

void print_elements(vector<int> container) {
    int length = container.size();
    for (int i = 0; i < length; i++)
        cout << container[i] << " ";
    cout << "\n";
}

void quick_sort(vector<int>& container, int start, int end) { // Sorting in ascending order
    if (start >= end) // If the length of sublist is 1, terminate
        return;

    int pivot_index = random_integer(start, end); // Any index can be pivot. But a random pivot is more stable in time complexity.
    swap(container[pivot_index], container[start]); // The pivot should be at the beginning of the elements.

    int i = start + 1, j = end;

    while (1) {
        // Find an element bigger than pivot. Only elements smaller than or equal to pivot remain on the left of i.
        while (i < end && container[i] <= container[start])
            i++;
        //-----
        // Find an element smaller than pivot. Only elements bigger than or equal to pivot remain on the right of j.
        while (j > start && container[j] >= container[start])
            j--;
        //-----
        // container[i] is always bigger than container[j] when i is on the left of j, so they have to swapped 
        // to be in ascending order.
        if (i < j)
            swap(container[i], container[j]);
        //-----
        // When i is not on the left of j, container[i] and container[j] are in ascending order because there 
        // are only elements bigger than pivot on the left of j, so they can't be swapped.
        // container[j] is smaller than or equal to the pivot, container[start]. Swap them.
        else {
            swap(container[j], container[start]);
            printf("Dividing number : (%d) -> ", container[j]); 
            print_elements(container);
            break;
        }
        //-----
    }

    // Divide the list into 2 sublists.
    quick_sort(container, start, j - 1);
    quick_sort(container, j + 1, end);
}

void main() {
    vector<int> container = { 5,1,7,6,2,3,8,9,4 };
    printf("Elements to sort : "); print_elements(container);
    quick_sort(container, 0, container.size() - 1);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149634336-ef46147c-7d3c-40b0-8fdb-ac170517ba98.png)
