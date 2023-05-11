# Making e^x using the improved Euler's method
![image](https://user-images.githubusercontent.com/67142421/150201715-d2add600-ac30-4f92-bf3c-007255ea6b3c.png)

## RK2 method(Improved Euler's method)
A numerical method to solve an ordinary differential equation where the error of dy is reduced by using the average of the current slope and the next slope.<br>

~~~c++
#include <iostream>
using namespace std;

double get_dy_dx(double x, double y) { // differential equation dy/dx = y
    return y;
}

void RK2(double target_x) { // RK2
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;
    double x = 0, y = 1; // Initial state of y=e^x
    double k1, k2; // two slopes

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x += x_step; // next x
        k1 = get_dy_dx(x, y);
        k2 = get_dy_dx(x + x_step, y + x_step * k1);
        y += x_step * ((k1 + k2) / 2); // Reduce the error by using the average of the current slope and the next slope.

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
