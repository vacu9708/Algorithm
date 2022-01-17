# Tower of Hanoi

## Rule
* Only one disk may be moved at a time.
* No disk may be placed on top of a disk that is smaller than it.
* Each move consists of taking the upper disk from one of the stacks and placing it on an empty rod.

## Explanation
**How to move an Nth disk and disks on top of it to the target rod**
1. The N-1th(a disk on top disk N) disk has to be moved to the auxiliary rod so that the Nth disk can be moved to the target rod.
2. Move the Nth disk to the target rod.
3. Move the N-1th disk that was in the auxiliary rod to the target rod.

~~~python
A = [3, 2, 1]
B = []
C = []

def tower_of_hanoi(disk, source, target, auxiliary):
    if disk == 0: # Termination condition
        return 
    tower_of_hanoi(disk - 1, source, auxiliary, target) # Step 1
    # Step 2 : moving
    print("Move disk : (", disk,')')
    target.append(source.pop())
    print(A, B, C,"-----", sep = '\n')
    #-----
    tower_of_hanoi(disk - 1, auxiliary, target, source) # Step 3

tower_of_hanoi(len(A), A, C, B) # Move 3 disks from source A to target C with auxiliary B
~~~
![image](https://user-images.githubusercontent.com/67142421/149809489-804d05a9-6654-4a4e-8fff-2908e4834f24.png)
