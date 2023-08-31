# [의상](https://school.programmers.co.kr/learn/courses/30/lessons/42578?language=python3)
### (math)combination
~~~python
from collections import defaultdict
def solution(clothes):
    # Put clothes into hashmap
    hashmap=defaultdict(list)
    for clothing in clothes:
        hashmap[clothing[1]].append(clothing[0])
    # Calculate the number of cases
    answer=1
    for collection in hashmap.values():
        # +1 to account for the case when that nothing is worn
        answer*=len(collection)+1
    # -1 since there is no case when nothing is worn
    return answer-1
~~~
### Recursion EXCEEDS time limit
~~~python
from collections import defaultdict
def solution(clothes):
    # Put clothes into hashmap
    hashmap=defaultdict(list)
    for clothing in clothes:
        hashmap[clothing[1]].append(clothing[0])
    clothes=list(hashmap.values())
    # Calculate the number of cases
    def combination(max_depth, depth, start, n_of_cases, answer):
        if depth>max_depth:
            answer[0]+=n_of_cases
            return
        for i in range(start,len(clothes)):
            combination(max_depth,depth+1,i+1,n_of_cases*len(clothes[i]),answer)
            
    answer=[0]
    for i in range(0,len(clothes)):
        combination(i,0,0,1,answer)
    return answer[0]
~~~
