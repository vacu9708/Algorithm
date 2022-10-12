# [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)
### Newton's method
~~~javascript
var mySqrt = function(x) {
    current_x=x
    while(Math.abs(current_x**2-x)>0.0001)
        current_x = ((current_x + x/current_x) / 2)
    return Math.floor(current_x)
};
~~~
