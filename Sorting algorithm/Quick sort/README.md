# Quick sort
>Quick sort is the most effective sorting algorithm that takes **nlog(n) time** on average.<br>
>It is one of the *Divide and conquer* algorithms.

## Features
* It can't preserve the elements with the same value. In other words, the order of elements with the same value can be changed.
* A list is divided into 2 sublists. This process is repeated.
* The "pivot" is used to partition the array into two sub-arrays, based on its value.

## Process
1. Choose a pivot element.
2. Partition the array into two sub-arrays, one with elements less than or equal to the pivot, and the other with elements greater than or equal to the pivot.
3. Recursively apply steps 1 and 2 to the two sub-arrays.

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
using namespace std;

void print_elements(vector<int> elements) {
    for (int i = 0; i < elements.size(); i++)
        cout << elements[i] << " ";
    cout << "\n";
}

void quick_sort(vector<int>& elements, int left, int right) {
    if (left >= right)
        return;

    int pivot = elements[(left + right) / 2]; // Any element can be pivot. But a middle element is stable in terms of time complexity.
    int i = left, j = right;
    while (1) {
        // Find an element greater than or equal to pivot
        while (i < right && elements[i] < pivot) i++;
        // Find an element less than or equal to pivot
        while (j > left && elements[j] > pivot) j--;
        if (i < j) swap(elements[i], elements[j]);
        else break;
    }

    // All the elements before j are less than those after j
    quick_sort(elements, left, j - 1);
    quick_sort(elements, j + 1, right);
}

void main() {
    vector<int> elements = { 5,1,7,6,2,3,8,9,4 };
    printf("Before sort : "); print_elements(elements);
    quick_sort(elements, 0, elements.size() - 1);
    printf("After sort : "); print_elements(elements);
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/155838057-809dc268-f50f-46ed-8cab-1a5271015962.png)
