# Making e^x using Runge-Kutta method
![image](https://user-images.githubusercontent.com/67142421/150205521-0650b5f3-b837-4e23-a65e-389afa208193.png)

### 4th order Runge-Kutta (RK4) 
>4th order Runge-Kutta (RK4) : The most practical and useful method to solve an ordinary differential equation, which finds 4 slopes and uses the average of them to find
>a change in a y point.<br>
>The error of this method is proportional to the step size to the power of 4, which means reducing the step size to half decreases the error by about 16 times.<br>
![image](https://user-images.githubusercontent.com/67142421/150205501-f7e0c899-69ba-4212-9d07-3406762d7261.png)

~~~c++
#include <iostream>
using namespace std;

double dy_dx_function(double x, double y) {
    return y; // = dy/dx
}

void e_to_the_x_RK4(double target_x) {
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;
    double x = 0, y = 1;
    double k1 = dy_dx_function(x, y);
    double k2 = dy_dx_function(x + x_step / 2, y + (x_step / 2) * k1); // Add x_step / 2 to x and the change in y by it to y.
    double k3 = dy_dx_function(x + x_step / 2, y + (x_step / 2) * k2);
    double k4 = dy_dx_function(x + x_step, y + x_step * k3);

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x = x + x_step; // Change in x
        y = y + x_step * ((k1 + 2*k2 + 2*k3 + k4) / 6); // Find the change in y using the average of the two slopes.
        k1 = dy_dx_function(x, y);
        k2 = dy_dx_function(x + x_step / 2, y + (x_step / 2) * k1); // Add x_step / 2 to x and the change in y by it to y.
        k3 = dy_dx_function(x + x_step / 2, y + (x_step / 2) * k2);
        k4 = dy_dx_function(x + x_step, y + x_step * k3);
    }

    printf("x = %lf, y = %.10lf, dy/dx = %.10lf\n", x, y, k1);
}

int main() {
    int x = 5;
    printf("e^x at x = %d\n", x);
    e_to_the_x_RK4(x);
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/150208450-e1ce9982-33f8-4e35-aa1e-76a972058be5.png)
