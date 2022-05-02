# Newton-Raphson method (plus babylonian method)
* Newton-raphson method : A numerical algorithm to solve equations, which square roots can also be found with.
* Babylonian method : An algorithm used for approximating the value of square roots, which is derived from Newton-Raphson method. This method is much faster than finding it using the Newton-Raphson method.

## Process
![image](https://user-images.githubusercontent.com/67142421/149330217-6fd2fd36-1d0f-4210-8c69-289ea03a96d6.png)

1. Set an initial x point as near the answer as possible.
2. Check if f(x) converges to 0.
3. If it does, the x is the answer, if not, find the next x by differentiating.
4. Repeat the 2nd and 3rd step.

## The formulas
### Newton-Raphson method
![image](https://user-images.githubusercontent.com/67142421/149328643-8b2e5721-9b55-4bf0-819b-42f9ffc44f85.png)
### Babylonian method
<img src="https://user-images.githubusercontent.com/67142421/149328802-7c02f898-dedb-4ec7-b5b8-77116c1fc2aa.png" width="550" height="300">

## How to derive the formulas
![KakaoTalk_20220113_204543213](https://user-images.githubusercontent.com/67142421/149327997-af3a7a06-b48f-4d71-836c-196090a42123.jpg)<br>
or
![KakaoTalk_20220503_010407053](https://user-images.githubusercontent.com/67142421/166267186-43b2b195-7371-4c8a-8ed1-e9faa6be92f4.jpg)

~~~c++
#include <iostream>
using namespace std;

double target = 0;
double f(double x) {
    return pow(x, 2) - target;
}

double newton_raphson(double target) {
    ::target = target;
    // Find the best initial x point
    /*double x = 0;
    while (pow(x, 2) < target)
        x++;*/
    //-----
    double x = target;
    double infinitesimal = 1.0 / 987654321;
    while (f(x) > infinitesimal) { // If f(x) converges to 0, the x is the answer.
        double derivative = (f(x + infinitesimal) - f(x - infinitesimal)) / (infinitesimal * 2); // Derivative at x
        x = x - (f(x) / derivative); // Find the next x
    }
    return x;
}

double babylonian_method(double target) {
    double x = target;
    while (target/(x * x) < 0.9999999) { // If f(x) converges to 0, the x is the answer.
        x = (x + (target / x)) / 2; // Find the next x
    }
    return x;
}

int main() {
    double target = 5;
    cout << "The square root of (" << target << ") = " << newton_raphson(target) << "\n";
    cout << "The square root of (" << target << ") = " << babylonian_method(target) << "\n";
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149326923-5046ef89-6d71-453c-be48-e8990949d902.png)
