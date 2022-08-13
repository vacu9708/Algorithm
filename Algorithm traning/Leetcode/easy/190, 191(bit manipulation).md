# [190. Reverse Bits](https://leetcode.com/problems/reverse-bits/)

## First solution
~~~python
class Solution:
    def reverseBits(self, n: int) -> int:
        #Make 32bits of binary
        binary=""
        while n:
            binary=str(n%2)+binary
            n=n//2
        for i in range(32-len(binary)):
            binary='0'+binary
        #Binary to decimal
        exp=0
        output=0
        for digit in binary:
            output+=(ord(digit)-ord('0'))*2**exp #int(digit) is slow
            exp+=1
        return output
~~~

## Bit manipulation
~~~python
class Solution:
    def reverseBits(self, n):
        output = 0
        for i in range(32):
            output = (output << 1) + (n & 1) #Put the lowest digit of n to the right of output
            n >>= 1 #Prepare the higher digit
        return ans
~~~

# [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

~~~python
class Solution:
    def hammingWeight(self, n: int) -> int:
        output=0
        while n:
            if n&1:
                output+=1
            n>>=1
        return output
~~~
