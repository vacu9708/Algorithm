# [Multi-level Marketing](https://school.programmers.co.kr/learn/courses/30/lessons/77486)
~~~python
def solution(enroll, referral, seller, amount):
    answer = [0 for i in range(len(enroll))]
    # Hashmap to find sellers' index fast
    hashmap={}
    for i, name in enumerate(enroll):
        hashmap[name]=i
    
    def earn_money(name_i, money):
        commission=money//10
        answer[name_i]+=money-commission
        # Distribute the profit to the recruiter
        # money>=1 is needed to prevent stack overflow
        if referral[name_i]!='-' and money>=1:
            earn_money(hashmap[referral[name_i]], commission)
        
    for i, name in enumerate(seller):
        earn_money(hashmap[name], amount[i]*100)
    return answer
~~~
