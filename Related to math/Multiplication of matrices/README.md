# Dot product
Consider the dot product of two matrices whose dimensions are (m X n) and (p X q) respectively.<br>

## Rule
The number of columns in the first matrix must equal the number of rows in the second matrix.<br>
In terms of dimensions, n must be equal to p.

## Resulting Matrix Dimension
The resulting matrix will have a dimension of (m X q)

## Code
~~~python
matrix1 = [[1,2,3], [4,5,6]]
matrix2 = [[1,2], [3,4], [5,6]]

def multiplication_of_matrices(matrix1, matrix2):
    row1 = len(matrix1)
    column1 = len(matrix1[0])
    row2 = len(matrix2)
    column2 = len(matrix2[0])

    if column1 != row2:
        print("The number of columns in matrix1 has to be equal to the number of rows in matrix2.")
        return

    # Make an empty matrix
    result_matrix = []
    for i in range(row1):
        a_row = []
        for j in range(column2):
            a_row.append(0)
        result_matrix.append(a_row) # Add a row
    #-----
    for i in range(row1):
        for j in range(column2):
            for k in range(column1): # column2 can't be put here
                result_matrix[i][j] += matrix1[i][k] * matrix2[k][j] # Fix the row of matrix1 and the column of matrix2
    print(result_matrix)

print(matrix1, " X ", matrix2, " = ", end = "");
multiplication_of_matrices(matrix1, matrix2)
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149186390-e335f0b8-e312-425d-a137-444dd8178690.png)
