# [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)
~~~python
def a_roman(c: str):
    if c=='I': return 1
    if c=='V': return 5
    if c=='X': return 10
    if c=='L': return 50
    if c=='C': return 100
    if c=='D': return 500
    if c=='M': return 1000

class Solution:
    def romanToInt(self, s: str) -> int:
        roman_sum=0
        length=len(s)
        i=0
        while i<length:
            if i != length-1 and a_roman(s[i]) < a_roman(s[i+1]):
                roman_sum+=a_roman(s[i+1])-a_roman(s[i])
                i+=2
            else:
                roman_sum+=a_roman(s[i])
                i+=1
        return roman_sum
~~~
