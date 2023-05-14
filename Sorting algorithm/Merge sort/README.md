# Merge sort
>Merge sort is one of the most efficient sorting algorithm that takes **Nlog(N)** on average.<br>
>It uses a *Divide and conquer* approach.

![image](https://user-images.githubusercontent.com/67142421/149567895-7ef189fb-abcd-4430-bf6a-5cef1dd9ea8f.png)

## Characteristics
- A stable sort, which means that the order of equal elements is maintained.
- Bottom-up sorting (Quick sort is top-down)

## Time complexity
![image](https://user-images.githubusercontent.com/67142421/234135296-56675120-907a-431b-93ae-b7dfc1cc95f2.png)

>In each recursive iteration, the number of elements decreases to half. If the last level of the recursion tree is is log(N) as written in [Binary search](https://github.com/vacu9708/Algorithm/tree/main/Searching%20algorithm/Binary%20search).<br>
>The last level of the tree is reached N times. Therefore, the time complexity of merge sort is **O(NlogN)**

~~~python
def merge_sort(lst, temp, left, right):
    if left == right:
        return

    mid = (left + right) // 2
    merge_sort(lst, temp, left, mid)
    merge_sort(lst, temp, mid + 1, right)

    i, j, temp_i = left, mid + 1, left
    while i <= mid and j <= right:
        if lst[i] < lst[j]:
            temp[temp_i] = lst[i]
            i += 1
        else:
            temp[temp_i] = lst[j]
            j += 1
        temp_i += 1

    while i <= mid:
        temp[temp_i] = lst[i]
        i += 1
        temp_i += 1
    while j <= right:
        temp[temp_i] = lst[j]
        j += 1
        temp_i += 1

    for i in range(left, right + 1):
        lst[i] = temp[i]

# Usage example
lst = [8,7,6,5,4,3,2,1]
print(f'Before sort: {lst}')
merge_sort(lst, [0] * len(lst), 0, len(lst) - 1)
print(f'After sort: {lst}')

~~~
