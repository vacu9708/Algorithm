# Quick sort
>Quick sort is one of the most efficient sorting algorithm that takes **Nlog(N)** on average.<br>
>It uses a *Divide and conquer* approach.

## Features
- It can't preserve the elements with the same value. In other words, the order of equal elements may be changed. (unstable)
- "Pivot" is used to partition the array into two sub-arrays, based on its value.
- Top-down sorting (Merge sort is bottom-up)

## Process
1. Choose a pivot element.
2. Partition the array into two sub-arrays, one with elements less than or equal to the pivot, and the other with elements greater than or equal to the pivot.
3. Recursively apply steps 1 and 2 to the two sub-arrays.

## Time complexity
Same as [Merge sort](https://github.com/vacu9708/Algorithm/tree/main/Sorting%20algorithm/Merge%20sort)

## The worst case where O(n^2) is taken
If the worst pivot, either the maximum or minimum, is selected in every step, **O(n^2)** is taken.<br>
But this situation occurs only when elements are already sorted in either ascending or descending order, which rarely happens.<br>
Also, this problem can be solved by using a method like the middle pivot.
### Example
There are sorted elements {1,2,3,4,5}(n = 5). What will happen if the minimum is selected as a pivot in every step?<br>
1. Let's pick the minimum 1 as a pivot. "j" will try to find a value smaller than 1.
2. In the end, "j" will get to the far left after n times of repetitions.
3. In the next iteration, 2 is selected as a pivot and the same process is repeated.

>(n-1) + (n-2) + (n-3) + ... + 1 = **O(n^2)**

~~~python
def quick_sort(arr, left, right):
    if left >= right:
        return

    pivot = arr[left]
    i, j = left + 1, right

    while i <= j:  # Until i and j cross each other
        # Find element on left that should be on right
        while i <= j and arr[i] <= pivot:  # Include equal to pivot for stability
            i += 1
        # Find element on right that should be on left
        while i <= j and arr[j] >= pivot:  # Include equal to pivot for stability
            j -= 1
        if i < j:  # Swap elements if i and j have not crossed
            arr[i], arr[j] = arr[j], arr[i]

    # Swap pivot into correct position. This doesn't work without the equal(i <= j) above.
    arr[j], arr[left] = arr[left], arr[j]

    # Recursively sort the partitions
    quick_sort(arr, left, j - 1)
    quick_sort(arr, j + 1, right)

# Example
arr = [5, 1, 7, 6, 2, 3, 8, 9, 4]
quick_sort(arr, 0, len(arr) - 1)
print(f'After sort: {arr}')

# Additional example arrays
examples = [
    [10, 7, 8, 9, 1, 5],
    [64, 34, 25, 12, 22, 11, 90],
    [32, 45, 67, 2, 7],
    [1, 4, 3, 2],
    [10, 9, 8, 7, 6, 5, 4, 3, 2, 1],
    [],
    [1],
    [2, 1],
    [3, 3, 3],
    [1, 2, 3, 4, 5],
    [5, 4, 3, 2, 1],
    [4, 5, 3, 1, 2],
    [-1, -5, -3, -4, -2],
    [1.1, 3.3, 2.2, 5.5, 4.4],
]

# Sort each example array
for example in examples:
    quick_sort(example, 0, len(example) - 1)
    print(f'After sort: {example}')
~~~

~~~python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]  # Choose the middle element as the pivot
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)

# Example usage:
arr = [3, 6, 8, 10, 1, 2, 1]
sorted_arr = quick_sort(arr)
print(sorted_arr)
~~~
