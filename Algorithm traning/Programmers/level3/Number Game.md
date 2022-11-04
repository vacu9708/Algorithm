# [Number Game](https://school.programmers.co.kr/learn/courses/30/lessons/12987)
## sort
~~~python
def solution(A, B):
    answer = 0
    A.sort()
    B.sort()
    pA=pB=0
    while pA<len(A):
        while pB<len(B): 
            if B[pB]>A[pA]:
                answer+=1
                break
            pB+=1
        pB+=1
        pA+=1
    return answer
~~~
