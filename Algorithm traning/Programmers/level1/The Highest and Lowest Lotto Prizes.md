# [The Highest and Lowest Lotto Prizes](https://school.programmers.co.kr/learn/courses/30/lessons/77484)
~~~python
def solution(lottos, win_nums):
    answer = []
    # Hashmap for fast lookups
    win_nums_map={}
    for win_num in win_nums:
        win_nums_map[win_num]=True
    # Count
    match_count=scribble_count=0
    for i in range(len(lottos)):
        if lottos[i] in win_nums_map:
            match_count+=1
        elif lottos[i]==0:
            scribble_count+=1
    # Decide the prize
    if match_count+scribble_count==0:
        answer.append(6)
    else:
        answer.append(7-(match_count+scribble_count))
    if match_count==0:
        answer.append(6)
    else:
        answer.append(7-match_count)
    return answer
~~~
