# [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix)
~~~python
def min(list):
    result=list[0]
    for i in range(1, len(list)):
        if list[i] < result:
            result=list[i]
    return result

class Solution:
    def longestCommonPrefix(self, strs) -> str:
        prefix=""
        lengths=[]
        for str in strs:
            lengths.append(len(str))

        min_length=min(lengths)
        for i in range(min_length):
            for j in range(1, len(strs)):
                if strs[0][i] != strs[j][i]:
                    return prefix
            prefix+=strs[0][i]
        return prefix
~~~
