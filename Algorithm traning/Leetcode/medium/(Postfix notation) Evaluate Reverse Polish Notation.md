### Algorithm to convert infix to postfix and calculate it
~~~python
def infix_to_postfix(expression):
    print('\n'+expression)
    # Priority of operators
    priority = {'+': 1, '-': 1, '*': 2, '/': 2, '(': 0}
  
    stack = [] # Stack for operators (Operators that are calculated earlier are in a higher position of the stack)
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

def evaluate_postfix(expression):
    stack = []
    for token in expression.split():
        if token.isdigit():
            stack.append(int(token))
        else:
            right = stack.pop()
            left = stack.pop()
            if token == '+':
                stack.append(left + right)
            elif token == '-':
                stack.append(left - right)
            elif token == '*':
                stack.append(left * right)
            elif token == '/':
                stack.append(left / right)
            # Add more operators if needed
    return stack.pop()

# Example
expression = "2+3*(4-5)"
postfix = infix_to_postfix(expression)
print(postfix)
print(evaluate_postfix(postfix))
expression = "(2*3+4)*5+6"
postfix = infix_to_postfix(expression)
print(postfix)
print(evaluate_postfix(postfix))
expression = "2*3+4*(5-6)"
postfix = infix_to_postfix(expression)
print(postfix)
print(evaluate_postfix(postfix))
~~~

# Related problem in leetcode
[Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
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
