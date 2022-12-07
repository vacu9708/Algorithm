# Tower of Hanoi

![image](https://user-images.githubusercontent.com/67142421/176498793-a2874a2c-41c8-4a91-bc6f-687b45fe0be0.png)

## Rule
* Only one disk may be moved at a time.
* No disk may be placed on top of a smaller disk
* Each move consists of taking the upper disk from one of the stacks and placing it on an empty rod.

## Explanation
**How to move an Nth disk and disks on top of it to the target rod**
1. The (N-1)th(a disk on top disk N) disk has to be moved to the auxiliary rod so that the Nth disk can be moved to the target rod.
2. Move the Nth disk to the target rod.
3. Move the N-1th disk that was in the auxiliary rod to the target rod.

~~~python
A = [2, 1, 0] # Start
B = [] # Auxiliary
C = [] # Target

def tower_of_hanoi(i, source, auxiliary, target):
    if i == 3:
        return 
    # Step 1 : Move (i+1)th disk to the auxiliary rod to move (i)th disk.
    tower_of_hanoi(i+1, source, target, auxiliary)
    # Step 2 : Move i'th disk from source to target.
    target.append(source.pop())
    print(A, B, C,"-----", sep = '\n')
    # Step 3 : Move (i+1)th disk that was in auxiliary rod to target rod.
    tower_of_hanoi(i+1, auxiliary, source, target)

tower_of_hanoi(0, A, B, C) # Start with moving the disk at the bottom
~~~
![image](https://user-images.githubusercontent.com/67142421/206175159-b03395a1-aafc-4ac6-a1ee-01c12521d718.png)
