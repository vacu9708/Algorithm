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
    if disk == -1: # Termination condition (Top disk found)
        return 
        
    # Step 1 : Move (N-1)disk to the auxiliary rod to move the Nth disk.
    tower_of_hanoi(disk - 1, source, auxiliary, target)
    
    # Move Nth disk from source to target.
    print("Move disk : (", disk,')')
    target.append(source.pop())
    print(A, B, C,"-----", sep = '\n')

    # Step 3 : Move the N-1th disk that was in the auxiliary rod to the target rod.
    tower_of_hanoi(disk - 1, auxiliary, target, source)

tower_of_hanoi(len(A) - 1, A, C, B) # Move 3 disks from source A to target C with auxiliary B, starting from the disk at the bottom.
~~~
![image](https://user-images.githubusercontent.com/67142421/160593181-716bd6b5-cef8-4f01-8e22-e0463666eacd.png)
