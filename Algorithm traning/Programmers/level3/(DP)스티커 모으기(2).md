# [스티커 모으기(2)](https://school.programmers.co.kr/learn/courses/30/lessons/12971)
- dp[i] = dp[i-2]+sticker[i]: Pick one and add to the dp[i-2] combination
- dp[i] = dp[i-1]: Pick nothing and use the dp[i-1] combination
~~~python
def solution(sticker):
    if len(sticker)==1:
        return sticker[0]
    # Pick the 1st one
    dp1 = [0] * len(sticker)
    dp1[0] = dp1[1] = sticker[0]
    for i in range(2, len(sticker)-1):
        dp1[i] = max(dp1[i-2]+sticker[i], dp1[i-1])
    # Pick the 2nd one
    dp2=[0]*len(sticker)
    dp2[1]=sticker[1]
    for i in range(2, len(sticker)):
        dp2[i] = max(dp2[i-2]+sticker[i], dp2[i-1])
    return max(dp1[-2], dp2[-1])
~~~
