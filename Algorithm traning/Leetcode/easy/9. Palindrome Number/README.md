# [9. Palindrome Number](https://leetcode.com/problems/palindrome-number)
![image](https://user-images.githubusercontent.com/67142421/164774001-7fb5df82-d114-4689-aee8-f2508018c49d.png)

~~~javascript
var isPalindrome = function(x) {
    num_string = x.toString();
    num_length = num_string.length;
    for(let i = 0; i < num_length; i++){
        if(num_string[i] != num_string[num_length-1-i])
            return false;
    }
    return true;
};
~~~
