# [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)
~~~javascript
var mySqrt = function(x) {
    current_x=x
    while(x/(current_x*current_x)<0.99999999999)
        current_x = ((current_x + x/current_x) / 2)
    return Math.floor(current_x)
};
~~~
