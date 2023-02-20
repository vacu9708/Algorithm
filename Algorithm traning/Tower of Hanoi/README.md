# Tower of Hanoi
Move all the disks to the target rod.

![image](https://user-images.githubusercontent.com/67142421/176498793-a2874a2c-41c8-4a91-bc6f-687b45fe0be0.png)

# Rule
* Only one disk may be moved at a time.
* No disk may be placed on top of a smaller disk
* Each move consists of taking the upper disk from one of the stacks and placing it on an empty rod.

~~~python
A = [2, 1, 0] # Start
B = [] # Auxiliary
C = [] # Target

def tower_of_hanoi(i, source, auxiliary, target):
    if i < 0:
        return 
    # Step 1 : Move disk (i-1) from source to auxiliary for step 2.
    tower_of_hanoi(i-1, source, target, auxiliary)
    # Step 2 : Move disk (i) from source to target.
    target.append(source.pop())
    print(A, B, C,"-----", sep = '\n')
    # Step 3 : Move disk (i-1) that was in auxiliary to target rod.
    tower_of_hanoi(i-1, auxiliary, source, target)

tower_of_hanoi(len(A) - 1, A, B, C) # Start with moving the disk at the bottom
~~~
# Output
![image](https://user-images.githubusercontent.com/67142421/206175159-b03395a1-aafc-4ac6-a1ee-01c12521d718.png)
