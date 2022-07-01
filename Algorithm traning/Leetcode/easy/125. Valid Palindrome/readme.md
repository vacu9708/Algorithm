### [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

~~~python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s=list(s) # To control characters of the string
        i=0
        j=len(s)-1
        while i<=j:
            while not( (s[i]>='a' and s[i]<='z') or (s[i]>='A' and s[i]<='Z') or
                     (s[i]>='0' and s[i]<='9') ) : # Skip non-alphanumeric characters 
                i+=1
                if i==len(s): # There is no alphanumeric character
                    return True
            while not( (s[j]>='a' and s[j]<='z') or (s[j]>='A' and s[j]<='Z') or
                      (s[j]>='0' and s[j]<='9') ) : # Skip non-alphanumeric characters 
                j-=1
            
            # Convert the uppercase letter into the lowercase letter
            if s[i]>='A' and s[i]<='Z':
                s[i]=s[i].lower()
            if s[j]>='A' and s[j]<='Z':
                s[j]=s[j].lower()
                
            if s[i]!=s[j]: # not palindrome
                return False
            i+=1
            j-=1
        return True
~~~
