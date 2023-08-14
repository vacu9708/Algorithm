# [타겟 넘버](https://school.programmers.co.kr/learn/courses/30/lessons/43165)
Recursion for the number of cases
~~~python
def solution(numbers, target):
    def compute_cases(depth, visited, sum, answer):
        if depth==len(numbers):
            if sum==target:
                answer[0]+=1
            return
        for operator in ('-', '+'):
            if operator == '+':
                compute_cases(depth+1, visited, sum+int(numbers[depth]), answer)
            else:
                compute_cases(depth+1, visited, sum-int(numbers[depth]), answer)
        
    answer=[0]
    visited=[False]*len(numbers)
    compute_cases(0, visited, 0, answer)
    return answer[0]
~~~
