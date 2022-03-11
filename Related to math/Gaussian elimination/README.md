# Gaussian elimination
>Gaussian elimination is an algorithm for solving simultaneous equations.

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
    n = len(b) # The number of solutions
    last_row = n - 1
    x = numpy.zeros(n) # The answer
    # Forward elimination
    for k in range(0, n-1): # Use kth row to eliminate X_k
        for i in range(k+1, n): # from (k+1)th row.
            m = A[i][k] / A[k][k] # The number to multiply with the new row.
            #-----
            # Make a new row from X_(k+1)th column
            # X_k doesn't need to be calculated since it is 0, which means 
            # it won't be taken into account in the back substitution after all.
            # So, calculate from (k+1)th column
            for j in range(k+1, n):
                A[i][j] -= m*A[k][j]
            b[i] -= m*b[k]
    #-----
    # Back substitution
    x[last_row] = b[last_row] / A[last_row][last_row] # Find the first solution at the very bottom.
    for i in range(last_row-1, -1, -1): # Find X_i from X_(last row-1) to X_0.
        right_side = b[i] # Get the initial value of the right side of the current equation.
        for j in range(i+1, n): # Make the right side of the current equation.
            right_side -= A[i][j]*x[j] # Use pre-found solutions to find X[i]
        x[i] = right_side / A[i][i]
        
    return x

A = numpy.array( [[2, 8, 2], [1, 6, -1], [2, -1, 2]] ); # Coefficient matrix
b = numpy.array( [14, 13, 5] ) # The right side of the simultaneous equation
print(gaussian_elimination(A,b))
~~~

## Output
### X0 = 5<br>
### X1 = 1<br>
### X2 = -2
