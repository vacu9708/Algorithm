# Quick sort
>Quick sort is the most effective sorting algorithm that takes **nlog(n) time** on average.<br>
>It is one of *Divide and conquer* algorithms.

## Features
* It can't preserve the elements with the same value. In other words, the order of elements with the same value can be changed.
* A list is divided into 2 sublists. This process is repeated.

## Working process (ascending order)
1. A pivot is selected and swapped with the first element.
2. "i" searches for an element bigger than the pivot from the 2nd index and "j" searches for an element smaller than the pivot from the last index.
3. Swap found 2 elements. This process leaves elements smaller than pivot on the left of i and elements bigger than pivot on the right of j.
4. Once "i" is no longer on the left of "j", swap list[j] and the pivot so that elements on the left of j are in ascending order.

## The worst case where O(n^2) is taken
>If the worst pivot, either the maximum or minimum of the elements, is selected, **O(n^2)** is taken.<br>
>But this situation occurs only when elements are already sorted in either ascending or descending order, which rarely happens.<br>
>Also, this problem can be solved by using a middle pivot.
### Example
>There are sorted elements {1,2,3,4,5}(n = 5). What will happen if only the minimum is selected as a pivot?<br>
>Let's pick the minimum 1 as a pivot. "i" can leave only elements smaller than or equal to 1 and "j" can leeve only elements bigger than or equal to 1.<br>
>In the end, "j" will get to the pivot where 2n iterations were performed. And then the minimum in the next sublist, 2 is selected as a pivot and the same process is performed. n-1 times of iteration is performed.<br>
>(n-1) + (n-2) + (n-3) + ... + 1 = **O(n^2)**

~~~c++
#include <iostream>
#include <vector>
#include <random>
using namespace std;

int random_integer(int min, int max) { // Selecting a middle element is faster than random pivot.
    random_device seed; // Generate a random seed
    mt19937_64 mersenne(seed());
    uniform_int_distribution<> random(min, max);
    return random(mersenne);
}

void print_elements(vector<int> elements) {
    int length = elements.size();
    for (int i = 0; i < length; i++)
        cout << elements[i] << " ";
    cout << "\n";
}

void quick_sort(vector<int>& elements, int first, int last) { // Sorting in asclasting order
    if (first >= last)
        return;

    int pivot_index = (first + last) / 2; // Any element can be pivot. But a middle element is stable in time complexity.
    swap(elements[pivot_index], elements[first]); // The pivot has to be at the beginning of the elements.

    int i = first + 1, j = last;

    while (1) {
        //Find an element bigger than pivot to leave only elements smaller than pivot on the left of i.
        while (i < last && elements[i] <= elements[first])
            i++;

        //Find an element smaller than pivot to leave only elements bigger than pivot on the right of j.
        while (j > first && elements[j] >= elements[first])
            j--;

        //Swap elements[i], which is bigger than pivot with elements[j], which is smaller than pivot
        if (i < j)
            swap(elements[i], elements[j]);

        //Once "i" is no longer on the left of "j", swap list[j] and the pivot so that elements on the left of j are in ascending order.
        else {
            swap(elements[j], elements[first]);
            // Show the process
            printf("Dividing number : (%d) -> ", elements[j]);
            print_elements(elements);

            break;
        }
    }

    //Divide the list into 2 sublists.
    quick_sort(elements, first, j - 1);
    quick_sort(elements, j + 1, last);
}

void main() {
    vector<int> elements = { 5,1,7,6,2,3,8,9,4 };
    printf("Elements to sort : "); print_elements(elements);
    quick_sort(elements, 0, elements.size() - 1);
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/155838057-809dc268-f50f-46ed-8cab-1a5271015962.png)
