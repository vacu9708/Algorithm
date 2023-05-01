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
def bubble_sort(lst):
    for i in range(len(lst)-1,0,-1):
        for j in range(i):
            if lst[j]>lst[j+1]:
                lst[j], lst[j+1]=lst[j+1], lst[j]
        print(lst)
lst=[5,4,3,2,1]
bubble_sort(lst)
print(lst)
~~~

## Compile and run
Sort 5 4 3 2 1 in ascending order.

![Untitled](https://user-images.githubusercontent.com/67142421/149509160-b5323404-3059-4bc6-8535-d1da481906ac.png)
