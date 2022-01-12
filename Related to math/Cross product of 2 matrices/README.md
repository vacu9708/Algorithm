# Cross product of 2 matrices

~~~python
matrix1 = [[1,2,3], [4,5,6]]
matrix2 = [[1,2], [3,4], [5,6]]

def cross_product(matrix1, matrix2):
    row1 = len(matrix1)
    column1 = len(matrix1[0])
    row2 = len(matrix2)
    column2 = len(matrix2[0])

    if column1 != row2:
        print("The number of columns in matrix1 has to be equal to the number of rows in matrix2.")
        return

    result_matrix = []
    for i in range(row1):
        a_row = []
        for j in range(column2):
            a_row.append(0)
        result_matrix.append(a_row) # Add a row
    print(result_matrix)
        
    for i in range(row1):
        for j in range(column2):
            for k in range(column1): #column2 can't be put here
                result_matrix[i][j] += matrix1[i][k] * matrix2[k][j] #Fix the row of matrix1 and the column of matrix2
    print(result_matrix)

cross_product(matrix1, matrix2)
~~~
