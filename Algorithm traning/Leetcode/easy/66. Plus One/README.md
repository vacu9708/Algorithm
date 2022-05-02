# [66. Plus One](https://leetcode.com/problems/plus-one/)
~~~javascript
var plusOne = function(digits) {
    carry=1;
    for(i=digits.length-1; i>=0; i--){
        sum_of_a_digit=digits[i]+carry;
        digits[i]=sum_of_a_digit%10;
        carry=Math.floor((sum_of_a_digit)/10);
    }
    if(carry)
        digits.splice(0,0,carry)
    return digits
};
~~~
