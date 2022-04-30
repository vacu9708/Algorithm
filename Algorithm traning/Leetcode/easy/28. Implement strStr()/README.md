# [28. Implement strStr()](https://leetcode.com/problems/implement-strstr/)
~~~python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if needle=='':
            return 0
        len_needle=len(needle)
        for i in range(len(haystack)+1-len_needle):
            if haystack[i:i+len_needle]==needle:
                return i
        return -1
~~~
