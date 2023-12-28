# [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

[Recursive(inefficient)](https://github.com/vacu9708/Algorithm/tree/main/Related%20to%20math/Complex%20calculation%20in%20a%20recursive%20way)<br>

floor() and int() are different in python!<br>
~~~python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        operator_map = {
                '+': lambda num1, num2: num1+num2,
                '-': lambda num1, num2: num1-num2,
                '*': lambda num1, num2: num1*num2,
                '/': lambda num1, num2: int(num1/num2),
        }
        nums=[] # Mimics a stack
        for token in tokens:
            if token not in operator_map:
                nums.append(int(token))
            else:
                nums[len(nums)-2] = operator_map[token](nums[len(nums)-2], nums[len(nums)-1])
                del nums[len(nums)-1]
        return nums[0]
~~~

### Algorithm to covert infix to postfix
~~~python
def infix_to_postfix(expression):
    print('\n'+expression)
    # Priority of operators
    priority = {'+': 1, '-': 1, '*': 2, '/': 2, '(': 0}
  
    stack = [] # Stack for operators
    postfix = []
    number = ''
  
    # Iterate over each character in the expression
    for char in expression:
        if char.isdigit():
            # Build the number from consecutive digits
            number += char
        else:
            if number:
                # Append the complete number to postfix and reset number
                postfix.append(number)
                number = ''
            if char == '(':
                stack.append(char)
            elif char == ')':
                while stack and stack[-1] != '(':
                    postfix.append(stack.pop())
                stack.pop()  # Remove the left parenthesis
            else: # To calculate operators with higher priority!
                while stack and priority[char] <= priority[stack[-1]]:
                    postfix.append(stack.pop())
                stack.append(char)
        print(stack, postfix)
  
    # Add the last number if there is one
    if number:
        postfix.append(number)
  
    # Pop any remaining operators from the stack to the output
    while stack:
        postfix.append(stack.pop())
  
    return ' '.join(postfix)
  
# Example
expression = "2+3*(4-5)"
postfix = infix_to_postfix(expression)
print(postfix)
expression = "(2*3+4)*5+6"
postfix = infix_to_postfix(expression)
print(postfix)
expression = "2*3+4*(5-6)"
postfix = infix_to_postfix(expression)
print(postfix)
~~~
