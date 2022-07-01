### [118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)

~~~python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        rows=[]
        for i in range(numRows):
            row=[]
            for j in range(i+1):
                if j==0 or j==i: # If first index or last index of a row
                    row.append(1)
                else: # Else add [j-1] and [j] of the previous row
                    row.append(rows[i-1][j-1]+rows[i-1][j])
            rows.append(row)
        return rows # Answer
~~~
