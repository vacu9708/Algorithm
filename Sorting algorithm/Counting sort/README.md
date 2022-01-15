# Counting sort
>Counting sort is a sorting algorithm that sorts elements by counting the number of occurrences of each element. The count is stored in an auxiliary container.

## Working process
![image](https://user-images.githubusercontent.com/67142421/149512925-70c84dce-3f55-486f-b01c-e2edc77a2b15.png)

## Characteristics
* Strengths:
  >Linear time. Counting sort runs in **O(n)** time, making it much faster than other comparison-based sorting algorithms like quicksort or merge sort.
* Weaknesses:
  >Restricted inputs. Counting sort only works when the range of potential items in the input is known ahead of time.<br>
  >Space cost. If the range of potential values is big, then counting sort requires a lot of space. For example, when sorting elements such as (1, 2, 3, 88) an array of 89
  >size is needed even though there are only 4 elements.

~~~c++
#include <iostream>
using namespace std;

int arr[8] = { 5,4,3,2,5,4,3,2 };
int length = sizeof(arr) / sizeof(arr[0]);

void counting_sort() {
    // Find the max of the array
    int max = arr[0];
    for (int i = 1; i < length; i++)
        if (arr[i] > max)
            max = arr[i];
    //-----
    int* count = new int[max + 1]{ 0, };

    for (int i = 0; i < length; i++) // Sort by counting the number of occurences of elements)
        count[arr[i]]++;

    for (int i = 0; i <= max; i++) // Print the result
        for (int j = 0; j < count[i]; j++) // Print as many as the number of an element
            cout << i << " ";

    delete[] count;
}

int main() {
    printf("Original array : ");
    for (int i = 0; i < length; i++)
        printf("%d ", arr[i]);
    printf("\nSorted array : ");
    counting_sort();
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149512485-f871766c-6848-4ee1-8f96-6c14afd7badc.png)
