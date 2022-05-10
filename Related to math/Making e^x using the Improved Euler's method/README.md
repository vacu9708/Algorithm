# Making e^x using the improved Euler's method
![image](https://user-images.githubusercontent.com/67142421/150201715-d2add600-ac30-4f92-bf3c-007255ea6b3c.png)

## RK2 method(Improved Euler's method)
>Improved Euler's method : A method to solve an ordinary differential equation by repeatedly finding two slopes at the points of a function and using them to find changes in 
>y points.<br>
>### h means x step(dx)
![image](https://user-images.githubusercontent.com/67142421/150201532-c7a4f44a-4cbc-4861-af31-9ecb29f13ca8.png)

~~~c++
#include <iostream>
using namespace std;

double dy_dx(double x, double y) { // y = e^x
    return y;
}

void RK2(double target_x) { // RK2
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;
    double x = 0, y = 1;
    double k1, k2; // two slopes

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        k1 = dy_dx(x, y);
        k2 = dy_dx(x + x_step, y + x_step * k1);
        x += x_step; // new x
        y += x_step * ((k1 + k2) / 2); // Find new y with the change in y using the average of two slopes.

    }

    printf("x = %lf, y = %.10lf, dy/dx = %.10lf\n", x, y, k1);
}

int main() {
    int x = 5;
    printf("e^x at x = %d\n", x);
    RK2(x);
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/150208208-a07f6bd3-11a5-4a36-b822-c5bfa79b10f5.png)
