# Making e^x using Euler's method of differential equation
![image](https://user-images.githubusercontent.com/67142421/149747518-9a60f957-4e0c-4538-bfa8-e99a5b91dbba.png)

### Euler's method(RK1)
>Euler's method(RK1) : A numerical method to solve an ordinary differential equation. This method is the most inaccurate and slowest.<br>
![image](https://user-images.githubusercontent.com/67142421/150194690-5656e5cd-6411-4e41-97f2-f07142c0e727.png)

~~~c++
#include <iostream>
using namespace std;

double x_points[9876543]{ 0 };
double y_points[9876543]{ 1 };
double dy_dxs[9876543]{ 1 };

double dy_dx_function(double x, double y) {
    return y; // = dy/dx
}

void e_to_the_x_RK1_with_arrays(double target_x) { // RK1
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x_points[i + 1] = x_points[i] + x_step;
        y_points[i + 1] = y_points[i] + dy_dxs[i] * x_step; // y_points[i+1] is equal to y_points[i] + change in y
        dy_dxs[i + 1] = dy_dx_function(x_points[i + 1], y_points[i + 1]); // The solution of this differential equation(dy/dx = y) is y=e^x. (using separation of variables method)
    }

    int i = target_x * compensation_for_x_step;
    printf("x = %lf, y = %.10lf, dy/dx = %.10lf\n", x_points[i], y_points[i], dy_dxs[i]);
}

void e_to_the_x_RK1(double target_x) { // RK1
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;
    double x = 0, y = 1, dy_dx = dy_dx_function(x, y);

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x = x + x_step;
        y = y + dy_dx * x_step;
        dy_dx = dy_dx_function(x, y);
    }

    printf("x = %lf, y = %.10lf, dy/dx = %.10lf\n", x, y, dy_dx);
}

int main() {
    int x = 5;
    printf("e^x at x = %d\n", x);
    e_to_the_x_RK1(x);
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/150207611-e7d93bfb-fde7-4ba7-b296-0ef40250864e.png)
