# [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

~~~python
class Solution:
    def isValid(self, s: str) -> bool:
        if s[0]==')' or s[0]=='}' or s[0]==']':
            return False

        stack=[]
        for c in s:
            if c=='(' or c=='{' or c=='[':
                stack.append(c)
                continue

            if len(stack)==0: # Closed without a matching parenthesis
                return False

            if (c==')' and stack[-1]=='(') or \
                (c=='}' and stack[-1]=='{') or \
                (c==']' and stack[-1]=='['):
                del stack[-1]
            else: # Closed with a wrong parenthesis
                return False
            
        return len(stack)==0
~~~
