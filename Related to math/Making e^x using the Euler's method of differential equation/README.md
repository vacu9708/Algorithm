# Making e^x using the Euler's method of differential equation
![image](https://user-images.githubusercontent.com/67142421/149747518-9a60f957-4e0c-4538-bfa8-e99a5b91dbba.png)

### Euler's method(RK1)
A numerical method to solve an ordinary differential equation. This method is the most inaccurate and slowest.<br>
Function ***y*** is made step by step.

![image](https://github.com/vacu9708/Algorithm/assets/67142421/471a42d9-c4df-45f5-9451-074ec6716e4d)
* h = instantaneous rate of change at the current x
* f(x, y) = y value at x 

~~~c++
#include <iostream>
using namespace std;

double x_points[9876543]{ 0 };
double y_points[9876543]{ 1 };
double dy_dxs[9876543]{ 1 };

double get_dy_dx(double x, double y) { // differential equation dy/dx = y
    return y;
}

void RK1_with_arrays(double target_x) { // RK1
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x_points[i + 1] = x_points[i] + x_step;
        y_points[i + 1] = y_points[i] + dy_dxs[i] * x_step; // y_points[i+1] is equal to y_points[i] + change in y
        dy_dxs[i + 1] = get_dy_dx(x_points[i + 1], y_points[i + 1]); // The solution of this differential equation(dy/dx = y) is y=e^x. (using separation of variables method)
    }

    int i = target_x * compensation_for_x_step;
    printf("x = %lf, y = %.10lf, dy/dx = %.10lf\n", x_points[i], y_points[i], dy_dxs[i]);
}

void RK1(double target_x) { // RK1
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;
    double x = 0, y = 1, dy_dx = get_dy_dx(x, y); // Initial state of y=e^x

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x += x_step; // Change of x
        y += dy_dx * x_step; // Change of y
        dy_dx = get_dy_dx(x, y); // For next step
    }

    printf("x = %lf, y = %.10lf, dy/dx = %.10lf\n", x, y, dy_dx);
}

int main() {
    int x = 5;
    printf("e^x at x = %d\n", x);
    RK1(x);
    RK1_with_arrays(x);
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/150207611-e7d93bfb-fde7-4ba7-b296-0ef40250864e.png)
