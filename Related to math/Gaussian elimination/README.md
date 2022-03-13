# Gaussian elimination
>Gaussian elimination is an algorithm for solving simultaneous equations.

## The number of solutions
* When all numbers on the left side are 0 and the right side is also 0 : The linear system has infinitely many solutions
* When all numbers on the left side are 0 and the right side is not 0 : The linear system has no solution
* When the left side is not 0 and the simultaneous equation is undetermined (When there are more unknowns than equations)

## Augmented matrix used in this code
|Coefficient| |
|:---------:|-|
|2    8    2|14|
|1    6   -1|13|
|2   -1    2|5|

## Solving manually
![KakaoTalk_20220311_225949094](https://user-images.githubusercontent.com/67142421/157882047-da871823-0e94-4a36-903d-e53371c74a50.jpg)

~~~Python
import numpy

def gaussian_elimination(A, b):
    n_of_rows = len(A)
    n_of_columns = len(A[0])
    last_row = n_of_rows - 1

    x = numpy.zeros(n_of_columns) # The answer
    # Forward elimination
    for k in range(0, n_of_rows-1): # Use kth row to eliminate X_k
        for i in range(k+1, n_of_rows): # from (k+1)th row.
            m = A[i][k] / A[k][k] # Find m_ik to multiply by the new row. (m_ik means eliminating X_k in i'th row)
            #-----
            # Make a new row from X_(k+1)th column
            # X_k doesn't need to be calculated since it is 0, which means 
            # it won't be taken into account in the back substitution after all.
            # So, calculate from (k+1)th column
            for j in range(k, n_of_columns):
                A[i][j] -= m*A[k][j]
            b[i] -= m*b[k]
        
        print('After eliminating X_{}\n{} = {}\n'.format(k,A,b))
    #-----
    # Exception handling
    # Check if all numbers on the left side of the last row are 0
    infinitesimal = 1/987654321 # Due to the inaccuracy of float data
    is_left_side_zero = True
    for column in range(last_row, n_of_columns):
        if abs(A[last_row][column]) > infinitesimal: # if the left side isn't 0
            is_left_side_zero = False
            break
    #-----
    if is_left_side_zero == True:
        if abs(b[last_row]) < infinitesimal: # If the right side is 0
            print('Infinitely many solutions')
            return
        else: # If the right side isn't 0
            print('There is no solution')
            return
    elif n_of_columns != n_of_rows: # Else if the simultaneous equation is under-determined
        print('Infinitely many solutions(Under-determined with the left side that is not 0)')
        return
    #-----
    # Back substitution
    x[last_row] = b[last_row] / A[last_row][last_row] # Find the first solution at the very bottom.
    for i in range(last_row-1, -1, -1): # Find X_i from X_(last row-1) to X_0.
        right_side = b[i] # Get the initial value of the right side of the current equation.
        for j in range(i+1, n_of_columns): # Make the right side of the current equation.
            right_side -= A[i][j]*x[j] # Use pre-found solutions to find X[i]
        x[i] = right_side / A[i][i]
    
    print(x)

# infinitely many solutions
A = numpy.array([ [3,2,2,-5], [0.6,1.5,1.5,-5.4], [1.2,-0.3,-0.3,2.4] ], dtype=float)
b = numpy.array([8, 2.7, 2.1], dtype=float)
#-----
# No solution
#A = numpy.array([ [3,2,1], [2,1,1], [6,2,4] ], dtype=float)
#b = numpy.array([3,0,6], dtype=float)
#-----
# Infinitely many solutions(Undetermined with the left side that is not 0)
#A = numpy.array([ [2,8,2,9], [1,6,-1,9], [2,-1,2,9] ], dtype=float)
#b = numpy.array( [14, 13, 5], dtype=float)
#-----
# One solution
#A = numpy.array([ [2,8,2], [1,6,-1], [2,-1,2] ]) # Coefficient matrix
#b = numpy.array( [14, 13, 5] ) # The right side of the simultaneous equation
#-----
gaussian_elimination(A,b)
~~~

## Output
### X0 = 5<br>
### X1 = 1<br>
### X2 = -2
