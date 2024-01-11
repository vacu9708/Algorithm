# Bubble sort
>Bubble sort is a sorting algorithm simple to implement but is one of the slowest sorting algorithms that takes O(n^2).


## Working process
![image](https://user-images.githubusercontent.com/67142421/149490296-a057ecca-c8ec-44c6-b3fc-603a0dcd7031.png)

Elements in the wrong order are swapped.

## Time complexity
> N = the number of elements to sort.
> In the first iteration of the first loop, N-1 of comparison is conducted >> In the 2nd iteration, N-2 >> N-3 ... 2 ... 1 = 
> (N-1)+(N-2)+(N-3)+...+2+1 = N-1(2+N-1-1) = (N-1)N/2 =
> By the sum of arithmetical series : **Time complexity : O(n^2)**
![image](https://user-images.githubusercontent.com/67142421/149508649-d1d4efed-9e65-4b85-bff7-7a851a2dadff.png)

~~~python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        # Flag to check if any swaps were made in the pass
        swapped = False
        for j in range(n - 1 - i):
            if arr[j] > arr[j + 1]:
                # Swap two elements
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        # If no swaps were made in the pass, the array is already sorted, so exit
        if not swapped:
            break

# Example integer array
arr = [64, 34, 25, 12, 22, 11, 90]
bubble_sort(arr)
print("Sorted array:", arr)
~~~
