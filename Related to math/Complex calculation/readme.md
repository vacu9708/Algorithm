# Postfix notation
[Postfix notation](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/Leetcode/medium/(Postfix%20notation)%20Evaluate%20Reverse%20Polish%20Notation.md)

# Infix notation recursively(inefficient)
~~~python
def recursion(expression: str):    
    start=0 # Start index of the parentheses
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
        end+=1

    # Termination condition: If there is no parentheses, parse the expression
    if start==len(expression):
        return parse(expression)
    # Recursion: parse recursively the expression inside the parentheses
    if expression[start] == '(':
        return parse(expression[:start] + str(recursion(expression[start+1:end])) + expression[end+1:])
    
def parse(expression: str):
    operator_map = {
                '+': lambda num1, num2: num1+num2,
                '-': lambda num1, num2: num1-num2,
                '*': lambda num1, num2: num1*num2,
                '/': lambda num1, num2: num1/num2,
                '^': lambda num1, num2: num1**num2
                }
    # Parse the expression into numbers and operator_map
    nums=[]
    operators=[]
    start=0
    for i in range(len(expression)):
        if expression[i] in operator_map:
            nums.append(int(expression[start:i]))
            operators.append(expression[i])
            start=i+1
    nums.append(int(expression[start:]))
    return calculate(operator_map, nums, operators)
 
def calculate(operator_map, nums, operators):
    # Calculate using the parsed expression (higher priority first, lower priority last)
    i=0
    while i<len(operators):
        if operators[i]=='^':
            nums[i]=operator_map[operators[i]](nums[i], nums[i+1])
            del nums[i+1]
            del operators[i]
        else:
            i+=1
    i=0
    while i<len(operators):
        if operators[i]=='*' or operators[i]=='/':
            nums[i]=operator_map[operators[i]](nums[i], nums[i+1])
            del nums[i+1]
            del operators[i]
        else:
            i+=1
    i=0
    while i<len(operators):
        if operators[i]=='+' or operators[i]=='-':
            nums[i]=operator_map[operators[i]](nums[i], nums[i+1])
            del nums[i+1]
            del operators[i]
        else:
            i+=1
    return nums[0]


# expression='1+(1+(2+2-2)*2)*3' # 16
# expression='2+3*2-2+3*2' # 12
expression='1+(1+(2^3+2-2)*2)*3' # 52
print(f'{expression} = {recursion(expression)}')
~~~
