# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
### Fibonacci sequence!!! It has to be found that the regularity is a fibonacci sequence.
~~~javascript
var climbStairs = function(n) {
    a = b = 1 // 0th and 1st term
    while (n--){
        b += a // new b = old b + old a
        a = b - a // new a = old b
    }
    return a
};
~~~
