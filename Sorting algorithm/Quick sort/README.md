# Quick sort
>Quick sort is the most effective sorting algorithm that takes **nlog(n) time** on average.<br>
>It is one of the *Divide and conquer* algorithms.

## Features
* It can't preserve the elements with the same value. In other words, the order of elements with the same value can be changed. (unstable)
* "Pivot" is used to partition the array into two sub-arrays, based on its value.

## Process
1. Choose a pivot element.
2. Partition the array into two sub-arrays, one with elements less than or equal to the pivot, and the other with elements greater than or equal to the pivot.
3. Recursively apply steps 1 and 2 to the two sub-arrays.

## Time complexity
Same as [Merge sort](https://github.com/vacu9708/Algorithm/tree/main/Sorting%20algorithm/Merge%20sort)

## The worst case where O(n^2) is taken
>If the worst pivot, either the maximum or minimum of the elements, is selected, **O(n^2)** is taken.<br>
>But this situation occurs only when elements are already sorted in either ascending or descending order, which rarely happens.<br>
>Also, this problem can be solved by using a middle pivot.
### Example
>There are sorted elements {1,2,3,4,5}(n = 5). What will happen if only the minimum is selected as a pivot?<br>
>Let's pick the minimum 1 as a pivot. "i" can leave only elements smaller than or equal to 1 and "j" can leave only elements bigger than or equal to 1.<br>
>In the end, "j" will get to the pivot where 2n iterations were performed. And then the minimum in the next sublist, 2 is selected as a pivot and the same process is performed. n-1 times of iteration is performed.<br>
>(n-1) + (n-2) + (n-3) + ... + 1 = **O(n^2)**

~~~python
def quick_sort(arr, left, right):
    if left>=right:
        return
    pivot=arr[(left + right) // 2]
    i,j = left, right
    while 1:
        # Find an element greater than or equal to pivot
        while i < right and arr[i] < pivot: i+=1 # Value same as the pivot cannot be passed
        # Find an element less than or equal to pivot
        while j > left and arr[j] > pivot: j-=1
        if i < j: arr[i], arr[j] = arr[j], arr[i]
        else: break
    # All the elements before j are less than those after j
    quick_sort(arr, left, j - 1)
    quick_sort(arr, j + 1, right)

arr=[5,1,7,6,2,3,8,9,4]
print(f'Before sort: {arr}')
quick_sort(arr,0,len(arr)-1)
print(f'After sort: {arr}')
~~~
