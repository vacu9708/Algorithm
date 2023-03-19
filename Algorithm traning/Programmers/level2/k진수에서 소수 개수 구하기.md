# [k진수에서 소수 개수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/92335)
~~~python
def base10To(base10, base):
    converted=''
    while base10>=base:
        converted=str(base10%base)+converted
        base10//=base
    return str(base10)+converted
        
def prime_check(n):
    if n == 1:
        return False
    for i in range(2, int(n**0.5)+1): # root n because of the symmetry of divisors
        if n%i == 0:
            return False
    return True

def solution(n, k):
    # base-10 to base-k
    base_k=base10To(n,k)
    # Check candidates
    base_ks=base_k.split('0')
    result=0
    for candidate in base_ks:
        if candidate and prime_check(int(candidate)):
            result+=1
    return result
~~~
