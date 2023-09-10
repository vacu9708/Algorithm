~~~python
import math, collections

def recursion(expression: str):    
    start=0
    # Find an opening parentheses
    while start<len(expression) and expression[start]!='(':
        start+=1
    # Find the corresponding closing parentheses
    end, n_opened_parentheses=start+1, 1
    while end<len(expression):
        if expression[end]=='(':
            n_opened_parentheses+=1
        elif expression[end]==')':
            n_opened_parentheses-=1

        if n_opened_parentheses==0:
            break
        else:
            end+=1

    # Termination condition: If there is no parentheses, calculate the expression
    if start==len(expression):
        return calculate(expression)
    # Recursion: Calculate the expression inside the parentheses
    if expression[start] == '(':
        return calculate(expression[:start] + str(recursion(expression[start+1:end])) + expression[end+1:])
    
def calculate(expression: str):
    operators = {
                '+': lambda num1, num2: num1+num2,
                '-': lambda num1, num2: num1-num2,
                '*': lambda num1, num2: num1*num2,
                '/': lambda num1, num2: num1/num2,
                '^': lambda num1, num2: num1**num2
                }
    # Parse the expression into numbers and operators
    nums=[]
    symbols=[]
    start=0
    for i in range(len(expression)):
        if expression[i] in operators:
            nums.append(int(expression[start:i]))
            symbols.append(expression[i])
            start=i+1
    nums.append(int(expression[start:]))
    # return calculate_efficient(operators, nums, symbols)
    return calculate(operators, nums, symbols)
 
def calculate(operators, nums, symbols):
    # Calculate using the parsed expression (higher priority first)
    i=0
    while i<len(symbols):
        if symbols[i]=='^':
            nums[i]=operators[symbols[i]](nums[i], nums[i+1])
            del nums[i+1]
            del symbols[i]
            i-=1
        i+=1
    i=0
    while i<len(symbols):
        if symbols[i]=='*' or symbols[i]=='/':
            nums[i]=operators[symbols[i]](nums[i], nums[i+1])
            del nums[i+1]
            del symbols[i]
            i-=1
        i+=1
    i=0
    while i<len(symbols):
        if symbols[i]=='+' or symbols[i]=='-':
            nums[i]=operators[symbols[i]](nums[i], nums[i+1])
            del nums[i+1]
            del symbols[i]
            i-=1
        i+=1
    return nums[0]


# expression='1+(1+(2+2-2)*2)*3' # 16
expression='2+3*2-2+3*2' # 12
# expression='1+(1+(2^3+2-2)*2)*3' # 52
print(f'{expression} = {recursion(expression)}')
~~~
