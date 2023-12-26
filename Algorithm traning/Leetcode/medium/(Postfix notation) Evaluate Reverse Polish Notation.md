[Recursive and inefficient](https://github.com/vacu9708/Algorithm/tree/main/Related%20to%20math/Complex%20calculation%20in%20a%20recursive%20way)<br>

floor() and int() are different in python!!<br>
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
