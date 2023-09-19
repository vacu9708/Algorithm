# [전화번호 목록](https://school.programmers.co.kr/learn/courses/30/lessons/42577)
~~~python
def solution(phone_book):
    # Put the phone numbers in the hashmap
    hashmap={}
    for phone_num in phone_book:
        hashmap[phone_num]=True
    # Iterate through the phone book and look up the subset of the phone number
    for phone_num in phone_book:
        for i in range(1,len(phone_num)):
            if phone_num[:i] in hashmap:
                return False
    return True
~~~
