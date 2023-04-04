# [50. Pow(x, n)](https://leetcode.com/problems/powx-n/description/)
# Example 7<sup>11</sup>
11 = 1011(binary) = 8+2+1<br>
Therefore, 7<sup>11</sup> = 7<sup>8</sup> * 7<sup>2</sup> * 7<sup>1</sup>

### Iteration 1
- result = 1 × 7 = 7
- x = 7 * 7 = 7<sup>2</sup>
- n = 1011 >> 1 = 0101

### Iteration 2
- result = 7 * 7<sup>2</sup> = 343
- x = 7<sup>2</sup> * 7<sup>2</sup> = 7<sup>4</sup>
- n = 0101 >> 1 = 0010

### Iteration 3
- x = 7<sup>4</sup> * 7<sup>4</sup> = 7<sup>8</sup>
- n = 0010 >> 1 = 0001

### Iteration 4
- result = 343 * 7<sup>8</sup> = 1977326743
- x = 7<sup>8</sup> * 7<sup>8</sup> = 7<sup>16</sup>
- n = 0001 >> 1 = 0000

### O(logN)!!
~~~python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n<0:
            x=1/x
            n=-n
            
        result = 1
        while n:
            if n & 1:
                result *= x
            x *= x
            n >>= 1 # same as n//=2
        return result
~~~

## Recursive method
![image](https://user-images.githubusercontent.com/67142421/229672228-224e6e47-8e3d-444a-a0db-1ef644c1e437.png)

(n is odd) is the same as (n&1 == 1)<br>
(n is even) is the same as (n&1 == 0)
~~~python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        def recursion(base, exponent):
            if exponent == 0:
                return 1
            elif exponent % 2 == 0:
                return recursion(base * base, exponent // 2)
            else:
                return base * recursion(base * base, (exponent) // 2)

        result = recursion(x, abs(n))
        return result if n >= 0 else 1/result
~~~
